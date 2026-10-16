---
tipo: resumo
disciplina: "Fundamentos de Evidências, Dados e Inteligência Artificial"
tema: "Inferências e erros de raciocínio"
status: novo
data: "2026-10-16"
tags: [resumo, dados-ia, cgu-2026]
---

# Resumo: Inferências e erros de raciocínio

> [!info] MOC: [[Fundamentos de Evidências, Dados e Inteligência Artificial]]
> Edital nº 1/2026 – CGU – AFFC · **Conhecimentos complementares** · Item 3 — *Inferências e erros de raciocínio*.

## Escopo no edital (checklist)

- [x] 3.1 Associação e causalidade
- [x] 3.1 Seleção e representatividade
- [x] 3.1 Explicações alternativas e incerteza
- [x] 3.2 Generalizações indevidas, falácia ecológica e viés de confirmação
- [x] 3.2 Falsos positivos e falsos negativos

## Resumo

Este bloco cuida da **passagem dos dados para conclusões** — onde a maioria dos erros de análise acontece. A lição central é que **associação não implica causalidade**: duas coisas podem variar juntas por acaso, por **causa comum (confundimento)** ou por **causalidade reversa**, sem que uma cause a outra. Estabelecer causa exige desenho (experimento, grupo de controle), pensamento **contrafactual** e, em dados observacionais, leitura cuidadosa dos **critérios de Bradford Hill** — que são *auxílios de julgamento*, não provas.

A segunda metade sistematiza os **vieses** que corrompem a inferência (seleção, confirmação, sobrevivência, publicação, falácia ecológica, generalização indevida) e a lógica dos **erros de decisão** (falso positivo/falso negativo, erro tipo I/tipo II, sensibilidade e especificidade). O pano de fundo é o mesmo: **incerteza** é inerente, e o bom analista a torna **explícita** em vez de escondê-la.

## 1. Associação e causalidade (3.1)

### 1.1 Associação (correlação) ≠ causalidade

**Associação/correlação** é a variação conjunta entre duas variáveis (medida por coeficiente de correlação, testes de associação). **Causalidade** exige que a mudança numa produza a mudança na outra. A associação pode decorrer de:

- **acaso** (flutuação amostral);
- **causa comum / confundimento** (uma terceira variável C causa A e B: sorvetes e afogamentos — o verão é a causa comum);
- **causalidade reversa** (A e B associadas, mas B → A, não A → B);
- **correlação espúria** (associação sem mecanismo causal real, frequentemente por coincidência ou pela forma de medir — ex.: séries temporais com tendência comum correlacionam sem relação causal).

### 1.2 Estabelecendo causalidade

- **Experimento com aleatorização (RCT):** o padrão-ouro — a **randomização** torna os grupos comparáveis e isola o efeito.
- **Grupo de controle vs. tratamento:** a diferença de desfecho entre eles estima o efeito.
- **Contrafactual:** "o que teria acontecido ao tratado se **não** tivesse sido tratado?" — o efeito causal é a **diferença entre o resultado observado e o contrafactual**. Em avaliação de políticas, o contrafactual é estimado (grupo controle, pareamento, diferenças-em-diferenças, regressão descontínua, variáveis instrumentais).
- **Controle estatístico de confundidores:** em dados observacionais, ajustar por variáveis que afetam tanto a exposição quanto o desfecho — limitado pelos confundidores **não medidos**.

### 1.3 Critérios de Bradford Hill (auxílios de julgamento, não prova)

Propostos por Austin Bradford Hill (1965) para avaliar se associação é causal — ele próprio os chamou de "viewpoints", e **nenhum é condição sine qua non**:

1. **Força (tamanho do efeito):** associação maior é mais sugestiva de causa (mas associação fraca não descarta).
2. **Consistência (reprodutibilidade):** achado repetido em lugares, amostras e métodos diferentes.
3. **Especificidade:** causa ligada a um efeito específico (critério hoje considerado o mais fraco).
4. **Temporalidade:** a causa deve **preceder** o efeito — **único critério indispensável**.
5. **Gradiente biológico (dose-resposta):** mais exposição → mais efeito.
6. **Plausibilidade:** mecanismo causal verossímil (limitada pelo conhecimento atual).
7. **Coerência:** compatível com o conhecimento existente.
8. **Experimento:** evidência experimental disponível.
9. **Analogia:** semelhança com relações causais já estabelecidas.

(Alguns autores acrescentam **reversibilidade**: removida a causa, o efeito some.)

### 1.4 Paradoxo de Simpson

