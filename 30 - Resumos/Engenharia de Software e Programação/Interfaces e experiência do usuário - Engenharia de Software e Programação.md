---
tipo: resumo
disciplina: "Engenharia de Software e Programação"
tema: "Interfaces e experiência do usuário"
status: novo
data: "2026-10-16"
tags: [resumo, engenharia-software, cgu-2026]
---

# Resumo: Interfaces e experiência do usuário

> [!info] MOC: [[Engenharia de Software e Programação]]
> Edital nº 1/2026 – CGU – AFFC · **Conhecimentos específicos** · Cargo 4 (TI / Desenvolvimento de Sistemas) · Item 4 — *Interfaces e experiência do usuário*.

## Escopo no edital (checklist)

- [x] 4.1 Usabilidade, prototipagem e desenho responsivo.
- [x] 4.2 Acessibilidade e barreiras digitais.
- [x] 4.3 Componentes de interface e reaproveitamento.
- [x] 4.4 Validação com usuários e prevenção de erros no uso dos serviços.
- [x] 4.5 Desenvolvimento de interfaces com JavaScript e Vue.js: componentes, reatividade, tratamento de eventos e consumo de APIs.

## Resumo

Este item cobre a **camada de interface**: projetar experiências **usáveis, acessíveis e responsivas**, compô-las a partir de **componentes reutilizáveis** e construí-las com **JavaScript + Vue.js**. O fio condutor é colocar o **cidadão/usuário no centro** e **prevenir erros** no uso do serviço.

1. **Usabilidade** (eficácia, eficiência, satisfação) orienta o design; **prototipagem** valida cedo; **design responsivo** adapta a interface a múltiplos dispositivos.
2. **Acessibilidade (WCAG)** elimina **barreiras digitais** para pessoas com deficiência, seguindo os princípios **POUR** (Perceptível, Operável, Compreensível, Robusto).
3. **Componentes** encapsulam interface + comportamento e são **reaproveitados** (design systems), reduzindo custo e aumentando consistência.
4. **Validação com usuários** (testes de usabilidade) e **prevenção de erros** (feedback, restrições, desfazer) aumentam a qualidade do serviço.
5. **JavaScript e Vue.js** concretizam a interface: **reatividade**, **componentes** (`props`/`emit`), **eventos** e **consumo de APIs** (`fetch`/`axios`).

## 1. Usabilidade, prototipagem e desenho responsivo (4.1)

### 1.1 Usabilidade (retomada aplicada)

- **ISO 9241-11:** usabilidade = **eficácia** (concluir a tarefa), **eficiência** (gasto mínimo de recursos) e **satisfação**, num **contexto de uso**.
- **Heurísticas de Nielsen** (10) embasam inspeções rápidas (avaliação heurística).
- **Métricas de interface:** taxa de sucesso, tempo de tarefa, taxa de erro, satisfação (SUS), *task completion*.

### 1.2 Prototipagem de interface

- **Wireframe:** esqueleto estático (estrutura/layout), baixa fidelidade.
- **Mockup:** representação visual (cores, tipografia), fidelidade média.
- **Protótipo navegável:** simula a interação (cliques, fluxos), alta fidelidade — valida usabilidade antes de codificar.
- **Ferramentas:** Figma, Sketch, Adobe XD, Axure, código (HTML/CSS/JS).
- O protótipo reduz risco, descobre requisitos e alinha o time (relação com o item 1.4).

### 1.3 Design responsivo

O objetivo: a interface **adapta-se** a diferentes tamanhos de tela e dispositivos (desktop, tablet, celular) com uma **única base de código**.

| Técnica | Descrição |
| --- | --- |
| **Viewport meta** | `<meta name="viewport" content="width=device-width, initial-scale=1">` — evita zoom/overflow em mobile |
| **Media queries** | `@media (max-width: 768px) { ... }` — regras CSS condicionais por largura |
| **Layout fluido** | Usar `%`, `em`/`rem`, `fr` (grid) em vez de larguras fixas em `px` |
| **Imagens flexíveis** | `max-width: 100%` para escalar sem estourar |
| **CSS Grid / Flexbox** | Layouts flexíveis que reordenam elementos |
| **Mobile-first** | Projetar primeiro para mobile e expandir para telas maiores |

- **Mobile-first** (progressive enhancement): começa pelo menor dispositivo e adiciona recursos conforme a tela cresce.
- **Breakpoints:** pontos de quebra onde o layout muda (ex.: 480px, 768px, 1024px).

## 2. Acessibilidade e barreiras digitais (4.2)

### 2.1 Conceito e barreiras

