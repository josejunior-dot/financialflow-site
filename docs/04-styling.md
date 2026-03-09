# 04 — Sistema de Estilos CSS

Documentacao completa do sistema de estilos do FinancialFlow Site. Todos os estilos estao inline no `index.html` dentro de uma tag `<style>`.

---

## 1. CSS Variables (Custom Properties)

Todas as variaveis estao definidas em `:root`:

### Cores Primarias

| Variavel | Valor | Descricao |
|---|---|---|
| `--primary` | `#10B981` | Verde principal (emerald) |
| `--primary-light` | `#34D399` | Verde claro |
| `--primary-dark` | `#059669` | Verde escuro (hover) |

### Cores de Destaque (Accent)

| Variavel | Valor | Descricao |
|---|---|---|
| `--accent` | `#6366F1` | Indigo/roxo principal |
| `--accent-light` | `#818CF8` | Indigo claro |
| `--accent-bg` | `#EEF2FF` | Background indigo suave |

### Cores Especiais

| Variavel | Valor | Descricao |
|---|---|---|
| `--gold` | `#F59E0B` | Dourado (destaques, performance) |
| `--gold-light` | `#FBBF24` | Dourado claro |
| `--danger` | `#EF4444` | Vermelho (alertas, temperatura "hot") |
| `--cold` | `#3B82F6` | Azul (temperatura "cold") |

### Cores Neutras

| Variavel | Valor | Descricao |
|---|---|---|
| `--bg` | `#F8FAFC` | Background geral (cinza muito claro) |
| `--text` | `#0F172A` | Texto principal (quase preto) |
| `--muted` | `#64748B` | Texto secundario/muted |
| `--border` | `#E2E8F0` | Bordas e divisores |
| `--white` | `#FFF` | Branco |

### Sombras

| Variavel | Valor | Descricao |
|---|---|---|
| `--shadow-sm` | `0 1px 3px rgba(0,0,0,0.06)` | Sombra leve (navbar scrolled) |
| `--shadow-md` | `0 4px 20px rgba(0,0,0,0.08)` | Sombra media (hover de cards) |
| `--shadow-lg` | `0 8px 40px rgba(0,0,0,0.1)` | Sombra forte (feature cards hover) |

### Border Radius

| Variavel | Valor | Uso |
|---|---|---|
| `--radius` | `16px` | Padrao para cards e containers |
| `--radius-sm` | `10px` | Cards menores, inputs, FAQs |
| `--radius-lg` | `24px` | Dashboards, pricing gate |

### Outros Tokens

| Variavel | Valor | Descricao |
|---|---|---|
| `--max-w` | `1200px` | Largura maxima do container |
| `--icon-bg` | `#ECFDF5` | Background de icones (verde ultra-claro) |
| `--icon-color` | `var(--primary)` | Cor de icones (herda do primary) |

---

## 2. Paleta de Cores Completa

```
Verde (Primary):    #059669 → #10B981 → #34D399
Indigo (Accent):    #6366F1 → #818CF8
Dourado (Gold):     #F59E0B → #FBBF24
Vermelho (Danger):  #EF4444
Azul (Cold):        #3B82F6

Neutros:
  Background:       #F8FAFC
  Texto:            #0F172A
  Muted:            #64748B
  Border:           #E2E8F0
  Branco:           #FFFFFF

Hero/CTA (gradientes escuros):
  #021a0f → #062b1c → #0a3d2e → #0f1b3d → #1a0f3d

Footer:
  Background:       #020a06
```

---

## 3. Tipografia

### Fonte Principal

- **Familia:** `'Inter', -apple-system, BlinkMacSystemFont, sans-serif`
- **Carregamento:** Google Fonts com `display=swap`
- **Pesos carregados:** 300, 400, 500, 600, 700, 800, 900

### Configuracoes Globais

```css
html { font-size: 16px; }
body { line-height: 1.6; -webkit-font-smoothing: antialiased; }
```

### Escala Tipografica (por componente)