Uma associação observada **nos subgrupos** pode **inverter** (ou desaparecer) quando os dados são **agregados** — por conta de uma variável de confusão (composição) diferente entre os grupos. É a expressão estatística do problema de **confundimento**, e ilustra por que "controle" e desagregação importam.

## 2. Seleção e representatividade (3.1)

### 2.1 Viés de seleção

Distorção causada pela **forma como os sujeitos/casos entram na análise**. A amostra não representa a população-alvo, e a conclusão sobre o todo fica comprometida. Exemplos: pesquisar apenas quem respondeu (não resposta), apenas quem tem acesso, apenas os registros "visíveis".

### 2.2 Representatividade

Amostra é **representativa** quando sua composição espelha a população em relação às características relevantes. Garante-se principalmente por **seleção aleatória (probabilística)** e tamanho adequado. **Amostra grande ≠ amostra representativa**: uma amostra enorme de voluntários é grande mas não representativa (erro que surge com frequência em "big data" e pesquisas de conveniência).

### 2.3 Vieses de seleção específicos

- **Viés de sobrevivência:** analisar apenas o que "sobreviveu" a um filtro (empresas ainda ativas, contratos não cancelados, pacientes que sobreviveram) — ignora os que saíram e distorce a conclusão (ex.: achar que "todo avião da 2ª Guerra voltava com furos nas asas" e blindar o lugar errado, esquecendo os que **não** voltaram).
- **Viés de publicação:** resultados **publicados/reportados** não são os resultados **totais** — estudos com achado "positivo" têm mais chance de publicação (gaveta de arquivo). Metanálises e indicadores de "tudo que deu certo" sofrem dele.
- **Viés de não resposta / autosseleção:** quem participa (ouvidoria, pesquisas voluntárias) difere de quem não participa.
- **Viés de Berkson / de encaminhamento:** composição diferente em amostras hospitalares/institucionais (casos que chegam ao serviço não são a população geral).

### 2.4 Amostragem e margem de erro

- **Erro amostral:** flutuação devida ao sorteio (medido pela **margem de erro**/intervalo de confiança) — **diminui** com o tamanho da amostra.
- **Erro não amostral (viés):** defeito de coleta/cobertura — **não diminui** com tamanho; ao contrário, pode ser amplificado.
- Distinguir os dois é essencial: "a pesquisa ouviu 100 mil pessoas" responde ao erro amostral, **não** ao viés de seleção.

## 3. Explicações alternativas e incerteza (3.1)

### 3.1 Rivalidade de explicações

Antes de afirmar "A causou B", liste **explicações alternativas** para a associação: acaso, confundimento, causalidade reversa, viés de seleção/medição, regressão à média, efeito de outra intervenção simultânea, tendência secular. Boa análise **testa e descarta** alternativas, não apenas confirma a hipótese favorita (que é o viés de confirmação, seção 4).

### 3.2 Regressão à média

Valores extremos tendem a ser seguidos por valores **mais próximos da média** (por flutuação aleatória). Atribuir a "melhora" a uma intervenção sem grupo de comparação ignora esse fenômeno — clássico em avaliações de "piores desempenhos que melhoraram depois".

### 3.3 Incerteza como parte da resposta

- Expressar **intervalos de confiança**, não só estimativas pontuais.
- Declarar **pressupostos** e **limitações** (confundidores não medidos, qualidade da fonte).
- Distinguir **incerteza aleatória** (quantificável) de **incerteza estrutural** (modelo, definições).
- Conclusão robusta é aquela que **sobrevive** a variações razoáveis de pressuposto (análise de sensibilidade).

## 4. Generalizações indevidas, falácia ecológica e viés de confirmação (3.2)

### 4.1 Generalização indevida

Estender uma conclusão **além do que os dados autorizam**: do caso particular para o geral (generalização apressada), de uma amostra **não representativa** para a população, ou de um contexto para outro (validade externa). A pergunta-chave é: **a amostra/caso é representativa do alvo da conclusão?**

### 4.2 Falácia ecológica

Inferir **características individuais** a partir de **dados agregados (de grupo)**. Ex.: "municípios com maior renda média têm maior taxa de X, logo indivíduos ricos fazem mais X" — a associação **no nível do grupo** pode não valer **no nível do indivíduo** (e pode até inverter). Oposto: **falácia atomística/individualista** (inferir o grupo a partir do indivíduo).

### 4.3 Falácia da composição e da divisão

- **Composição:** o que vale para a parte vale para o todo ("cada jogador é excelente, logo o time é excelente").
- **Divisão:** o que vale para o todo vale para a parte ("o país é rico, logo todo cidadão é rico").

### 4.4 Viés de confirmação

