# Arquitetura — Haras Manager

Documento técnico de referência sobre a arquitetura do sistema. Descreve decisões de design, padrões aplicados e fluxos de dados — **sem exposição de código-fonte, credenciais ou configurações de ambiente**.

---

## Índice

1. [Visão Geral](#1-visão-geral)
2. [Arquitetura em Camadas](#2-arquitetura-em-camadas)
3. [Clean Architecture](#3-clean-architecture)
4. [Repository Pattern](#4-repository-pattern)
5. [Riverpod — Gerenciamento de Estado](#5-riverpod--gerenciamento-de-estado)
6. [Hive — Persistência Local](#6-hive--persistência-local)
7. [Firebase — Backend e Nuvem](#7-firebase--backend-e-nuvem)
8. [APIs REST — Integrações Externas](#8-apis-rest--integrações-externas)
9. [Sincronização Offline-First](#9-sincronização-offline-first)
10. [Organização por Features](#10-organização-por-features)
11. [Decisões Arquiteturais](#11-decisões-arquiteturais)

---

## 1. Visão Geral

O Haras Manager foi projetado como uma aplicação mobile **offline-first**, com arquitetura em camadas e organização por domínios de negócio (features). A solução equilibra:

- **Experiência do usuário** — interface responsiva e operação em campo
- **Confiabilidade de dados** — sincronização robusta entre local e nuvem
- **Manutenibilidade** — código modular, testável e evolutivo
- **Escalabilidade funcional** — novos módulos sem impacto nos existentes

### Diagrama de Alto Nível

```
┌──────────────────────────────────────────────────────────────────┐
│                         DISPOSITIVO MOBILE                       │
│  ┌────────────────────────────────────────────────────────────┐  │
│  │                    CAMADA DE APRESENTAÇÃO                │  │
│  │         Pages · Widgets · Providers (Riverpod)             │  │
│  └──────────────────────────┬─────────────────────────────────┘  │
│                             │                                    │
│  ┌──────────────────────────▼─────────────────────────────────┐  │
│  │                      CAMADA DE DOMÍNIO                       │  │
│  │           Entities · Use Cases · Repository Interfaces       │  │
│  └──────────────────────────┬─────────────────────────────────┘  │
│                             │                                    │
│  ┌──────────────────────────▼─────────────────────────────────┐  │
│  │                       CAMADA DE DADOS                        │  │
│  │     Repository Impl · Data Sources · Models · Adapters       │  │
│  └──────────────┬─────────────────────────────┬─────────────────┘  │
│                 │                             │                    │
│  ┌──────────────▼──────────┐   ┌──────────────▼─────────────────┐  │
│  │     Hive (Local)        │   │   Sync Queue · Metadata        │  │
│  │   Cache · Offline       │   │   Fila de sincronização        │  │
│  └─────────────────────────┘   └────────────────────────────────┘  │
└──────────────────────────────┬───────────────────────────────────┘
                               │ Conectividade
┌──────────────────────────────▼───────────────────────────────────┐
│                        SERVIÇOS EXTERNOS                         │
│  ┌─────────────┐  ┌─────────────┐  ┌──────────────────────────┐  │
│  │  Firebase   │  │  REST APIs  │  │  Serviços de Terceiros   │  │
│  │ Auth · DB   │  │  Boletos    │  │  Notificações · Storage  │  │
│  │  Storage    │  │  OTA Update │  │                          │  │
│  └─────────────┘  └─────────────┘  └──────────────────────────┘  │
└──────────────────────────────────────────────────────────────────┘
```

---

## 2. Arquitetura em Camadas

O sistema segue uma separação rigorosa em quatro camadas principais, com dependências unidirecionais (de fora para dentro).

### Camada de Apresentação

Responsável pela interface do usuário e interação.

| Componente | Responsabilidade |
|---|---|
| **Pages** | Telas completas e navegação |
| **Widgets** | Componentes reutilizáveis de UI |
| **Providers** | Estado reativo e injeção de dependências |
| **Services (UI)** | Lógica de apresentação (formatação, PDF viewer) |

### Camada de Domínio

Núcleo de regras de negócio, independente de frameworks.

| Componente | Responsabilidade |
|---|---|
| **Entities** | Objetos de negócio puros |
| **Use Cases** | Orquestração de regras e fluxos |
| **Repository Interfaces** | Contratos de acesso a dados |

### Camada de Dados

Implementação concreta de persistência e comunicação.

| Componente | Responsabilidade |
|---|---|
| **Repository Implementations** | Orquestração local + remoto |
| **Data Sources** | Acesso direto a Hive, Firestore, APIs |
| **Models** | Representação serializável dos dados |
| **Adapters** | Conversão entre models e entities |

### Camada de Infraestrutura

Serviços transversais e integrações.

| Componente | Responsabilidade |
|---|---|
| **Sync Service** | Sincronização bidirecional |
| **Connectivity Service** | Monitoramento de rede |
| **Firebase Service** | Abstração dos serviços Firebase |
| **Notification Scheduler** | Agendamento de lembretes |

---

## 3. Clean Architecture

A Clean Architecture foi adotada como fundamento do projeto, garantindo:

### Princípios Aplicados

| Princípio | Aplicação |
|---|---|
| **Independência de frameworks** | Domínio não depende de Flutter, Firebase ou Hive |
| **Testabilidade** | Use cases testáveis sem infraestrutura |
| **Independência de UI** | Regras de negócio separadas da apresentação |
| **Independência de banco** | Repositories abstraem a fonte de dados |
| **Regra de dependência** | Camadas externas dependem das internas, nunca o contrário |

### Fluxo de Dependências

```
Presentation → Domain ← Data → Infrastructure
                  ▲
                  │
            (interfaces)
```

A camada de **Domínio** é o centro — não conhece Flutter, Firebase ou Hive. As camadas externas implementam os contratos definidos pelo domínio.

### Benefícios Observados

- Adição de novos módulos (ex.: estoque) sem refatoração massiva
- Testes unitários isolados para regras financeiras e reprodutivas
- Substituição de data sources sem impacto na UI
- Onboarding técnico facilitado pela estrutura previsível

---

## 4. Repository Pattern

Cada entidade de negócio possui um repositório que abstrae a origem dos dados (local, remoto ou ambos).

### Estrutura do Padrão

```
┌─────────────────┐
│   Use Case      │
└────────┬────────┘
         │ chama
┌────────▼────────┐
│  Repository     │  ← Interface (Domain)
│  (abstract)     │
└────────┬────────┘
         │ implementa
┌────────▼────────┐
│  Repository     │  ← Implementação (Data)
│  (concrete)     │
└────────┬────────┘
         │
    ┌────┴────┐
    ▼         ▼
┌───────┐ ┌──────────┐
│ Hive  │ │ Firestore│
└───────┘ └──────────┘
```

### Repositórios Principais

| Repositório | Entidades Gerenciadas |
|---|---|
| Animal | Cadastro, pedigree, status, mídia |
| Financeiro | Lançamentos, vendas, parcelas |
| LoteCompra | Insumos e notas fiscais |
| CustoRecorrente | Despesas fixas mensais |
| Lembrete | Alertas e agendamentos |
| Cliente | Compradores e parceiros |
| Contrato | Documentos PDF gerados |
| Lixeira | Itens excluídos (soft delete) |

### Comportamento Padrão

1. **Leitura** — prioriza cache local (Hive), atualiza via sync
2. **Escrita** — persiste localmente + enfileira para sincronização remota
3. **Exclusão** — soft delete com fila de sincronização
4. **Conflitos** — resolução por timestamp (`updatedAt`)

---

## 5. Riverpod — Gerenciamento de Estado

O **Riverpod** foi escolhido como solução de gerenciamento de estado e injeção de dependências.

### Por que Riverpod?

| Critério | Benefício |
|---|---|
| **Compile-safe** | Erros detectados em tempo de compilação |
| **Testabilidade** | Providers substituíveis em testes |
| **Reatividade** | UI atualiza automaticamente com mudanças de dados |
| **Desacoplamento** | Sem dependência de `BuildContext` para acesso a estado |
| **Composição** | Providers derivados de outros providers |

### Padrões Utilizados

| Padrão | Uso |
|---|---|
| **Provider** | Instâncias de serviços e repositórios |
| **FutureProvider** | Dados assíncronos (carregamento inicial) |
| **StateNotifierProvider** | Estado mutável complexo (dashboard, formulários) |
| **Provider.family** | Dados parametrizados (animal por ID, mês financeiro) |

### Fluxo de Dados Reativo

```
Firestore/Hive → Repository → Provider → Widget (UI)
                                    ▲
                                    │
                              User Action
```

---

## 6. Hive — Persistência Local

O **Hive** é o banco de dados NoSQL local, responsável pelo cache offline e operação sem conectividade.

### Estratégia de Uso

| Aspecto | Decisão |
|---|---|
| **Tipo** | Key-value store com boxes tipados |
| **Serialização** | Code generation para models (type adapters) |
| **Escopo** | Um box por entidade de negócio |
| **Lifecycle** | Boxes abertos na inicialização do app |

### Boxes Principais

| Box | Conteúdo |
|---|---|
| Animais | Cadastro completo do rebanho |
| Financeiro | Lançamentos e transações |
| Insumos | Lotes de compra |
| Custos Recorrentes | Despesas fixas |
| Lembretes | Alertas agendados |
| Sync Queue | Fila de operações pendentes |
| Sync Metadata | Timestamps de sincronização |
| App Update Cache | Metadados de versão OTA |

### Vantagens para o Domínio Equestre

- **Operação offline** — haras frequentemente em áreas com conectividade limitada
- **Performance** — leitura instantânea sem latência de rede
- **Resiliência** — dados preservados mesmo com falha de sync
- **Fila de sincronização** — nenhuma operação perdida por falta de rede

---

## 7. Firebase — Backend e Nuvem

O **Firebase** compõe a infraestrutura de backend, autenticação e armazenamento em nuvem.

### Serviços Utilizados

| Serviço | Função no Sistema |
|---|---|
| **Authentication** | Login com e-mail/senha e Google Sign-In |
| **Cloud Firestore** | Banco de dados NoSQL em tempo real |
| **Cloud Storage** | Armazenamento de fotos, PDFs e documentos |
| **Security Rules** | Isolamento de dados por usuário autenticado |

### Modelo de Dados na Nuvem

```
users/
  └── {userId}/
       ├── animais/
       ├── financeiro/
       ├── insumos/
       ├── lembretes/
       ├── custos_recorrentes/
       ├── lixeira/
       └── contratos/
```

Cada usuário possui **isolamento total** de dados — nenhum dado é compartilhado entre contas.

### Listeners em Tempo Real

O sistema mantém listeners ativos no Firestore para sincronização bidirecional:

- Alterações remotas refletem instantaneamente no cache local
- Alterações locais são enviadas via fila de sincronização
- Reconexão automática processa fila pendente

### Segurança

- Autenticação obrigatória para qualquer operação
- Regras de segurança garantem acesso apenas aos dados do próprio usuário
- Credenciais e configurações **não são expostas** neste repositório

---

## 8. APIs REST — Integrações Externas

Serviços externos acessados via HTTP/REST para funcionalidades especializadas.

### Integrações Implementadas

| Integração | Finalidade | Protocolo |
|---|---|---|
| **Emissão de boletos** | Geração e consulta de boletos bancários | REST + JSON |
| **Distribuição OTA** | Atualização automática do aplicativo Android | REST + APK download |
| **Compartilhamento** | Envio de documentos via WhatsApp e outras apps | Platform channels |

### Padrão de Integração

```
┌──────────────┐     HTTP/REST     ┌──────────────────┐
│  Data Source │ ◄──────────────► │  Serviço Externo  │
│  (Remote)    │                   │  (API REST)       │
└──────┬───────┘                   └──────────────────┘
       │
┌──────▼───────┐
│  Repository  │
└──────────────┘
```

### Tratamento de Erros

- Retry automático com backoff para falhas transientes
- Cache de respostas quando aplicável
- Feedback visual ao usuário em caso de indisponibilidade
- Operações enfileiradas quando offline

---

## 9. Sincronização Offline-First

A estratégia **offline-first** é um dos pilares arquiteturais do projeto.

### Fluxo de Sincronização

```
┌─────────────┐    ┌──────────────┐    ┌─────────────┐
│  Ação do    │───►│  Persiste    │───►│  Enfileira  │
│  Usuário    │    │  no Hive     │    │  Sync Queue │
└─────────────┘    └──────────────┘    └──────┬──────┘
                                              │
                    ┌─────────────────────────▼──────┐
                    │     Conectividade disponível?   │
                    └──────────┬──────────┬─────────┘
                          Sim  │          │ Não
                    ┌──────────▼──┐   ┌───▼──────────┐
                    │  Processa   │   │  Mantém na   │
                    │  fila → FB  │   │  fila local  │
                    └─────────────┘   └──────────────┘
```

### Componentes do Sync

| Componente | Função |
|---|---|
| **SyncService** | Orquestrador central de sincronização |
| **SyncQueueRepository** | Fila persistente de operações pendentes |
| **SyncMetadataRepository** | Controle de timestamps por documento |
| **ConnectivityService** | Monitor de status de rede |
| **Realtime Listeners** | Atualizações push do Firestore |

### Garantias

- Nenhuma operação do usuário é perdida por falta de conectividade
- Dados locais preservados após logout (sync retoma no próximo login)
- Indicador visual de pendências na interface
- Sincronização automática ao retomar o app ou reconectar

---

## 10. Organização por Features

O código-fonte é organizado por **domínios de negócio** (features), não por tipo técnico.

### Estrutura de uma Feature

```
features/
└── {nome_feature}/
    ├── data/
    │   ├── datasources/
    │   ├── models/
    │   └── repositories/
    ├── domain/
    │   ├── entities/
    │   ├── repositories/
    │   └── usecases/
    └── presentation/
        ├── pages/
        ├── widgets/
        └── providers/
```

### Features do Sistema

| Feature | Domínio |
|---|---|
| `animals` | Gestão de animais |
| `breeding` | Reprodução e gestações |
| `finance` | Gestão financeira |
| `supplies` | Insumos e custos |
| `clients` | Clientes e compradores |
| `contratos` | Contratos PDF |
| `sales` | Pretensões e catálogos |
| `reminders` | Lembretes e alertas |
| `reports` | Relatórios consolidados |
| `auth` | Autenticação e perfil |
| `app_update` | Atualização OTA |

### Serviços Compartilhados (Core)

| Módulo | Função |
|---|---|
| `core/routes` | Roteamento da aplicação |
| `core/theme` | Design system e tokens visuais |
| `core/services` | Sync, connectivity, notifications |
| `core/data` | Sync queue e metadata |
| `shared/widgets` | Componentes UI reutilizáveis |

---

## 11. Decisões Arquiteturais

Registro das principais decisões técnicas e suas justificativas.

| Decisão | Alternativa Considerada | Justificativa |
|---|---|---|
| **Flutter** | React Native, nativo | Performance, UI consistente, single codebase |
| **Clean Architecture** | MVC, MVVM simples | Escalabilidade e testabilidade a longo prazo |
| **Hive (local)** | SQLite, Isar | Simplicidade, performance, type-safe adapters |
| **Firestore** | PostgreSQL, MongoDB | Tempo real, offline SDK, escalabilidade automática |
| **Riverpod** | BLoC, Provider | Compile-safe, composição, menos boilerplate |
| **Offline-first** | Online-only | Operação em áreas rurais com conectividade instável |
| **Feature modules** | Layer modules | Coesão de domínio, equipes paralelas, isolamento |
| **PDF nativo** | WebView, templates HTML | Controle total de layout, performance, offline |

---

<p align="center">
  <sub>Documento de arquitetura — Haras Manager Showcase</sub>
</p>