| Elemento | Tamanho | Peso | Extras |
|---|---|---|---|
| Hero h1 | `clamp(2.4rem, 4.5vw, 3.6rem)` | 900 | `letter-spacing: -.03em`, `line-height: 1.1` |
| Section title | `clamp(2rem, 4vw, 3rem)` | 800 | `letter-spacing: -.03em`, `line-height: 1.15` |
| CTA h2 | `clamp(2rem, 4vw, 3rem)` | 900 | `letter-spacing: -.03em` |
| Hero subtitle | `1.15rem` | 400 | `line-height: 1.7` |
| Section subtitle | `1.1rem` | 400 | `line-height: 1.7`, cor `--muted` |
| Section label | `.8rem` | 600 | `text-transform: uppercase`, `letter-spacing: .08em` |
| Feature title | `1.15rem` | 700 | — |
| Feature desc | `.9rem` | 400 | `line-height: 1.6`, cor `--muted` |
| Navbar links | `.88rem` | 500 | — |
| Hero stat value | `1.8rem` | 800 | `letter-spacing: -.02em` |
| Metric value | `2.5rem` | 900 | `letter-spacing: -.03em` |
| Pricing price | `2.2rem` | 900 | `letter-spacing: -.03em` |
| Chat message | `.72rem` | 400 | `line-height: 1.5` |

---

## 4. Animacoes (@keyframes)

### `float`
Flutuacao vertical suave. Usada nas particulas do hero.
```css
@keyframes float {
  0%, 100% { transform: translateY(0); }
  50%      { transform: translateY(-20px); }
}
```

### `floatSlow`
Flutuacao lenta com leve rotacao. Usada no phone mockup e float cards.
```css
@keyframes floatSlow {
  0%, 100% { transform: translateY(0) rotate(0deg); }
  50%      { transform: translateY(-10px) rotate(2deg); }
}
```

### `pulse-glow`
Pulsacao com glow verde. Usada no badge dot do hero.
```css
@keyframes pulse-glow {
  0%, 100% { box-shadow: 0 0 20px rgba(16,185,129,0.3); }
  50%      { box-shadow: 0 0 40px rgba(16,185,129,0.6); }
}
```

### `fadeInUp`
Entrada de baixo para cima com fade. Usada nos elementos do hero (badge, h1, subtitle, actions, stats).
```css
@keyframes fadeInUp {
  from { opacity: 0; transform: translateY(40px); }
  to   { opacity: 1; transform: translateY(0); }
}
```

### `fadeInRight`
Entrada da direita com fade. Usada no visual do hero (phone mockup).
```css
@keyframes fadeInRight {
  from { opacity: 0; transform: translateX(40px); }
  to   { opacity: 1; transform: translateX(0); }
}
```

### `gradient-shift`
Animacao do background gradient do hero. Ciclo de 15s.
```css
@keyframes gradient-shift {
  0%   { background-position: 0% 50%; }
  50%  { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}
```

### `message-in`
Entrada de mensagens do chat (phone mockup). Efeito de subir + scale.
```css
@keyframes message-in {
  from { opacity: 0; transform: translateY(10px) scale(0.95); }
  to   { opacity: 1; transform: translateY(0) scale(1); }
}
```

### `dash`
Animacao de SVG stroke para o circulo de score na secao Intelligence.
```css
@keyframes dash {
  to { stroke-dashoffset: 0; }
}
```

---

## 5. Sistema de Scroll Animation

### Classe Base

```css
.animate-on-scroll {
  opacity: 0;
  transform: translateY(40px);
  transition: all .8s cubic-bezier(.16, 1, .3, 1);
}
```

### Estado Ativo

```css
.animate-on-scroll.visible {
  opacity: 1;
  transform: translateY(0);
}
```

A classe `.visible` e adicionada via JavaScript (IntersectionObserver) quando o elemento entra no viewport.

### Classes de Delay

| Classe | Delay |
|---|---|
| `.delay-1` | `0.1s` |
| `.delay-2` | `0.2s` |
| `.delay-3` | `0.3s` |
| `.delay-4` | `0.4s` |
| `.delay-5` | `0.5s` |

### Delays de Mensagem do Chat

| Classe | Delay |
|---|---|
| `.msg-delay-1` | `0.3s` |
| `.msg-delay-2` | `0.8s` |
| `.msg-delay-3` | `1.5s` |
| `.msg-delay-4` | `2.2s` |
| `.msg-delay-5` | `3.0s` |
| `.msg-delay-6` | `3.8s` |
| `.msg-delay-7` | `4.6s` |

### Easing Padrao

O projeto usa consistentemente o cubic-bezier `(.16, 1, .3, 1)` para transicoes suaves com leve "overshoot". Esse easing aparece em:
- Scroll animations
- Hover de cards (feature, how-step, perf-card, pricing-card)
- Transicao da navbar

---

## 6. Breakpoints Responsivos

