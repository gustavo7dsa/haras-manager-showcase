# Haras Manager

![Banner Haras Manager](./assets/screenshots/banner.png)

> **Case de Transformação Digital** — Plataforma para gestão integrada de haras (mobile + web), desenvolvida com foco em operação, processos e tomada de decisão.

[![Site](https://img.shields.io/badge/Site-harasbroglio.com.br-070708?style=flat-square)](https://harasbroglio.com.br)
[![Plataforma](https://img.shields.io/badge/Plataforma-Android%20%7C%20Web%20PWA-3DDC84?style=flat-square&logo=flutter&logoColor=white)](https://harasbroglio.com.br/painel/)
[![Arquitetura](https://img.shields.io/badge/Arquitetura-Clean%20Architecture-0A9396?style=flat-square)](./docs/architecture.md)
[![Versão](https://img.shields.io/badge/Vers%C3%A3o-1.6.3-FFA311?style=flat-square)](./docs/roadmap.md)

---

## Descrição Executiva

O **Haras Manager** (Haras Broglio) é uma solução de gestão operacional e comercial voltada ao setor equestre. O sistema centraliza informações de animais, reprodução, saúde, finanças, clientes e documentos em um único ambiente digital — **no celular e no navegador** — substituindo planilhas, anotações dispersas e controles manuais por um fluxo integrado, rastreável e orientado a indicadores.

O projeto nasceu da necessidade real de proprietários e gestores de haras que precisavam de visibilidade sobre custos, gestações, vendas e saúde do rebanho — com operação em campo, conectividade intermitente e exigência de confiabilidade dos dados.

| Canal | URL |
|---|---|
| **Site e painel web** | [harasbroglio.com.br](https://harasbroglio.com.br) |
| **Painel de gestão** | [harasbroglio.com.br/painel](https://harasbroglio.com.br/painel/) |
| **App Android** | Google Play Store |

> **Nota:** Este repositório é um **showcase de portfólio**. Não contém código-fonte, credenciais ou dados operacionais. Para detalhes técnicos e funcionais, consulte a documentação em [`/docs`](./docs).

---

## Problema que o Sistema Resolve

| Desafio Operacional | Impacto | Solução Entregue |
|---|---|---|
| Dados espalhados em planilhas e cadernos | Perda de informação e retrabalho | Cadastro unificado e sincronização em nuvem |
| Falta de visibilidade financeira | Decisões reativas e sem base | Dashboard financeiro com KPIs mensais |
| Controle manual de gestações e reprodução | Risco de perda de marcos críticos | Módulo de reprodução com marcos e alertas |
| Documentos e contratos desorganizados | Risco jurídico e comercial | Geração e armazenamento documental estruturado |
| Operação offline em áreas rurais | Interrupção do fluxo de trabalho | Cache local com sincronização inteligente |
| Gestão só no celular | Limitação para equipe e escritório | Painel web PWA com os mesmos dados em tempo real |

---

## Minha Atuação

Atuei de forma **end-to-end** na concepção, arquitetura e evolução do produto, conectando visão de negócio, engenharia de processos e desenvolvimento de software.

| Área | Responsabilidade |
|---|---|
| **Levantamento de requisitos** | Entrevistas com usuários, mapeamento de fluxos operacionais e priorização de funcionalidades |
| **Planejamento funcional** | Definição de módulos, jornadas de uso e critérios de aceite |
| **Arquitetura da solução** | Modelagem em camadas, separação de domínios e estratégia offline-first |
| **Modelagem de banco de dados** | Estruturação de entidades, relacionamentos e regras de sincronização |
| **Desenvolvimento Flutter** | App Android com interfaces, lógica de negócio e experiência mobile |
| **Desenvolvimento Web** | Site institucional, painel de gestão, PWA e geração de PDF no navegador |
| **Integrações Firebase** | Auth, Firestore, Storage, Hosting, Security Rules e Cloud Functions |
| **Monetização** | Assinatura Google Play, cupons premium e gate de acesso web |
| **Integrações REST API** | Boletos e distribuição de atualizações OTA |
| **Versionamento Git/GitHub** | Controle de versão, branches e histórico de evolução do produto |
| **Aplicação de SOLID e Clean Architecture** | Código modular, testável e organizado por features |
| **Evolução contínua do produto** | Iterações incrementais com feedback operacional |

---

## Tecnologias Utilizadas

| Camada | Tecnologias |
|---|---|
| **Frontend Mobile** | Flutter, Dart |
| **Frontend Web** | HTML/CSS/JS (painel), Firebase Hosting, PWA |
| **Gerenciamento de Estado** | Riverpod (mobile) |
| **Persistência Local** | Hive (mobile) |
| **Backend & Nuvem** | Firebase (Auth, Firestore, Storage, Hosting, Functions) |
| **Integrações** | REST API, HTTP/Dio, Google Play Billing |
| **Documentos** | Geração de PDF (Flutter + pdf-lib no navegador) |
| **Notificações** | Push locais (mobile), lembretes e notificações web |
| **Gráficos & Dashboards** | Biblioteca de charts para KPIs |
| **Controle de Versão** | Git, GitHub |
| **Qualidade** | Testes unitários, linting, análise estática |

---

## Arquitetura Utilizada

O sistema adota **Clean Architecture** no mobile, com **painel web** espelhando os mesmos módulos de negócio e compartilhando Firestore em tempo real.

```
┌──────────────────────┐     ┌──────────────────────┐
│   App Flutter        │     │   Painel Web (PWA)   │
│   Android · Offline  │     │   Hosting · Desktop  │
└──────────┬───────────┘     └──────────┬───────────┘
           │                            │
           └────────────┬───────────────┘
                        ▼
           ┌────────────────────────────┐
           │  Firebase (Auth · Firestore │
           │  · Storage · Functions)    │
           └────────────────────────────┘
```

Principais padrões aplicados:

- **Clean Architecture** — separação clara de responsabilidades no app
- **Repository Pattern** — abstração de fontes de dados
- **Offline-first** — operação local com fila de sincronização (mobile)
- **Feature-based modules** — domínios isolados e coesos
- **Single source of truth** — mesma base Firestore para app e web

Documentação completa: [`docs/architecture.md`](./docs/architecture.md) · [`docs/web-platform.md`](./docs/web-platform.md)

---

## Principais Funcionalidades

| Módulo | Descrição Resumida |
|---|---|
| 🐎 **Gestão de Animais** | Cadastro completo, pedigree, fotos, status reprodutivo e histórico |
| 🤰 **Reprodução** | Gestações, cruzamentos, marcos reprodutivos e edição de cruzamento |
| 🏥 **Saúde Animal** | Exames, procedimentos, vacinas e acompanhamento clínico |
| 💰 **Financeiro** | Dashboard, vendas, compras, parcelas, boletos e relatórios PDF |
| ⚙️ **Gestão Operacional** | Insumos, custos recorrentes, clientes e lembretes |
| 📄 **Gestão Documental** | Contratos PDF, catálogos comerciais e upload de documentos |
| 🌐 **Painel Web** | Gestão completa no navegador, instalável como PWA |
| 🔐 **Assinatura Premium** | Google Play (app) + cupons (app e web) |
| 📊 **Dashboards** | KPIs financeiros e operacionais com visão mensal |

Detalhamento completo: [`docs/features.md`](./docs/features.md)

---

## Benefícios Operacionais

- **Centralização da informação** — um único ponto de verdade para todo o haras
- **Multiplataforma** — campo no celular, escritório no navegador
- **Redução de retrabalho** — eliminação de duplicidade entre planilhas e anotações
- **Visibilidade financeira** — acompanhamento de receitas, despesas e margens por período
- **Rastreabilidade reprodutiva** — histórico completo de gestações, partos e cruzamentos
- **Operação em campo** — uso offline com sincronização automática ao reconectar
- **Agilidade comercial** — geração rápida de catálogos, contratos e propostas
- **Conformidade documental** — contratos padronizados com layout profissional
- **Proatividade operacional** — lembretes e alertas para marcos críticos

---

## Diferenciais do Projeto

1. **Produto real em produção** — app na Play Store e painel em [harasbroglio.com.br](https://harasbroglio.com.br)
2. **Arquitetura enterprise** — Clean Architecture e SOLID no mobile; painel web modular
3. **Estratégia offline-first** — fila de sincronização, cache local e listeners em tempo real
4. **Integração financeira operacional** — vínculo entre animais, vendas, compras e fluxo de caixa
5. **Geração documental avançada** — PDFs de contratos e catálogos no app e no navegador
6. **Experiência orientada ao gestor** — dashboards e KPIs pensados para tomada de decisão
7. **Monetização integrada** — assinatura Play Store com trial e cupons administráveis
8. **Visão multidisciplinar** — une engenharia, processos, gestão e tecnologia

---

## Roadmap Futuro

| Fase | Iniciativa | Objetivo |
|---|---|---|
| 🔮 Curto prazo | Dashboards avançados | Drill-down por animal, cliente e período |
| 🤖 Médio prazo | IA para análise operacional | Insights automáticos sobre custos e reprodução |
| 📈 Médio prazo | Indicadores preditivos | Projeções de fluxo de caixa e partos |
| 💳 Médio prazo | Pagamento na web | Stripe ou Mercado Pago para assinatura web |
| 📦 Longo prazo | Gestão de estoque | Controle de insumos com alertas de reposição |
| 🔗 Longo prazo | Integração financeira | Conciliação bancária e ERPs |

Roadmap detalhado: [`docs/roadmap.md`](./docs/roadmap.md)

---

## Screenshots

| Tela | Descrição |
|---|---|
| ![Home](./assets/screenshots/home.png) | **Tela inicial (app)** — hub central com acesso a todos os módulos |
| ![Animais](./assets/screenshots/animais.png) | **Gestão de animais** — cadastro, filtros e detalhes |
| ![Gestação](./assets/screenshots/gestacao.png) | **Reprodução** — acompanhamento de gestações e marcos |
| ![Financeiro](./assets/screenshots/financeiro.png) | **Dashboard financeiro** — KPIs e visão mensal |
| ![Contratos](./assets/screenshots/contratos.png) | **Gestão documental** — contratos e catálogos PDF |
| ![Relatórios](./assets/screenshots/relatorios.png) | **Exportação** — catálogos e relatórios compartilháveis |

> Painel web em [harasbroglio.com.br/painel](https://harasbroglio.com.br/painel/) — screenshot `painel-web.png` pode ser adicionado em `assets/screenshots/`.

---

## Competências Demonstradas

| Competência | Evidência no Projeto |
|---|---|
| **Gestão de Projetos** | Condução end-to-end desde requisitos até entrega e evolução |
| **Transformação Digital** | Digitalização de processos manuais em solução integrada |
| **Desenvolvimento Full Stack** | Flutter mobile + painel web + Firebase |
| **Arquitetura de Software** | Clean Architecture, SOLID e padrões de projeto |
| **Banco de Dados** | Modelagem, sincronização e persistência híbrida |
| **Integração de Sistemas** | Firebase, REST APIs, Google Play Billing |
| **DevOps / Publicação** | Firebase Hosting, Play Store, domínio customizado |
| **Melhoria Contínua** | Iterações incrementais baseadas em feedback operacional |

---

## Documentação

| Documento | Conteúdo |
|---|---|
| [`docs/features.md`](./docs/features.md) | Descrição detalhada de todos os módulos |
| [`docs/architecture.md`](./docs/architecture.md) | Arquitetura técnica e padrões aplicados |
| [`docs/web-platform.md`](./docs/web-platform.md) | Site, painel web, PWA e deploy |
| [`docs/roadmap.md`](./docs/roadmap.md) | Melhorias futuras e visão de produto |

---

## Contato

Este repositório serve como **portfólio profissional**. Para conversar sobre o projeto, oportunidades ou demonstração ao vivo, entre em contato via perfil profissional ou LinkedIn.

---

<p align="center">
  <sub>Haras Manager — Transformação digital aplicada à gestão equestre.</sub>
</p>
