---
tipo: resumo
disciplina: "Fundamentos de Evidências, Dados e Inteligência Artificial"
tema: "Uso responsável de inteligência artificial"
status: novo
data: "2026-10-16"
tags: [resumo, dados-ia, cgu-2026]
---

# Resumo: Uso responsável de inteligência artificial

> [!info] MOC: [[Fundamentos de Evidências, Dados e Inteligência Artificial]]
> Edital nº 1/2026 – CGU – AFFC · **Conhecimentos complementares** · Item 5 — *Uso responsável de inteligência artificial*.

## Escopo no edital (checklist)

- [x] 5.1 Possibilidades de classificação, busca, síntese e apoio à análise
- [x] 5.1 Escolha entre IA, solução simples e revisão humana
- [x] 5.2 Erros, conteúdo não sustentado, vieses e efeitos sobre grupos
- [x] 5.2 Proteção de informações, supervisão, rastreabilidade e contestação
- [x] 5.3 Verificação de fontes e limites da automação de decisões que afetam direitos.

## Resumo

Este bloco encerra a disciplina integrando a **IA generativa e preditiva ao ciclo da evidência** — mas sob a lógica do **uso responsável**. A IA amplia capacidades de **classificação, busca, síntese e apoio à análise**; o desafio é **escolher quando** ela é a solução adequada (em vez de uma regra simples ou de revisão humana) e **gerenciar** seus erros característicos — **alucinação, conteúdo não sustentado, viés algorítmico e efeitos desproporcionais sobre grupos**.

A segunda metade cuida das **salvaguardas**: proteção de informações, **supervisão humana**, **rastreabilidade** e **contestação**, culminando nos **limites da automação de decisões que afetam direitos** — com destaque para o **art. 20 da LGPD** (direito de revisão) e os **princípios de governança de IA** (OECD AI Principles). O eixo é o mesmo de toda a disciplina: a IA **apoia**, mas **não substitui** o julgamento responsável e a responsabilização humana.

## 1. Possibilidades de classificação, busca, síntese e apoio à análise (5.1)

### 1.1 Classificação

Modelos que **atribuem rótulos/categorias** a itens: classificar documentos por tema, manifestações de ouvidoria por tipo (denúncia × reclamação × solicitação), contratos por nível de risco, textos por sentimento. Duas famílias:

- **supervisionada:** treinada com exemplos rotulados (requer dados anotados);
- **não supervisionada:** agrupa por similaridade sem rótulos prévios (clustering).

Herda as métricas do resumo de inferências — **sensibilidade/especificidade, falsos positivos/negativos** — e, com LLMs, pode classificar por **instrução** (zero/few-shot), com menos dados, porém com menor garantia de consistência.

### 1.2 Busca (recuperação semântica)

IA permite **buscar por significado**, não só por palavra exata: representações vetoriais (embeddings) aproximam documentos **semanticamente** relacionados e viabilizam **RAG (geração aumentada por recuperação)** — recuperar trechos relevantes e gerar resposta **fundamentada** neles. Amplia a localização de informação em acervos grandes e não estruturados.

### 1.3 Síntese

Capacidade de **resumir** grandes volumes (atas, relatórios, manifestações), **extrair** entidades/fatos e **consolidar** múltiplas fontes. É a aplicação de maior ganho de produtividade — e também de maior risco, pois a síntese pode **omitir, distorcer ou inventar** (ver item 3).

### 1.4 Apoio à análise

IA como **assistente**: gerar hipóteses, redigir rascunhos, traduzir, revisar consistência, sugerir cruzamentos. O papel é **aumentar** o analista (IA **aumentada**), não **substituí-lo** — o julgamento, a responsabilização e a decisão permanecem humanos.

### 1.5 Limite de escopo dessas possibilidades

As quatro tarefas compartilham a natureza de **apoio**: produzem **candidatos/rascunhos**, que exigem **verificação** (item 3 e 5.3). Classificação e busca **reduzem** o trabalho; síntese e apoio **aceleram**, mas nenhuma **elimina** a necessidade de revisão e de fundamentação.

## 2. Escolha entre IA, solução simples e revisão humana (5.1)

### 2.1 Princípio da parcimônia (a solução mais simples adequada)

Antes de usar IA, pergunte se o problema **precisa** dela:

- **regra simples/determinística** (consulta a banco, filtro, regex, árvore de decisão, planilha) — previsível, auditável, barata;
- **estatística clássica** — quando há modelo interpretável e dados estruturados;
- **IA/ML** — quando há padrão complexo, muitos dados e tolerância a erro;
- **IA generativa (LLM)** — quando há linguagem natural, síntese/geração e contexto pouco estruturado.

**Critério de escolha:** o que atende à **necessidade com o menor risco e custo**. Usar LLM para o que um `IF` resolve é **excesso de complexidade** (e de risco: alucinação, custo, opacidade).

