# Funcionalidades — Haras Manager

Documento de referência funcional do sistema, organizado por módulos de negócio. Descreve capacidades, fluxos e valor entregue — sem exposição de implementação técnica ou dados sensíveis.

---

## Índice

1. [Gestão de Animais](#1-gestão-de-animais)
2. [Reprodução](#2-reprodução)
3. [Saúde Animal](#3-saúde-animal)
4. [Financeiro](#4-financeiro)
5. [Gestão Operacional](#5-gestão-operacional)
6. [Gestão Documental](#6-gestão-documental)
7. [Dashboards](#7-dashboards)
8. [Relatórios](#8-relatórios)

---

## 1. Gestão de Animais

### Visão Geral

Módulo central do sistema. Consolida o cadastro completo de cada animal do haras, servindo como base para reprodução, saúde, finanças e comercialização.

### Funcionalidades

| Funcionalidade | Descrição |
|---|---|
| **Cadastro completo** | Apelido, nome, sexo, raça, pelagem, tipo, proprietário e criador |
| **Pedigree e genealogia** | Registro de pai, mãe, garanhão e árvore genealógica visual |
| **Registro ABQM** | Campo dedicado para identificação oficial |
| **Fotos e mídia** | Avatar, galeria de registros (fotos e vídeos) |
| **Status reprodutivo** | Prenha, confirmando gestação, vazio, castrado |
| **Histórico reprodutivo** | Linha do tempo de cruzamento, confirmação, parto e aborto |
| **Dados de aquisição** | Valor de compra, data, parcelas e entrada |
| **Dados de venda** | Comprador, valor, parcelas, data e status vendido |
| **Pretensão de venda** | Valor pretendido e data de inclusão no catálogo comercial |
| **Lixeira** | Exclusão segura com possibilidade de recuperação |
| **Busca e filtros** | Localização rápida por apelido, status e características |

### Fluxos Principais

```
Cadastro → Detalhamento → Vinculação (reprodução/saúde/financeiro) → Comercialização ou Baixa
```

### Valor de Negócio

- Fonte única de verdade sobre o rebanho
- Rastreabilidade completa do ciclo de vida de cada animal
- Base para decisões comerciais e reprodutivas

---

## 2. Reprodução

### Visão Geral

Módulo dedicado ao acompanhamento reprodutivo de éguas, gestões de cruzamentos e marcos críticos do ciclo gestacional.

### Funcionalidades

| Funcionalidade | Descrição |
|---|---|
| **Lista de gestações** | Visão consolidada de éguas em reprodução ativa |
| **Registro de cruzamento** | Data de inseminação, garanhão e método |
| **Marcos gestacionais** | Confirmação de prenhez, ultrassom, vacinas gestacionais |
| **Data estimada de parto** | Cálculo automático com base na inseminação |
| **Status visual** | Indicadores claros: confirmado, aguardando confirmação |
| **Ordenação inteligente** | Priorização por proximidade do parto |
| **Catálogo de gestações PDF** | Geração de material comercial para potros/embriões |
| **Relatório de gestações** | Consolidação para compartilhamento com equipe ou clientes |
| **Integração com animais** | Sincronização bidirecional com cadastro do animal |

### Fluxos Principais

```
Cruzamento → Confirmação de prenhez → Acompanhamento → Parto → Atualização do plantel
```

### Valor de Negócio

- Redução de perda de marcos reprodutivos críticos
- Material comercial profissional para potros e gestações
- Visibilidade sobre pipeline reprodutivo do haras

---

## 3. Saúde Animal

### Visão Geral

Módulo de acompanhamento clínico e sanitário integrado ao cadastro de cada animal, garantindo histórico médico acessível e organizado.

### Funcionalidades

| Funcionalidade | Descrição |
|---|---|
| **Exames** | Registro de exames realizados com data, tipo e resultados |
| **Procedimentos** | Histórico de procedimentos veterinários e manejo |
| **Vacinas** | Controle de vacinação com datas e tipos aplicados |
| **Timeline de saúde** | Visualização cronológica de eventos clínicos |
| **Vinculação ao animal** | Todos os registros associados ao cadastro individual |
| **Alertas via lembretes** | Integração com módulo de lembretes para próximas ações |

### Fluxos Principais

```
Evento clínico → Registro no animal → Lembrete (se aplicável) → Acompanhamento
```

### Valor de Negócio

- Histórico sanitário completo e auditável
- Suporte a decisões veterinárias informadas
- Conformidade com protocolos de manejo e bem-estar animal

---

## 4. Financeiro

### Visão Geral

Módulo de gestão financeira integrada à operação do haras, conectando receitas de vendas, despesas de aquisição, insumos e custos recorrentes.

### Funcionalidades

| Funcionalidade | Descrição |
|---|---|
| **Dashboard financeiro** | Visão consolidada por mês com KPIs principais |
| **Receitas de vendas** | Controle de animais vendidos, valores e parcelas |
| **Despesas de aquisição** | Registro de compras de animais com condições de pagamento |
| **Custos operacionais** | Integração com insumos e custos recorrentes |
| **Status de pagamentos** | Acompanhamento de parcelas pendentes e recebidas |
| **Boletos** | Integração com serviço REST para emissão e gestão |
| **Seletor de período** | Navegação mensal para análise histórica |
| **Relatório financeiro PDF** | Exportação profissional para arquivo ou compartilhamento |
| **Sincronização automática** | Vínculo entre vendas de animais e lançamentos financeiros |

### Indicadores Monitorados

- Total de receitas no período
- Total de despesas no período
- Saldo líquido
- Parcelas pendentes e recebidas
- Distribuição por categoria

### Valor de Negócio

- Visibilidade real sobre saúde financeira do haras
- Eliminação de controles financeiros paralelos
- Base para planejamento e precificação

---

## 5. Gestão Operacional

### Visão Geral

Conjunto de funcionalidades que sustentam a operação diária do haras: insumos, clientes, lembretes e rotinas administrativas.

### 5.1 Insumos e Compras

| Funcionalidade | Descrição |
|---|---|
| **Lotes de compra** | Registro de aquisições de insumos com nota fiscal |
| **Custos recorrentes** | Despesas fixas mensais (aluguel, salários, serviços) |
| **Resumo mensal** | Consolidação de gastos por período |
| **Visualização de NF** | Acesso a documentos fiscais anexados |
| **Integração financeira** | Reflexo automático no módulo financeiro |

### 5.2 Clientes

| Funcionalidade | Descrição |
|---|---|
| **Cadastro de clientes** | Dados completos de compradores e parceiros |
| **Animais por cliente** | Vínculo entre clientes e animais adquiridos |
| **Histórico comercial** | Rastreabilidade de transações por cliente |

### 5.3 Lembretes

| Funcionalidade | Descrição |
|---|---|
| **Agendamento** | Criação de lembretes com data e descrição |
| **Notificações locais** | Alertas no dispositivo para marcos próximos |
| **Badge na home** | Contador de lembretes nos próximos 3 dias |
| **Integração operacional** | Lembretes vinculados a vacinas, exames e gestações |

### 5.4 Pretensões de Venda

| Funcionalidade | Descrição |
|---|---|
| **Catálogo comercial** | Seleção de animais disponíveis para venda |
| **Configuração de catálogo** | Personalização de layout e conteúdo |
| **Geração de PDF** | Catálogo profissional com fotos, pedigree e valores |
| **Compartilhamento** | Envio via WhatsApp e outras plataformas |

### Valor de Negócio

- Operação administrativa centralizada
- Redução de esquecimentos operacionais
- Agilidade na comunicação comercial

---

## 6. Gestão Documental

### Visão Geral

Módulo responsável pela geração, armazenamento e gestão de documentos oficiais e comerciais do haras.

### Funcionalidades

| Funcionalidade | Descrição |
|---|---|
| **Contratos de compra e venda** | Geração automática de contratos PDF profissionais |
| **Cláusulas configuráveis** | Templates jurídicos adaptáveis ao tipo de negociação |
| **Parcelamento no contrato** | Detalhamento de condições de pagamento |
| **Identificação do animal** | Dados completos do equino no documento |
| **QR Code de verificação** | Identificador único por contrato |
| **Upload de contratos** | Armazenamento de contratos assinados digitalmente |
| **Catálogos PDF** | Material comercial para animais e gestações |
| **Relatórios financeiros PDF** | Demonstrativos exportáveis |
| **Armazenamento em nuvem** | Backup seguro de documentos gerados |

### Fluxos Principais

```
Negociação → Geração de contrato → Assinatura → Upload → Arquivo histórico
```

### Valor de Negócio

- Padronização documental com aparência profissional
- Redução de risco jurídico em transações
- Arquivo digital organizado e acessível

---

## 7. Dashboards

### Visão Geral

Painéis visuais que consolidam indicadores-chave para tomada de decisão rápida pelo gestor do haras.

### Dashboard Financeiro

| Indicador | Descrição |
|---|---|
| **Receitas do mês** | Total de entradas no período selecionado |
| **Despesas do mês** | Total de saídas consolidadas |
| **Saldo** | Resultado líquido do período |
| **Gráficos** | Visualização gráfica de distribuição e tendências |
| **Detalhamento** | Drill-down por categoria e lançamento |

### Dashboard Operacional (Home)

| Elemento | Descrição |
|---|---|
| **Hub de módulos** | Acesso rápido a todas as áreas do sistema |
| **Badge de lembretes** | Alertas visuais de pendências próximas |
| **Status de sincronização** | Indicador de conectividade e fila pendente |
| **Identificação do haras** | Personalização com nome e perfil do usuário |

### Valor de Negócio

- Visão executiva em tempo real
- Decisões baseadas em dados, não em estimativas
- Redução do tempo para identificar desvios operacionais

---

## 8. Relatórios

### Visão Geral

Capacidade de consolidar informações operacionais em formatos exportáveis e compartilháveis.

### Tipos de Relatório

| Relatório | Conteúdo | Formato |
|---|---|---|
| **Relatório completo de animais** | Cadastro, pedigree, saúde e status de cada animal | Texto compartilhável |
| **Relatório de gestações** | Éguas prenhas, datas e status reprodutivo | Texto / WhatsApp |
| **Relatório financeiro** | Demonstrativo mensal de receitas e despesas | PDF |
| **Catálogo de animais** | Material comercial com fotos e dados | PDF |
| **Catálogo de gestações** | Potros e embriões disponíveis | PDF |

### Funcionalidades Transversais

- Geração sob demanda
- Compartilhamento nativo (WhatsApp, e-mail, drive)
- Data e hora de geração registradas
- Formatação profissional padronizada

### Valor de Negócio

- Comunicação estruturada com equipe, clientes e parceiros
- Eliminação de relatórios manuais demorados
- Material comercial de qualidade profissional

---

## Matriz de Integração entre Módulos

```
                    ┌──────────────┐
                    │   Animais    │◄──── Cadastro central
                    └──────┬───────┘
           ┌───────────────┼───────────────┐
           ▼               ▼               ▼
    ┌────────────┐  ┌────────────┐  ┌────────────┐
    │ Reprodução │  │   Saúde    │  │ Financeiro │
    └──────┬─────┘  └──────┬─────┘  └──────┬─────┘
           │               │               │
           └───────────────┼───────────────┘
                           ▼
              ┌────────────────────────┐
              │  Documentos · Reports  │
              │  Clientes · Lembretes  │
              └────────────────────────┘
```

---

<p align="center">
  <sub>Documento funcional — Haras Manager Showcase</sub>
</p>
