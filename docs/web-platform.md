# Plataforma Web — Haras Manager

Documento de referência sobre o **site** e o **painel de gestão web**, publicados em produção no domínio [harasbroglio.com.br](https://harasbroglio.com.br).

---

## Visão Geral

A expansão web complementa o app Android, permitindo gestão no escritório, em telas maiores e sem instalar aplicativo — com os **mesmos dados** sincronizados via Firebase Firestore.

| URL | Conteúdo |
|---|---|
| `https://harasbroglio.com.br/` | Landing page institucional |
| `https://harasbroglio.com.br/login.html` | Login |
| `https://harasbroglio.com.br/cadastro.html` | Cadastro de haras |
| `https://harasbroglio.com.br/painel/` | Painel de gestão (SPA) |
| `https://harasbroglio.com.br/politica-privacidade.html` | Política de privacidade |
| `https://harasbroglio.com.br/exclusao-conta.html` | Exclusão de conta |

---

## Arquitetura Web

```
┌─────────────────────────────────────────────────────────┐
│                    Firebase Hosting                       │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────────┐  │
│  │   Landing   │  │ Auth pages  │  │  Painel (SPA)   │  │
│  │   + Legal   │  │ login/cad.  │  │  ES modules JS  │  │
│  └─────────────┘  └─────────────┘  └────────┬────────┘  │
└─────────────────────────────────────────────┼───────────┘
                                              │
                    ┌─────────────────────────▼───────────┐
                    │  Firebase Auth · Firestore · Storage  │
                    │  Security Rules · Cloud Functions     │
                    └───────────────────────────────────────┘
                              ▲
                    ┌─────────┴─────────┐
                    │  App Flutter      │
                    │  Android (sync)   │
                    └───────────────────┘
```

### Stack

| Camada | Tecnologia |
|---|---|
| Hospedagem | Firebase Hosting (projeto `harasdsa-07`) |
| Domínio | `harasbroglio.com.br` com SSL automático |
| Painel | JavaScript ES modules, HTML/CSS vanilla |
| Autenticação | Firebase Auth (e-mail/senha, Google) |
| Dados | Cloud Firestore (mesma estrutura do app) |
| Arquivos | Cloud Storage (fotos, PDFs, contratos) |
| PDF no navegador | pdf-lib + fontkit (catálogos, contratos, financeiro) |
| PWA | `manifest-painel.webmanifest` + service worker |

---

## Módulos do Painel Web

O painel espelha as áreas principais do app Flutter:

| Módulo | Funcionalidades web |
|---|---|
| **Início** | Hub de acesso e resumo operacional |
| **Animais** | Cadastro, fotos, procedimentos, relatórios |
| **Gestações** | Acompanhamento reprodutivo, edição de cruzamento, PDF |
| **Vendas / Aquisições** | Histórico comercial e parcelas |
| **Clientes** | Cadastro e vínculo com animais |
| **Insumos** | Lotes de compra e notas fiscais |
| **Financeiro** | Dashboard, boletos, relatórios PDF |
| **À venda** | Pretensões e catálogo comercial |
| **Contratos** | Geração e gestão de contratos PDF |
| **Lembretes** | Agenda com notificações no navegador |
| **Perfil** | Dados do haras, exclusão de conta, segurança |

---

## PWA — Instalar no Desktop ou Celular

O painel pode ser instalado como aplicativo:

1. Acessar `https://harasbroglio.com.br/painel/`
2. No Chrome/Edge: **Instalar aplicativo** / **Instalar este site**
3. Atalho na área de trabalho ou tela inicial

Recursos PWA entregues:

- Manifest com ícone e tema
- Service worker para cache básico
- Atalho de instalação no desktop
- Notificações de lembretes (quando permitido pelo navegador)

---

## Assinatura e Acesso Web

O painel exige **assinatura premium** ou **cupom válido**, alinhado ao modelo do app:

| Canal | Como obter acesso |
|---|---|
| **App Android** | Assinatura Google Play (`haras_premium`) com trial |
| **Web** | Cupom resgatado no painel (Firestore) |
| **Ambos** | Mesma conta Firebase — dados sincronizados |

O gate de assinatura (`subscription-gate-web`) bloqueia módulos até validação do entitlement.

---

## Geração de PDF na Web

Catálogos, contratos e relatórios financeiros são gerados **no navegador**, espelhando o layout do app Flutter:

- Módulo `catalog-pdf/` com widgets reutilizáveis (capa, ficha animal, chrome)
- Embutimento de fotos via Firebase Storage (CORS configurado)
- Upload do PDF gerado para Storage com link de compartilhamento

---

## Site Institucional e Auth

### Landing e páginas legais

- Página inicial com apresentação do produto
- Política de privacidade e exclusão de conta (exigências Play Store)
- Tema escuro com card branco nas telas de login/cadastro

### Experiência mobile no site

- Banner para download do app Android na Google Play
- CTA Play Store nas páginas de autenticação
- `theme-color` e `color-scheme` otimizados para mobile

---

## Deploy e Infraestrutura

| Item | Detalhe |
|---|---|
| **Hosting** | `firebase deploy --only hosting` |
| **Regras** | Firestore e Storage com isolamento por `uid` |
| **CORS Storage** | Necessário para fotos nos PDFs web |
| **Cache** | Headers `no-cache` em assets críticos do PDF |
| **Functions** | Cloud Functions para operações server-side |

---

## Decisões de Produto

| Decisão | Justificativa |
|---|---|
| Painel em JS vanilla (não Flutter Web) | Performance, bundle leve, iteração rápida no desktop |
| Mesmo Firestore do app | Single source of truth, sync em tempo real |
| PWA em vez de app nativo desktop | Instalação simples, sem loja de aplicativos |
| PDF no cliente | Geração offline-capable, sem custo de servidor por documento |
| Cupom na web | Acesso administrativo sem depender da Play Store |

---

<p align="center">
  <sub>Plataforma web — Haras Manager Showcase</sub>
</p>
