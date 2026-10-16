---
tipo: resumo
disciplina: "Fundamentos de Evidências, Dados e Inteligência Artificial"
tema: "Leitura de dados e indicadores"
status: novo
data: "2026-10-16"
tags: [resumo, dados-ia, cgu-2026]
---

# Resumo: Leitura de dados e indicadores

> [!info] MOC: [[Fundamentos de Evidências, Dados e Inteligência Artificial]]
> Edital nº 1/2026 – CGU – AFFC · **Conhecimentos complementares** · Item 2 — *Leitura de dados e indicadores*.

## Escopo no edital (checklist)

- [x] 2.1 Interpretação de tabelas, gráficos, proporções, taxas e medidas descritivas
- [x] 2.1 Denominadores, qualidade e comparabilidade
- [x] 2.2 Distinção entre indicadores de percepção, experiência, denúncias, detecção e sanções na análise da corrupção
- [x] 2.2 Subnotificação e limites de inferência sobre sua ocorrência

## Resumo

Este bloco trata da **alfabetização estatística aplicada ao controle**: ler corretamente tabelas e gráficos, distinguir **proporção, razão e taxa**, compreender **medidas de tendência central e de dispersão** (média, mediana, desvio-padrão) e — o ponto mais cobrado — escolher e criticar o **denominador** de um indicador. Um indicador sem denominador correto engana: comparar números absolutos de municípios de tamanhos diferentes, por exemplo, é erro clássico.

A segunda parte é específica da **análise da corrupção**: há uma família de indicadores que medem coisas **diferentes** — *percepção*, *experiência/vitimização*, *denúncias*, *detecção* e *sanções* — e confundi-las é o erro mais frequente (inclusive em debates públicos sobre o Índice de Percepção da Corrupção). Fecha-se com a **subnotificação** (a "cifra oculta"): os indicadores disponíveis captam apenas uma fração do fenômeno, e há **limites de inferência** sobre o que não é observado.

## 1. Interpretação de tabelas, gráficos, proporções, taxas e medidas descritivas (2.1)

### 1.1 Leitura de tabelas

- Identificar **título, fonte, período, unidade de medida e nota de rodapé** antes de concluir.
- Distinguir **frequência absoluta** (contagem) de **frequência relativa** (percentual/proporção).
- Observar o **total de referência (n)** — percentuais sobre bases pequenas são instáveis.
- Em tabelas com **"não informado"/"não se aplica"**, verificar se o percentual é sobre o total ou sobre os válidos.

### 1.2 Leitura de gráficos

- **Eixo truncado** (não iniciar em zero) exagera diferenças — armadilha recorrente.
- **Escalas diferentes** entre gráficos comparados induzem erro de leitura.
- **Gráfico de barras vs. linha:** barra para categorias; linha para série temporal.
- **Gráfico de pizza** exige partes mutuamente exclusivas e exaustivas (somam 100%).
- **Escala logarítmica** comprime variações relativas — adequada para taxas de crescimento, mas pode enganar quem lê distâncias lineares.

### 1.3 Proporção, razão e taxa (não confundir)

- **Proporção:** parte/total (numerador **contido** no denominador); varia de 0 a 1 (ou 0 a 100%). Ex.: proporção de contratos com irregularidade.
- **Razão:** quociente entre duas grandezas **independentes** (numerador **não** contido no denominador). Ex.: número de leitos por mil habitantes; razão denúncias/auditores.
- **Taxa (coeficiente):** razão com **tempo embutido** no denominador (mede risco/velocidade de ocorrência). Ex.: incidência por 100 mil habitantes-ano.
- **Percentual (percentagem):** proporção × 100. **Ponto percentual (p.p.) × percentual:** variação de 10% para 15% é +5 p.p. (e +50% em termos relativos) — distinção que a banca explora.

### 1.4 Medidas de tendência central

- **Média (aritmética):** soma/n. **Sensível a valores extremos (outliers)**; adequada para distribuições simétricas.
- **Mediana:** valor central (50% dos dados). **Robusta a outliers**; preferível em distribuições assimétricas (ex.: valores de contratos, salários).
- **Moda:** valor mais frequente; única medida aplicável a variáveis categóricas.

### 1.5 Medidas de dispersão