- **Acessibilidade digital:** capacidade de um produto ser **percebido, operado e compreendido** por **todas** as pessoas, inclusive com deficiência (visual, auditiva, motora, cognitiva).
- **Barreiras digitais** incluem: imagens sem texto alternativo, contraste insuficiente, navegação que depende só do mouse, formulários sem rótulos, conteúdo que não funciona com leitor de tela, vídeos sem legendas, e CAPTCHAs inacessíveis.
- A acessibilidade beneficia a todos (design inclusivo) e, no setor público brasileiro, é **obrigatória** (Lei Brasileira de Inclusão, Lei nº 13.146/2015; modelo eMAG do governo).

### 2.2 WCAG (W3C/WAI)

As **Web Content Accessibility Guidelines (WCAG)** organizam-se em **4 princípios (POUR)** e **13 diretrizes** (WCAG 2.2), com **critérios de sucesso** testáveis.

| Princípio | Significado | Exemplos de critérios |
| --- | --- | --- |
| **Perceptível (Perceivable)** | O conteúdo pode ser percebido | Texto alternativo em imagens; legendas; contraste mínimo |
| **Operável (Operable)** | A interface pode ser operada | Tudo acessível por teclado; tempo suficiente; sem conteúdo que cause convulsão |
| **Compreensível (Understandable)** | Conteúdo e operação são compreensíveis | Texto legível; comportamento previsível; ajuda para correção de erros |
| **Robusto (Robust)** | Funciona em tecnologias atuais/futuras (agentes) | HTML/ARIA válidos; compatibilidade com leitores de tela |

### 2.3 Níveis de conformidade

- **Nível A** (mínimo): barreiras básicas removidas (ex.: alternativa textual, sem teclado preso).
- **Nível AA** (alvo comum/padrão): contraste 4.5:1 (texto) e 3:1 (texto grande), foco visível, rótulos consistentes.
- **Nível AAA** (máximo): contraste 7:1, linguagem de sinais, não estritamente exigido para sites inteiros.

### 2.4 Técnicas essenciais

- **HTML semântico:** `<header>`, `<nav>`, `<main>`, `<footer>`, `<button>`, `<label for="...">`.
- **Atributos `alt`** descritivos em imagens informativas (vazio `alt=""` para decorativas).
- **Navegação por teclado:** todos os elementos focáveis; ordem lógica; **foco visível**.
- **ARIA (`role`, `aria-label`, `aria-live`, `aria-expanded`)**: complementa semântica para componentes dinâmicos.
- **Contraste e tamanho de fonte** adequados; não depender só de cor para transmitir informação.
- **Formulários:** `label` associado, mensagens de erro acessíveis (`aria-describedby`), instruções claras.
- **Redução de movimento** (`prefers-reduced-motion`) e **foco não roubado** sem aviso.

## 3. Componentes de interface e reaproveitamento (4.3)

### 3.1 Componentização

- **Componente:** unidade de interface **encapsulada** (estrutura + estilo + comportamento) com **interface explícita** (props/eventos) e **reutilizável**.
- Vantagens: **consistência** visual/funcional, **menos duplicação**, **manutenção localizada**, **testabilidade** e **composição** de telas a partir de peças.

### 3.2 Design system

- **Design system:** conjunto padronizado de **princípios, tokens de design** (cores, espaçamentos, tipografia), **componentes** e **documentação** que orienta a construção de interfaces.
- Inclui **biblioteca de componentes** (implementação) + **guias de uso** (documentação).
- Exemplos: Material Design (Google), Carbon (IBM), gov.br Design System (padrão do governo federal brasileiro).
- **Tokens de design** (variáveis) permitem **theming** e mudanças consistentes.

### 3.3 Reaproveitamento

- Componentes **genéricos** (botão, campo, modal, tabela) são usados em vários contextos com **props** para variar comportamento.
- **Composição** (componentes dentro de componentes) em vez de herança; **slots** permitem injetar conteúdo.
- Reaproveitamento **reduz retrabalho** e garante que a correção de um bug/ajuste de acessibilidade **propague** a todos os usos (conexão com o item 5).

## 4. Validação com usuários e prevenção de erros (4.4)

### 4.1 Validação com usuários

- **Testes de usabilidade:** usuários reais executam tarefas observadas, com coleta de métricas e problemas.
- **Entrevistas/testes de guerrilha**, **teste A/B**, **pesquisas de satisfação**, **análise de uso (analytics)**.
- **Iteração:** os achados voltam ao design (construir-medir-aprender); a validação é **contínua**, não um marco final.
- **Acessibilidade** também se valida: testes com leitores de tela, auditoria WCAG, testes de teclado.