### 2.2 Revisão humana vs. automação

- **Revisão humana:** indispensável quando há **juízo de valor, contexto, exceções** e consequências relevantes — é mais cara/lenta, mas responsabilizável.
- **Automação:** adequada a tarefas **repetitivas, bem definidas e de baixo risco**, com regras claras.
- **Human-in-the-loop:** decisão **proposta** pela IA, **aprovada** por humano — padrão para casos de médio/alto impacto.
- **Human-on-the-loop:** humano **supervisiona** e pode intervir (monitoramento contínuo).

### 2.3 Matriz de decisão (simplificada)

| Situação | Escolha adequada |
| --- | --- |
| Regra objetiva e estável | Solução simples/determinística |
| Padrão complexo, dados abundantes, erro tolerável | ML preditivo/classificador |
| Linguagem natural, síntese, triagem de texto | IA generativa (LLM), com verificação |
| Decisão com direitos/consequências relevantes | Revisão humana (IA no máximo como apoio) |
| Ação irreversível/alto impacto | Human-in-the-loop (aprovação humana) |

### 2.4 Escolha transparente e auditável

A escolha deve ser **justificada e documentada** (por que IA, qual modelo, que salvaguardas). A "IA por modismo" sem análise de adequação é, ela própria, uma violação do uso responsável.

## 3. Erros, conteúdo não sustentado, vieses e efeitos sobre grupos (5.2)

### 3.1 Alucinação e conteúdo não sustentado

- **Alucinação:** geração de conteúdo **plausível, porém falso/inventado** (citação inexistente, dado fabricado, jurisprudência que não existe).
- **Conteúdo não sustentado (não fundamentado):** afirmação **sem base na fonte/contexto** — mesmo quando "parece certa".
- **Causas:** natureza estatística da geração (prediz o próximo token), ausência de conhecimento factual, prompt ambíguo, recuperação ruim (RAG).
- **Mitigação:** **RAG** (fundamentar em fontes recuperadas), **citação obrigatória**, **verificação de fontes** (item 5.3), redução de aleatoriedade quando pertinente — lembrando que **RAG reduz, mas não elimina** a alucinação.

### 3.2 Vieses algorítmicos

O modelo **herda vieses dos dados de treino** e pode **amplificá-los**:

- **viés de representação:** sub-representação de grupos nos dados;
- **viés histórico/social:** dados refletem discriminações passadas;
- **viés de medição:** rótulos/proxies enviesados (usar variável correlata inadequada);
- **viés de seleção/sobrevivência:** dados não representativos (retoma o resumo de inferências).

### 3.3 Efeitos sobre grupos (disparidade/impacto desproporcional)

O viés se materializa em **efeitos desiguais sobre grupos** (por origem, gênero, região, renda): classificação de risco que pune mais um grupo, triagem de currículos, priorização de auditoria. Distinguir:

- **tratamento desigual intencional** (discriminação direta) de **impacto desproporcional** (discriminação indireta/estatística — resultado desigual sem intenção);
- **disparidade ≠ discriminação** sempre: exige análise do **porquê** (a LGPD veda tratamento para fins **discriminatórios ilícitos ou abusivos** — art. 6º, IX).

### 3.4 Monitoramento de equidade

Avaliar **métricas por grupo** (taxa de erro, falsos positivos por grupo), **auditar** o modelo (análise de viés) e prever **recurso/contestação** ao afetado (item 5.2).

## 4. Proteção de informações, supervisão, rastreabilidade e contestação (5.2)

### 4.1 Proteção de informações

- **Não enviar dados pessoais/sensíveis ou sigilosos** a serviços de IA **sem base legal e salvaguardas** (LGPD: dados pessoais, sensíveis, segredos);
- **verificar** política de retenção/uso do provedor (dados usados para treinar?);
- **preferir processamento local/controlado** para dados sensíveis;
- aplicar **minimização** (enviar só o necessário) e **anonimização/pseudonimização** quando possível;
- **menor privilégio** no acesso a ferramentas e bases pelos agentes de IA.

### 4.2 Supervisão humana

- **Human-in-the-loop** para ações de impacto; **human-on-the-loop** para monitoramento;
- **supervisão proporcional ao risco** (mais risco → mais supervisão);
- **separar decisão de execução:** a IA propõe, o sistema/pessoa valida autorização e escopo;
- a supervisão deve ser **efetiva**, não protocolar (evitar "fadiga de aprovação").

### 4.3 Rastreabilidade

- **Registrar** entradas, saídas, modelo/versão, fontes recuperadas e decisões (auditoria do uso de IA);
- **versionar** modelo, prompt, dados e parâmetros (reprodutibilidade);
- **linhagem dos dados** usados (retoma o item 4.1 de integridade);
- permitir **reconstituir** por que a IA produziu certo resultado (explicabilidade).