- **Amplitude:** máximo − mínimo (grosseira, sensível a outliers).
- **Variância:** média dos quadrados dos desvios em relação à média (unidade ao quadrado).
- **Desvio-padrão:** raiz quadrada da variância; mesma unidade da variável; mede dispersão **em torno da média**.
- **Coeficiente de variação (CV = dp/média):** dispersão **relativa**; permite comparar variabilidade entre grandezas de escalas diferentes.

### 1.6 Prevalência e incidência (medidas de frequência)

- **Incidência:** **casos novos** num período / população sob risco — mede **risco/velocidade**.
- **Prevalência:** **casos existentes** (novos + antigos) num momento / população — é uma "fotografia" (estoque).
- **Relação:** prevalência ≈ incidência × duração média da condição. Prevalência é afetada por **entradas** (casos novos, migração) e **saídas** (cura, óbito, saída do grupo).

## 2. Denominadores, qualidade e comparabilidade (2.1)

### 2.1 O denominador correto

O denominador deve representar a **população de risco/exposta** ao fenômeno:

- denúncias sobre **processos** (não sobre o total de servidores, se nem todos podem ser objeto daquele processo);
- auditorias com achados sobre **auditorias concluídas** (não sobre as "planejadas");
- homicídios por 100 mil **habitantes** (não por 100 mil "moradores da capital").

**Erro clássico:** comparar **números absolutos** entre grupos de tamanho diferente ("município A teve mais denúncias que B" — sem considerar população).

### 2.2 Qualidade do indicador

Um bom indicador deve ter: **validade** (mede o que pretende), **confiabilidade** (estável/reprodutível), **sensibilidade** (muda quando o fenômeno muda), **especificidade** (não muda por causas alheias), **simplicidade, oportunidade e baixo custo**. Propriedades frequentemente lembradas: **relevância, precisão, pontualidade, acessibilidade, coerência** (dimensões de qualidade estatística).

### 2.3 Comparabilidade

- **Temporal:** mesma metodologia ao longo do tempo; quebras de série devem ser sinalizadas.
- **Espacial/entre grupos:** mesma definição e mesmo denominador.
- **Conceitual:** mudanças de definição (ex.: o que conta como "denúncia" ou "achado") invalidam comparação ingênua.
- **Padronização:** ajustar por estrutura etária ou outros fatores quando se comparam populações diferentes (taxas padronizadas).

### 2.4 Composição (efeito composição)

Indicadores **agregados** podem esconder diferenças de composição (Paradoxo de Simpson, tratado no resumo de inferências). Comparar médias entre grupos sem controlar a composição interna pode inverter a conclusão.

## 3. Indicadores de corrupção: percepção, experiência, denúncias, detecção e sanções (2.2)

### 3.1 Percepção

Medem o que **pessoas ou especialistas acreditam** sobre a corrupção. Ex.: **Índice de Percepção da Corrupção (IPC/CPI)** da Transparência Internacional, que agrega percepções de especialistas/empresários. **Limite central:** mede **percepção, não a ocorrência real**; sofre de inércia, de efeitos de mídia e de comparação internacional questionável. A própria CGU já se manifestou ressaltando que o IPC foca na *percepção*, e não na *ocorrência* dos fatos.

### 3.2 Experiência / vitimização

Medem a **vivência direta** do cidadão — por exemplo, ter pago propina ou ter sido solicitado a pagar. Ex.: **Barômetro Global da Corrupção (GCB)** da Transparência Internacional, que pergunta sobre **experiências de suborno** em serviços públicos. É mais próximo do fato do que a percepção, mas ainda é **autorrelato** (sujeito a memória, desejabilidade social) e restrito a certos setores.

### 3.3 Denúncias

Registros de **relatos à ouvidoria/canais** (Fala.BR, Disque Denúncia, canais internos). Medem a **demanda por apuração** e a **disposição de reportar**, não a incidência do ilícito. Variam com **confiança institucional, medo de retaliação e conhecimento do canal** — por isso crescer em denúncias **não** implica crescer em corrupção (pode ser justamente o efeito de maior confiança).

### 3.4 Detecção

Casos **efetivamente encontrados por órgãos de controle** — auditorias da CGU, fiscalizações do TCU, investigações. Medem a **capacidade de detecção** do sistema, condicionada a **planejamento, amostragem e critério de risco** (auditar "onde há mais risco" concentra achados, o que não significa que ali haja mais corrupção em termos absolutos).

### 3.5 Sanções

