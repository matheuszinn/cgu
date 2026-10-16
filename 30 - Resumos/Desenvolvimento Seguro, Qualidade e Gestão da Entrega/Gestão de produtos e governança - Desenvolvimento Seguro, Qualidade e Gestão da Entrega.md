---
tipo: resumo
disciplina: "Desenvolvimento Seguro, Qualidade e Gestão da Entrega"
tema: "Gestão de produtos e governança"
status: novo
data: "2026-10-16"
tags: [resumo, desenvolvimento-seguro, cgu-2026]
---

# Resumo: Gestão de produtos e governança

> [!info] MOC: [[Desenvolvimento Seguro, Qualidade e Gestão da Entrega]]
> Edital nº 1/2026 – CGU – AFFC · **Conhecimentos específicos** · Cargo 4 (TI / Desenvolvimento de Sistemas) · Item 4 — *Gestão de produtos e governança*.

## Escopo no edital (checklist)

- [x] 4.1 Descoberta de necessidades, entrega e ciclo de vida de produtos digitais.
- [x] 4.2 Scrum e Kanban.
- [x] 4.3 Priorização, critérios de aceitação e indicadores de resultado.
- [x] 4.4 PDTIC, plano de transformação digital e plano de dados abertos aplicados a produtos e integrações.
- [x] 4.5 Riscos, responsabilidades e evidências de efetividade de controles.

## Resumo

O item reúne **gestão de produtos digitais** e **governança** no setor público: como **descobrir necessidades**, **entregar** e gerir o **ciclo de vida** do produto, operando com métodos ágeis (**Scrum** e **Kanban**), **priorização**, **critérios de aceitação** e **indicadores de resultado** (OKRs); e como esses produtos se conectam aos instrumentos de governança pública (**PDTIC**, **plano de transformação digital**, **plano de dados abertos**), com gestão de **riscos**, **responsabilidades** e **evidências de efetividade de controles**.

Três ideias-força:

1. **Produto digital é contínuo, não projeto pontual:** passa por **descoberta contínua** (entender o problema/usuário) e **entrega contínua** (incrementos de valor), com **ciclo de vida** (concepção → crescimento → maturidade → declínio). **MVP** valida hipóteses com o mínimo viável.
2. **Scrum e Kanban são métodos ágeis diferentes:** Scrum é **framework empírico** com papéis, eventos e artefatos (timebox); Kanban é **método de fluxo** contínuo com limites de WIP. Ambos usam **critérios de aceitação** e **DoD** para garantir qualidade do que é entregue.
3. **Governança pública amarra tudo:** o **PDTIC** (tático) alinha-se à **Estratégia de Governo Digital** e ao **plano de transformação digital**; a **Lei 14.129/2021** e o **Decreto 10.332/2020** orientam governo digital e **dados abertos**. Riscos e controles exigem **evidências de efetividade** (quem é responsável, o que foi feito, com que resultado).

## 1. Descoberta de necessidades, entrega e ciclo de vida (4.1)

### 1.1 Descoberta e descoberta contínua

- **Descoberta (discovery):** entender o **problema**, o **usuário** e o **valor** antes de construir. **Continuous discovery** (Teresa Torres) mantém esse entendimento sempre atualizado ao longo da vida do produto.
- Técnicas: entrevistas, **personas**, **jornadas do usuário**, **mapa de empatia**, protótipos, testes de usabilidade, análise de dados.
- **Problema × solução:** primeiro validar o **problema** (as pessoas têm a dor?), depois a **solução** (resolve a dor?), depois a **entrega** (a solução funciona em escala?).

### 1.2 MVP e entrega

- **MVP (Minimum Viable Product):** versão mínima para **aprender** com o menor esforço (não é "produto capenga"; é o menor experimento que valida a hipótese).
- **Entrega contínua de valor:** pequenos incrementos frequentes, medindo resultado (não só output). **Outcome (resultado)** = mudança de comportamento/valor; **output (saída)** = artefato entregue.
- **Feedback loop:** construir → medir → aprender (ciclo *Build-Measure-Learn*, Lean Startup).

### 1.3 Ciclo de vida de produto

- Fases típicas: **concepção/descoberta → desenvolvimento → lançamento (introdução) → crescimento → maturidade → declínio/descontinuação**.
- **Gestão de ciclo de vida:** decisões de investir, manter, evoluir ou **aposentar** (sunset); gerenciar **EOL (end-of-life)**, migração de usuários e **dívida técnica**.
- **Roadmap de produto:** orientado a **temas/objetivos** (agora/próximo/mais tarde) mais que a datas fixas.

## 2. Scrum e Kanban (4.2)

### 2.1 Scrum (Scrum Guide 2020)