### 4.4 Contestação

Garantir **mecanismo de revisão/recurso** ao afetado por decisão apoiada em IA:

- **direito de revisão** de decisão automatizada (LGPD, art. 20);
- **canal de contestação** claro e humano;
- **ônus de transparência** sobre os critérios (LGPD, art. 20, §1º).

### 4.5 Marcos de governança (OECD AI Principles)

Os **OECD AI Principles** (adotados em 2019, atualizados em 2024; o Brasil é aderente) estruturam IA **confiável** em cinco princípios baseados em valores:

1. **Crescimento inclusivo, desenvolvimento sustentável e bem-estar;**
2. **Direitos humanos e valores democráticos, incluindo equidade (fairness) e privacidade;**
3. **Transparência e explicabilidade;**
4. **Robustez, segurança e proteção (security and safety);**
5. **Responsabilização (accountability).**

A eles somam-se recomendações de política pública (investimento em P&D, ecossistema, governança interoperável, capacitação humana, cooperação internacional). Esses princípios espelham, em governança, o que a disciplina exige conceitualmente: **transparência, robustez e accountability**.

## 5. Verificação de fontes e limites da automação de decisões que afetam direitos (5.3)

### 5.1 Verificação de fontes (a IA não "sabe" — recupera)

- A IA **não garante veracidade**: tudo o que gera é **candidato** a ser checado.
- **Exigir citação/fonte** e **conferir na fonte primária** (a citação pode ser alucinada).
- **Avaliar procedência, autoridade, atualidade e conflito de fontes** (retoma item 1.2 da disciplina).
- **Desconfiar de referências que não se consegue localizar** — sinal clássico de alucinação.
- Em **RAG**, verificar se a resposta é **fiel ao contexto recuperado** (fidelidade/fundamentação), não só fluente.

### 5.2 Limites da automação de decisões que afetam direitos

- **Princípio:** decisões que **afetam direitos/interesses relevantes** não devem ser **totalmente automatizadas** sem salvaguardas — exigem **supervisão humana e possibilidade de revisão/contestação**.
- **Base legal brasileira — LGPD, art. 20:** o titular tem direito de **solicitar a revisão** de decisões tomadas **unicamente com base em tratamento automatizado** de dados pessoais que afetem seus interesses (perfil pessoal, profissional, de consumo, crédito, personalidade).
  - **§1º:** o controlador deve fornecer **informações claras e adequadas** sobre os **critérios e procedimentos** da decisão automatizada (ressalvados segredos comercial e industrial).
  - **§2º:** se negar informações sob alegação de segredo, a **ANPD pode auditar** para verificar **aspectos discriminatórios**.
  - **Nuance decisiva:** a redação final **não exige** que a revisão seja feita **por pessoa natural** — a exigência de "revisão humana" (§3º) foi **VETADA**. A LGPD garante **revisão**, que pode ser automatizada, mas **acompanhada de transparência e fiscalização** contra discriminação.
- **Princípio da não discriminação** (LGPD, art. 6º, IX): veda tratamento para fins **discriminatórios ilícitos ou abusivos**.

### 5.3 Racionalidade dos limites

A automação é **limitada** onde há: **direitos e interesses relevantes**, **discricionariedade/juízo de valor**, **efeitos irreversíveis** ou **exigência legal de motivação/contraditório**. Nesses casos, a IA pode **apoiar** (triagem, rascunho, sumário), mas a **decisão** e sua **motivação** permanecem com o responsável humano — preservando **accountability** (alguém responde pela decisão).

### 5.4 Síntese: IA como apoio, não como substituto

A IA classifica, busca, resume e rascunha — **acelera** o analista; **não o substitui** na verificação, no juízo e na responsabilização. Uso responsável = **tarefa adequada + salvaguarda proporcional + supervisão + transparência + contestação**.

## Detalhes que merecem destaque

- **IA generativa alucina** — todo resultado é **candidato a verificação**, não fato.
- **RAG reduz, não elimina** alucinação e não elimina vieses/erros.
- **Parcimônia:** usar a **solução mais simples** que atenda à necessidade com menor risco.
- **Viés algorítmico é herdado e amplificado** dos dados de treino.
- **Disparidade ≠ discriminação sempre** — importa o *porquê* (LGPD art. 6º, IX).
- **LGPD art. 20:** direito de **revisão** (não necessariamente humana — o §3º foi **vetado**).
- **OECD AI Principles (5):** crescimento inclusivo; direitos humanos/equidade/privacidade; transparência/explicabilidade; robustez/segurança; accountability.
- **Supervisão proporcional ao risco:** human-in-the-loop para impacto, human-on-the-loop para monitoramento.
- **Rastreabilidade e contestação** são indissociáveis do uso responsável.