Resultados **punitivos/administrativos**: condenações (TCU), penalidades da Lei Anticorrupção (responsabilização de pessoas jurídicas), demissões e penalidades disciplinares (correição), condenações judiciais. É a **ponta mais estreita do funil** — depende de todo o fluxo anterior (detectar, instruir, julgar), com forte defasagem temporal.

### 3.6 O funil da corrupção (por que os números divergem)

`Ocorrência real → percebida/experimentada → denunciada → detectada → sancionada`. Cada etapa **perde casos** e introduz **filtros próprios**. Por isso **nenhum** indicador isolado "mede a corrupção"; cada um mede **uma etapa**, com viés próprio. Confundir etapas (usar sanções como medida de incidência, ou percepção como medida de ocorrência) é o erro conceitual mais cobrado.

### 3.7 Tabela-síntese dos indicadores

| Indicador | O que mede | Exemplo | Viés/limite |
| --- | --- | --- | --- |
| Percepção | Crença/opinião | IPC (Transparência Intl.) | Não mede ocorrência; inércia, efeito-mídia |
| Experiência/vitimização | Vivência direta (autorrelato) | GCB (suborno) | Autorrelato; cobertura setorial |
| Denúncias | Relatos recebidos | Fala.BR, ouvidorias | Depende de confiança/medo; não é incidência |
| Detecção | Casos achados pelo controle | Auditorias CGU/TCU | Condicionada a planejamento/amostragem |
| Sanções | Penalidades aplicadas | Condenações, demissões | Defasada; ponta estreita do funil |

## 4. Subnotificação e limites de inferência sobre sua ocorrência (2.2)

### 4.1 A cifra oculta (dark figure)

**Subnotificação** é a diferença entre o **total de ocorrências** e o **total registrado**. A "cifra oculta/negra" (da criminologia) é o conjunto de casos **não reportados, não detectados ou não descobertos**. Em corrupção, a subnotificação é estruturalmente **alta** — o ilícito é consensual, sigiloso, sem "vítima individual" evidente e as partes têm incentivo ao silêncio.

### 4.2 Por que subnotifica (fatores)

- **não percepção** do fato como ilícito;
- **medo de retaliação** (denunciante);
- **desconfiança** na apuração/impunidade percebida;
- **desconhecimento do canal**;
- **cumplicidade/benefício mútuo** no ato;
- **custo** (tempo, exposição) de denunciar.

### 4.3 Limites de inferência

- **Não se conclui ausência a partir do silêncio:** "poucas denúncias" **não** significa "pouca corrupção".
- **Aumento de registros ≠ aumento do fenômeno:** pode refletir melhora do canal, campanha ou confiança.
- **Perfil do que aparece ≠ perfil do total:** o que chega ao sistema é um **subconjunto enviesado** (casos mais visíveis, menos arriscados de reportar).
- **Inferir o oculto exige método próprio** (pesquisas de vitimização, técnicas de captura-recaptura, triangulação), sempre com **margem de incerteza** — nunca por extrapolação simples do registrado.

### 4.4 O que é legítimo inferir

- Uso de **denúncias/detecção como piso** (mínimo) do fenômeno;
- Uso como **sinal** (onde há mais registro, há ao menos mais *visibilidade* daquele tipo);
- Comparação **de tendências do mesmo indicador** (se a metodologia é estável), nunca de níveis entre indicadores de etapas diferentes.

## Detalhes que merecem destaque

- **Proporção ≠ razão ≠ taxa:** a taxa tem **tempo** no denominador; a proporção tem o numerador **contido** no denominador.
- **Ponto percentual ≠ percentual:** +5 p.p. sobre 10% é +50% relativo.
- **Média é sensível a outliers; mediana é robusta** — em dados assimétricos (contratos, salários), mediana é preferível.
- **Incidência = casos novos (fluxo); prevalência = casos existentes (estoque).**
- **Denominador = população de risco/exposta**; comparar absolutos entre grupos de tamanhos diferentes é o erro nº 1.
- **IPC mede percepção, não ocorrência** — crítica metodológica reiterada pela própria CGU.
- **Denúncia crescente pode indicar mais confiança, não mais corrupção.**
- **Cifra oculta:** o registrado é um piso enviesado; silêncio não prova ausência.

## Comparações que a banca costuma cobrar (certo/errado)