- **Framework empírico** baseado em **transparência, inspeção e adaptação**.
- **Scrum Team** (3 accountabilities — a edição 2020 eliminou o "Development Team" como papel separado):
  - **Product Owner:** maximiza o valor; é dono do **Product Backlog** (ordenação e priorização).
  - **Scrum Master:** serve ao time e à organização; garante o Scrum (facilita eventos, remove impedimentos) — **não** é chefe.
  - **Developers:** criam o incremento; comprometidos com o **Sprint Backlog** e a **Definition of Done**.
- **Eventos (timeboxes):**
  - **Sprint:** contêiner de todos os eventos; **≤ 1 mês**, duração fixa.
  - **Sprint Planning:** planeja o trabalho do Sprint (Why/What/How) — até 8h para Sprint de 1 mês.
  - **Daily Scrum:** inspeção diária (15 min) do progresso rumo ao **Sprint Goal**.
  - **Sprint Review:** inspeção do **incremento** e ajuste do Product Backlog (stakeholders participam).
  - **Sprint Retrospective:** inspeção do **processo** (o que melhorar).
- **Artefatos e compromissos (commitments):**
  | Artefato | Compromisso (commitment) |
  | --- | --- |
  | Product Backlog | **Product Goal** |
  | Sprint Backlog | **Sprint Goal** |
  | Increment | **Definition of Done (DoD)** |
- **Definition of Done (DoD):** descrição formal do estado do **incremento** quando atinge a qualidade exigida. Item do backlog que **não** cumpre a DoD **não pode ser liberado**.

### 2.2 Kanban

- **Método de gestão de fluxo** (não framework com papéis/eventos fixos). Princípios: começar pelo que se faz hoje; buscar **mudança evolutiva**; respeitar papéis atuais; **liderança** em todos os níveis.
- **Práticas:** visualizar o fluxo (**quadro Kanban**), **limitar o WIP** (work in progress), gerenciar o fluxo, tornar políticas explícitas, implementar **feedback loops**, melhorar colaborativamente.
- **Métricas de fluxo:** **lead time** (do pedido à entrega), **cycle time** (do início do trabalho à entrega), **throughput**, **WIP**, **CFD (Cumulative Flow Diagram)**.
- **Kanban vs. Scrum:** Kanban não tem Sprint nem papéis obrigatórios; é **puxado** (pull) contínuo com WIP limitado; Scrum é **iterativo** com timebox. Podem combinar-se (**Scrumban**).

## 3. Priorização, critérios de aceitação e indicadores (4.3)

### 3.1 Priorização

- **MoSCoW:** **M**ust (obrigatório), **S**hould (desejável), **C**ould (poderia), **W**on't (não agora). Define **escopo de entrega** (o que entra ou não).
- **RICE:** pontuação = **Reach × Impact × Confidence ÷ Effort** — **ordena** o backlog com nota comparável.
- **Outros:** **ICE** (Impact, Confidence, Ease — triagem rápida), **WSJF** (Weighted Shortest Job First — do SAFe, usa *cost of delay*), **Kano** (satisfação × investimento), **value vs. effort** (matriz).
- **RICE ordena; MoSCoW delimita escopo** — não são excludentes; podem ser usados em conjunto.

### 3.2 Critérios de aceitação e DoD

- **Critérios de aceitação:** condições que uma história/funcionalidade deve satisfazer para ser **aceita** pelo Product Owner/usuário. Formato comum: **Gherkin** (Given/When/Then) ou lista de verificação.
- **Definition of Done:** padrão de **qualidade do incremento** (testado, revisado, integrado, documentado) — diferente dos critérios de aceitação (que são específicos de cada item).
- **INVEST** para histórias: **I**ndependent, **N**egotiable, **V**aluable, **E**stimable, **S**mall, **T**estable.

### 3.3 Indicadores de resultado

- **KPI (Key Performance Indicator):** métrica de desempenho (pode medir processo/resultado).
- **OKR (Objectives and Key Results):** **Objective** (objetivo qualitativo ambicioso) + **Key Results** (resultados-chave mensuráveis, 3–5, verificáveis). Conecta produto à estratégia.
- **Outcome vs. output:** indicadores de **resultado** medem valor/impacto (ex.: redução de tempo de serviço), não só entregas (ex.: nº de telas).
- **Métricas de produto:** adoção, retenção, engajamento, satisfação (NPS/CSAT), conversão, **north-star metric** (métrica-guia).

## 4. PDTIC, plano de transformação digital e dados abertos (4.4)

### 4.1 PDTIC

- **PDTIC (Plano Diretor de Tecnologia da Informação e Comunicação):** instrumento de **diagnóstico, planejamento e gestão** de recursos e processos de TIC, de nível **tático**, alinhado à estratégia do órgão. Referência: **Guia de PDTIC do SISP** e **IN SGD/ME nº 1/2019** (processo de contratação de TIC exige alinhamento com o PDTIC).
- Elementos típicos: princípios/diretrizes, **inventário de necessidades**, plano de metas/ações, plano de gestão de pessoas, orçamento e **gestão de riscos**.

