---
tipo: resumo
disciplina: "Fundamentos de Evidências, Dados e Inteligência Artificial"
tema: "Integridade da evidência e proteção"
status: novo
data: "2026-10-16"
tags: [resumo, dados-ia, cgu-2026]
---

# Resumo: Integridade da evidência e proteção

> [!info] MOC: [[Fundamentos de Evidências, Dados e Inteligência Artificial]]
> Edital nº 1/2026 – CGU – AFFC · **Conhecimentos complementares** · Item 4 — *Integridade da evidência e proteção*.

## Escopo no edital (checklist)

- [x] 4.1 Rastreabilidade e verificação de informações
- [x] 4.1 Comunicação proporcional dos resultados e limites
- [x] 4.2 Escuta sem indução, confidencialidade e risco de identificação indireta.
- [x] 4.3 Distinção entre as condições e os regimes de proteção de entrevistados em auditoria, participantes de pesquisa e denunciantes.

## Resumo

Este bloco trata da **confiabilidade ética e técnica do processo de produção de evidência**. Não basta o dado ser verdadeiro: é preciso que seu **caminho seja rastreável** (de onde veio, como foi tratado), que os resultados sejam **comunicados de modo proporcional** (sem exagerar certeza nem esconder limites) e que as pessoas envolvidas — entrevistados, participantes de pesquisa, denunciantes — tenham seus **direitos e sua identidade protegidos**.

O ponto de maior especificidade é a **distinção entre regimes de proteção**: o entrevistado em **auditoria**, o participante de **pesquisa** e o **denunciante** estão sob normas, finalidades e garantias **diferentes**. Misturar esses regimes (aplicar regra de pesquisa a uma auditoria, ou tratar denunciante como mero "entrevistado") é o erro conceitual central. O fio condutor é a **integridade da evidência**: uma evidência obtida com indução, sem consentimento adequado ou com risco de identificação indevida é **insegura** — tanto do ponto de vista ético quanto probatório.

## 1. Rastreabilidade e verificação de informações (4.1)

### 1.1 Rastreabilidade

Capacidade de **reconstituir o caminho** de uma informação: fonte primária, data, método de coleta, transformações, agregações e a cadeia de quem a produziu/manipulou. Elementos:

- **origem e autoria** (quem, quando, com que finalidade);
- **método** (pesquisa, registro administrativo, estimativa);
- **linhagem/linage** dos dados (transformações aplicadas — filtros, junções, recodificações);
- **versionamento e metadados** (o dado muda? qual versão foi usada?).

Rastreabilidade é condição para **reprodutibilidade**: outro analista deve conseguir **refazer** o caminho e chegar (ou não) ao mesmo resultado.

### 1.2 Verificação de informações

Conjunto de **checagens** antes de usar uma informação: autenticidade, integridade (não foi alterada?), exatidão, atualidade e pertinência. Práticas: conferir na **fonte primária**, conferir **cálculos**, testar **consistência interna** (totais batem com as partes?) e **consistência externa** (fonte independente corrobora?).

### 1.3 Reprodutibilidade e transparência

- **Documentar** decisões analíticas (definições, cortes, exclusões);
- **registrar** código/rotinas (análise reproduzível);
- **distinguir** resultado bruto de resultado processado;
- **preservar** a evidência (guarda de documentos/dados que sustentam o achado) — relevante no controle, em que o achado pode ser contestado.

## 2. Comunicação proporcional dos resultados e limites (4.1)

### 2.1 Proporcionalidade da afirmação

A conclusão deve ser **proporcional à força da evidência**:

- não afirmar **causalidade** onde só há **associação**;
- não generalizar para a **população** o que vem de **amostra não representativa**;
- não transformar **indício/sinal** em **fato**;
- não converter **percepção** em **ocorrência**.

"Proporcional" significa: **o grau de certeza expresso acompanha o grau de certeza sustentado pelos dados**.

### 2.2 Declaração de limites

Comunicação íntegra **explicita**:

- **fonte e qualidade** do dado;
- **margem de erro / intervalo de confiança**;
- **limitações metodológicas** (confundidores, cobertura, definições);
- **o que o dado NÃO mostra** (evitar uso indevido);
- **contexto de comparação** (denominador, período).

