---
tipo: resumo
disciplina: "Engenharia de Software e Programação"
tema: "Problemas e requisitos"
status: novo
data: "2026-10-16"
tags: [resumo, engenharia-software, cgu-2026]
---

# Resumo: Problemas e requisitos

> [!info] MOC: [[Engenharia de Software e Programação]]
> Edital nº 1/2026 – CGU – AFFC · **Conhecimentos específicos** · Cargo 4 (TI / Desenvolvimento de Sistemas) · Item 1 — *Problemas e requisitos*.

## Escopo no edital (checklist)

- [x] 1.1 Necessidades de usuários.
- [x] 1.2 Requisitos funcionais e não funcionais.
- [x] 1.3 Restrições e critérios de aceitação.
- [x] 1.4 Desenho centrado nas pessoas.
- [x] 1.5 Relações entre problema público, processo de trabalho e solução digital.

## Resumo

Este item cobre o **início do ciclo de vida**: entender o problema antes de escrever código. O fio condutor é transformar uma **necessidade real de um usuário/cidadão** em um **requisito testável** que orienta uma **solução digital**, respeitando **restrições** e o **processo de trabalho** público.

1. **Necessidades de usuários** são o ponto de partida — descobertas por **elicitação** (entrevistas, observação, questionários, workshops, análise de documentos) e representadas por **personas**, **jornadas** e **histórias de usuário**.
2. **Requisitos** dividem-se em **funcionais** (o que o sistema *faz* — comportamentos e regras de negócio) e **não funcionais** (o *como* — desempenho, segurança, usabilidade, disponibilidade), sendo que estes últimos costumam cair em prova como "qualidades/atributos" (ISO/IEC 25010, FURPS+).
3. **Critérios de aceitação** tornam a história **verificável** (formato Gherkin *Dado/Quando/Então*), e **restrições** limitam as opções de solução (técnicas, legais, orçamentárias, prazos).
4. **Desenho centrado nas pessoas** (UCD/ISO 9241-210) coloca o usuário no centro: pesquisa, **prototipagem**, **testes de usabilidade** e iteração contínua.
5. A **relação problema público → processo de trabalho → solução digital** é o que distingue TI governamental: a solução digital existe para atender uma **política/serviço público**, respeitando **Lei de Acesso à Informação, LGPD, transparência** e o marco do **Governo Digital (Lei nº 14.129/2021)**.

## 1. Necessidades de usuários (1.1)

### 1.1 Conceitos centrais

- **Necessidade:** o que o usuário *precisa* fazer/alcançar (problema a resolver), não a solução. "Preciso renovar minha CNH" ≠ "quero um botão X".
- **Requisito:** uma **declaração verificável** sobre o que o sistema deve fazer (funcional) ou sobre atributos/restrições (não funcional).
- **Stakeholder (parte interessada):** qualquer pessoa/órgão afetado ou que influencia o sistema — cidadão, servidor, gestor, órgão de controle, equipe técnica.
- A distinção **problema × solução** é cobrada com frequência: um requisito deve descrever o **problema/necessidade**, deixando a solução técnica para a fase de design.

### 1.2 Técnicas de elicitação (levantamento)

| Técnica | Descrição | Quando usar |
| --- | --- | --- |
| **Entrevista** | Conversa estruturada/semiestruturada com stakeholders | Aprofundar contexto e motivações |
| **Questionário/survey** | Perguntas em massa | Validar hipóteses com muitos usuários |
| **Workshop** (JAD) | Sessão colaborativa com vários stakeholders | Alinhar visões conflitantes |
| **Observação** | Ver o usuário trabalhar (job shadowing) | Descobrir o que ele *faz* vs o que *diz* |
| **Análise de documentos/legislação** | Leis, portarias, processos existentes | Domínio público/normativo |
| **Prototipagem** | Modelo exploratório da solução | Validar entendimento cedo |
| **Brainstorming** | Geração livre de ideias | Expandir alternativas |
| **Análise de concorrentes/benchmark** | Estudar soluções semelhantes | Reuso de boas práticas |

### 1.3 Artefatos de descoberta