Tendência a **buscar, interpretar e lembrar** informação que **confirma** crenças/hipóteses prévias, ignorando a que contraria. Manifestações na análise: selecionar evidências favoráveis (*cherry-picking*), formular perguntas que já induzem a resposta, desmerecer fontes divergentes, parar de coletar quando "já deu certo". Antídoto: **buscar ativamente a evidência que refuta** (testar a hipótese contra si mesma), triangulação e decisão por critérios **predefinidos**.

### 4.5 Outros vieses cognitivos recorrentes

- **Viés de ancoragem:** apego ao primeiro número/informação.
- **Viés de disponibilidade:** supervalorizar o que vem facilmente à memória (casos recentes/impactantes).
- **Viés de retrospecto (hindsight):** achar que o ocorrido "era previsível".
- **Correlação ilusória:** ver padrão onde há acaso.

## 5. Falsos positivos e falsos negativos (3.2)

### 5.1 A lógica do teste de hipóteses

Decidimos entre **H0 (hipótese nula** — "não há efeito/diferença") e **H1 (alternativa)**. Decisões podem errar de dois modos:

- **Erro tipo I (falso positivo):** rejeitar H0 quando ela é **verdadeira** (afirmar que há efeito quando não há). Probabilidade = **α (nível de significância)**, convencionalmente 5%.
- **Erro tipo II (falso negativo):** **não** rejeitar H0 quando ela é **falsa** (deixar de detectar efeito que existe). Probabilidade = **β**; **poder = 1 − β**.

### 5.2 Sensibilidade e especificidade (testes diagnósticos)

Aplicável a **classificadores/triagens** (ex.: modelos que sinalizam risco de irregularidade):

- **Sensibilidade** = VP / (VP + FN): capacidade de **detectar quem tem** a condição (evita falsos negativos).
- **Especificidade** = VN / (VN + FP): capacidade de **identificar quem não tem** (evita falsos positivos).
- **Falso positivo:** sinalizar a condição em quem **não** a tem (relação com erro tipo I).
- **Falso negativo:** deixar de sinalizar em quem **tem** (relação com erro tipo II).

### 5.3 Valor preditivo e prevalência

O **valor preditivo positivo (VPP)** depende da **prevalência**: mesmo com teste muito específico, se a condição é **rara**, a maioria dos positivos pode ser **falsa** (ex.: especificidade de 98% em 10.000 sadios ainda gera 200 falsos positivos). Por isso, em triagens de baixa prevalência (irregularidades raras), é preciso alta especificidade e interpretação cuidadosa do alerta.

### 5.4 Trade-off e ponto de corte

Sensibilidade e especificidade **variam em direções opostas** com o ponto de corte: afrouxar o critério aumenta sensibilidade (e falsos positivos); endurecer aumenta especificidade (e falsos negativos). A escolha depende do **custo relativo** de cada erro — em controle, um falso positivo gera custo de apuração indevida; um falso negativo deixa ilícito impune.

### 5.5 Tabela de confusão

|  | Condição presente | Condição ausente |
| --- | --- | --- |
| **Teste positivo** | VP (verdadeiro positivo) | FP (falso positivo) |
| **Teste negativo** | FN (falso negativo) | VN (verdadeiro negativo) |

## Detalhes que merecem destaque

- **Correlação não implica causalidade** — a tríade clássica: acaso, confundimento, causalidade reversa.
- **Temporalidade é o único critério de Hill indispensável** (a causa precede o efeito).
- **Critérios de Hill são auxílios de julgamento, não prova** — nenhum é condição *sine qua non*.
- **Contrafactual** é a base da inferência causal: efeito = observado − (o que teria ocorrido sem a intervenção).
- **Amostra grande ≠ representativa** — tamanho reduz erro **amostral**, não **viés de seleção**.
- **Falácia ecológica:** dado de grupo **não** autoriza conclusão sobre o indivíduo.
- **Viés de confirmação:** buscar o que refuta, não o que confirma.
- **Erro tipo I = falso positivo; tipo II = falso negativo** (relação com α e β).
- **VPP depende da prevalência** — triagem de evento raro exige alta especificidade.
- **Regressão à média** explica "melhoras" espúrias de valores extremos.

## Comparações que a banca costuma cobrar (certo/errado)