Ocultar limites para "fortalecer" a conclusão é **desinformação por omissão** — inverte a integridade da evidência.

### 2.3 Comunicação e audiência

- Linguagem **clara e honesta** (evitar jargão que mascara incerteza);
- **separar** fato, interpretação e juízo de valor (retoma o item 1.2);
- apresentar **contra-argumentos/alternativas** quando relevantes;
- evitar **números descontextualizados** e gráficos manipulados (eixo truncado, escalas enganosas).

### 2.4 Risco de mau uso

Comunicar prevendo o **reuso indevido** do dado (manchete, recorte, comparação espúria). A integridade inclui **antecipar e neutralizar** leituras distorcidas, registrando o que o dado permite e o que não permite afirmar.

## 3. Escuta sem indução, confidencialidade e risco de identificação indireta (4.2)

### 3.1 Escuta sem indução (neutralidade da coleta)

Na **entrevista/coleta** (auditoria, pesquisa, ouvidoria), as perguntas e a condução **não devem induzir** a resposta:

- **evitar perguntas sugestivas** ("o gestor agiu de má-fé, não é?");
- **evitar enquadramento enviesado** (apresentar só um lado);
- **não confirmar expectativa** por tom, ordem ou reação;
- **registrar fielmente** o relato (sem "completar" o que não foi dito).

Pergunta **induzida** vicia a evidência: a resposta passa a medir a **sugestão do entrevistador**, não o fenômeno. É o equivalente qualitativo do viés de medição.

### 3.2 Confidencialidade

Compromisso de **não divulgar** a informação obtida nem associá-la ao informante **sem autorização**:

- **esclarecer previamente** o que será confidencial e os limites legais;
- **restringir o acesso** ao necessário (princípio do menor acesso/necessidade);
- **separar** a informação substantiva da informação **identificadora**;
- observar a **LGPD** (dados pessoais/sensíveis) no tratamento.

Confidencialidade **não é anonimato absoluto** nem sigilo ilimitado — tem **limites legais** (ordem judicial, dever de reportar), que devem ser informados.

### 3.3 Risco de identificação indireta (re-identificação)

Mesmo sem nome, a combinação de atributos pode **identificar** alguém (**quase-identificadores**): cargo + órgão + período + ocorrência. Técnicas de proteção:

- **anonimização** (perde a possibilidade de associação, direta ou indireta — LGPD art. 5º, XI);
- **pseudonimização** (substitui o identificador, mantendo a chave separada — LGPD art. 13, §4º);
- **agregação** e **supressão** de células pequenas (k-anonimato e variações);
- **perturbação/ruído** e **generalização** de categorias.

O risco é **contextual**: a mesma base pode ser "segura" isolada e **identificável** cruzada com outra (risco de **re-identificação por linkage**). A proteção exige **reavaliação permanente** diante de novas bases/técnicas.

### 3.4 Agregação vs. granularidade

Publicar **dados agregados** reduz risco de identificação, mas **perde informação** e pode inviabilizar a análise (e agravar a falácia ecológica). Há **trade-off** entre utilidade e privacidade — decidido por avaliação de risco e finalidade.

## 4. Regimes de proteção: auditoria, pesquisa e denúncia (4.3)

### 4.1 Entrevistado em auditoria

Na **auditoria governamental** (CGU), o "entrevistado" é, em regra, **agente público ou parte relacionada ao objeto auditado**. Características do regime:

- **finalidade:** instruir achado/evidência de auditoria, com valor **probatório/administrativo**;
- **não há consentimento livre de pesquisa** no sentido acadêmico — há **dever funcional** de colaborar;
- a declaração pode ser usada no **processo** (achado, contraditório), com **identificação** no expediente;
- aplicam-se **normas de auditoria** (documentação da evidência, matriz de achados, qualidade) e o **devido processo**;
- a **confidencialidade** é relativa e subordinada à **finalidade de controle** e à lei.

### 4.2 Participante de pesquisa

Na **pesquisa científica/avaliativa** envolvendo seres humanos, vigora regime **ético-científico**:

- **base normativa:** Resolução CNS nº 466/2012 (e normas do sistema CEP/CONEP);
- **requisito central:** **consentimento livre e esclarecido (TCLE)** — participação **voluntária**, informada, com possibilidade de desistir sem prejuízo;
- **garantias:** **confidencialidade e privacidade**, proteção da **imagem** e **não estigmatização**;
- **avaliação dos riscos/benefícios** e submissão a **comitê de ética**;
- a informação é usada para **conhecimento**, não para **responsabilizar** o participante;
- o participante **não tem dever** de participar (diferentemente do agente público em auditoria).

### 4.3 Denunciante

O **denunciante** (relata ilícito/irregularidade) tem regime próprio de **proteção da identidade**:

- **base normativa (federal):** Lei nº 13.608/2018 (disque-denúncia e proteção da identidade), **Decreto nº 10.153/2019** (salvaguardas de proteção à identidade na administração pública federal), Portaria CGU nº 581/2021 (orientações às ouvidorias), além da garantia de **anonimato/sigilo** no canal Fala.BR (que sequer coleta o IP);
- **garantias:** sigilo dos elementos de identificação; **não retaliação**; tramitação com **pseudonimização/extrato** quando necessário; restrição de acesso;
- **finalidade:** proteger quem **relata** para **apurar** o ilícito;
- a identidade só é revelada em **hipóteses legais estritas** (ex.: requisitada quando **indispensável** à apuração, nos termos do Decreto 10.153/2019, art. 7º);
- distinto do **anonimato de manifestação** (que protege quem não quer se identificar) e do **sigilo legal** de quem se identifica.

### 4.4 Tabela comparativa dos regimes

| Dimensão | Auditoria (entrevistado) | Pesquisa (participante) | Denúncia (denunciante) |
| --- | --- | --- | --- |
| Finalidade | Instruir achado/controle | Produzir conhecimento | Relatar ilícito para apurar |
| Base normativa | Normas de auditoria/Legal | Resolução CNS 466/2012, CEP | Lei 13.608/2018; Dec. 10.153/2019; Port. CGU 581/2021 |
| Participação | Dever funcional de colaborar | Voluntária (TCLE) | Voluntária (relato) |
| Confidencialidade | Relativa (probatória) | Confidencialidade/privacidade | Sigilo/proteção da identidade |
| Identificação | Integra o expediente | Protegida, não estigmatizar | Sigilosa, salvo hipóteses legais |
| Uso da informação | Contraditório/achado | Análise/anônima | Apuração (com extrato/pseudonimização) |

### 4.5 Por que distinguir importa

Aplicar o regime errado gera **dupla falha**: (i) **proteção insuficiente** (tratar denunciante como mero entrevistado e expor sua identidade) ou (ii) **proteção excessiva/imprópria** (exigir TCLE de pesquisa em uma auditoria, inviabilizando o controle). A banca costuma cobrar **a troca de requisitos entre os regimes**.

## Detalhes que merecem destaque

- **Rastreabilidade é condição de reprodutibilidade** — documentar o caminho até o dado.
- **Comunicação proporcional:** o grau de certeza expresso deve acompanhar a força da evidência.
- **Ocultar limites é desinformação por omissão.**
- **Escuta sem indução:** pergunta sugestiva vicia a evidência (mede a sugestão, não o fenômeno).
- **Identificação indireta:** quase-identificadores re-identificam mesmo sem nome (risco de *linkage*).
- **Anonimização ≠ pseudonimização:** a anonimização elimina a associação; a pseudonimização mantém a chave separada.
- **Regimes distintos:** auditoria (dever funcional, valor probatório), pesquisa (TCLE/voluntário), denúncia (sigilo/proteção da identidade).
- **Denunciante:** proteção desde o **recebimento** (Portaria CGU 581/2021), não como etapa posterior.

## Comparações que a banca costuma cobrar (certo/errado)