| Conceito A | Conceito B | Diferença-chave |
| --- | --- | --- |
| Proporção | Taxa | Proporção = parte/total (sem tempo); taxa = frequência com tempo no denominador. |
| Proporção | Razão | Na proporção o numerador está contido no denominador; na razão são grandezas independentes. |
| Média | Mediana | Média usa todos os valores (sensível a outliers); mediana é o valor central (robusta). |
| Variância | Desvio-padrão | Variância está em unidade ao quadrado; desvio-padrão na mesma unidade da variável. |
| Incidência | Prevalência | Incidência = novos casos (fluxo); prevalência = existentes (estoque). |
| Percepção | Experiência/vitimização | Percepção = opinião/crença; experiência = vivência direta autorrelatada. |
| Denúncia | Detecção | Denúncia = relato do cidadão; detecção = achado do órgão de controle. |
| Detecção | Sanção | Detecção = encontrar o caso; sanção = penalidade aplicada (ponta final, defasada). |
| Variação em % | Variação em p.p. | p.p. é diferença de percentuais; % é variação relativa sobre a base. |

## Pegadinhas e erros comuns

> Cuidado com termos absolutos ("sempre", "nunca", "exclusivamente") e com a troca de requisitos.

- Achar que **aumento de denúncias = aumento de corrupção** — pode ser efeito de confiança/canal, não do fenômeno.
- Usar **IPC como medida de ocorrência** da corrupção — é medida de **percepção**.
- Comparar **números absolutos** entre grupos de tamanho diferente sem corrigir o denominador.
- Confundir **média com mediana** em distribuição assimétrica ("a renda média subiu" não informa sobre a maioria).
- Ler **gráfico com eixo truncado** como se a diferença fosse proporcional à área.
- Confundir **incidência com prevalência** (novos vs. existentes).
- Inferir **prevalência populacional** a partir de dados de **ouvidoria** (autosselecionados).
- Tratar **sanções** como medida de incidência (são a ponta estreita e defasada do funil).
- Achar que **subnotificação** é problema só "de registro", sem consequência para a inferência.

## Notas atômicas relacionadas

```dataview
LIST FROM "20 - Notas"
WHERE disciplina = this.disciplina
  AND contains(tema, this.tema)
SORT file.name ASC
```

## Fontes

- https://transparenciainternacional.org.br/ipc/ (Transparência Internacional — Índice de Percepção da Corrupção: o que mede e limites)
- https://www.transparency.org/en/gcb (Transparência Internacional — Global Corruption Barometer: experiências/vitimização)
- https://transparenciainternacional.org.br/publicacoes/barometro-global-da-corrupcao-2019-america-latina-e-caribe/ (Barômetro Global da Corrupção — América Latina; experiência direta de suborno)
- https://www.cnnbrasil.com.br/politica/limitacoes-metodologicas-cgu-rebate-queda-do-pais-em-indice-de-corrupcao/ (CGU — crítica metodológica: percepção ≠ ocorrência)
- https://www.ibge.gov.br/ (IBGE — fontes estatísticas oficiais; medidas e indicadores)
- https://www.scielo.br/j/jbpneu/a/yzdNrrMgb8xMwJ6sgQnrmWt/?lang=pt (Incidência × prevalência — definições e cálculo)
- http://scielo.iec.gov.br/scielo.php?script=sci_arttext&pid=S0104-16732000000400006 (Terminologia das medidas e indicadores em epidemiologia — razão, proporção, taxa)
- https://www.epsjv.fiocruz.br/pdtsp/includes/header_pdf.php?id=266&ext=.pdf&titulo=EPIDEMIOLOGIA (Fiocruz — epidemiologia e indicadores; incidência, prevalência)
- https://www.est.ufmg.br/~enricoc/pdf/medicina/aula9_10.pdf (UFMG — princípios de bioestatística; sensibilidade/especificidade)
- https://revistas.usp.br/ee/article/download/162269/165875/454692 (Determinantes da cifra oculta do crime no Brasil — subnotificação)
- https://en.wikipedia.org/wiki/Dark_figure_of_crime (Dark figure of crime — conceito de cifra oculta)
- https://falabr.cgu.gov.br/ (Fala.BR — fonte de dados de denúncias/manifestações)
- https://www.gov.br/cgu/pt-br/assuntos/auditoria-e-fiscalizacao/enccla (CGU/ENCCLA — detecção e combate à corrupção)
- https://repositorio.ipea.gov.br/bitstreams/62f3855e-df51-4783-a1a6-bf8d6f5444d4/download (IPEA — sistemas e ciclos de monitoramento e avaliação; indicadores)