### 4.2 Prevenção de erros no uso dos serviços

- **Prevenir é melhor que remediar** (heurística nº 5 de Nielsen). Estratégias:

| Estratégia | Exemplo |
| --- | --- |
| **Restrições (constraints)** | Desabilitar opções inválidas; máscara de CPF; `input` com `type="number"` |
| **Defaults inteligentes** | Pré-selecionar a opção mais comum |
| **Confirmação de ações destrutivas** | "Tem certeza que deseja excluir?" |
| **Feedback imediato** | Validação inline ("CPF inválido") em vez de erro no envio |
| **Desfazer (undo)** | Permitir reverter a última ação |
| **Instruções claras** | Rótulos, placeholders, ajuda contextual |
| **Formatos esperados** | Exibir o formato (data, telefone) antes do preenchimento |

- **Validação de formulário:** preferir **validação no cliente** (UX imediata) **e** no **servidor** (segurança — o cliente pode ser burlado).
- **Mensagens de erro:** claras, próximas ao campo, dizendo **o que fazer** (não só "erro").
- **Estado vazio/loading/sucesso** bem comunicados evitam confusão.

## 5. JavaScript e Vue.js (4.5)

### 5.1 JavaScript (fundamentos para interfaces)

- **`let`/`const`** (escopo de bloco) vs `var` (escopo de função, hoisting) — preferir `let`/`const`.
- **Arrow functions** (`=>`), **template literals** (`` `texto ${var}` ``), **destructuring**, **spread/rest** (`...`).
- **Promises e `async/await`** para código assíncrono.
- **Módulos ES6** (`export`/`import`).
- **Manipulação de DOM** e **eventos** (hoje encapsulados pelo framework).

```js
// async/await com fetch
async function buscarDados(url) {
  const resposta = await fetch(url);          // Promise<Response>
  if (!resposta.ok) throw new Error('HTTP ' + resposta.status);
  const dados = await resposta.json();        // converte para objeto
  return dados;
}
```

### 5.2 Vue.js: visão geral e reatividade

- **Vue 3** é um framework **progressivo** para interfaces. Duas APIs de composição de componentes:
  - **Options API:** `data()`, `methods`, `computed`, `watch`, `mounted` — mais explícita e familiar.
  - **Composition API (`<script setup>`):** `ref`, `reactive`, `computed`, `watch`, `onMounted` — mais flexível e reutilizável.

```vue
<script setup>
import { ref, computed, onMounted } from 'vue'

const contador = ref(0)                       // estado reativo (primitivo)
const dobro = computed(() => contador.value * 2)

function incrementar() { contador.value++ }

onMounted(() => console.log('montado'))
</script>

<template>
  <button @click="incrementar">{{ contador }} (dobro: {{ dobro }})</button>
</template>
```

- **Reatividade:** quando o estado reativo muda, a **view é atualizada automaticamente**. `ref` embrulha primitivos (acesso via `.value`); `reactive` embrulha objetos.
- **`computed`** (cacheia, deriva) × **`watch`** (observa mudanças e dispara efeitos) × **métodos** (executam sob demanda).

### 5.3 Diretivas (sintaxe `v-*`)

| Diretiva | Função |
| --- | --- |
| `v-bind:attr` / `:attr` | Liga um atributo/`prop` a uma expressão |
| `v-model` | Ligação **bidirecional** em inputs/componentes |
| `v-if` / `v-else-if` / `v-else` | Renderização **condicional** (remove do DOM) |
| `v-show` | Alterna `display` (mantém no DOM) |
| `v-for="(item, i) in itens" :key="item.id"` | Renderização de listas (sempre com `:key`) |
| `v-on:event` / `@event` | Escuta eventos (`@click`, `@submit.prevent`) |
| `v-html` | Insere HTML (risco de XSS — usar com cuidado) |

- **`v-if` × `v-show`:** `v-if` cria/destrói o nó (custo maior, melhor para condições raras); `v-show` só alterna CSS (`display:none`, barato para alternâncias frequentes).
- **Modificadores de evento:** `.prevent` (`@submit.prevent`), `.stop`, `.once`, `.keyup.enter`.

### 5.4 Componentes: props e emit

- **Fluxo de dados unidirecional:** dados descem via **`props`** (pai→filho); eventos sobem via **`emit`** (filho→pai). Filhos **não** devem mutar props diretamente.

```vue
<!-- Filho.vue -->
<script setup>
const props = defineProps({ titulo: String, total: Number })
const emit = defineEmits(['selecionar'])

function clicar() { emit('selecionar', props.total) }
</script>

<template>
  <button @click="clicar">{{ titulo }}</button>
</template>
```