| Conceito A | Conceito B | Diferença-chave |
| --- | --- | --- |
| Rastreabilidade | Reproductibilidade | Rastrear = refazer o caminho do dado; reproduzir = obter o mesmo resultado refazendo a análise. |
| Anonimização | Pseudonimização | Anonimização elimina a associação; pseudonimização substitui o identificador mantendo a chave separada. |
| Confidencialidade | Anonimato | Confidencialidade = não divulgar a quem se conhece; anonimato = não se conhece a identidade. |
| Participante de pesquisa | Entrevistado em auditoria | Pesquisa = voluntário/TCLE; auditoria = dever funcional, valor probatório. |
| Entrevistado em auditoria | Denunciante | Auditoria = colabora com o controle; denunciante = relata e tem **proteção de identidade**. |
| Sigilo do denunciante | Anonimato do manifestante | Sigilo protege quem **se identifica**; anonimato protege quem **não quer** se identificar. |
| Indução (pergunta sugestiva) | Viés de medição | Indução é o mecanismo qualitativo que produz o viés de medição. |
| Proporção da afirmação | Força da evidência | Afirmação deve ser proporcional à evidência; exagero ou omissão violam a integridade. |

## Pegadinhas e erros comuns

> Cuidado com termos absolutos ("sempre", "nunca", "exclusivamente") e com a troca de requisitos.

- Exigir **TCLE (pesquisa)** numa **auditoria** governamental — regimes distintos, finalidades distintas.
- Tratar **denunciante** como simples "entrevistado" e **expor sua identidade**.
- Achar que **anonimização é sempre irreversível** — LGPD considera pessoal o dado cuja anonimização pode ser **revertida** com esforço razoável.
- Confundir **confidencialidade com anonimato** — são conceitos diferentes.
- Achar que remover o **nome** garante não-identificação — os **quase-identificadores** re-identificam.
- Supor que **sigilo do denunciante é absoluto** — cede a hipóteses legais estritas (indispensabilidade à apuração).
- Comunicar resultado **sem declarar limites** (fonte, margem de erro, definição).
- Afirmar **certeza** onde os dados sustentam apenas **indício** (desproporção da afirmação).
- Usar **pergunta sugestiva** e depois tratar a resposta como evidência neutra.

## Notas atômicas relacionadas

```dataview
LIST FROM "20 - Notas"
WHERE disciplina = this.disciplina
  AND contains(tema, this.tema)
SORT file.name ASC
```

## Fontes

- https://www.planalto.gov.br/ccivil_03/_ato2019-2022/2019/decreto/d10153.htm (Decreto nº 10.153/2019 — salvaguardas de proteção à identidade do denunciante)
- https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709.htm (LGPD — anonimização (art. 5º), pseudonimização (art. 13), princípios (art. 6º))
- https://bvsms.saude.gov.br/bvs/saudelegis/cns/2013/res0466_12_12_2012.html (Resolução CNS nº 466/2012 — pesquisa com seres humanos; consentimento e confidencialidade)
- https://www.gov.br/conselho-nacional-de-saude/pt-br/atos-normativos/resolucoes/2012/resolucao-no-466.pdf/view (Resolução CNS 466/2012 — texto integral)
- https://falabr.cgu.gov.br/ (Fala.BR — canal de manifestações; denúncia com proteção de identidade)
- https://www.gov.br/ouvidorias/pt-br/ouvidorias/sisouv/acervo/portarias-cgu/normas-procedimentais/protecao-ao-denunciante (CGU/OGU — normas de proteção ao denunciante)
- https://schiefler.adv.br/protecao-ao-denunciante-e-apuracao-segura-o-que-as-orientacoes-da-cgu-sinalizam-para-canais-de-denuncia-e-investigacoes-internas/ (Portaria CGU 581/2021 — proteção desde o recebimento)
- https://www.gov.br/cgu/pt-br (CGU — auditoria governamental e controle)
- https://www.ufsb.edu.br/ouvidoria-servicos/protecao-ao-denunciante (Proteção ao denunciante — sigilo dos dados e restrição de acesso)
- https://www.scielo.br/j/reben/a/fTyd8SGbT8jcFdWfsSvHCqR/?format=pdf&lang=pt (Pesquisa com seres humanos e LGPD — confidencialidade)
- http://www.planalto.gov.br/ccivil_03/_ato2011-2014/2011/lei/l12527.htm (Lei de Acesso à Informação — transparência e restrições de acesso)
- https://basedeconhecimento.cgu.gov.br/items/147989fc-0bd9-45f4-a9b7-396269832483 (CGU — Decreto 10.153/2019 comentado)
