# financialflow-site - Development Log

> Registro completo do processo de construção, decisões arquiteturais, problemas encontrados e soluções.

**Repositório:** https://github.com/josejunior-dot/financialflow-site
**Documentação:** [docs/](./docs/)
**Status:** Produto Concluído (modelo B2B)
**Início do desenvolvimento:** 09/03/2026

---

## Sumário

- [1. Visão Geral do Produto](#1-visão-geral-do-produto)
- [2. Stack Tecnológica](#2-stack-tecnológica)
- [3. Cronologia de Desenvolvimento](#3-cronologia-de-desenvolvimento)
- [4. Arquitetura e Decisões Técnicas](#4-arquitetura-e-decisões-técnicas)
- [5. Estrutura do Projeto](#5-estrutura-do-projeto)
- [9. Deploy e Infraestrutura](#9-deploy-e-infraestrutura)
- [10. Problemas Encontrados e Soluções](#10-problemas-encontrados-e-soluções)
- [11. Métricas do Projeto](#11-métricas-do-projeto)

---

## 1. Visão Geral do Produto

Landing page e site de marketing do **LeadFlow Financial**, um CRM com IA e Multicálculo voltado para assessores de investimento. O site apresenta as funcionalidades do produto, seções de social proof, pipeline kanban, multicálculo visual, integrações, planos e FAQ. A seção de planos foi substituída por "Consulte seu agente comercial" com formulário de solicitação de proposta (modelo B2B). Todos os CTAs redirecionam para o formulário de solicitação de proposta. Integração futura prevista com ComercialFlow (CRM B2B da SaltusCon) via `POST /api/leads`.

Site estático (HTML/CSS/JS puro) hospedado no GitHub Pages.

---

## 2. Stack Tecnológica

| Camada | Tecnologia | Versão |
|--------|-----------|--------|
| **Markup** | HTML5 | - |
| **Estilo** | CSS3 (inline no HTML) | - |
| **Script** | JavaScript vanilla (inline) | - |
| **Fontes** | Google Fonts (Inter) | CDN |
| **Ícones** | Lucide Icons | CDN |
| **Deploy** | GitHub Pages | - |

---

## 3. Cronologia de Desenvolvimento

<!-- ADICIONAR NOVAS ENTRADAS AQUI (mais recente primeiro) -->

### Sessão 2 — 09/03/2026

**Objetivo:** Mudança de estratégia comercial para modelo B2B com integração futura ao ComercialFlow

- Substituição da seção "Planos / Lista de Espera" por "Consulte seu agente comercial" com formulário de solicitação de proposta
- Remoção de todos os links de WhatsApp direto do site — contato agora é exclusivamente via formulário B2B
- Botão principal do hero e CTA alterado de "Entrar na lista de espera" para "Solicitar proposta"
- CTA da navbar alterado para "Solicitar proposta"
- Mensagem de sucesso do formulário agora informa que "um consultor vai entrar em contato pelo WhatsApp"
- Definição da arquitetura de integração futura com ComercialFlow (CRM B2B da SaltusCon):
  - Formulário do site → `POST /api/leads` do ComercialFlow
  - ComercialBot engaja via WhatsApp (8 stations: CONSENT → WELCOME → DISCOVERY → FILTER → VALUE → CLOSING → HANDOFF → FOLLOW_UP)
  - Pipeline avança automaticamente (PROSPECÇÃO → QUALIFICAÇÃO → REUNIÃO → PROPOSTA → NEGOCIAÇÃO → GANHO)
  - Consultor recebe briefing e assume → Proposta e contrato gerados no ComercialFlow
- Atualização da documentação (03-components, 05-javascript, 06-content, DEVELOPMENT_LOG)

**Commits:**
- *(documentação atualizada nesta sessão)*

---

### Sessão 1 — 09/03/2026

**Objetivo:** Criação completa da landing page baseada no modelo do leadflow-site, adaptada para o segmento financeiro

- Análise do site referência leadflow-site (1591 linhas) para entender estrutura e padrão visual
- Leitura da documentação do FinancialFlow (business rules, multicálculo, README, CLAUDE.md)
- Criação do `index.html` completo (~984 linhas) com todas as seções: navbar, hero com phone mockup, social proof, problema/solução, como funciona, features grid, bot+multicálculo timeline, pipeline kanban, multicálculo visual, performance, inteligência do lead, integrações, métricas, planos, FAQ, CTA, footer
- Correção ortográfica completa (cedilhas, tis, acentos, remoção de em-dashes)
- Substituição da logo por imagem customizada (`logo.png`) na navbar e footer
- Ajuste de tamanho da logo (200px com margens negativas para compensar whitespace da imagem original)
- Criação do repositório GitHub e deploy no GitHub Pages
- Bloqueio da seção de planos (substituída por lista de espera "em breve")
- Remoção de todos os links de WhatsApp (substituídos por "Entrar na lista de espera")
- Geração da documentação completa

**Commits:**
- `feat: site landing page LeadFlow Financial` — criação inicial do site completo
- `chore: trigger pages build` — commit vazio para forçar rebuild no GitHub Pages
- `feat: bloqueia seção de planos com lista de espera` — planos substituídos por aviso "em breve"
- `feat: remove links WhatsApp e redireciona para lista de espera` — CTAs apontam para lista de espera

---

## 4. Arquitetura e Decisões Técnicas

### Decisão 1: Site estático (HTML/CSS/JS puro)
**Escolha:** Não utilizar frameworks (React, Next.js, etc.)
**Motivo:** Landing page simples de marketing, sem necessidade de roteamento, estado ou SSR. HTML puro com CSS e JS inline resulta em deploy instantâneo no GitHub Pages, zero dependências e carregamento ultra-rápido.

### Decisão 2: CSS e JS inline no HTML
**Escolha:** Tudo em um único arquivo `index.html`
**Motivo:** Simplicidade de manutenção para um site de página única. Elimina requisições extras de CSS/JS e facilita o deploy.

### Decisão 3: Baseado no leadflow-site
**Escolha:** Usar o leadflow-site como referência de estrutura e design
**Motivo:** Manter consistência visual entre os produtos da linha LeadFlow, reaproveitando padrões de layout e seções já validados.

### Decisão 4: Modelo comercial B2B com agente comercial
**Escolha:** Substituir planos fixos e lista de espera por "Consulte seu agente comercial" com formulário de solicitação de proposta
**Motivo:** Estratégia B2B com propostas personalizadas por consultor, em vez de planos self-service. O formulário alimentará o ComercialFlow (CRM B2B da SaltusCon) via `POST /api/leads` quando estiver em produção.

### Decisão 5: Integração futura com ComercialFlow
**Escolha:** Arquitetar o fluxo de captação do site para integrar com o ComercialFlow (https://github.com/josejunior-dot/comercialflow)
**Motivo:** O ComercialFlow é o CRM B2B da SaltusCon (Next.js 16, React 19, Prisma 7, PostgreSQL) com bot WhatsApp, propostas e contratos. O fluxo completo será: formulário do site → API do ComercialFlow → ComercialBot engaja via WhatsApp (8 stations) → pipeline avança → consultor assume com briefing → proposta e contrato gerados no CRM.

---

## 5. Estrutura do Projeto

```
financialflow-site/
├── index.html      # Página principal (HTML + CSS + JS inline, ~984 linhas)
├── logo.png        # Logo LeadFlow Financial (1536x1024, com whitespace)
└── docs/           # Documentação do projeto
    └── DEVELOPMENT_LOG.md
```

---

## 9. Deploy e Infraestrutura

- **Plataforma:** GitHub Pages
- **URL:** https://josejunior-dot.github.io/financialflow-site/
- **Branch de deploy:** `master`
- **Deploy automático:** Sim, após cada push na branch master
- **Domínio customizado:** Não configurado

### Como fazer deploy

```bash
git add .
git commit -m "descrição da alteração"
git push origin master
# GitHub Pages atualiza automaticamente em ~1-2 minutos
```

---

## 10. Problemas Encontrados e Soluções

### Problema 1: Conceito errado na criação inicial
**Sintoma:** O site foi criado inicialmente como uma calculadora financeira, não como um CRM
**Causa:** Falta de leitura da documentação completa do projeto antes de iniciar
**Solução:** Leitura completa da documentação do FinancialFlow (business rules, multicálculo, README) e reescrita total do site como landing page de CRM com IA

### Problema 2: Ortografia com erros massivos
**Sintoma:** Centenas de palavras sem acentos, cedilhas e tis
**Causa:** Geração inicial do conteúdo sem tratamento adequado de caracteres especiais do português
**Solução:** Batch replace com `sed` para corrigir todas as ocorrências de uma vez

### Problema 3: Logo aparecendo pequena
**Sintoma:** Logo no navbar ficava muito pequena e desproporcional
**Causa:** Imagem original (1536x1024) possui muito whitespace ao redor do logo
**Solução:** Aumentar height para 200px e usar margens negativas para compensar o espaço em branco

### Problema 4: GitHub Pages retornando 404
**Sintoma:** Após o primeiro push, o site retornava erro 404
**Causa:** O primeiro deploy não trigou o build automático do GitHub Pages
**Solução:** Commit vazio (`git commit --allow-empty`) para forçar novo rebuild

### Problema 5: localtunnel pedia senha
**Sintoma:** Ao usar localtunnel para preview externo, era necessário informar senha/IP
**Causa:** Política de segurança do localtunnel para evitar uso indevido
**Solução:** Migração para GitHub Pages como ambiente de preview e produção

---

## 11. Métricas do Projeto

| Métrica | Valor |
|---------|-------|
| **Arquivos** | 2 (index.html + logo.png) |
| **Linhas HTML** | ~900 |
| **Seções da landing page** | 17 |
| **Commits** | 4 |
| **Frameworks/dependências** | 0 (vanilla) |
| **Tempo de desenvolvimento** | 1 sessão |

---

*Última atualização: 09/03/2026 (Sessão 2 — modelo B2B)*
