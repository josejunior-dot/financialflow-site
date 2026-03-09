# 05 - JavaScript do FinancialFlow Site

Documentacao completa de todo o JavaScript utilizado no site institucional do FinancialFlow. Todo o codigo esta inline no final do arquivo `index.html`, dentro de uma unica tag `<script>`.

---

## Visao Geral

O JavaScript do site e composto por funcoes e listeners que cuidam de:

1. Inicializacao de icones (Lucide)
2. Comportamento da navbar no scroll
3. Menu mobile (abrir/fechar)
4. Animacoes de scroll (IntersectionObserver)
5. Smooth scroll em links ancora
6. Accordion do FAQ
7. Replay de animacao do chat mockup
8. Efeito parallax nas particulas do hero
9. Formulario de solicitacao de proposta (B2B)

Nao ha arquivos `.js` externos — tudo esta embutido no HTML.

---

## 1. Inicializacao dos Icones Lucide

```javascript
lucide.createIcons();
```

- **O que faz:** Varre o DOM e substitui todos os elementos `<i data-lucide="nome-do-icone">` pelos SVGs correspondentes da biblioteca Lucide Icons.
- **Quando executa:** Imediatamente ao carregar o script.
- **Dependencia:** Biblioteca Lucide carregada via CDN antes deste script.
- **Nota:** E chamado novamente dentro de `submitWaitlist()` apos injetar novo HTML com icones.

---

## 2. Navbar Scroll Behavior

```javascript
const navbar = document.getElementById('navbar');
window.addEventListener('scroll', () => {
  navbar.classList.toggle('scrolled', window.scrollY > 50);
});
```

- **Elemento alvo:** `#navbar`
- **O que faz:** Adiciona a classe CSS `.scrolled` na navbar quando o usuario rola mais de 50px para baixo. Remove a classe quando volta ao topo.
- **Efeito visual:** A classe `.scrolled` tipicamente aplica fundo solido (com blur/backdrop-filter) e sombra na navbar, que comeca transparente.
- **Evento:** `scroll` no objeto `window`.

---

## 3. Menu Mobile

### `toggleMobileMenu()`

```javascript
function toggleMobileMenu() {
  document.getElementById('mobileMenu').classList.toggle('active');
}
```

- **Parametros:** Nenhum.
- **Elemento alvo:** `#mobileMenu`
- **O que faz:** Alterna (toggle) a classe `.active` no menu mobile. Se o menu esta fechado, abre; se esta aberto, fecha.
- **Chamada:** Pelo botao hamburger na navbar (atributo `onclick`).

### `closeMobileMenu()`

```javascript
function closeMobileMenu() {
  document.getElementById('mobileMenu').classList.remove('active');
}
```

- **Parametros:** Nenhum.
- **Elemento alvo:** `#mobileMenu`
- **O que faz:** Remove a classe `.active` do menu mobile, forçando o fechamento.
- **Chamada:** Pelos links dentro do menu mobile (ao clicar em um item, o menu fecha automaticamente).

---

## 4. Scroll Animations (IntersectionObserver)

```javascript
const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) entry.target.classList.add('visible');
  });
}, { threshold: 0.1, rootMargin: '0px 0px -50px 0px' });

document.querySelectorAll('.animate-on-scroll').forEach(el => observer.observe(el));
```

- **Elementos alvo:** Todos os elementos com a classe `.animate-on-scroll`.
- **O que faz:** Observa quando cada elemento entra na viewport. Ao entrar, adiciona a classe `.visible`.
- **Configuracao do Observer:**
  - `threshold: 0.1` — Dispara quando pelo menos 10% do elemento esta visivel.
  - `rootMargin: '0px 0px -50px 0px'` — Cria uma margem negativa de 50px no fundo, ou seja, o elemento precisa subir 50px a mais para ser considerado "visivel". Isso cria um efeito de delay natural.
