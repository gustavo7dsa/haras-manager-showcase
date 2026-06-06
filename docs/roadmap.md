# Roadmap — Haras Manager

Visão de evolução do produto, organizada por horizonte temporal e impacto esperado. Este documento reflete o planejamento estratégico baseado em feedback operacional, tendências do setor e oportunidades de transformação digital.

---

## Estado Atual

O Haras Manager encontra-se em **produção ativa**, com os seguintes módulos entregues e operacionais:

| Módulo | Status |
|---|---|
| Gestão de Animais | ✅ Entregue |
| Reprodução e Gestações | ✅ Entregue |
| Saúde Animal | ✅ Entregue |
| Financeiro com Dashboard | ✅ Entregue |
| Insumos e Custos | ✅ Entregue |
| Clientes | ✅ Entregue |
| Contratos PDF | ✅ Entregue |
| Catálogos Comerciais | ✅ Entregue |
| Lembretes e Notificações | ✅ Entregue |
| Relatórios | ✅ Entregue |
| Sincronização Offline | ✅ Entregue |
| Atualização OTA (Android) | ✅ Entregue |

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

**Competências envolvidas:** Engenharia de Dados, UX, Desenvolvimento Flutter

---

### Melhorias de UX e Performance

| Iniciativa | Descrição |
|---|---|
| Onboarding guiado | Tour interativo para novos usuários |
| Busca global | Pesquisa unificada across módulos |
| Atalhos na home | Widgets configuráveis pelo gestor |
| Otimização de sync | Redução de consumo de dados e bateria |

---

## Horizonte 2 — Médio Prazo (6–12 meses)

### IA para Análise Operacional

**Objetivo:** Introduzir inteligência artificial para gerar insights automáticos sobre a operação do haras.

| Capacidade | Descrição | Valor |
|---|---|---|
| **Análise de custos** | Identificação automática de anomalias em despesas | Alertas proativos de overspending |
| **Recomendações reprodutivas** | Sugestões de cruzamentos baseadas em histórico | Otimização genética e comercial |
| **Assistente operacional** | Chatbot para consultas rápidas ("Quantas éguas prenhas?") | Agilidade na operação diária |
| **Classificação automática** | Categorização inteligente de despesas | Redução de trabalho manual |
| **Resumo executivo** | Relatório narrativo gerado por IA sobre o período | Comunicação com investidores/sócios |

**Competências envolvidas:** Machine Learning, NLP, Integração Firebase AI, Engenharia de Prompts

**Abordagem técnica prevista:**

```
Dados operacionais → Processamento → Modelo de IA → Insights acionáveis
     (Firestore)        (Cloud Fn)      (Gemini API)     (Notificações/UI)
```

---

### Indicadores Preditivos

**Objetivo:** Antecipar cenários operacionais e financeiros com base em dados históricos.

| Indicador | Descrição |
|---|---|
| **Projeção de fluxo de caixa** | Estimativa de receitas e despesas para próximos 3–6 meses |
| **Previsão de partos** | Calendário preditivo com base em histórico reprodutivo |
| **Custo por animal** | Projeção de custo total de manutenção por equino |
| **Tendência de vendas** | Análise de sazonalidade e pipeline comercial |
| **Alertas preditivos** | Notificações antecipadas de marcos críticos |

**Competências envolvidas:** Análise Preditiva, Estatística, Data Engineering

---

### Gestão de Estoque

**Objetivo:** Controle formal de insumos com alertas de reposição e rastreabilidade.

| Funcionalidade | Descrição |
|---|---|
| Cadastro de produtos | Ração, medicamentos, material de manejo |
| Controle de quantidade | Entrada, saída e saldo atual |
| Alerta de estoque mínimo | Notificação quando item atinge limite |
| Vinculação com custos | Integração automática com módulo financeiro |
| Histórico de consumo | Análise de padrões de uso por período |

**Competências envolvidas:** Engenharia de Processos, Modelagem de Dados, UX

---

## Horizonte 3 — Longo Prazo (12–24 meses)

### Aplicativo Web

**Objetivo:** Expandir o acesso para desktop e equipes administrativas.

| Aspecto | Descrição |
|---|---|
| **Plataforma** | Progressive Web App (PWA) ou Flutter Web |
| **Público-alvo** | Gestores, contadores, veterinários, equipe administrativa |
| **Funcionalidades prioritárias** | Dashboards, relatórios, gestão financeira, contratos |
| **Sincronização** | Mesma base de dados Firebase, tempo real |
| **Autenticação** | SSO com contas existentes do mobile |

**Benefícios esperados:**

- Gestão multi-dispositivo sem perda de contexto
- Telas maiores para análises complexas e edição de documentos
- Acesso para stakeholders que não operam em campo
- Redução de dependência exclusiva do smartphone

**Competências envolvidas:** Desenvolvimento Web, Responsive Design, DevOps

---

### Integração Financeira

**Objetivo:** Conectar o Haras Manager ao ecossistema financeiro externo.

| Integração | Descrição |
|---|---|
| **Conciliação bancária** | Importação de extratos e matching automático |
| **ERP/contabilidade** | Exportação para sistemas contábeis (Omie, Conta Azul) |
| **Gateway de pagamento** | Recebimento online de parcelas de vendas |
| **Nota fiscal eletrônica** | Emissão de NF-e integrada às vendas |
| **Open Finance** | Consulta de saldos e movimentações via APIs bancárias |

**Competências envolvidas:** Integração de Sistemas, Compliance Financeiro, APIs REST

---

## Visão de Produto

### Posicionamento Futuro

```
                    HOJE                          FUTURO
         ┌─────────────────────┐      ┌─────────────────────────┐
         │   App Mobile        │      │   Plataforma Integrada  │
         │   Offline-first     │ ───► │   Mobile + Web + IA     │
         │   Gestão Operacional│      │   Inteligência de Negócio│
         └─────────────────────┘      └─────────────────────────┘
```

### Princípios de Evolução

1. **Incremental** — cada entrega agrega valor sem disruptar operação existente
2. **Data-driven** — decisões de produto baseadas em métricas de uso e feedback
3. **Offline-first mantido** — conectividade nunca será pré-requisito para operação
4. **Segurança primeiro** — novas integrações seguem princípios de least privilege
5. **Experiência unificada** — consistência visual e funcional entre plataformas

---

## Matriz de Priorização

| Iniciativa | Impacto | Esforço | Prioridade |
|---|---|---|---|
| Dashboards avançados | Alto | Médio | 🔴 Alta |
| IA para análise operacional | Alto | Alto | 🟡 Média |
| Indicadores preditivos | Alto | Alto | 🟡 Média |
| Gestão de estoque | Médio | Médio | 🟡 Média |
| Aplicativo Web | Alto | Alto | 🟢 Planejada |
| Integração financeira | Alto | Muito Alto | 🟢 Planejada |

---

## Métricas de Sucesso

| Métrica | Baseline | Meta (12 meses) |
|---|---|---|
| Tempo médio de cadastro de animal | ~5 min | < 3 min |
| Adoção do módulo financeiro | — | > 80% dos usuários ativos |
| Operações offline vs. online | — | > 30% offline |
| Relatórios gerados por mês | — | > 50 por usuário ativo |
| NPS do produto | — | > 8.0 |

---

<p align="center">
  <sub>Roadmap estratégico — Haras Manager Showcase</sub>
</p>