## Comparações que a banca costuma cobrar (certo/errado)

| Conceito A | Conceito B | Diferença-chave |
| --- | --- | --- |
| Alucinação | Conteúdo não sustentado | Alucinação = invenção plausível; não sustentado = sem base na fonte/contexto (pode ser "verdadeiro" por acaso). |
| Classificação supervisionada | Não supervisionada | Supervisionada = rótulos de treino; não supervisionada = agrupa sem rótulos. |
| Busca lexical | Busca semântica (IA) | Lexical = termo exato; semântica = significado (embeddings). |
| Regra simples | IA generativa | Regra = determinística/auditável; LLM = flexível, porém alucina/custa mais. |
| Human-in-the-loop | Human-on-the-loop | In-the-loop = **aprova antes**; on-the-loop = **monitora** e pode intervir. |
| Revisão humana (LGPD §3º vetado) | Revisão (LGPD art. 20 caput) | A lei garante **revisão**, mas **não** exige que seja por pessoa natural. |
| Viés de representação | Viés histórico/social | Representação = grupo sub-representado nos dados; histórico = dados refletem discriminação passada. |
| Transparência (OECD) | Explicabilidade | Transparência = divulgar uso/critérios; explicabilidade = compreender **como** chegou ao resultado. |
| Accountability | Supervisão | Accountability = **quem responde**; supervisão = mecanismo de **controle** humano. |

## Pegadinhas e erros comuns

> Cuidado com termos absolutos ("sempre", "nunca", "exclusivamente") e com a troca de requisitos.

- Achar que **a IA "sabe"** e confiar na resposta sem verificar fonte — a fonte pode ser **alucinada**.
- Afirmar que **RAG elimina alucinação/erro** — **reduz**, não elimina.
- Dizer que a **LGPD exige revisão por pessoa natural** — o dispositivo que exigia revisão humana (§3º) foi **VETADO**; a lei exige **revisão** + transparência + auditoria contra discriminação.
- Confundir **disparidade de resultado com discriminação** — exige análise da causa.
- Usar **IA generativa** onde uma **regra simples** resolve (violação de parcimônia).
- Enviar **dados pessoais/sensíveis** a serviço de IA sem base legal e salvaguardas.
- Achar que **explicabilidade e transparência** são a mesma coisa.
- Supor que **supervisão humana** dispensa **rastreabilidade e contestação** (são salvaguardas complementares).
- Tratar **viés algorítmico** como "mero erro técnico" — tem efeito **sobre grupos e direitos**.

## Notas atômicas relacionadas

```dataview
LIST FROM "20 - Notas"
WHERE disciplina = this.disciplina
  AND contains(tema, this.tema)
SORT file.name ASC
```

## Fontes

- https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709.htm (LGPD — art. 20 (revisão de decisões automatizadas), art. 6º, IX (não discriminação), definições de anonimização)
- https://blog.idp.edu.br/direito-digital/artigo-20-lgpd-revisao-decisoes-automatizadas/ (Artigo 20 da LGPD — revisão de decisões automatizadas)
- https://lgpd-brasil.info/capitulo_03/artigo_20 (LGPD — artigo 20 comentado)
- https://oecd.ai/en/ai-principles (OECD AI Principles — os cinco princípios baseados em valores e a definição de sistema de IA)
- https://legalinstruments.oecd.org/en/instruments/oecd-legal-0449 (OECD — Recommendation on AI (instrumento legal; princípios e recomendações))
- https://www.oecd.org/en/topics/sub-issues/ai-principles.html (OECD — AI principles; primeira norma intergovernamental sobre IA)
- https://genai.owasp.org/llm-top-10/ (OWASP Top 10 for LLM Applications 2025 — alucinação/misinformation, viés, riscos)
- https://genai.owasp.org/llmrisk/llm09-misinformation/ (OWASP LLM09 — misinformation/alucinação)
- https://www.mongodb.com/resources/basics/reciprocal-rank-fusion (Busca/recuperação — contexto de IA e RAG)
- https://developers.openai.com/api/docs/guides/embeddings (OpenAI — embeddings e busca semântica; base de RAG)
- https://www.anthropic.com/engineering/building-effective-agents (Anthropic — quando usar IA/simples/humano; workflows vs. agentes)
- https://confidata.com.br/blog/lgpd-comentada-13-prazos-decisoes-automatizadas (LGPD — decisões automatizadas e direito à revisão na prática)
- https://www.gov.br/cgu/pt-br (CGU — contexto de uso responsável de dados/IA no controle público)
- https://gutembergamorim.com.br/lgpd-ia-decisoes-automatizadas-e-discriminacao-algoritmica-o-direito-de-revisao-no-art-20-da-lgpd/ (LGPD + IA — discriminação algorítmica e direito de revisão)