- **CSS relacionado:**
  - `.animate-on-scroll` — Define `opacity: 0` e `transform: translateY(40px)` (elemento invisivel e deslocado para baixo).
  - `.animate-on-scroll.visible` — Define `opacity: 1` e `transform: translateY(0)` (elemento aparece e sobe para a posicao original).
  - A transicao usa `cubic-bezier(.16, 1, .3, 1)` com duracao de 0.8s.
  - Classes auxiliares `.delay-1` a `.delay-4` aplicam `transition-delay` de 0.1s a 0.4s para efeito cascata.
- **Nota:** A animacao e "one-way" — uma vez visivel, nao reverte ao rolar de volta para cima.

---

## 5. Smooth Scroll (Links Ancora)

```javascript
document.querySelectorAll('a[href^="#"]').forEach(anchor => {
  anchor.addEventListener('click', function(e) {
    const href = this.getAttribute('href');
    if (href === '#') return;
    e.preventDefault();
    const target = document.querySelector(href);
    if (target) target.scrollIntoView({ behavior: 'smooth', block: 'start' });
  });
});
```

- **Elementos alvo:** Todos os links `<a>` cujo `href` comeca com `#`.
- **O que faz:** Intercepta o clique em links ancora e realiza scroll suave ate a secao correspondente.
- **Comportamento:**
  1. Captura o valor do `href`.
  2. Se for apenas `#` (sem destino), ignora e nao faz nada.
  3. Previne o comportamento padrao do navegador (`e.preventDefault()`).
  4. Busca o elemento alvo pelo seletor e executa `scrollIntoView` com animacao suave.
- **Complemento:** O CSS tambem define `html { scroll-behavior: smooth }` como fallback.

---

## 6. FAQ Accordion

### `toggleFaq(btn)`

```javascript
function toggleFaq(btn) {
  const item = btn.closest('.faq-item');
  document.querySelectorAll('.faq-item').forEach(i => {
    if (i !== item) i.classList.remove('open');
  });
  item.classList.toggle('open');
}
```

- **Parametros:**
  - `btn` (HTMLElement) — O botao clicado dentro do item FAQ.
- **O que faz:**
  1. Encontra o `.faq-item` pai mais proximo do botao clicado (usando `.closest()`).
  2. Fecha todos os outros itens FAQ removendo a classe `.open`.
  3. Alterna a classe `.open` no item clicado.
- **Comportamento:** Apenas um item FAQ pode estar aberto por vez (accordion exclusivo). Clicar em um item ja aberto o fecha.
- **Chamada:** Pelo botao de cada pergunta do FAQ (atributo `onclick="toggleFaq(this)"`).

---

## 7. Chat Message Replay Loop

### `replayChat()`

```javascript
function replayChat() {
  document.querySelectorAll('.chat-msg').forEach(msg => {
    msg.style.animation = 'none';
    msg.offsetHeight; // force reflow
    msg.style.animation = '';
  });
}
setInterval(replayChat, 15000);
```

- **Parametros:** Nenhum.
- **Elementos alvo:** Todos os elementos com a classe `.chat-msg` (mensagens do mockup de celular no hero).
- **O que faz:** Reinicia a animacao CSS `message-in` de todas as mensagens do chat.
- **Tecnica:**
  1. Remove a animacao definindo `animation = 'none'`.
  2. Forca um reflow do DOM acessando `msg.offsetHeight` (truque classico para resetar animacoes CSS).
  3. Restaura a animacao removendo o override inline (`animation = ''`), fazendo o CSS original reassumir.
- **Intervalo:** Executa a cada 15 segundos via `setInterval`.
- **Efeito visual:** As mensagens do chat do mockup (lead conversando com o bot) reaparecem com a animacao de entrada, criando um loop visual continuo.

---

## 8. Efeito Parallax nas Particulas

```javascript
window.addEventListener('mousemove', (e) => {
  const ps = document.querySelectorAll('.particle');
  const x = e.clientX / window.innerWidth;
  const y = e.clientY / window.innerHeight;
  ps.forEach((p, i) => {
    const s = (i + 1) * 0.5;
    p.style.transform = `translate(${x * s * 20}px, ${y * s * 20}px)`;
  });
});
```