```vue
<!-- Pai.vue -->
<Filho :titulo="'Salvar'" :total="42" @selecionar="tratarSelecao" />
```

- **Slots** permitem injetar conteúdo no filho; **`v-model` em componentes** encapsula `prop` + `emit` para ligação bidirecional.

### 5.5 Ciclo de vida (Composition API)

- `onMounted` (montado), `onUpdated`, `onUnmounted`, `onBeforeMount`, `onBeforeUnmount` — ganchos para efeitos (buscar dados, assinar eventos, limpar).

### 5.6 Gerenciamento de estado: Pinia

- **Pinia** é o gerenciador de estado oficial do Vue 3 (sucessor do Vuex). Centraliza **estado compartilhado** entre componentes.

```js
// stores/contador.js
import { defineStore } from 'pinia'

export const useContadorStore = defineStore('contador', {
  state: () => ({ count: 0 }),               // estado
  getters: { dobro: (s) => s.count * 2 },    // derivados
  actions: { incrementar() { this.count++ } } // mutações/assíncrono
})
```

- **`state`** (dados), **`getters`** (derivados/computed), **`actions`** (mutações, inclusive assíncronas).
- Usar store num componente: `const store = useContadorStore(); store.incrementar()`.

### 5.7 Roteamento e consumo de APIs

- **Vue Router (`vue-router`)** mapeia rotas para componentes (SPA): `createRouter`, `createWebHistory`, `<router-view>`, `<router-link>`.
- **Consumo de API:** `fetch` (nativo) ou **axios** (interceptores, cancelamento, transforms), normalmente dentro de `onMounted` ou de ações do Pinia.

```js
import axios from 'axios'

async function carregar() {
  try {
    const { data } = await axios.get('https://api.exemplo.gov.br/pedidos')
    pedidos.value = data
  } catch (erro) {
    erroMsg.value = 'Falha ao carregar'
  }
}
```

- **CORS** (origens permitidas), **autenticação** (Bearer token), **tratamento de erros** e **estados de loading** fazem parte do consumo correto de APIs.

## Detalhes que merecem destaque

- **Usabilidade = eficácia + eficiência + satisfação** (ISO 9241-11), medida em contexto real de uso.
- **Design responsivo:** viewport + media queries + layout fluido + imagens flexíveis (mobile-first).
- **WCAG POUR:** Perceptível, Operável, Compreensível, Robusto — 13 diretrizes (WCAG 2.2), níveis **A/AA/AAA**.
- **Contraste AA:** 4.5:1 texto normal, 3:1 texto grande (AAA: 7:1).
- **Acessibilidade no Brasil:** Lei Brasileira de Inclusão (13.146/2015) e **eMAG** (modelo do governo).
- **Componente** = estrutura + estilo + comportamento encapsulados, com props/eventos, **reutilizável**; **design system** padroniza.
- **Vue 3:** `ref`/`reactive` (estado), `computed` (derivado/cacheado), `watch` (efeito), `onMounted` (ciclo de vida).
- **Diretivas:** `v-bind` (`:`), `v-model`, `v-if` (remove do DOM) × `v-show` (CSS), `v-for` (com `:key`), `v-on` (`@`).
- **Fluxo unidirecional:** dados descem por **props**, eventos sobem por **emit**; filhos não mutam props.
- **Pinia:** `state`/`getters`/`actions` para estado global; **Vue Router** para rotas SPA.
- **Consumo de API:** `fetch`/`axios` com `async/await`, tratamento de erro, loading e autenticação.
- **Prevenção de erros > mensagens de erro** (heurística de Nielsen); validação no cliente **e** no servidor.
- **`v-html` é risco de XSS** — usar com dados sanitizados.

## Comparações que a banca costuma cobrar (certo/errado)

| Conceito A | Conceito B | Diferença-chave |
| --- | --- | --- |
| Usabilidade | UX | Usabilidade = eficácia/eficiência/satisfação; UX = percepção ampla |
| Wireframe | Protótipo navegável | Wireframe é estático (estrutura); protótipo simula interação |
| Mobile-first | Desktop-first | Mobile-first projeta do menor para o maior; desktop-first o inverso |
| Media query | Viewport meta | Media query aplica regras condicionais; viewport controla a escala inicial |
| Acessibilidade | Usabilidade | Acessibilidade foca inclusão (deficiência); usabilidade foca facilidade geral |
| Nível A | Nível AA | A = barreiras mínimas; AA = padrão (contraste, foco) |
| `v-if` | `v-show` | v-if remove do DOM; v-show alterna `display` (mantém nó) |
| `computed` | `watch` | computed deriva/cacheia valor; watch observa e dispara efeito |
| `ref` | `reactive` | ref embrulha primitivo (`.value`); reactive embrulha objeto |
| Props | Emit | Props descem (pai→filho); emit sobe (filho→pai) |
| Options API | Composition API | Options usa `data/methods/computed`; Composition usa `ref/reactive` em `<script setup>` |
| Pinia | Vuex | Pinia é o atual (simples, TS-first); Vuex é o antecessor |
| `fetch` | axios | fetch é nativo (sem interceptores nativos); axios é lib com mais recursos |
| `v-bind` | `v-model` | v-bind é ligação unidirecional; v-model é bidirecional |
| Validação no cliente | Validação no servidor | Cliente melhora UX; servidor é obrigatório (cliente é burlável) |