### Desktop (> 1024px)
Layout padrao. Grids com ate 4 colunas.

### Tablet (max-width: 1024px)

| Componente | Mudanca |
|---|---|
| Hero | Grid 1 coluna, texto centralizado, visual (phone) oculto |
| Features grid | 2 colunas |
| Bot / Multicalc / Intelligence grid | 1 coluna |
| Performance grid | 2 colunas |
| How grid | Mantem 3 colunas, setas ocultas |
| Integrations grid | 2 colunas |
| Metrics grid | 2 colunas |
| Problem grid | 2 colunas |
| Pricing cards | 2 colunas |
| Footer grid | 2 colunas |

### Mobile (max-width: 768px)

| Componente | Mudanca |
|---|---|
| Sections | Padding reduzido para `60px 0` |
| Navbar | Links desktop ocultos, botao hamburger visivel |
| Features / How grid | 1 coluna |
| Performance / Integrations | 2 colunas |
| Problem grid | 1 coluna |
| Hero actions | Flex-direction column, centralizado |
| Hero stats | Coluna com gap reduzido (16px) |
| Pipeline | Coluna (vertical) |
| Footer grid | 1 coluna, gap 32px |
| Footer bottom | Coluna, centralizado |
| Proof cards | Coluna, centralizado |
| Pricing cards | 1 coluna |

### Small Mobile (max-width: 480px)

| Componente | Mudanca |
|---|---|
| Performance grid | 1 coluna |
| Metrics grid | 1 coluna |
| Integrations grid | 1 coluna |

---

## 7. Componentes Reutilizaveis

### Botoes

#### `.btn-hero`
Botao principal da secao hero. Border-radius pill (50px), padding generoso, inline-flex com gap para icone.

```css
padding: 16px 36px;
border-radius: 50px;
font-weight: 700;
font-size: 1rem;
```

Variantes:
- **`.btn-hero-primary`** — Gradiente verde (`--primary` → `--primary-light`), sombra verde. Hover: sobe 3px, sombra mais forte.
- **`.btn-hero-outline`** — Transparente com borda branca semi-transparente. Hover: fundo branco translucido.

#### `.btn-nav`
Botao da navbar. Pill shape, menor que o hero.

```css
padding: 10px 24px;
border-radius: 50px;
font-weight: 600;
font-size: .88rem;
```

Variante:
- **`.btn-nav-primary`** — Background `--primary`, texto branco. Hover: sobe 2px + sombra verde.

#### `.btn-pricing`
Botao de preco. Full-width, pill shape.

```css
width: 100%;
padding: 12px;
border-radius: 50px;
font-weight: 700;
font-size: .88rem;
```

Variantes:
- **`.btn-pricing-primary`** — Gradiente verde→indigo. Hover: sobe 2px + sombra.
- **`.btn-pricing-outline`** — Borda verde, fundo branco. Hover: inverte (fundo verde, texto branco).

#### `.btn-pricing-gate`
Botao do formulario de pricing gate. Similar ao hero mas com gradiente verde→indigo.

### Labels e Titulos de Secao

#### `.section-label`
Label acima do titulo de secao. Inline-flex com icone, uppercase, letter-spacing.

```css
font-size: .8rem;
font-weight: 600;
color: var(--primary);
text-transform: uppercase;
letter-spacing: .08em;
```

#### `.section-title`
Titulo principal de secao. Responsivo com `clamp()`.

```css
font-size: clamp(2rem, 4vw, 3rem);
font-weight: 800;
line-height: 1.15;
letter-spacing: -.03em;
```

#### `.section-subtitle`
Subtitulo de secao.

```css
font-size: 1.1rem;
color: var(--muted);
max-width: 600px;
line-height: 1.7;
```

### Gradientes de Texto

#### `.text-gradient`
Gradiente verde→indigo aplicado em texto.

```css
background: linear-gradient(135deg, var(--primary), var(--accent));
-webkit-background-clip: text;
-webkit-text-fill-color: transparent;
```

#### `.text-gradient-gold`
Gradiente dourado→laranja aplicado em texto.

```css
background: linear-gradient(135deg, var(--gold), #F97316);
-webkit-background-clip: text;
-webkit-text-fill-color: transparent;
```

### Container

```css
.container {
  max-width: var(--max-w);  /* 1200px */
  margin: 0 auto;
  padding: 0 24px;
}
```

### Icones (Lucide)

#### `.lc`
Wrapper para icones Lucide (inline-flex, centralizado).