- **Evento:** `mousemove` no objeto `window`.
- **Elementos alvo:** Todos os elementos com a classe `.particle` (circulos decorativos na secao hero).
- **O que faz:** Move as particulas levemente com base na posicao do mouse, criando um efeito parallax/profundidade.
- **Calculo:**
  - `x` e `y` sao normalizados entre 0 e 1 (posicao proporcional do mouse na tela).
  - `s` (speed) aumenta para cada particula subsequente: a primeira se move com fator 0.5, a segunda com 1.0, a terceira com 1.5, etc.
  - O deslocamento maximo e de `s * 20` pixels em cada eixo.
- **Efeito visual:** Particulas mais "fundas" na lista se movem mais rapido, criando sensacao de profundidade.
- **Nota:** Este efeito so funciona em dispositivos com mouse. Em dispositivos touch, as particulas ficam estaticas.

---

## 9. Formulario de Solicitacao de Proposta (B2B)

### `submitWaitlist(e)`

```javascript
function submitWaitlist(e) {
  e.preventDefault();
  const name = document.getElementById('gateName').value.trim();
  const email = document.getElementById('gateEmail').value.trim();
  const phone = document.getElementById('gatePhone').value.trim();
  const size = document.getElementById('gateSize').value;
  if (!name || !email || !phone || !size) return false;
  console.log('Waitlist lead:', { name, email, phone, size });
  const gate = document.getElementById('pricingGate');
  gate.innerHTML = '<div class="pricing-gate-icon" ...>...</div>' +
    '<h3>Proposta solicitada!</h3>' +
    '<p>Obrigado, ' + name.split(' ')[0] + '! Um consultor vai entrar em contato...</p>';
  lucide.createIcons();
  return false;
}
```

- **Parametros:**
  - `e` (Event) — O evento de submit do formulario.
- **Campos capturados:**
  - `gateName` — Nome completo do assessor.
  - `gateEmail` — E-mail profissional.
  - `gatePhone` — Telefone/WhatsApp.
  - `gateSize` — Tamanho da equipe (select com opcoes).
- **O que faz:**
  1. Previne o envio padrao do formulario (`e.preventDefault()`).
  2. Captura e limpa (trim) os valores dos campos.
  3. Valida se todos os campos estao preenchidos. Se algum estiver vazio, retorna `false` sem fazer nada.
  4. Loga os dados no console (futuramente, enviara via `POST /api/leads` ao ComercialFlow).
  5. Substitui todo o conteudo do container `#pricingGate` por uma mensagem de confirmacao: "Proposta solicitada! Um consultor vai entrar em contato pelo WhatsApp."
  6. Chama `lucide.createIcons()` novamente para renderizar o icone de check no HTML injetado.
  7. Retorna `false` para garantir que o formulario nao submeta.
- **Chamada:** Pelo atributo `onsubmit="return submitWaitlist(event)"` no formulario.
- **Integracao futura com ComercialFlow:** Quando o ComercialFlow (https://github.com/josejunior-dot/comercialflow) estiver em producao, a funcao `submitWaitlist` sera atualizada para enviar os dados via `POST /api/leads` ao ComercialFlow. A partir dai, o ComercialBot (bot WhatsApp do ComercialFlow) assumira o engajamento do lead com 8 stations automaticas (CONSENT → WELCOME → DISCOVERY → FILTER → VALUE → CLOSING → HANDOFF → FOLLOW_UP), avancando o pipeline ate o consultor humano assumir.
- **Nota:** Atualmente os dados sao apenas logados no console. A funcao mantem o nome `submitWaitlist` por compatibilidade, mas o fluxo agora e de solicitacao de proposta B2B, nao lista de espera.

---

## Resumo de Dependencias Externas

| Dependencia | Tipo | Uso |
|---|---|---|
| Lucide Icons | CDN (JS) | Renderizacao de icones SVG via `data-lucide` |

## APIs do Navegador Utilizadas

| API | Uso |
|---|---|
| `IntersectionObserver` | Animacoes de scroll |
| `scrollIntoView` | Smooth scroll para ancoras |
| `setInterval` | Loop de replay do chat |
| `mousemove` event | Parallax nas particulas |
| `scroll` event | Toggle de classe na navbar |

---

*Documentacao gerada em 2026-03-09 para o projeto FinancialFlow Site.*