### 4.2 Plano de transformação digital e governo digital

- **Decreto nº 10.332/2020:** instituiu a **Estratégia de Governo Digital 2020–2022**, que previu, entre os instrumentos, o **Plano de Transformação Digital** dos órgãos (ações de digitalização de serviços).
- **Lei nº 14.129/2021 (Governo Digital):** dispõe sobre princípios, regras e instrumentos para **governo digital** e aumento da **eficiência pública**. Princípios/diretrizes incluem **desburocratização**, **interoperabilidade de sistemas**, **promoção de dados abertos**, **serviços digitais** e **uso de tecnologias emergentes**.
- Implicações para produtos/integrações: **API-first**, **integração governamental** (ex.: gov.br), **identidade digital** (Login Único), **interoperabilidade** e **dados abertos por padrão**.

### 4.3 Plano de dados abertos (PDA)

- **Dados abertos:** dados acessíveis ao público, em **formato aberto**, legíveis por máquina, com **licença livre** para uso/reuso (definição alinhada à Lei 14.129/2021).
- **Plano de Dados Abertos (PDA):** instrumento que planeja a **abertura** de bases de dados do órgão, priorizando dados de maior interesse público. Regulamentado por normas federais (ex.: **Decreto nº 8.777/2016** — Política de Dados Abertos do Poder Executivo federal — e resoluções da **CGU/INDA**).
- **LAI (Lei 12.527/2011)** é o fundamento da **transparência ativa**; dados abertos são a forma técnica de cumpri-la.
- **8 princípios dos dados abertos governamentais:** completos, primários, atuais, acessíveis, processáveis por máquina, não discriminatórios, não proprietários, livres de licença.

## 5. Riscos, responsabilidades e evidências de controles (4.5)

### 5.1 Gestão de riscos

- **Risco = probabilidade × impacto.** Ciclo: identificar, analisar/avaliar, tratar (evitar, mitigar, transferir, aceitar), monitorar, comunicar.
- **Matriz de probabilidade × impacto** classifica riscos (baixo/médio/alto/crítico). **Apetite/tolerância a risco** definem o que aceitar.
- Em produto/TI: riscos de **segurança**, **continuidade**, **dependência de fornecedor (lock-in)**, **conformidade legal (LGPD, LAI)**, **entrega**.

### 5.2 Responsabilidades

- **Governança:** definir **papéis e responsabilidades** claros (dono do produto, comitê, gestor de risco, auditor). Modelo **RACI** (Responsible, Accountable, Consulted, Informed).
- **Segregação de funções (SoD):** separar quem desenvolve, quem aprova e quem audita — evitar conflito de interesses.
- **Accountability (responsabilização):** o responsável presta contas pelos resultados.

### 5.3 Evidências de efetividade de controles

- **Controle** = política + procedimento + mecanismo para garantir objetivos. **Efetividade** = o controle **funciona na prática** e reduz o risco.
- **Evidências** comprovam: **design** (o controle existe?) e **operação** (foi executado?). Ex.: logs de aprovação, registros de revisão, atas de comitê, relatórios de testes, trilhas de auditoria.
- **Linhas de defesa:** 1ª (gestão/controles operacionais), 2ª (gestão de riscos/compliance), 3ª (auditoria interna). Alinhado a **COSO** (ERM) e **ISO 31000**.
- **Auditoria/TCU:** órgãos de controle avaliam a **efetividade** dos controles, não apenas sua existência formal.

## Detalhes que merecem destaque

- **Scrum Guide 2020:** três **accountabilities** (PO, SM, Developers); "Development Team" deixou de ser papel separado; os **compromissos** (Product Goal, Sprint Goal, DoD) dão transparência e foco.
- **Definition of Done** é compromisso do **Incremento**; **critérios de aceitação** são específicos de cada **item do backlog** — não confundir.
- **Kanban limita WIP** (puxado, fluxo contínuo); **Scrum usa timebox** (iterativo). Métricas Kanban: **lead time, cycle time, throughput, CFD**.
- **RICE = (Reach × Impact × Confidence) ÷ Effort** — **ordena**; **MoSCoW** — **delimita escopo**.
- **Outcome (resultado) ≠ output (entrega)** — indicadores de resultado medem **valor/impacto**, não nº de artefatos.
- **PDTIC** é **tático**; a **Estratégia de Governo Digital** (Decreto 10.332/2020) é **estratégica**; o **plano de transformação digital** é instrumento do governo digital.
- **Dados abertos** são **acessíveis, em formato aberto, legíveis por máquina e com licença livre** (Lei 14.129/2021).
- **Evidência de efetividade** exige provar **design + operação** do controle (existir e funcionar).