| Conceito A | Conceito B | Diferença-chave |
| --- | --- | --- |
| Associação | Causalidade | Associação = variação conjunta; causalidade = mudança numa **produz** mudança na outra. |
| Confundimento | Causalidade reversa | Confundimento = terceira variável causa ambas; reversa = a direção é invertida (B→A). |
| Erro tipo I | Erro tipo II | Tipo I = rejeitar H0 verdadeira (falso positivo); tipo II = não rejeitar H0 falsa (falso negativo). |
| Sensibilidade | Especificidade | Sensibilidade = detecta quem tem (evita FN); especificidade = identifica quem não tem (evita FP). |
| Falácia ecológica | Falácia da composição | Ecológica = do grupo para o indivíduo; composição = da parte para o todo. |
| Viés de sobrevivência | Viés de publicação | Sobrevivência = só os que passaram por filtro; publicação = só os resultados positivos reportados. |
| Erro amostral | Viés (erro não amostral) | Amostral diminui com n; viés é defeito de coleta e não diminui com n. |
| α (significância) | Poder (1−β) | α = risco de falso positivo; poder = capacidade de detectar efeito verdadeiro. |
| Correlação espúria | Causalidade genuína | Espúria = associação sem mecanismo causal; genuína = efeito real com mecanismo. |

## Pegadinhas e erros comuns

> Cuidado com termos absolutos ("sempre", "nunca", "exclusivamente") e com a troca de requisitos.

- Afirmar que **correlação alta prova causalidade** — prova no máximo associação.
- Tratar os **critérios de Hill como "teste" obrigatório** — são **auxílios**, e só a **temporalidade** é indispensável.
- Achar que **amostra grande garante representatividade** — tamanho não corrige viés de seleção.
- Concluir sobre **indivíduos** a partir de **dados municipais** (falácia ecológica).
- Confundir **sensibilidade com especificidade** (detectar quem tem × excluir quem não tem).
- Achar que **VPP alto** é garantido por teste específico, **ignorando a prevalência**.
- Atribuir **melhora de um caso extremo à intervenção** sem grupo de controle (regressão à média).
- Ignorar **explicações alternativas** e "confirmar" apenas a hipótese favorita (viés de confirmação).
- Generalizar **conclusão de amostra voluntária** (autosselecionada) para a população.

## Notas atômicas relacionadas

```dataview
LIST FROM "20 - Notas"
WHERE disciplina = this.disciplina
  AND contains(tema, this.tema)
SORT file.name ASC
```

## Fontes

- https://en.wikipedia.org/wiki/Bradford_Hill_criteria (Bradford Hill criteria — os 9 "viewpoints" e a ressalva de que nenhum é sine qua non)
- https://pt.wikipedia.org/wiki/Crit%C3%A9rios_de_Hill (Critérios de Hill — versão em português)
- https://www.ime.usp.br/~tonelli/pub/outros/assoc.pdf (IME-USP — associação e causalidade; regras de inferência)
- https://bookdown.org/cienciadedadosnaep/ebook_ciencia_de_dados/_book/cap4.html (Correlação e causalidade; grupo de tratamento e controle)
- https://medium.com/data-hackers/introdu%C3%A7%C3%A3o-%C3%A0-infer%C3%AAncia-causal-ed3da2c12da4 (Introdução à inferência causal; correlação ≠ causalidade)
- https://www.paulogala.com.br/correlacao-vs-causalidade-a-armadilha-das-inferencias-espurias-e-os-metodos-para-evita-la/ (Correlação × causalidade e inferência espúria)
- https://www.est.ufmg.br/~enricoc/pdf/medicina/aula9_10.pdf (UFMG — sensibilidade, especificidade, erros tipo I e II)
- https://www.blogs.unicamp.br/covid-19/meu-teste-deu-positivo-e-agora-entendendo-a-sensibilidade-e-a-especificidade-dos-testes-diagnosticos/ (UNICAMP — sensibilidade/especificidade e valores preditivos)
- https://www.resumosmedicina.com.br/blog/especificidade-em-testes-diagnosticos-o-guia-completo-para-calcular-e-interpretar (Especificidade e impacto da prevalência nos falsos positivos)
- https://pt.wikipedia.org/wiki/Vi%C3%A9s_de_sobreviv%C3%AAncia (Viés de sobrevivência — conceito e exemplos)
- https://jornal.ufg.br/n/90450-vies-de-confirmacao-e-publicacao-cientifica (Viés de confirmação e viés de publicação)
- https://en.wikipedia.org/wiki/Dark_figure_of_crime (Dark figure of crime — conceito usado também na inferência sobre o oculto)
- https://repositorio.fgv.br/server/api/core/bitstreams/7e2da3ca-af7f-4338-95a3-88dbd640fd42/content (FGV — pensamento contrafactual e inferência causal em avaliação)
- https://repositorio.ipea.gov.br/entities/book/40676951-eabf-494c-8aea-348c820eeebd (IPEA — avaliação ex ante; desenho causal e contrafactual)