- **Persona:** perfil fictício, porém baseado em dados reais, que representa um grupo de usuários (nome, contexto, objetivos, dores). Ajuda a decidir "para quem" se projeta.
- **Jornada do usuário (user journey):** linha do tempo das etapas, ações, emoções e pontos de dor do usuário ao tentar cumprir uma tarefa.
- **História de usuário (user story):** descrição curta no formato **"Como [papel/persona], quero [ação/capacidade], para [benefício/valor]"**.
- **Épico:** história grande, de granulação grossa, quebrada em histórias menores ao longo do backlog.
- **Story mapping:** organiza histórias no fluxo da jornada, priorizando por valor.

> Exemplo: *"Como cidadão, quero acompanhar o andamento do meu pedido de informação, para saber quando receberei a resposta."*

### 1.4 Os 3 Cs e INVEST

- **3 Cs da história:** **Card** (registro conciso), **Conversation** (o detalhe emerge da conversa com o time/PO), **Confirmation** (critérios de aceitação que confirmam que foi feita).
- **INVEST** (qualidades de uma boa história): **I**ndependent, **N**egotiable, **V**aluable, **E**stimable, **S**mall, **T**estable.

## 2. Requisitos funcionais e não funcionais (1.2)

### 2.1 Requisitos funcionais (RF)

Descrevem **comportamentos e regras de negócio** — o que o sistema deve **fazer**. São testáveis como "entrada → processamento → saída".

- "O sistema deve permitir registrar um pedido de acesso à informação."
- "O sistema deve validar CPF e rejeitar cadastros duplicados."
- "O sistema deve gerar relatório mensal de atendimentos."

### 2.2 Requisitos não funcionais (RNF)

Descrevem **atributos de qualidade e restrições** sobre *como* o sistema funciona. São os mais cobrados em prova; a banca gosta de trocar RF por RNF.

- "O sistema deve responder em até **2 segundos** para 95% das requisições." (desempenho)
- "O sistema deve estar disponível **99,9%** do tempo." (disponibilidade)
- "Os dados pessoais devem ser **criptografados** em repouso e em trânsito." (segurança)
- "A interface deve ser utilizável por **leitores de tela**." (acessibilidade/usabilidade)

### 2.3 Modelos de classificação de RNF

- **ISO/IEC 25010** (modelo de qualidade do produto): adequação funcional, **eficiência de desempenho**, **compatibilidade**, **usabilidade**, **confiabilidade**, **segurança**, **manutenibilidade**, **portabilidade**.
- **FURPS(+):** **F**unctionality, **U**sability, **R**eliability, **P**erformance, **S**upportability (+ restrições de design, implementação, interface e físicas).
- Outros RNF comuns: **escalabilidade**, **interoperabilidade**, **auditabilidade**, **conformidade legal**, **acessibilidade (WCAG)**.

### 2.4 Por que separar RF de RNF

- RNFs são **transversais** e impactam a **arquitetura** (um requisito de desempenho pode exigir cache, filas, escalabilidade horizontal).
- RNFs mal definidos viram **débito técnico** e **falhas de serviço** (relação com os itens 5.1 e 5.4).
- RNFs devem ser **mensuráveis** (métrica + meta + condição), não vagos ("rápido" → "≤ 2 s").

## 3. Restrições e critérios de aceitação (1.3)

### 3.1 Restrições (constraints)

Limitações que **restringem as opções de design/solução**, impostas por fatores externos ou decisões anteriores. Não são "requisitos de comportamento", mas **regras que a solução deve respeitar**.

| Tipo | Exemplo |
| --- | --- |
| **Legal/normativa** | LGPD (Lei nº 13.709/2018), LAI (Lei nº 12.527/2011), Lei do Governo Digital (14.129/2021) |
| **Tecnológica** | "Usar a plataforma já homologada (Java/Spring)"; "hospedar no ambiente do órgão" |
| **Orçamentária** | Limite de custo de licenças/hospedagem |
| **Temporal** | Prazo limite definido por decreto/portaria |
| **Organizacional** | Processos internos, padrões corporativos, segurança da informação |
| **Interoperabilidade** | "Integrar com o barramento/API do governo (gov.br)" |

### 3.2 Critérios de aceitação (CA)

Condições **objetivas e verificáveis** que definem quando uma história/requisito está **concluído**. São a base dos **testes de aceitação**. Diferença sutil que a banca explora:

- **Critério de aceitação** = condição que a *funcionalidade* deve cumprir (testável).
- **Definition of Done (DoD)** = critério **transversal** de "pronto" aplicável a toda entrega (testado, documentado, revisado, em produção).