```css
.lc svg, i[data-lucide] {
  width: 24px;
  height: 24px;
  stroke-width: 1.75;
}
```

### Cards

#### `.feature-card`
Card de funcionalidade. Borda top animada (gradiente verde→indigo) que aparece no hover via `::before` com `scaleX(0) → scaleX(1)`.

#### `.proof-card`
Card de depoimento. Background `--bg`, borda `--border`. Hover: sombra + sobe 2px.

#### `.perf-card`
Card de performance (secao escura). Background semi-transparente branco. Hover: sobe 4px.

#### `.pricing-card`
Card de preco. Variante `.featured` com borda verde e badge "Mais popular" via `::before`.

#### `.pipeline-card`
Card estilo kanban. Cursor grab, hover sobe 2px.

### Tags de Temperatura

```css
.temp-hot  { background: rgba(239,68,68,.1);  color: var(--danger); }
.temp-warm { background: rgba(245,124,0,.1);   color: #F57C00; }
.temp-cold { background: rgba(59,130,246,.1);  color: var(--cold); }
```

### Barras de Inteligencia

Barras de progresso com gradientes coloridos:
- `.bar-green` — `--primary` → `--primary-light`
- `.bar-purple` — `--accent` → `--accent-light`
- `.bar-gold` — `--gold` → `--gold-light`

---

## 8. Efeitos Visuais Especiais

### Navbar com Glassmorphism
Quando scrolled, a navbar ganha backdrop-filter blur + saturate:

```css
.navbar.scrolled {
  background: rgba(255,255,255,.92);
  backdrop-filter: blur(20px) saturate(180%);
}
```

### Hero Grid Overlay
Grid sutil sobre o hero para dar textura:

```css
.hero-grid {
  background-image:
    linear-gradient(rgba(255,255,255,.03) 1px, transparent 1px),
    linear-gradient(90deg, rgba(255,255,255,.03) 1px, transparent 1px);
  background-size: 60px 60px;
}
```

### Float Cards
Cards flutuantes no hero com glassmorphism:

```css
.hero-float-card {
  background: rgba(255,255,255,.12);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255,255,255,.2);
}
```

### Scrollbar Customizada

```css
::-webkit-scrollbar { width: 6px; }
::-webkit-scrollbar-track { background: transparent; }
::-webkit-scrollbar-thumb { background: var(--border); border-radius: 3px; }
::-webkit-scrollbar-thumb:hover { background: var(--muted); }
```

### Mobile Menu
Overlay fullscreen com slide da direita:

```css
.mobile-menu {
  background: rgba(0,0,0,.95);
  backdrop-filter: blur(20px);
  transform: translateX(100%);
  transition: transform .4s cubic-bezier(.16, 1, .3, 1);
}
.mobile-menu.active { transform: translateX(0); }
```

---

## 9. Padroes de Hover

O projeto segue um padrao consistente para hover em cards:

| Componente | Transform | Sombra |
|---|---|---|
| Feature card | `translateY(-4px)` | `--shadow-lg` |
| How step | `translateY(-4px)` | `--shadow-lg` |
| Proof card | `translateY(-2px)` | `--shadow-md` |
| Perf card | `translateY(-4px)` | Sem sombra extra |
| Pricing card | `translateY(-4px)` | `--shadow-lg` |
| Pipeline card | `translateY(-2px)` | `--shadow-md` |
| Metric card | `translateY(-4px)` | `--shadow-md` |
| Integ card | `translateY(-2px)` | `--shadow-md` |
| Btn hero primary | `translateY(-3px)` | `box-shadow` verde |
| Btn nav primary | `translateY(-2px)` | `box-shadow` verde |

---

## 10. Resumo de Decisoes de Design

- **Inline CSS:** Todos os estilos estao no `<style>` do `index.html`, sem arquivos `.css` externos.
- **Sem framework CSS:** Nao usa Tailwind, Bootstrap ou similar. CSS puro com custom properties.
- **Icones:** Lucide Icons via `data-lucide` attributes, inicializados via JS.
- **Fonte unica:** Inter cobrindo todo o range de pesos (300-900).
- **Espacamento de secoes:** `padding: 100px 0` no desktop, `60px 0` no mobile.
- **Easing padrao:** `cubic-bezier(.16, 1, .3, 1)` para transicoes suaves.
- **Gradiente primario:** `135deg` de verde para indigo, usado em texto, botoes e decoracoes.
