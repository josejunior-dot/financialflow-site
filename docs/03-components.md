# 03 - Componentes (Secoes do Site)

> Documentacao de todas as secoes visuais do site FinancialFlow.
> O projeto e um HTML estatico (`index.html`), entao "componentes" sao as secoes do layout.

---

## Indice

1. [Mobile Menu](#1-mobile-menu)
2. [Navbar](#2-navbar)
3. [Hero](#3-hero)
4. [Social Proof](#4-social-proof)
5. [Problema vs Solucao](#5-problema-vs-solucao)
6. [Como Funciona](#6-como-funciona)
7. [Features Grid](#7-features-grid)
8. [Bot + Multicalculo (Timeline)](#8-bot--multicalculo-timeline)
9. [Pipeline](#9-pipeline)
10. [Multicalculo Visual](#10-multicalculo-visual)
11. [Performance](#11-performance)
12. [Inteligencia do Lead](#12-inteligencia-do-lead)
13. [Integracoes](#13-integracoes)
14. [Metricas](#14-metricas)
15. [Consulte seu Agente Comercial (Solicitar Proposta)](#15-consulte-seu-agente-comercial-solicitar-proposta)
16. [FAQ](#16-faq)
17. [CTA](#17-cta)
18. [Footer](#18-footer)

---

## 1. Mobile Menu

**Elemento:** `<div class="mobile-menu" id="mobileMenu">`

Menu fullscreen para dispositivos moveis. Fica oculto por padrao (`transform: translateX(100%)`) e desliza da direita quando ativado via classe `.active`.

| Classe | Descricao |
|---|---|
| `.mobile-menu` | Container fullscreen fixo, fundo escuro com `backdrop-filter: blur(20px)`, z-index 999. Flexbox centralizado vertical/horizontal. |
| `.mobile-menu.active` | `transform: translateX(0)` — exibe o menu com transicao suave. |
| `.mobile-menu-close` | Botao X no canto superior direito. |

**Links:** Replica os mesmos links da navbar desktop (Como funciona, Funcionalidades, Bot + Multicalculo, Pipeline, Inteligencia, Planos, FAQ). Cada link chama `closeMobileMenu()` ao clicar.

**Comportamento JS:**
- `toggleMobileMenu()` — alterna classe `.active`
- `closeMobileMenu()` — remove classe `.active`

---

## 2. Navbar

**Elemento:** `<nav class="navbar" id="navbar">`

Barra de navegacao fixa no topo (`position: fixed`, `z-index: 1000`).

| Classe | Descricao |
|---|---|
| `.navbar` | Fixa no topo, padding 16px, transicao suave de 0.4s. |
| `.navbar.scrolled` | Ativada via JS quando `scrollY > 50`. Fundo branco com blur (`backdrop-filter: blur(20px) saturate(180%)`), borda inferior, sombra, padding reduzido (10px). |
| `.navbar-brand` | Logo com flexbox, gap 10px, font-weight 800. Usa `<img>` com classe `.brand-logo` (height 200px com margin negativo para overflow). |
| `.navbar-links` | Lista horizontal de links (`display: flex`, gap 28px). |
| `.btn-nav` | Botao arredondado (border-radius 50px). |
| `.btn-nav-primary` | Variante verde (cor primaria). |
| `.navbar-mobile-toggle` | Hamburguer menu, oculto em desktop (`display: none`), visivel em `<= 768px`. Tres `<span>` formam as linhas. |

**Comportamento de scroll:**
- Sem scroll: Logo branca (filtro `brightness(0) invert(1)`), links brancos semi-transparentes.
- Com scroll (`.scrolled`): Logo original, links cinza (`var(--muted)`), hover verde.

**Responsivo:**
- `<= 768px`: `.navbar-links` oculto, `.navbar-mobile-toggle` visivel.

---

## 3. Hero

**Elemento:** `<section class="hero">`

Secao principal (above the fold), ocupa `min-height: 100vh`.

### Estrutura

| Classe | Descricao |
|---|---|
| `.hero` | Background gradient animado (verde escuro -> azul escuro), `background-size: 400% 400%`, animacao `gradient-shift` 15s. Pseudo-elemento `::before` com radial gradients decorativos. |
| `.hero-grid` | Grid decorativo de fundo (linhas 60x60px em branco 3% opacidade). |
| `.hero-particles` | 4 particulas (`.particle-1` a `.particle-4`) com animacao `float` e parallax via mousemove. |
| `.hero .container` | Grid 2 colunas (`1fr 1fr`), gap 60px, padding-top 100px. |

### Coluna Esquerda (`.hero-content`)

| Classe | Descricao |
|---|---|
| `.hero-badge` | Badge pill "Powered by IA + Multicalculo" com dot pulsante (`pulse-glow`). |
| `.hero h1` | Titulo responsivo `clamp(2.4rem, 4.5vw, 3.6rem)`, font-weight 900, branco. `.highlight` aplica gradient text (verde -> roxo). |
| `.hero-subtitle` | Subtitulo branco 75% opacidade, 1.15rem. |
| `.hero-actions` | Dois botoes lado a lado. |
| `.btn-hero-primary` | Botao verde gradient com sombra verde. Hover: translateY(-3px). |
| `.btn-hero-outline` | Botao transparente com borda branca 25%. |
| `.hero-stats` | 3 metricas em linha (< 1 min, 6+, 9 perfis). |
| `.hero-stat-value` | 1.8rem, font-weight 800, branco. |
| `.hero-stat-label` | 0.8rem, branco 55%. |
| `.hero-stat-sub` | 0.7rem, cor primaria clara. |

### Coluna Direita (`.hero-visual`)

| Classe | Descricao |
|---|---|
| `.hero-phone` | Mockup de celular (300x600px, border-radius 36px, fundo #111). Animacao `floatSlow` 6s. Sombra com brilho verde. |
| `.phone-notch` | Notch superior 120x28px. |
| `.phone-screen` | Tela do celular com fundo WhatsApp (#ECE5DD). |
| `.phone-header` | Header estilo WhatsApp (fundo #075E54) com avatar "FF" e nome "FinancialFlow Bot". |
| `.chat-messages` | Container das mensagens com gap 6px. |
| `.chat-msg-bot` | Mensagem do bot (fundo branco, alinhada a esquerda). |
| `.chat-msg-user` | Mensagem do usuario (fundo verde WhatsApp #DCF8C6, alinhada a direita). |
| `.chat-msg-ia` | Mensagem especial da IA (gradient verde/roxo claro, borda verde, badge "Multicalculo"). |
| `.msg-delay-1` a `.msg-delay-7` | Delays de animacao (0.3s a 4.6s) para efeito de digitacao sequencial. |

**Mensagens do chat (6 mensagens):**
1. Bot: Saudacao + termos de privacidade
2. User: "Aceito! Quero investir"
3. Bot: Pergunta valor e perfil
4. User: "50 mil, sou moderado"
5. IA: Resultado do Multicalculo (CDB BTG 103%, LCI Inter 94%, Tesouro IPCA+ 6.2%)
6. Bot: Assessor Ricardo ja tem o comparativo

**Chat replay:** `setInterval(replayChat, 15000)` — reinicia animacoes a cada 15s.

### Floating Cards

| Classe | Descricao |
|---|---|
| `.hero-float-card` | Cards flutuantes posicionados absolutamente ao redor do phone. Fundo branco 12% com blur, borda branca 20%. Animacao `floatSlow`. |
| `.float-card-1` | Top 60px, right -30px — "Multicalculo / 6 cotacoes" |
| `.float-card-2` | Bottom 100px, left -40px — "Perfil detectado / Moderado" |
| `.float-card-3` | Top 220px, left -60px — "Lead qualificado / Score 87" |

**Responsivo:**
- `<= 1024px`: `.hero-visual` oculto (`display: none`), grid vira 1 coluna, conteudo centralizado.
- `<= 768px`: Botoes empilhados verticalmente, stats empilhados.

---

## 4. Social Proof

**Elemento:** `<div class="social-proof">`

Secao de prova social com quotes e metricas. Nao e `<section>` (padding menor: 48px).

| Classe | Descricao |
|---|---|
| `.social-proof` | Background branco, padding 48px, borda inferior. |
| `.proof-label` | Label uppercase cinza centralizado. |
| `.proof-cards` | Flexbox com gap 24px, centralizado. |
| `.proof-card` | Card com fundo `var(--bg)`, borda, border-radius 16px, max-width 360px. Hover: sombra + translateY(-2px). |
| `.proof-quote` | Texto italico 0.9rem. |
| `.proof-author` | Flexbox com avatar circular (36px) + nome e cargo. |
| `.proof-avatar` | Circulo com borda verde, fundo verde claro, iniciais em verde. |
| `.proof-metrics` | 4 metricas em linha com gap 32px. |
| `.proof-metric-value` | 1.6rem, font-weight 800, cor primaria. |

**Conteudo:**
- 2 quotes (Ricardo M. - Assessor XP, Camila S. - Gerente SaltusCon)
- 4 metricas: < 1 min, ~100%, 6+, 9

---

## 5. Problema vs Solucao

**Elemento:** `<div class="problem-section">`

Grid de 2 colunas comparando CRM tradicional vs FinancialFlow.

| Classe | Descricao |
|---|---|
| `.problem-section` | Background branco, padding 80px. |
| `.problem-grid` | Grid 2 colunas, gap 40px. |
| `.problem-col` | Card arredondado com padding 36px. |
| `.problem-col-old` | Fundo vermelho claro (#FFF5F5), borda vermelha. |
| `.problem-col-new` | Fundo verde claro (#ECFDF5), borda verde. |
| `.problem-col-tag` | Badge pill com icone (X vermelho ou Check verde). |
| `.problem-list` | Lista sem marcadores com icones. |
| `.problem-punchline` | Texto centralizado de fechamento abaixo do grid. |

**Conteudo:**
- Coluna "CRM Tradicional": 6 problemas com icones X vermelhos
- Coluna "FinancialFlow": 6 solucoes com icones check verdes
- Punchline: "A diferenca? No FinancialFlow, o dado nasce da conversa..."

**Responsivo:**
- `<= 1024px`: Mantem 2 colunas.
- `<= 768px`: 1 coluna (empilha).

---

## 6. Como Funciona

**Elemento:** `<section class="how-it-works" id="como-funciona">`

3 passos com setas entre eles.

| Classe | Descricao |
|---|---|
| `.how-it-works` | Background `var(--bg)` (cinza claro). |
| `.how-grid` | Grid 3 colunas, gap 32px. |
| `.how-step` | Card branco centralizado com borda, position relative. Hover: sombra + translateY(-4px). |
| `.how-number` | Circulo verde 48px com numero branco, font-weight 800. |
| `.how-step-title` | 1.15rem, font-weight 700. |
| `.how-step-desc` | 0.9rem, cor muted. |
| `.how-arrow` | Seta `→` posicionada absolutamente (top 50%, right -24px). |

**3 passos:**
1. Lead manda mensagem (bot responde, LGPD, qualificacao via WhatsApp)
2. Multicalculo roda (simulacao paralela em XP, BTG, Inter, Nubank)
3. Assessor so fecha (briefing completo + comparativo + perfil)

**Responsivo:**
- `<= 1024px`: Mantem 3 colunas, setas ocultas.
- `<= 768px`: 1 coluna.

---

## 7. Features Grid

**Elemento:** `<section class="features" id="features">`

Grid de 6 cards de funcionalidades.

| Classe | Descricao |
|---|---|
| `.features` | Background branco. |
| `.features-header` | Centralizado com label, titulo e subtitulo. |
| `.features-grid` | Grid 3 colunas, gap 24px. |
| `.feature-card` | Card branco com borda, border-radius 16px, padding 32px. Pseudo-elemento `::before` cria barra superior gradient (verde -> roxo) que aparece no hover via `scaleX`. |
| `.feature-icon` | Caixa 52px com border-radius 12px, fundo verde claro, icone verde. |
| `.feature-title` | 1.15rem, font-weight 700. |
| `.feature-desc` | 0.9rem, cor muted. |

**6 cards:**
1. Bot WhatsApp com IA (icone: message-square-text)
2. Multicalculo (icone: calculator)
3. Pipeline Automatico (icone: columns-3)
4. 9 Perfis Comportamentais (icone: scan-face)
5. Automacoes Inteligentes (icone: repeat)
6. Gestao de Performance (icone: bar-chart-3)

**Hover:** Borda transparente, sombra grande, translateY(-4px), barra gradient superior aparece.

**Responsivo:**
- `<= 1024px`: 2 colunas.
- `<= 768px`: 1 coluna.

---

## 8. Bot + Multicalculo (Timeline)

**Elemento:** `<section class="bot-section" id="bot">`

Timeline vertical com 6 estacoes (nao 5 como inicialmente estimado — sao 6 no HTML).

| Classe | Descricao |
|---|---|
| `.bot-section` | Background gradient vertical (`var(--bg)` -> branco). Circulo decorativo verde no canto superior direito. |
| `.bot-grid` | Grid 2 colunas, gap 80px. Coluna esquerda: texto. Coluna direita: timeline. |
| `.bot-flow` | Container flexbox vertical. |
| `.bot-step` | Flexbox horizontal (icone + conteudo), padding 20px vertical. |
| `.bot-step-dot` | Quadrado arredondado 48px (border-radius 14px), fundo verde claro, icone verde. |
| `.bot-step-line` | Linha vertical conectora (2px, gradient verde -> transparente), posicionada absolutamente. Oculta no ultimo step. |
| `.bot-step-title` | 1rem, font-weight 700. |
| `.bot-step-desc` | 0.85rem, cor muted. |

**6 estacoes da timeline:**
1. Consentimento LGPD (icone: shield-check)
2. Qualificacao pela Conversa (icone: message-circle)
3. Match de Produtos (icone: search)
4. Multicalculo Automatico (icone: calculator)
5. Handoff com Briefing Completo (icone: user-check)
6. Follow-up + Reaplicacao (icone: refresh-cw)

**Responsivo:**
- `<= 1024px`: 1 coluna (texto em cima, timeline embaixo).

---

## 9. Pipeline

**Elemento:** `<section class="pipeline-section" id="pipeline">`

Kanban visual com 6 colunas representando o funil de vendas.

| Classe | Descricao |
|---|---|
| `.pipeline-section` | Background branco. |
| `.pipeline-visual` | Flexbox horizontal com gap 16px, overflow-x auto (scroll horizontal). |
| `.pipeline-col` | Coluna do kanban, min-width 150px, fundo `var(--bg)`, border-radius 16px. |
| `.pipeline-col-header` | Flexbox com titulo e badge de contagem. |
| `.pipeline-col-title` | 0.75rem, uppercase, font-weight 700. Cada coluna tem cor diferente (inline style). |
| `.pipeline-col-count` | Badge numerico 24px, fundo verde claro. |
| `.pipeline-card` | Card de lead (fundo branco, borda, border-radius 10px). Hover: sombra + translateY(-2px). `cursor: grab`. |
| `.pipeline-card-name` | Nome do lead, 0.8rem, font-weight 600. |
| `.pipeline-card-info` | Info do investimento, 0.7rem, cor muted. |
| `.pipeline-card-temp` | Badge de temperatura (pill). |
| `.temp-hot` | Vermelho claro — "Quente". |
| `.temp-warm` | Laranja claro — "Morno". |
| `.temp-cold` | Azul claro — "Frio". |

**6 colunas:**
1. **Novo** (verde, 5 leads) — Marcos A. (Quente), Julia P. (Morno)
2. **Qualificado** (roxo, 3 leads) — Ana C. (Quente)
3. **Simulacao** (dourado, 2 leads) — Carlos M. (Quente)
4. **Negociacao** (laranja, 2 leads) — Pedro L. (Quente)
5. **Contrato** (verde, 1 lead) — Lucia F. (Quente)
6. **Ativo** (verde escuro, 8 leads) — Roberto C. (Investindo)

**Responsivo:**
- `<= 768px`: Flex-direction column (empilha verticalmente).

---

## 10. Multicalculo Visual

**Elemento:** `<section class="multicalc-visual" id="multicalculo">`

Dashboard comparativo de instituicoes + lista de features.

| Classe | Descricao |
|---|---|
| `.multicalc-visual` | Background branco. |
| `.multicalc-grid` | Grid 2 colunas, gap 80px. |
| `.mc-dashboard` | Container do dashboard, fundo `var(--bg)`, border-radius 24px, borda. |
| `.mc-dash-header` | Flexbox com titulo ("Multicalculo | CDB R$ 50.000 / 12 meses") e badge "Moderado". |
| `.mc-result` | Lista vertical de cards de resultado. |
| `.mc-result-card` | Card de instituicao (flexbox, borda, fundo branco). Hover: sombra + translateY(-2px). |
| `.mc-result-card.best` | Destaque: borda verde, background gradient verde claro. |
| `.mc-result-logo` | Quadrado 36px com iniciais da instituicao (cores inline). |
| `.mc-result-rate` | Valor do rendimento, 1rem, font-weight 800. |
| `.mc-best-tag` | Badge "Melhor" (pill verde, texto branco). |
| `.mc-ai-tag` | Texto centralizado com recomendacao da IA (cor roxa). |

**4 cards de resultado:**
1. **BTG Pactual** (melhor) — CDB 103% CDI, R$ 5.248 liquido
2. **Banco Inter** — CDB 102% CDI, R$ 5.196
3. **Nubank** — CDB 100% CDI, R$ 5.094
4. **XP Investimentos** — LCI 93% CDI, R$ 5.310 (isento IR)

**Recomendacao IA:** "LCI XP (isencao de IR compensa no prazo de 12 meses)"

**Coluna direita:** 4 features reutilizando classes `.intel-feature`:
1. Cotacao em Paralelo (icone: zap)
2. Rentabilidade Liquida Real (icone: percent)
3. FGC e Seguranca (icone: shield-check)
4. IA que Recomenda (icone: brain)

**Responsivo:**
- `<= 1024px`: 1 coluna.

---

## 11. Performance

**Elemento:** `<section class="performance">`

Secao dark com 4 cards de diferenciais.

| Classe | Descricao |
|---|---|
| `.performance` | Background gradient escuro (verde -> azul -> roxo), cor branca. Pseudo-elemento com radial gradients decorativos (dourado e roxo). |
| `.performance-content` | Container com z-index 2 (acima dos pseudo-elementos). |
| `.performance-header` | Centralizado. Label em dourado (`var(--gold)`), subtitulo branco 65%. |
| `.section-title` com `.text-gradient-gold` | Titulo com gradient dourado -> laranja. |
| `.perf-grid` | Grid 4 colunas, gap 20px. |
| `.perf-card` | Card com fundo branco 4%, borda branca 8%, border-radius 16px, centralizado. Hover: fundo branco 8%, translateY(-4px). |
| `.perf-icon` | Caixa 52px, fundo branco 6%, icone branco 90%. |
| `.perf-title` | 0.95rem, font-weight 700. |
| `.perf-desc` | 0.75rem, branco 45%. |

**4 cards:**
1. Resposta < 1 min (icone: clock)
2. Cotacao Automatica (icone: calculator)
3. Handoff Completo (icone: user-check)
4. Reaplicacao 30/60/90d (icone: refresh-cw)

**Responsivo:**
- `<= 1024px`: 2 colunas.
- `<= 768px`: 2 colunas (mantem).
- `<= 480px`: 1 coluna.

---

## 12. Inteligencia do Lead

**Elemento:** `<section class="intelligence" id="inteligencia">`

Dashboard de score + barras de progresso + features.

| Classe | Descricao |
|---|---|
| `.intelligence` | Background `var(--bg)`. |
| `.intelligence-grid` | Grid 2 colunas, gap 80px. |

### Dashboard (coluna esquerda)

| Classe | Descricao |
|---|---|
| `.intel-dashboard` | Card branco, border-radius 24px, borda, padding 32px. |
| `.intel-score` | Flexbox: circulo de score + detalhes. |
| `.score-circle` | SVG circular 100x100px. |
| `.score-circle-bg` | Circulo de fundo (cinza, stroke-width 8). |
| `.score-circle-fill` | Circulo preenchido com gradient (verde -> roxo). `stroke-dasharray: 251.2`, `stroke-dashoffset: 50.24` (~80% preenchido). Animacao `dash`. |
| `.score-value` | Numero "87" centralizado no circulo, 1.5rem, font-weight 800. |
| `.score-tags` | Tags pill: "Quente" (vermelho), "Moderado" (roxo). |
| `.intel-bars` | 3 barras de progresso verticais. |
| `.intel-bar-track` | Track cinza 8px com border-radius. |
| `.intel-bar-fill` | Preenchimento com transicao 1.5s. |
| `.bar-green` | Gradient verde (Engajamento: 85%). |
| `.bar-purple` | Gradient roxo (Urgencia: 72%). |
| `.bar-gold` | Gradient dourado (Fit produto: 93%). |

### Features (coluna direita)

Reutiliza classes `.intel-feature`, `.intel-feature-icon`, `.intel-feature-title`, `.intel-feature-desc`.

**4 features:**
1. 9 Perfis Comportamentais (icone: scan-face)
2. Temperatura em Tempo Real (icone: thermometer)
3. Educacao Financeira Integrada (icone: graduation-cap)
4. Briefing Automatico (icone: file-text)

**Responsivo:**
- `<= 1024px`: 1 coluna.

---

## 13. Integracoes

**Elemento:** `<section class="integrations" id="integracoes">`

4 cards de integracoes + barra de seguranca.

| Classe | Descricao |
|---|---|
| `.integrations` | Background branco. |
| `.integrations-header` | Centralizado. |
| `.integ-grid` | Grid 4 colunas, gap 20px. |
| `.integ-card` | Card com fundo `var(--bg)`, borda, centralizado. Hover: sombra + translateY(-2px). |
| `.integ-icon` | Caixa 52px, fundo verde claro, icone verde. |
| `.integ-name` | 0.9rem, font-weight 600. |
| `.integ-desc` | 0.75rem, cor muted. |

**4 cards:**
1. WhatsApp Cloud API (icone: message-circle) — "API oficial da Meta"
2. OpenAI GPT-4 (icone: sparkles) — "Dados sensiveis mascarados"
3. Banco Central BCB (icone: landmark) — "Selic, CDI, IPCA e TR em tempo real"
4. Push Notifications (icone: bell) — "Alertas pro assessor"

### Barra de Seguranca

| Classe | Descricao |
|---|---|
| `.security-bar` | Barra horizontal com fundo `var(--bg)`, borda, border-radius 16px, flexbox centralizado. |
| `.security-item` | Item com icone check verde + texto. |

**5 itens:** LGPD Compliance, Consentimento obrigatorio, Criptografia AES-256, Dados no Brasil (sa-east-1), RBAC por funcao.

**Responsivo:**
- `<= 1024px`: 2 colunas.
- `<= 768px`: 2 colunas.
- `<= 480px`: 1 coluna.

---

## 14. Metricas

**Elemento:** `<section class="metrics">`

4 cards de metricas com numeros grandes.

| Classe | Descricao |
|---|---|
| `.metrics` | Background `var(--bg)`, padding 80px (menor que secoes padrao). |
| `.metrics-grid` | Grid 4 colunas, gap 24px. |
| `.metric-card` | Card branco, borda, border-radius 16px, centralizado. Hover: sombra + translateY(-4px). |
| `.metric-value` | 2.5rem, font-weight 900. Classe `.text-gradient` aplica gradient verde -> roxo. |
| `.metric-label` | 0.85rem, cor muted. |
| `.metric-sublabel` | 0.7rem, cor primaria, font-weight 600. |

**4 metricas:**
1. < 1 min — Tempo medio de resposta — "24/7 com o bot ativo"
2. ~100% — Leads respondidos — "Com automacao ativa"
3. 6+ — Instituicoes — "XP, BTG, Inter, Nubank..."
4. 9 — Automacoes ativas — "Follow-up, reaplicacao, cross-sell"

**Responsivo:**
- `<= 1024px`: 2 colunas.
- `<= 768px`: 2 colunas.
- `<= 480px`: 1 coluna.

---

## 15. Consulte seu Agente Comercial (Solicitar Proposta)

**Elemento:** `<section class="pricing-section" id="precos">`

Formulario B2B de solicitacao de proposta comercial. Substituiu a antiga secao de planos/lista de espera. O modelo agora e "Consulte seu agente comercial" — nao ha planos fixos exibidos no site.

| Classe | Descricao |
|---|---|
| `.pricing-section` | Background branco, padding 100px. |
| `.pricing-gate` | Card centralizado max-width 600px, fundo `var(--bg)`, border-radius 24px, padding 40px. |
| `.pricing-gate-icon` | Icone 64px com gradient (verde -> roxo). Icone: clock. |
| `.pricing-gate-form` | Formulario vertical (flexbox column, gap 12px), max-width 400px. |
| `.pricing-gate-input` | Input com borda, border-radius 10px, focus: borda verde. |
| `.pricing-gate-select` | Select estilizado igual ao input. |
| `.btn-pricing-gate` | Botao gradient (verde -> roxo), border-radius 50px. Hover: translateY(-2px), sombra verde. Texto: "Solicitar proposta". |
| `.pricing-gate-benefits` | 3 beneficios em linha com icones check. |
| `.pricing-gate-note` | Nota de privacidade em cinza. |

**Campos do formulario:**
1. Nome (text, required)
2. Email (email, required)
3. WhatsApp com DDD (tel, required)
4. Tamanho da equipe (select: autonomo, pequena, media, grande, escritorio)

**Beneficios:** Sem compromisso, Proposta personalizada, Atendimento consultivo.

**Comportamento JS (`submitWaitlist`):**
- Previne submit padrao
- Loga dados no console
- Substitui conteudo do gate por mensagem de confirmacao ("Proposta solicitada! Um consultor vai entrar em contato pelo WhatsApp.")
- Recria icones Lucide apos substituicao do HTML
- **Integracao futura:** Quando o ComercialFlow (CRM B2B da SaltusCon) estiver em producao, os dados do formulario serao enviados via `POST /api/leads` para o ComercialFlow, que acionara o ComercialBot via WhatsApp para engajar o lead

**Fluxo B2B completo (futuro):**
1. Visitante preenche formulario no site
2. Dados enviados ao ComercialFlow via API (`POST /api/leads`)
3. ComercialBot engaja o lead via WhatsApp (8 stations: CONSENT → WELCOME → DISCOVERY → FILTER → VALUE → CLOSING → HANDOFF → FOLLOW_UP)
4. Pipeline avanca automaticamente (PROSPECCAO → QUALIFICACAO → REUNIAO → PROPOSTA → NEGOCIACAO → GANHO)
5. Consultor recebe briefing completo e assume o atendimento
6. Proposta e contrato gerados no ComercialFlow

**ComercialFlow:** https://github.com/josejunior-dot/comercialflow — CRM B2B com Next.js 16, React 19, Prisma 7, PostgreSQL, bot WhatsApp, propostas comerciais, contratos.

### Planos ocultos (`.pricing-revealed`)

Existem classes preparadas para 4 cards de planos (`.pricing-cards`, `.pricing-card`, `.pricing-card.featured`), mas o container `.pricing-revealed` fica com `display: none` e nao ha logica no JS atual para revela-lo. Com a mudanca para modelo B2B, os planos fixos foram descartados em favor de propostas personalizadas via agente comercial.

---

## 16. FAQ

**Elemento:** `<section class="faq" id="faq">`

Accordion com 6 perguntas.

| Classe | Descricao |
|---|---|
| `.faq` | Background `var(--bg)`. |
| `.faq-header` | Centralizado. |
| `.faq-grid` | Container vertical max-width 800px, centralizado, gap 12px. |
| `.faq-item` | Card branco com borda, border-radius 10px. Hover: borda verde. |
| `.faq-question` | Botao full-width, flexbox space-between, 0.95rem, font-weight 600. Hover: cor verde. |
| `.faq-chevron` | Icone chevron-down com rotacao 180deg quando `.open`. |
| `.faq-answer` | Conteudo oculto (`display: none`). Visivel quando `.faq-item.open`. |

**Comportamento JS (`toggleFaq`):**
- Fecha todos os outros itens (accordion single-open)
- Alterna classe `.open` no item clicado

**6 perguntas:**
1. O que e o Multicalculo?
2. Minha equipe precisa preencher formularios?
3. O bot consegue educar leads que nao entendem de investimentos?
4. Como funciona a reaplicacao automatica?
5. A IA fala errado ou inventa informacao?
6. E seguro em relacao a LGPD?

---

## 17. CTA

**Elemento:** `<section class="cta-section" id="cta">`

Secao dark de chamada final.

| Classe | Descricao |
|---|---|
| `.cta-section` | Background gradient escuro (verde -> verde medio -> roxo), padding 120px. Pseudo-elemento com radial gradients decorativos (verde e roxo). |
| `.cta-content` | Centralizado, z-index 2, max-width 700px. |
| `.cta-content h2` | Titulo responsivo `clamp(2rem, 4vw, 3rem)`, branco, font-weight 900. Span com gradient inline (verde -> roxo). |
| `.cta-content p` | Subtitulo branco 65%, 1.1rem. |
| `.cta-note` | Nota final branco 40%, 0.8rem. |

**Conteudo:**
- Titulo: "Chega de CRM que ninguem usa. Garanta seu lugar na fila."
- Subtitulo: Fase final de desenvolvimento, lista de espera.
- Botao: "Entrar na lista de espera" (link para #precos, reutiliza `.btn-hero-primary`).
- Nota: "Sem compromisso . Condicoes de lancamento . Acesso antecipado"

---

## 18. Footer

**Elemento:** `<footer class="footer">`

Rodape com 4 colunas e barra inferior.

| Classe | Descricao |
|---|---|
| `.footer` | Background escuro (#020a06), padding 60px top 30px bottom, cor branca 50%. |
| `.footer-grid` | Grid 4 colunas (`2fr 1fr 1fr 1fr`), gap 48px. |
| `.footer-brand` | Primeira coluna (2fr): logo + descricao. Logo branca via `filter: brightness(0) invert(1)`. |
| `.footer-col-title` | Titulo de coluna, 0.8rem, uppercase, branco 70%. |
| `.footer-links` | Lista vertical de links, gap 10px. Links brancos 40%, hover verde. |
| `.footer-bottom` | Barra inferior com borda top sutil. Flexbox space-between. |
| `.footer-social` | 3 icones sociais (LinkedIn, Instagram, YouTube) em quadrados 36px com border-radius 10px. Hover: fundo verde, icone branco. |

**4 colunas:**
1. **Brand** (2fr): Logo + "O CRM com Multicalculo pra assessores de investimento..."
2. **Produto**: Como funciona, Funcionalidades, Bot + Multicalculo, Pipeline
3. **Recursos**: Lead Intelligence, Multicalculo, Planos e Precos, FAQ
4. **Empresa**: Sobre nos, Contato, Privacidade, Termos de uso

**Copyright:** "(c) 2026 FinancialFlow by SaltusCon. Todos os direitos reservados."

**Responsivo:**
- `<= 1024px`: 2 colunas.
- `<= 768px`: 1 coluna, footer-bottom empilhado e centralizado.

---

## Variaveis CSS Globais (`:root`)

| Variavel | Valor | Uso |
|---|---|---|
| `--primary` | `#10B981` | Verde principal |
| `--primary-light` | `#34D399` | Verde claro |
| `--primary-dark` | `#059669` | Verde escuro |
| `--accent` | `#6366F1` | Roxo (indigo) |
| `--accent-light` | `#818CF8` | Roxo claro |
| `--accent-bg` | `#EEF2FF` | Fundo roxo |
| `--gold` | `#F59E0B` | Dourado |
| `--gold-light` | `#FBBF24` | Dourado claro |
| `--danger` | `#EF4444` | Vermelho |
| `--cold` | `#3B82F6` | Azul |
| `--bg` | `#F8FAFC` | Fundo cinza claro |
| `--text` | `#0F172A` | Texto principal |
| `--muted` | `#64748B` | Texto secundario |
| `--border` | `#E2E8F0` | Bordas |
| `--radius` | `16px` | Border-radius padrao |
| `--radius-sm` | `10px` | Border-radius pequeno |
| `--radius-lg` | `24px` | Border-radius grande |
| `--max-w` | `1200px` | Largura maxima do container |
| `--icon-bg` | `#ECFDF5` | Fundo de icones |
| `--icon-color` | `var(--primary)` | Cor de icones |

---

## Animacoes

| Nome | Descricao | Duracao |
|---|---|---|
| `float` | TranslateY 0 -> -20px -> 0 | 6s, ease-in-out, infinite |
| `floatSlow` | TranslateY 0 -> -10px + rotate 2deg | 5-6s, ease-in-out, infinite |
| `pulse-glow` | Box-shadow verde pulsante | 2s, infinite |
| `fadeInUp` | Opacity 0 + translateY(40px) -> visivel | 0.8s, ease |
| `fadeInRight` | Opacity 0 + translateX(40px) -> visivel | 1s, ease |
| `gradient-shift` | Background-position 0% -> 100% -> 0% | 15s, ease, infinite |
| `message-in` | Scale 0.95 + translateY(10px) -> normal | 0.5s, ease |
| `dash` | Stroke-dashoffset -> 0 | 1.5s, ease-in-out |

### Scroll Animations

| Classe | Descricao |
|---|---|
| `.animate-on-scroll` | Opacity 0, translateY(40px), transicao 0.8s cubic-bezier. |
| `.animate-on-scroll.visible` | Opacity 1, translateY(0). Ativado via IntersectionObserver (threshold 0.1). |
| `.delay-1` a `.delay-5` | Transition-delay de 0.1s a 0.5s. |

---

## JavaScript

Arquivo inline no final do `<body>`.

| Funcao/Bloco | Descricao |
|---|---|
| `lucide.createIcons()` | Inicializa icones Lucide de `<i data-lucide="...">`. |
| Scroll listener | Adiciona/remove `.scrolled` na navbar quando `scrollY > 50`. |
| `toggleMobileMenu()` | Alterna `.active` no menu mobile. |
| `closeMobileMenu()` | Remove `.active` do menu mobile. |
| `IntersectionObserver` | Adiciona `.visible` em elementos `.animate-on-scroll` quando entram no viewport. |
| Smooth scroll | `scrollIntoView({ behavior: 'smooth' })` para links `href="#..."`. |
| `toggleFaq(btn)` | Accordion single-open no FAQ. |
| `replayChat()` | Reinicia animacoes do chat no phone mockup. Intervalo: 15s. |
| Mousemove parallax | Move particulas do hero baseado na posicao do mouse. |
| `submitWaitlist(e)` | Processa formulario de solicitacao de proposta B2B (console.log + substituicao visual). Futuramente integrara com `POST /api/leads` do ComercialFlow. |

---

## Dependencias Externas

| Recurso | URL | Uso |
|---|---|---|
| Google Fonts (Inter) | `fonts.googleapis.com` | Tipografia principal (pesos 300-900) |
| Lucide Icons | `unpkg.com/lucide@latest/dist/umd/lucide.min.js` | Icones SVG via `data-lucide` |

---

## Observacoes

- Nao ha framework CSS ou JS — tudo e vanilla.
- Todo o CSS esta inline no `<style>` do `<head>`.
- Todo o JS esta inline no `<script>` antes do `</body>`.
- O formulario de solicitacao de proposta nao envia dados a nenhum backend atualmente (apenas `console.log`). Futuramente integrara com `POST /api/leads` do ComercialFlow (CRM B2B da SaltusCon).
- Os planos de precos existem no CSS (`.pricing-cards`, `.pricing-card`, etc.) mas o HTML nao renderiza nenhum card de plano — apenas o gate de lista de espera.
- O logo e referenciado como `logo.png` (arquivo local).