### 3.3 Formato Gherkin (Given/When/Then)

Usado para escrever CAs executáveis (BDD):

```gherkin
Funcionalidade: Registrar pedido de acesso à informação

Cenário: Pedido com CPF válido
  Dado que o cidadão informa nome e CPF válidos
  E um texto de pedido com até 500 caracteres
  Quando ele envia o pedido
  Então o sistema gera um número de protocolo
  E registra a data/hora de recebimento
```

- **Dado (Given):** pré-condição/contexto. **Quando (When):** ação disparada. **Então (Then):** resultado esperado.
- CAs devem ser **específicos, mensuráveis e verificáveis**; evite termos vagos ("rápido", "fácil", "bom").

### 3.4 Critério de aceitação × requisito

- Um requisito pode ter **vários** critérios de aceitação.
- CA define os **limites de sucesso** (e ajuda a derivar **testes de borda** — conexão com o item 2.6).

## 4. Desenho centrado nas pessoas (1.4)

### 4.1 UCD — User-Centered Design

- O **desenho centrado no usuário (DCU/UCD)** é um processo iterativo formalizado pela **ISO 9241-210** (ergonomia da interação humano-sistema). O usuário participa de **todas** as fases.
- Fases do ciclo UCD: **1)** entender e especificar o contexto de uso; **2)** especificar requisitos do usuário e da organização; **3)** produzir soluções de design; **4)** **avaliar** contra os requisitos — e iterar.
- Distinção frequente: **UX (experiência do usuário)** é o conjunto de percepções e respostas do usuário ao usar o sistema (emoção, satisfação); **usabilidade** é a medida de eficácia, eficiência e satisfação ao realizar tarefas.

### 4.2 Usabilidade (ISO 9241-11)

**Grau em que um produto pode ser usado por usuários específicos para atingir objetivos específicos com eficácia, eficiência e satisfação num contexto de uso específico.**

- **Eficácia:** o usuário **consegue** concluir a tarefa (precisão e completude).
- **Eficiência:** recursos gastos (tempo, esforço) para concluir.
- **Satisfação:** ausência de desconforto e atitude positiva.
- Medidas típicas: taxa de sucesso, tempo de tarefa, taxa de erro, escalas de satisfação (SUS).

### 4.3 Heurísticas de Nielsen (avaliação rápida)

Jakob Nielsen define **10 heurísticas** de usabilidade (usadas em **avaliação heurística**):

1. **Visibilidade do status** do sistema.
2. **Correspondência entre sistema e mundo real** (linguagem do usuário).
3. **Controle e liberdade** do usuário (desfazer/refazer).
4. **Consistência e padrões**.
5. **Prevenção de erros** (melhor que mensagens de erro).
6. **Reconhecimento em vez de memorização**.
7. **Flexibilidade e eficiência** de uso (atalhos).
8. **Design estético e minimalista**.
9. **Ajudar a reconhecer, diagnosticar e recuperar** de erros.
10. **Ajuda e documentação**.

### 4.4 Prototipagem

- **Protótipo:** representação antecipada e interativa (de baixa ou alta fidelidade) da solução, para **aprender e validar** antes de construir.
- **Baixa fidelidade:** papel, rabiscoframes (wireframes) — rápido, barato, foca estrutura/fluxo.
- **Alta fidelidade:** próximo do visual/interação final (HTML, Figma) — valida look & feel e usabilidade.
- **Throwaway (descartável)** vs **evolucionário** (evolui até virar o produto).
- O protótipo ajuda a **reduzir risco** e **descoberta de requisitos** (elicitação), evitando retrabalho caro.

### 4.5 Testes de usabilidade

- Sessões onde usuários reais executam tarefas enquanto se observa e coleta métricas (tempo, erros, satisfação).
- **Moderado vs não moderado**; **presencial vs remoto**; **teste A/B** compara variantes.
- Resultados alimentam **iteração** do design (ciclo construir-medir-aprender).

## 5. Problema público, processo de trabalho e solução digital (1.5)

### 5.1 A cadeia de valor pública

