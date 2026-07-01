# Roadmap — Haras Manager

Visão de evolução do produto, organizada por horizonte temporal e impacto esperado. Este documento reflete o planejamento estratégico baseado em feedback operacional, tendências do setor e oportunidades de transformação digital.

**Versão atual em produção:** `1.6.3` (app Android + painel web)

---

## Estado Atual

O Haras Manager encontra-se em **produção ativa**, com app na **Google Play Store** e painel web em [harasbroglio.com.br](https://harasbroglio.com.br).

| Módulo / Entrega | Status |
|---|---|
| Gestão de Animais | ✅ Entregue (app + web) |
| Reprodução e Gestações | ✅ Entregue (app + web) |
| Saúde Animal | ✅ Entregue (app) |
| Financeiro com Dashboard | ✅ Entregue (app + web) |
| Insumos e Custos | ✅ Entregue (app + web) |
| Clientes | ✅ Entregue (app + web) |
| Contratos PDF | ✅ Entregue (app + web) |
| Catálogos Comerciais PDF | ✅ Entregue (app + web) |
| Lembretes e Notificações | ✅ Entregue (app + web) |
| Sincronização Offline (mobile) | ✅ Entregue |
| Atualização OTA (Android) | ✅ Entregue |
| **Site institucional** | ✅ Entregue |
| **Painel web (PWA)** | ✅ Entregue |
| **Domínio harasbroglio.com.br** | ✅ Entregue |
| **Assinatura Google Play** | ✅ Entregue |
| **Cupons premium (Firestore)** | ✅ Entregue |
| **Gate de assinatura na web** | ✅ Entregue |
| **Exclusão de conta (web)** | ✅ Entregue |
| Cloud Functions (inicial) | ✅ Entregue |

---

## Entregas Recentes (v1.6.x)

| Entrega | Descrição |
|---|---|
| Painel web completo | Módulos espelhando o app, PDF no navegador |
| PWA instalável | Manifest, service worker, atalho desktop |
| Assinatura Play Store | Trial, paywall, vínculo por UID |
| Cupons web | Resgate lifetime multi-uso alinhado ao app |
| UI login/cadastro | Tema escuro, card branco, CTA Play Store |
| PDF web | Layout corrigido (capa, cabeçalho, ficha animal) |
| Gestação | Edição de cruzamento no painel |
| Perfil web | Exclusão de conta, termos, segurança |

---

## Horizonte 1 — Curto Prazo (3–6 meses)

### Dashboards Avançados

**Objetivo:** Evoluir os painéis atuais para análises mais profundas e interativas.

| Iniciativa | Descrição | Impacto |
|---|---|---|
| Drill-down financeiro | Navegação de KPI → categoria → lançamento individual | Decisões mais precisas |
| Dashboard reprodutivo | Taxa de prenhez, intervalo entre partos, produtividade | Gestão reprodutiva data-driven |
| Comparativo mensal | Gráficos de tendência com múltiplos períodos | Identificação de sazonalidade |
| Filtros avançados | Por animal, cliente, raça, status | Análises segmentadas |
| Exportação de dashboards | PDF e imagem dos painéis | Compartilhamento com stakeholders |

---

### Melhorias de UX e Performance

| Iniciativa | Descrição |
|---|---|
| Onboarding guiado | Tour interativo para novos usuários |
| Busca global | Pesquisa unificada across módulos |
| Atalhos na home | Widgets configuráveis pelo gestor |
| Otimização de sync | Redução de consumo de dados e bateria |
| Screenshots do painel web | Material visual para showcase e marketing |

---

## Horizonte 2 — Médio Prazo (6–12 meses)

### Pagamento na Web

**Objetivo:** Assinatura direta no painel, sem depender exclusivamente da Play Store.

| Aspecto | Descrição |
|---|---|
| **Gateway** | Stripe ou Mercado Pago |
| **Backend** | Cloud Functions para webhooks |
| **Entitlement** | Mesmo modelo Firestore do app |

---

### IA para Análise Operacional

**Objetivo:** Introduzir inteligência artificial para gerar insights automáticos sobre a operação do haras.

| Capacidade | Descrição | Valor |
|---|---|---|
| **Análise de custos** | Identificação automática de anomalias em despesas | Alertas proativos de overspending |
| **Recomendações reprodutivas** | Sugestões de cruzamentos baseadas em histórico | Otimização genética e comercial |
| **Assistente operacional** | Chatbot para consultas rápidas | Agilidade na operação diária |
| **Resumo executivo** | Relatório narrativo gerado por IA sobre o período | Comunicação com investidores/sócios |

**Abordagem técnica prevista:**

```
Dados operacionais → Processamento → Modelo de IA → Insights acionáveis
     (Firestore)        (Cloud Fn)      (Gemini API)     (Notificações/UI)
```

---

### Indicadores Preditivos

| Indicador | Descrição |
|---|---|
| **Projeção de fluxo de caixa** | Estimativa de receitas e despesas para próximos 3–6 meses |
| **Previsão de partos** | Calendário preditivo com base em histórico reprodutivo |
| **Custo por animal** | Projeção de custo total de manutenção por equino |
| **Alertas preditivos** | Notificações antecipadas de marcos críticos |

---

### Gestão de Estoque

| Funcionalidade | Descrição |
|---|---|
| Cadastro de produtos | Ração, medicamentos, material de manejo |
| Controle de quantidade | Entrada, saída e saldo atual |
| Alerta de estoque mínimo | Notificação quando item atinge limite |
| Vinculação com custos | Integração automática com módulo financeiro |

---

## Horizonte 3 — Longo Prazo (12–24 meses)

### Integração Financeira

**Objetivo:** Conectar o Haras Manager ao ecossistema financeiro externo.

| Integração | Descrição |
|---|---|
| **Conciliação bancária** | Importação de extratos e matching automático |
| **ERP/contabilidade** | Exportação para sistemas contábeis |
| **Nota fiscal eletrônica** | Emissão de NF-e integrada às vendas |
| **Open Finance** | Consulta de saldos e movimentações via APIs bancárias |

---

### Validação Server-Side Play Store

**Objetivo:** Verificação de assinatura via Google Play Developer API nas Cloud Functions (anti-fraude).

---

## Visão de Produto

### Posicionamento

```
         ANTES (2024)                    HOJE (2026)                    FUTURO
┌─────────────────────┐      ┌─────────────────────────┐      ┌─────────────────────────┐
│   App Mobile        │      │   Plataforma Híbrida    │      │   Plataforma Integrada  │
│   Offline-first     │ ───► │   Mobile + Web + Play   │ ───► │   Mobile + Web + IA     │
│   Gestão Operacional│      │   Assinatura + Cupons   │      │   Inteligência de Negócio│
└─────────────────────┘      └─────────────────────────┘      └─────────────────────────┘
```

### Princípios de Evolução

1. **Incremental** — cada entrega agrega valor sem disruptar operação existente
2. **Data-driven** — decisões de produto baseadas em métricas de uso e feedback
3. **Offline-first mantido** — conectividade nunca será pré-requisito no mobile
4. **Segurança primeiro** — novas integrações seguem princípios de least privilege
5. **Experiência unificada** — consistência entre app e painel web

---

## Matriz de Priorização

| Iniciativa | Impacto | Esforço | Prioridade |
|---|---|---|---|
| Dashboards avançados | Alto | Médio | 🔴 Alta |
| Pagamento na web | Alto | Médio | 🔴 Alta |
| Validação server-side Play | Alto | Médio | 🟡 Média |
| IA para análise operacional | Alto | Alto | 🟡 Média |
| Indicadores preditivos | Alto | Alto | 🟡 Média |
| Gestão de estoque | Médio | Médio | 🟡 Média |
| Integração financeira | Alto | Muito Alto | 🟢 Planejada |

---

## Métricas de Sucesso

| Métrica | Baseline | Meta (12 meses) |
|---|---|---|
| Tempo médio de cadastro de animal | ~5 min | < 3 min |
| Adoção do módulo financeiro | — | > 80% dos usuários ativos |
| Uso do painel web | — | > 40% dos usuários ativos |
| Operações offline vs. online | — | > 30% offline (mobile) |
| PDFs gerados por mês | — | > 50 por usuário ativo |
| NPS do produto | — | > 8.0 |

---

<p align="center">
  <sub>Roadmap estratégico — Haras Manager Showcase</sub>
</p>