## Comparações que a banca costuma cobrar (certo/errado)

| Conceito A | Conceito B | Diferença-chave |
| --- | --- | --- |
| Scrum | Kanban | Framework iterativo (timebox) × método de fluxo (WIP) |
| Product Owner | Scrum Master | Dona do valor/backlog × garante o processo/impedimentos |
| Sprint Review | Sprint Retrospective | Inspeciona o incremento/produto × inspeciona o processo |
| Product Backlog | Sprint Backlog | Tudo o que se quer no produto × trabalho do Sprint |
| Definition of Done | Critérios de aceitação | Padrão de qualidade do incremento × condições de cada item |
| RICE | MoSCoW | Ordena (pontuação) × delimita escopo (M/S/C/W) |
| KPI | OKR | Métrica de desempenho × objetivo + resultados-chave |
| Outcome | Output | Resultado/valor × entrega/artefato |
| PDTIC | Plano de transformação digital | Plano tático de TIC × ações de digitalização (governo digital) |
| Dados abertos | Transparência ativa (LAI) | Forma técnica (formato aberto) × dever legal de publicar |
| Risco | Controle | Probabilidade × impacto × mecanismo que reduz o risco |
| Design do controle | Operação do controle | Existe formalmente × funcionou na prática |

## Pegadinhas e erros comuns

> Cuidado com termos absolutos ("sempre", "nunca", "exclusivamente") e com a troca de requisitos.

- Achar que **Scrum Master é chefe/gerente do time** — ele **serve** e facilita, não comanda.
- Confundir **Product Owner com Scrum Master** (valor × processo).
- Confundir **Sprint Review** (produto) com **Retrospective** (processo).
- Trocar **Definition of Done** por **critérios de aceitação** — são níveis diferentes.
- Achar que **Kanban tem Sprint obrigatório** — Kanban é **fluxo contínuo**, sem timebox fixo.
- Achar que **MVP é um produto incompleto/ruim** — é o mínimo para **aprender** (validar hipótese).
- Achar que **output é outcome** — entregar telas (output) não é gerar valor (outcome).
- Confundir **PDTIC (tático)** com **Estratégia de Governo Digital (estratégica)**.
- Achar que **dado aberto é qualquer dado publicado** — exige **formato aberto + máquina + licença livre**.
- Achar que **controle existente = controle efetivo** — efetividade exige **evidência de operação**.
- Achar que **RICE e MoSCoW são excludentes** — podem ser combinados (MoSCoW delimita, RICE ordena).

## Notas atômicas relacionadas

```dataview
LIST FROM "20 - Notas"
WHERE disciplina = this.disciplina
  AND contains(tema, this.tema)
SORT file.name ASC
```

## Fontes

- https://scrumguides.org/scrum-guide.html (Scrum Guide 2020 — framework Scrum oficial)
- https://www.scrum.org/resources/what-definition-done (Scrum.org — Definition of Done)
- https://www.scrum.org/resources/what-is-a-product-backlog (Scrum.org — Product Backlog)
- https://www.atlassian.com/agile/kanban (Atlassian — Kanban e WIP)
- https://www.atlassian.com/agile/product-management/prioritization-framework (Atlassian — frameworks de priorização: RICE, MoSCoW, Kano)
- https://www.productplan.com/glossary/moscow-prioritization/ (ProductPlan — MoSCoW)
- https://www.intercom.com/blog/rice-simple-prioritization-for-product-managers/ (Intercom — RICE)
- https://www.planalto.gov.br/ccivil_03/_ato2019-2022/2021/lei/l14129.htm (Lei nº 14.129/2021 — Governo Digital)
- https://www.planalto.gov.br/ccivil_03/_ato2019-2022/2020/decreto/D10332.htm (Decreto nº 10.332/2020 — Estratégia de Governo Digital)
- https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2016/decreto/D8777.htm (Decreto nº 8.777/2016 — Política de Dados Abertos)
- https://www.gov.br/governodigital/pt-br/contratacoes-de-tic/legislacao/processo-de-contratacao-de-solucoes-de-tic-regido-pela-lei-ndeg-8-666-de-1993/instrucao-normativa-sgd-me-no-1-de-4-de-abril-de-2019 (IN SGD/ME nº 1/2019 — contratação de TIC e PDTIC)
- https://www.gov.br/governodigital/pt-br/sisp (SISP — Sistema de Administração dos Recursos de TIC; Guia de PDTIC)
- https://dados.gov.br/ (Portal Brasileiro de Dados Abertos)
- https://www.coso.org/ (COSO — gestão de riscos e controle interno)
- https://www.iso.org/iso-31000-risk-management.html (ISO 31000 — gestão de riscos)