- **Problema público:** situação que afeta a sociedade e que o Estado deve enfrentar (ex.: dificuldade do cidadão em acessar informações públicas).
- **Política pública / serviço público:** a resposta institucional ao problema (ex.: LAI e os serviços de acesso à informação).
- **Processo de trabalho:** o fluxo de atividades, atores e regras que operacionaliza o serviço (ex.: protocolo, triagem, análise, resposta).
- **Solução digital:** o software que **instrumenta/automatiza** o processo, **não** o substitui como fim em si.

> A armadilha conceitual: **a solução digital não é o objetivo**; ela é o **meio** para resolver o problema público. Automatizar um processo mal desenhado só escala a ineficiência.

### 5.2 Análise do processo antes da solução

- **AS-IS × TO-BE:** mapear o processo **atual** (as-is) e desenhar o **futuro** (to-be), eliminando etapas desnecessárias antes de digitalizar.
- **BPMN:** notação para modelar processos (eventos, tarefas, gateways, piscinas/raias).
- **Gaps de processo** identificados na elicitação viram requisitos de mudança (não apenas de sistema).

### 5.3 Governo digital e marco normativo

- **Lei nº 14.129/2021 (Governo Digital):** princípios como **digitalização de serviços públicos**, **governo como plataforma**, **interoperabilidade**, **acessibilidade**, **transparência ativa** e **dados abertos**.
- **Lei nº 12.527/2011 (LAI):** direito de acesso à informação, transparência ativa/passiva.
- **Lei nº 13.709/2018 (LGPD):** tratamento de dados pessoais (base legal, finalidade, minimização) — restrição transversal a qualquer solução.
- **Princípios de serviços digitais públicos (gov.br):** centrado no usuário, simples, acessível, baseado em evidências.
- **Transparência e controle social:** soluções públicas devem ser **auditáveis** e prestar contas (relação com o papel da CGU).

### 5.4 Do problema à solução: visão integrada

| Etapa | Pergunta-chave | Artefato |
| --- | --- | --- |
| Problema público | Que necessidade social existe? | Árvore de problemas, evidências/dados |
| Processo de trabalho | Como o serviço opera hoje? | Mapa AS-IS, BPMN, jornada |
| Requisitos | O que a solução deve fazer e como? | RFs, RNFs, histórias, CAs |
| Solução digital | Qual desenho atende os requisitos? | Protótipo, arquitetura, backlog |

## Detalhes que merecem destaque

- **Requisito funcional = comportamento; requisito não funcional = atributo de qualidade/restrição.** "Criptografar dados" é RNF (segurança); "listar pedidos" é RF.
- **Critério de aceitação ≠ Definition of Done:** CA é da funcionalidade; DoD é critério global de "pronto".
- **User story segue o formato "Como… quero… para…"** e deve atender **INVEST**; o detalhe nasce da **conversa** (3 Cs).
- **UCD (ISO 9241-210)** é **iterativo**: especificar contexto → requisitos → design → avaliar.
- **Usabilidade (ISO 9241-11)** = **eficácia + eficiência + satisfação** num contexto; UX é mais amplo (emoções/percepções).
- **Heurísticas de Nielsen** (10) embasam a **avaliação heurística** — inspeção rápida por especialistas.
- **Protótipo de baixa fidelidade** valida fluxo; **alta fidelidade** valida interação/visual.
- **Solução digital é meio, não fim**: automatizar processo ruim não resolve problema público.
- **Marco legal**: Lei 14.129/2021 (Governo Digital), LAI (12.527/2011), LGPD (13.709/2018) — restrições e princípios de TI pública.
- **Gherkin (Dado/Quando/Então)** torna critérios de aceitação **executáveis** (BDD) e deriva **testes de borda**.

## Comparações que a banca costuma cobrar (certo/errado)

| Conceito A | Conceito B | Diferença-chave |
| --- | --- | --- |
| Requisito funcional | Requisito não funcional | RF = o que faz; RNF = como/quão bem (qualidade/restrição) |
| Necessidade | Requisito | Necessidade é o problema; requisito é a declaração verificável da solução |
| Requisito | Restrição | Requisito descreve comportamento/atributo; restrição **limita** as opções de solução |
| Critério de aceitação | Definition of Done | CA = específico da história; DoD = transversal a toda entrega |
| User story | Caso de uso | Story é informal/negociável (agile); caso de uso é especificação detalhada de interações |
| Usabilidade | UX | Usabilidade = eficácia/eficiência/satisfação; UX = percepção/emoção ampla |
| Persona | Stakeholder | Persona é perfil-ficção do usuário-tipo; stakeholder é parte interessada real |
| Eficácia | Eficiência | Eficácia = conseguir concluir; eficiência = gastar menos recursos |
| Protótipo baixa fidelidade | Alta fidelidade | Baixa = estrutura/fluxo rápido; alta = visual/interação próxima do final |
| Avaliação heurística | Teste de usabilidade | Heurística = especialistas inspecionam; teste = usuários reais executam tarefas |
| Processo de trabalho | Solução digital | Processo é o fluxo do serviço; solução é o software que o instrumenta |