## Pegadinhas e erros comuns

> Cuidado com termos absolutos ("sempre", "nunca", "exclusivamente") e com a troca de requisitos.

- Achar que **acessibilidade = apenas deficiência visual** — abrange auditiva, motora, cognitiva e temporária.
- Reduzir **usabilidade a "ser bonito"** — é eficácia + eficiência + satisfação mensuráveis.
- Confundir **v-if** (remove do DOM) com **v-show** (só CSS `display`).
- Esquecer a **`:key`** no `v-for` — pode causar reutilização incorreta de elementos e bugs.
- Dizer que **props podem ser mutadas pelo filho** — fluxo é **unidirecional**; mutação deve usar `emit`.
- Confundir **computed** (cacheado, derivado) com **método** (executa sempre) ou **watch** (efeito).
- Afirmar que **validação no cliente dispensa a do servidor** — cliente pode ser burlado; servidor é obrigatório.
- Dizer que **`v-html` é seguro** — é vetor de **XSS** se o conteúdo não for sanitizado.
- Trocar **níveis WCAG**: achar que **AA é o mínimo (é o A)** ou que AAA é obrigatório em todo site.
- Achar que **contraste AA é 3:1 para texto normal** — é **4.5:1** (3:1 só para texto grande).
- Confundir **design responsivo** com "site mobile separado" — responsivo usa **uma base de código** adaptável.
- Dizer que **media query substitui o viewport meta** — são complementares.
- Achar que **acessibilidade é "opcional" no setor público** — é obrigatória (LBI/eMAG).
- Confundir **wireframe** (estático) com **mockup** (visual) e **protótipo** (interativo).

## Notas atômicas relacionadas

```dataview
LIST FROM "20 - Notas"
WHERE disciplina = this.disciplina
  AND contains(tema, this.tema)
SORT file.name ASC
```

## Fontes

- https://www.nngroup.com/articles/ten-usability-heuristics/ — Nielsen Norman Group, 10 heurísticas de usabilidade.
- https://www.nngroup.com/articles/response-time-3-important-limits/ — NNG, tempos de resposta e percepção de usabilidade.
- https://www.w3.org/WAI/standards-guidelines/wcag/ — W3C/WAI, visão geral das WCAG (POUR, níveis A/AA/AAA).
- https://www.w3.org/TR/WCAG22/ — WCAG 2.2 (especificação oficial dos critérios de sucesso).
- https://www.w3.org/WAI/fundamentals/accessibility-intro/ — W3C/WAI, introdução à acessibilidade web.
- https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Responsive_Design — MDN, design responsivo (media queries, viewport, fluid).
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide — MDN, guia de JavaScript (async/await, módulos, promises).
- https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API — MDN, Fetch API (consumo de APIs).
- https://vuejs.org/guide/introduction.html — Vue.js 3, introdução oficial.
- https://vuejs.org/guide/essentials/reactivity-fundamentals.html — Vue.js, fundamentos de reatividade (`ref`/`reactive`).
- https://vuejs.org/guide/essentials/component-basics.html — Vue.js, componentes (props/emit).
- https://vuejs.org/guide/essentials/event-handling.html — Vue.js, tratamento de eventos e modificadores.
- https://vuejs.org/guide/built-ins/directives.html — Vue.js, diretivas (`v-if`, `v-for`, `v-model`, etc.).
- https://pinia.vuejs.org/core-concepts/ — Pinia, conceitos centrais (`state`, `getters`, `actions`).
- https://router.vuejs.org/ — Vue Router (roteamento em SPAs).
- https://www.gov.br/governodigital/pt-br/acessibilidade-digital/emag — eMAG, Modelo de Acessibilidade em Governo Eletrônico.
- https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2015/lei/l13146.htm — Lei nº 13.146/2015, Lei Brasileira de Inclusão (acessibilidade).