## Pegadinhas e erros comuns

> Cuidado com termos absolutos ("sempre", "nunca", "exclusivamente") e com a troca de requisitos.

- Trocar **RF por RNF**: dizer que "tempo de resposta" é requisito funcional (é **não funcional**/desempenho).
- Afirmar que **RNF é "menos importante"** ou que "não precisa ser testado" — RNFs são testáveis e impactam a arquitetura.
- Confundir **critério de aceitação** com **Definition of Done**.
- Dizer que **user story é um requisito formal completo e detalhado** — ela é um **lembrete para a conversa**, negociável e pequena.
- Escrever critério de aceitação **vago** ("o sistema deve ser rápido") — deve ser **mensurável e verificável**.
- Confundir **persona** (perfil-ficção) com **usuário real individual** ou com **stakeholder**.
- Reduzir **usabilidade** a "ser bonito" — é **eficácia + eficiência + satisfação** mensuráveis.
- Afirmar que **UCD é uma etapa única** no início do projeto — é um **processo iterativo** ao longo de todo o ciclo.
- Achar que **protótipo substitui os requisitos** — ele é meio de **elicitação/validação**, não a especificação.
- Confundir **problema público** com a **solução digital** (automatizar ≠ resolver o problema).
- Ignorar **restrições legais** (LGPD/LAI) como se fossem "opcionais" — são impositivas no setor público.
- Dizer que **elicitação ocorre só no início** — é contínua (refinamento de backlog, descoberta contínua).

## Notas atômicas relacionadas

```dataview
LIST FROM "20 - Notas"
WHERE disciplina = this.disciplina
  AND contains(tema, this.tema)
SORT file.name ASC
```

## Fontes

- https://www.iso.org/standard/52075.html — ISO 9241-210, Human-centred design for interactive systems (UCD).
- https://www.iso.org/obp/ui/#iso:std:iso:9241:-11:ed-2:v1:en — ISO 9241-11, Usabilidade: eficácia, eficiência e satisfação.
- https://www.nngroup.com/articles/ten-usability-heuristics/ — Jakob Nielsen, 10 Usability Heuristics (avaliação heurística).
- https://www.nngroup.com/articles/usability-101-introduction-to-usability/ — Nielsen Norman Group, introdução à usabilidade e UX.
- https://www.mountaingoatsoftware.com/agile/user-stories — Mountain Goat Software, user stories (formato, 3 Cs, INVEST).
- https://www.mountaingoatsoftware.com/agile/non-functional-requirements-as-user-stories — RNF como user stories.
- https://cucumber.io/docs/gherkin/reference/ — Gherkin (Given/When/Then) para critérios de aceitação.
- https://iso25000.com/index.php/en/iso-25000-standards/iso-25010 — ISO/IEC 25010, modelo de qualidade de software (RNF).
- https://www.iso.org/standard/84948.html — ISO/IEC/IEEE 29148, Requirements Engineering (requisitos e elicitação).
- https://www.iiba.org/standards-and-resources/babok/ — IIBA BABOK, guia de análise de negócios e requisitos.
- https://www.ireb.org/en/cpre/ — IREB CPRE, Certified Professional for Requirements Engineering.
- https://www.planalto.gov.br/ccivil_03/_ato2019-2022/2021/lei/l14129.htm — Lei nº 14.129/2021, Governo Digital (princípios, serviços digitais).
- https://www.planalto.gov.br/ccivil_03/_ato2011-2014/2011/lei/l12527.htm — Lei nº 12.527/2011 (LAI), acesso à informação.
- https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709.htm — Lei nº 13.709/2018 (LGPD), proteção de dados.
- https://www.gov.br/governodigital/pt-br/estrategia-de-governanca-digital — Estratégia de Governo Digital (gov.br).
