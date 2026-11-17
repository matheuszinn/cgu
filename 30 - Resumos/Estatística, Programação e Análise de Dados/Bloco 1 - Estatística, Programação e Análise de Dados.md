---
tipo: resumo
disciplina: "Estatística, Programação e Análise de Dados"
tema: "Bloco 1 — Estatística, Programação e Análise de Dados (Completo)"
status: novo
data: "2026-11-03"
tags: [resumo, ciencia-de-dados, cgu-2026, cargo-2]
---

# Plano de Estudo Exaustivo: Estatística, Programação e Análise de Dados — Concurso CGU (AFFC — Ciência de Dados)

> [!info] MOC: [[Estatística, Programação e Análise de Dados]]
> Edital nº 1/2026 – CGU – AFFC · **Conhecimentos específicos** · Cargo 2 (TI / Ciência de Dados).

---

## 1. Resumo Estruturado

### 1.1 Exploração e Descrição de Dados

A estatística descritiva e a análise exploratória de dados (EDA) constituem a fundação analítica para o exame detalhado de bases de dados governamentais. O estudo das variáveis exige a distinção rigorosa entre variáveis **qualitativas** (**nominais**, que não possuem ordenação intrínseca, e **ordinais**, que estabelecem hierarquia) e **quantitativas** (**discretas**, resultantes de contagens, e **contínuas**, derivadas de medições em escala real).

As distribuições de frequências organizam a variabilidade dos dados em tabelas absolutas, relativas e acumuladas. Para resumir a posição central da distribuição, utilizam-se a **média aritmética** (soma dos valores dividida pelo total de observações $n$), a **mediana** (valor que divide a amostra ordenada em duas metades de 50%) e a **moda** (valor de maior frequência). A dispersão da distribuição é quantificada pela **amplitude total**, pela **variância amostral** ($s^2$, calculada com $n-1$ graus de liberdade no denominador para garantir a propriedade de estimador não tendencioso da variância populacional $\sigma^2$), pelo **desvio-padrão** ($s = \sqrt{s^2}$), pela **amplitude interquartil** ($\text{IQR} = Q_3 - Q_1$) e pelo **coeficiente de variação** ($\text{CV} = \frac{s}{\bar{x}} \times 100\%$), este último representando uma medida de dispersão relativa imune à escala das variáveis.

A exploração visual utiliza histogramas e gráficos de densidade empírica para avaliar a assimetria e a curtose (que mede o peso das caudas e o pico da distribuição, não apenas o achatamento), e diagramas **Boxplot** para sintetizar a distribuição por meio do resumo de cinco números: mínimo, primeiro quartil ($Q_1$), mediana ($Q_2$), terceiro quartil ($Q_3$) e máximo. Na identificação de anomalias pelo **critério de Tukey** em Boxplots, valores situados abaixo da barreira inferior ($Q_1 - 1,5 \times \text{IQR}$) ou acima da barreira superior ($Q_3 + 1,5 \times \text{IQR}$) são classificados formalmente como *outliers* leves, enquanto distâncias superiores a $3 \times \text{IQR}$ configuram *outliers* extremos.

Ao comparar grupos e períodos em dados administrativos, deve-se distinguir entre **comparações independentes** (grupos distintos avaliados sem vínculo direto entre as observações) e **comparações pareadas** (mesmas unidades avaliadas antes e depois de uma intervenção, analisando-se a distribuição das diferenças individuais $d_i = x_{\text{depois}} - x_{\text{antes}}$ para controlar a heterogeneidade basal), além de atentar para as limitações estruturais das fontes públicas, tais como atualizações de cadastros, descontinuidades administrativas, erros de preenchimento e truncamento de séries temporais.

No contexto do controle público exercido pela Controladoria-Geral da União (CGU), a análise exploratória é aplicada para examinar discrepâncias nos custos unitários de contratações de serviços de TI entre diferentes órgãos federais. Se a distribuição dos preços praticados apresentar forte assimetria à direita, impulsionada por contratos pontuais com valores discrepantes, a utilização da mediana e do IQR fornece um diagnóstico da tendência central e da variabilidade muito mais representativo da realidade do que a média e o desvio-padrão, evitando conclusões distorcidas por valores atípicos.

| Métrica | Sensibilidade a Outliers | Aplicação Principal | Medida de Dispersão Associada |
|---|---|---|---|
| **Média Aritmética ($\bar{x}$)** | Alta (não robusta; deslocada por valores extremos). | Distribuições simétricas sem caudas longas. | Desvio-padrão ($s$) e Variância ($s^2$). |
| **Mediana ($Q_2$)** | Nula ou Baixa (estatística robusta de posição). | Distribuições assimétricas ou com ruídos/outliers. | Amplitude Interquartil ($\text{IQR}$). |
| **Moda** | Insensível a extremos pontuais. | Identificação de picos em variáveis qualitativas/discretas. | Não possui medida de dispersão direta. |

**Pegadinhas da CEBRASPE:**
- Sustentar que a média aritmética é uma medida robusta a valores discrepantes e que deve ser preferida à mediana em distribuições de receitas ou gastos públicos fortemente assimétricas.
- Confundir a representação do traço central no diagrama Boxplot, afirmando que a linha interior da caixa indica a média da amostra, quando indica estritamente a mediana ($Q_2$).
- Inverter o cálculo da variância amostral ao utilizar o divisor $n$ em vez de $n-1$, afirmando que a utilização de $n-1$ introduz viés na estimativa da variância populacional.

---

### 2.1 Probabilidade e Inferência Estatística

A teoria da probabilidade fornece o aparato formal para modelar a incerteza inerente aos fenômenos sociais e econômicos. As distribuições teóricas de probabilidade dividem-se em **discretas** — destacando-se a **Binomial**, que modela o número de sucessos em $n$ ensaios independentes de Bernoulli com probabilidade constante $p$, e a de **Poisson**, que modela a contagem de ocorrências raras em um intervalo contínuo de tempo ou espaço — e **contínuas**, com centralidade para a **Distribuição Normal** ($\mathcal{N}(\mu, \sigma^2)$), caracterizada por sua simetria em torno da média $\mu$ e por sua densidade totalmente determinada por $\mu$ e $\sigma^2$. A **Distribuição Normal Padrão ($Z$)** é obtida pela transformação $Z = \frac{X - \mu}{\sigma}$, possuindo média 0 e variância 1.

A inferência estatística busca estimar parâmetros populacionais desconhecidos ($\theta$) a partir de estatísticas amostrais ($T$). A qualidade de um estimador pontual $\hat{\theta}$ é avaliada por quatro propriedades fundamentais: **não tendenciosidade** (ou ausência de viés, quando o valor esperado coincide com o parâmetro real, $E[\hat{\theta}] = \theta$), **consistência** (convergência em probabilidade para $\theta$ à medida que $n \to \infty$), **eficiência** (menor variância possível dentre os estimadores não tendenciosos) e **suficiência** (capacidade de capturar toda a informação relevante contida na amostra sobre o parâmetro $\theta$). A amostragem probabilística garante que cada elemento da população tenha uma probabilidade conhecida e não nula de pertencer à amostra:
- **Amostragem Aleatória Simples (AAS):** todos os elementos possuem a mesma probabilidade de seleção.
- **Amostragem Estratificada:** a população é dividida em subgrupos internamente homogêneos (estratos) e heterogêneos entre si, realizando-se o sorteio dentro de cada estrato para reduzir a variância do estimador.
- **Amostragem por Conglomerados:** a população é dividida em blocos heterogêneos internamente e homogêneos entre si (conglomerados), sorteando-se os blocos inteiros.

Pelo **Teorema do Limite Central (TLC)**, à medida que o tamanho da amostra $n$ cresce ($n \ge 30$), a distribuição amostral da média $\bar{X}$ aproxima-se de uma distribuição normal, independentemente da forma da distribuição da população original, com média $\mu$ e erro-padrão $\sigma_{\bar{x}} = \frac{\sigma}{\sqrt{n}}$ — ressalvando-se que o teorema exige variância finita e que "$n \ge 30$" é convenção prática, não garantia universal. A estimação por intervalo constrói o **Intervalo de Confiança (IC)**, expresso por $\bar{x} \pm z_{\alpha/2} \left(\frac{\sigma}{\sqrt{n}}\right)$, indicando a amplitude de valores razoáveis para o parâmetro sob um determinado nível de confiança $1-\alpha$.

Os testes de hipóteses formulam uma hipótese nula ($H_0$, ausência de efeito ou igualdade) contra uma hipótese alternativa ($H_1$). A decisão de rejeitar ou não $H_0$ baseia-se na comparação da estatística de teste com a região crítica ou na avaliação do $p$-valor.

Em uma auditoria de conformidade em um programa federal de concessão de benefícios sociais, a CGU precisa estimar a proporção de pagamentos indevidos em um universo de 5 milhões de beneficiários. Utilizando amostragem aleatória estratificada por estado e faixa de renda, o auditor extrai uma amostra de 2.000 processos e constrói um intervalo de confiança de 95% para a proporção populacional de irregularidades. Se a margem de erro for de 1,2%, o órgão de controle obtém uma estimativa precisa e juridicamente defensável da perda financeira global sem a necessidade de examinar a totalidade dos registros.

| Técnica de Amostragem | Homogeneidade Interna | Homogeneidade Entre Grupos | Seleção Amostral |
|---|---|---|---|
| **Amostragem Estratificada** | Alta dentro dos estratos. | Baixa entre os estratos. | Sorteio aleatório de elementos dentro de todos os estratos. |
| **Amostragem por Conglomerados** | Baixa dentro dos conglomerados. | Alta entre os conglomerados. | Sorteio aleatório de blocos inteiros (conglomerados). |
| **Amostragem Aleatória Simples** | Não estratifica a população. | Não se aplica. | Sorteio direto e equiprobabilístico de cada elemento. |

**Pegadinhas da CEBRASPE:**
- Afirmar que o Intervalo de Confiança de 95% indica que existe 95% de probabilidade de o valor numérico do parâmetro populacional estar contido nos limites do intervalo específico já calculado após a coleta da amostra.
- Confundir o Teorema do Limite Central, sustentando que ele garante que o aumento do tamanho da amostra transforma a distribuição empírica dos dados brutos observados em uma curva normal.
- Trocar as condições de uso da distribuição $t$-Student pela distribuição Normal Padrão ($Z$), afirmando que a distribuição $t$ deve ser empregada quando a variância populacional $\sigma^2$ é conhecida em pequenas amostras.

---

### 2.2 Pressupostos, Incerteza e Erros de Inferência; Significância Estatística e Relevância Prática

A aplicação rigorosa da inferência estatística exige a verificação continuada dos pressupostos teóricos e a gestão das incertezas associadas ao processo de tomada de decisão. Ao testar hipóteses, o auditor está sujeito a dois tipos fundamentais de erros inferenciais:
- **Erro Tipo I ($\alpha$):** consiste na rejeição indevida da hipótese nula ($H_0$) quando esta é verdadeira (falso positivo);
- **Erro Tipo II ($\beta$):** caracteriza-se pela não rejeição de $H_0$ quando esta é falsa (falso negativo).

O **poder estatístico do teste**, definido por $1 - \beta$, quantifica a capacidade da estatística em detectar um efeito ou irregularidade efetivamente existente na população.

O **$p$-valor** é definido formalmente como a probabilidade condicional de obter uma estatística de teste igual ou mais extrema do que a observada na amostra, sob a premissa de que a hipótese nula seja verdadeira: $P(\text{Dados Observados ou Mais Extremos} \mid H_0 \text{ é verdadeira})$. Um resultado é considerado estatisticamente significante quando o $p$-valor é inferior ao nível de significância $\alpha$ pré-fixado (comumente $0,05$ ou $0,01$).

No entanto, há uma diferença fundamental entre a **significância estatística** e a **relevância prática** ou econômica. Em cenários analíticos que envolvem grandes volumes de dados (*Big Data* ou bases administrativas governamentais), o erro-padrão tende a valores próximos de zero em virtude do elevado tamanho amostral $n$. Consequentemente, variações ínfimas na média amostral resultam em $p$-valores extremamente baixos ($p < 0,001$), conduzindo à rejeição de $H_0$. O pesquisador deve, portanto, calcular o **tamanho do efeito (*effect size*)**, utilizando métricas como o $d$ de Cohen para diferenças de médias ou a Razão de Chances (*Odds Ratio*), para determinar se a magnitude da diferença encontrada possui impacto real na gestão pública.

Ao analisar uma base contendo 10 milhões de notas fiscais eletrônicas de compras públicas de combustíveis, um algoritmo estatístico identifica que os postos da Região A cobram uma média de R$ 5,400 por litro, enquanto os da Região B cobram R$ 5,402. Devido ao tamanho massivo da amostra ($n = 10.000.000$), o teste $t$ resulta em $p < 0,0001$, confirmando significância estatística. No entanto, a diferença prática de R$ 0,002 por litro (dois décimos de centavo) não apresenta relevância prática ou materialidade orçamentária que justifique a abertura de um processo fiscalizatório pela CGU.

| Conceito Inferencial | Erro Tipo I ($\alpha$) | Erro Tipo II ($\beta$) |
|---|---|---|
| **Definição Operacional** | Rejeitar $H_0$ quando $H_0$ é verdadeira (Falso Positivo). | Não rejeitar $H_0$ quando $H_0$ é falsa (Falso Negativo). |
| **Taxa de Controle** | Fixada *a priori* pelo pesquisador ($\alpha = 0,05$). | Controlada pelo tamanho da amostra ($n$) e efeito. |
| **Poder Relacionado** | Nível de significância ($1 - \alpha$ é a confiança). | Poder do teste é dado por $1 - \beta$. |
| **Consequência em Auditoria** | Apontar irregularidade em um gestor regular. | Concluir por regularidade em um contrato fraudado. |

**Pegadinhas da CEBRASPE:**
- Definir o $p$-valor como a probabilidade direta de a hipótese nula ser verdadeira dada a amostra coletada, ou seja, $P(H_0 \text{ verdadeira} \mid \text{Dados})$.
- Afirmar que a obtenção de um $p$-valor extremamente pequeno ($p < 0,001$) em bases de dados massivas comprova, por si só, a presença de um impacto financeiro relevante no órgão auditado.
- Sustentar que a redução do nível de significância $\alpha$ de 5% para 1% reduz simultaneamente o risco de cometer Erro Tipo II ($\beta$), ignorando a relação inversa entre as taxas de erro para um tamanho de amostra fixo.

---

### 3.1 Correlação, Regressão e Análise de Variância (ANOVA)

A análise de relações entre variáveis investiga como duas ou mais características se associam, variam conjuntamente ou explicam um determinado desfecho continuado. O **Coeficiente de Correlação Linear de Pearson ($r$)** mensura a força e a direção da associação linear entre duas variáveis contínuas, variando no intervalo $[-1, 1]$. Para relações monótonas não necessariamente lineares ou variáveis ordinais, emprega-se o **Coeficiente de Spearman ($\rho$)**.

A **Regressão Linear por Mínimos Quadrados Ordinários (MQO)** modela a relação entre uma variável resposta $Y$ e uma ou mais variáveis explicativas $X$ por meio da equação $Y = \beta_0 + \beta_1 X_1 + \dots + \beta_k X_k + \varepsilon$. O método de MQO estima os parâmetros $\beta$ minimizando a soma dos quadrados dos resíduos ($\sum e_i^2$). A validade das inferências derivadas de MQO depende do atendimento de quatro pressupostos clássicos (**LINE**):
- **Linearidade:** a relação entre as variáveis explicativas e a resposta é linear nos parâmetros;
- **Independência:** os resíduos $\varepsilon_i$ não são autocorrelacionados;
- **Normalidade:** os resíduos seguem distribuição normal $\mathcal{N}(0, \sigma^2)$;
- **Homocedasticidade:** a variância dos resíduos é constante para todos os níveis dos regressores ($\operatorname{Var}(\varepsilon_i) = \sigma^2$).

A quebra da homocedasticidade (**heterocedasticidade**) preserva a propriedade de não tendenciosidade e consistência dos estimadores de MQO, mas destrói a sua eficiência (deixam de ser BLUE — *Best Linear Unbiased Estimator*), tornando os erros-padrão incorretos e invalidando os testes $t$ e $F$.

A **Análise de Variância (ANOVA)** testa a igualdade de médias entre três ou mais grupos independentes, decompondo a variância total dos dados em Variância Entre Grupos (explicada pelo tratamento ou categoria) e Variância Dentro dos Grupos (residual ou erro). A estatística do teste é a razão de variâncias $F = \frac{\text{QM}_{\text{Entre}}}{\text{QM}_{\text{Dentro}}}$. Os pressupostos da ANOVA exigem **independência** das observações, **normalidade dos resíduos** e **homogeneidade de variâncias** (homocedasticidade entre os grupos, verificada pelos testes de **Levene** ou **Bartlett**).

O ajuste do modelo de regressão é avaliado pelo **Coeficiente de Determinação ($R^2$)**, que mede a proporção da variância total de $Y$ explicada pelos regressores. Contudo, o $R^2$ simples aumenta monotonicamente à medida que novos regressores são adicionados ao modelo, mesmo que irrelevantes. Por essa razão, a comparação de modelos com diferente número de variáveis exige a utilização do **$R^2$ Ajustado ($R^2_{\text{adj}}$)**, que introduz uma penalização pelo número de parâmetros estimados relativo ao tamanho amostral. Para quantificar a magnitude prática das associações (tamanho de efeito), utilizam-se **$\eta^2$ (eta-quadrado) e $\eta^2$ parcial** e o **$f$ de Cohen** na ANOVA, bem como os **coeficientes padronizados ($\beta$)** e o **$f^2$ de Cohen** ($f^2 = \frac{R^2}{1 - R^2}$) na regressão.

Em um estudo sobre despesas hospitalares do SUS, a CGU constrói um modelo de regressão linear para prever o custo de internações em UTI com base no tempo de permanência, idade do paciente e complexidade do procedimento. Se a adição de uma nova variável (ex.: número de leitos do hospital) elevar o $R^2$ simples de 0,75 para 0,76, mas fizer o $R^2$ Ajustado cair de 0,74 para 0,72, o auditor conclui que a variável inserida não possui poder explicativo suficiente para compensar a perda de graus de liberdade, devendo ser descartada do modelo.

| Métrica / Teste | Propriedade Central | Sensibilidade a Graus de Liberdade | Função Principal |
|---|---|---|---|
| **$R^2$ Simples** | Cresce ou permanece constante ao adicionar variáveis. | Insensível ao número de parâmetros. | Medir a proporção da variância explicada no treino. |
| **$R^2$ Ajustado** | Penaliza a inclusão de regressores irrelevantes. | Diretamente ajustado por $n$ e $k$. | Comparar modelos de regressão com diferentes regressores. |
| **ANOVA (Teste $F$)** | Compara a variabilidade entre grupos e dentro dos grupos. | Depende dos graus de liberdade dos grupos e resíduos. | Testar a igualdade simultânea de 3 ou mais médias. |

**Pegadinhas da CEBRASPE:**
- Afirmar que a heterocedasticidade dos resíduos introduz viés sistemático nos coeficientes estimados por MQO, fazendo com que a média dos estimadores difira dos parâmetros reais da população.
- Sustentar que um elevado Coeficiente de Determinação ($R^2 = 0,95$) em um modelo de regressão comprova que a variável explicativa $X$ é a causa direta das alterações observadas na variável resposta $Y$.
- Indicar o Coeficiente de Pearson como a métrica adequada para quantificar a associação entre variáveis qualitativas nominais ou dados contínuos com relações não lineares senoidais.

---

### 3.2 Associação, Predição e Causalidade em Dados Administrativos

A utilização de registros administrativos governamentais — como os dados do CadÚnico, SIAFI, SISSU ou RAIS — impõe desafios conceituais profundos para a análise de dados e fiscalização de políticas públicas. A diferença formal entre **associação preditiva** e **inferência causal** reside na pergunta formulada: a associação preditiva busca estimar o valor esperado da variável resposta $Y$ condicionado à observação do regressor $X$, expresso por $P(Y \mid X)$; enquanto a inferência causal pretende determinar qual seria o valor de $Y$ se intervencionássemos ativamente alterando o estado de $X$, expresso no cálculo do contrafactual por $P(Y \mid do(X))$.

Registros administrativos não são desenhados originalmente para pesquisa estatística ou experimentos aleatorizados. Eles são gerados por processos operacionais e burocráticos, estando frequentemente sujeitos a **vícios de seleção**, truncamento, atrito sistemático e **variáveis de confusão** não observadas. O vício de seleção ocorre quando a probabilidade de uma unidade figurar no banco de dados ou ser contemplada por uma política pública está associada aos próprios desfechos que se pretende avaliar.

Para estabelecer relações causais válidas a partir de dados administrativos observacionais, o analista deve recorrer a métodos quase-experimentais voltados à identificação do contrafactual (o resultado que teria sido observado nos indivíduos tratados caso eles não tivessem recebido o tratamento):
- **Diferenças em Diferenças (DiD):** compara a variação temporal no grupo tratado com a variação temporal no grupo de controle, exigindo o pressuposto de tendências paralelas pré-tratamento;
- **Regressão Descontínua (RDD):** explora pontos de corte arbitrários na elegibilidade de políticas públicas, comparando unidades situadas imediatamente acima e abaixo do limite legal;
- **Pareamento por Escore de Propensão (PSM):** emparelha unidades tratadas e não tratadas que possuem probabilidades semelhantes de receber o tratamento com base em atributos observáveis;
- **Variáveis Instrumentais (IV):** emprega uma variável externa ($Z$) que afeta a resposta $Y$ apenas indiretamente através de seu efeito sobre a variável de tratamento $X$.

A CGU avalia a efetividade de um programa federal que concede apoio financeiro para modernização da gestão fiscal em municípios com Índice de Desenvolvimento Humano (IDH) abaixo de 0,60. Uma simples comparação de médias pós-programa revelaria vício de seleção, pois municípios pobres diferem estruturalmente dos demais em variáveis não observadas. Ao aplicar o desenho de Regressão Descontínua (RDD), o auditor compara os municípios com IDH de 0,599 (tratados) com os de IDH de 0,601 (não tratados). Como esses municípios são idênticos em praticamente todas as características estruturais, a diferença observada na arrecadação pode ser atribuída causalmente ao programa.

| Abordagem Analítica | Pergunta Formal | Principal Ameaça à Validade | Solução Metodológica em Dados Administrativos |
|---|---|---|---|
| **Associação Preditiva** | $P(Y \mid X)$: Qual o valor esperado de $Y$ ao observar $X$? | Mudança na distribuição dos dados (*concept drift*). | Validação cruzada e modelos supervisionados. |
| **Inferência Causal** | $P(Y \mid do(X))$: Qual o impacto contrafactual de alterar $X$? | Vício de seleção e variáveis de confusão. | Métodos quase-experimentais (DiD, RDD, PSM, IV). |

**Pegadinhas da CEBRASPE:**
- Sustentar que, por englobarem a totalidade dos registros cadastrais de um determinado programa social governamental (censo administrativo), os dados estão livres de vício de seleção e dispensam técnicas de pareamento ou controle por variáveis de confusão.
- Confundir validade interna (capacidade de demonstrar causalidade isenta de viés no estudo específico) com validade externa (capacidade de generalizar as conclusões causais para outros órgãos ou populações).
- Afirmar que algoritmos de aprendizado de máquina com alto poder preditivo ($R^2 = 0,99$ ou $\text{AUC-ROC} = 0,98$) são capazes de identificar autonomamente as relações de causa e efeito em bases de dados observacionais.

---

### 4.1 Programação em Python 3 para Análise de Dados

A linguagem Python 3 é uma das principais tecnologias adotadas para automação de processos analíticos e engenharia de dados. A linguagem opera como linguagem multiparadigma (OO, procedural e funcional), apresentando tipagem dinâmica. Suas estruturas de dados nativas dividem-se em **mutáveis** (cujo estado pode ser alterado *in-place* sem modificar o endereço de memória do objeto) e **imutáveis** (cuja alteração exige a alocação de um novo objeto).

- As **listas (`list`)** são sequências ordenadas e mutáveis de elementos delimitadas por colchetes;
- As **tuplas (`tuple`)** são sequências ordenadas e imutáveis delimitadas por parênteses;
- Os **dicionários (`dict`)** são mapeamentos mutáveis de chaves e valores baseados em tabelas hash; e
- Os **conjuntos (`set`)** são coleções mutáveis de elementos únicos não ordenados.

O controle de fluxo é estruturado pela indentação obrigatória em blocos `if-elif-else`, `for` e `while`. O tratamento de exceções utiliza o bloco `try-except-else-finally`. A cláusula `except` intercepta falhas em tempo de execução; a cláusula `else` é executada estritamente quando nenhuma exceção é lançada no bloco `try`; e o bloco `finally` é sempre executado, independentemente da ocorrência de erros, sendo ideal para a liberação de recursos, como o fechamento de conexões de banco de dados ou arquivos.

A organização modular do código em rotinas reutilizáveis emprega a criação de módulos (`.py`) e pacotes, suportada pelo uso de funções com escopo local e global. A reprodutibilidade de análises e a garantia de qualidade são mantidas por meio de testes unitários automatizados com as bibliotecas `unittest` ou `pytest`. Para depuração e rastreabilidade em pipelines de dados, utilizam-se `pdb`/`breakpoint()`, o módulo `logging`, a inspeção de pilhas de erro com `traceback` e verificações de invariantes via `assert`; já a manipulação de arquivos engloba a leitura e escrita de formatos CSV, JSON e Parquet com controle explícito de `encoding` (ex.: `utf-8`, `latin-1`) e gerenciamento multiplataforma de caminhos pelo módulo `pathlib`.

Um auditor da CGU desenvolve um script em Python para ler e depurar arquivos CSV volumosos contendo ordens bancárias do governo federal. O script utiliza estruturas `try-except` para capturar exceções do tipo `UnicodeDecodeError` e `KeyError` no processamento de linhas corrompidas. Ao estruturar a leitura dentro de um gerenciador de contexto (`with open(...) as arquivo:`), o código garante que o descritor do arquivo seja encerrado corretamente na memória mesmo que ocorra uma falha crítica na execução da rotina.

| Estrutura de Dados | Sintaxe | Ordenada? | Mutável? | Admite Duplicatas? |
|---|---|---|---|---|
| **Lista (`list`)** | `[1, 2, 2]` | Sim | Sim | Sim |
| **Tupla (`tuple`)** | `(1, 2, 2)` | Sim | Não | Sim |
| **Dicionário (`dict`)** | `{'a': 1}` | Sim (Python 3.7+) | Sim | Não para chaves; Sim para valores |
| **Conjunto (`set`)** | `{1, 2}` | Não | Sim | Não |

**Pegadinhas da CEBRASPE:**
- Afirmar que a cláusula `else` em uma estrutura `try-except-else-finally` será acionada sempre que uma exceção for capturada e tratada com sucesso pelo bloco `except`.
- Sustentar que a tentativa de alterar um elemento interno de uma tupla que contém uma lista mutável (ex.: `t = ([1, 2], 3)`) resulta obrigatoriamente em um erro `TypeError`, ignorando que a lista interna pode ser alterada *in-place* (`t[0].append(3)`).
- Afirmar que as listas em Python são estruturas imutáveis e que o método `append()` gera um novo objeto na memória com um identificador (`id()`) distinto do original.
- Ignorar que um `return` dentro do `finally` sobrescreve o valor de retorno do `try` (ou do `except`/`else`), além de suprimir eventuais exceções pendentes não tratadas.

---

### 5.1 Preparação de Dados, Engenharia de Atributos e Prevenção de Data Leakage

A etapa de preparação de dados transforma bases brutas contendo imperfeições em matrizes de atributos adequadas para algoritmos de análise e aprendizado de máquina. O tratamento de valores ausentes (*missing values*) deve considerar os mecanismos subjacentes:
- **MCAR (*Missing Completely at Random*):** a probabilidade de ausência é independente dos dados observados e não observados;
- **MAR (*Missing at Random*):** a ausência depende dos dados observados, mas não dos próprios valores ausentes;
- **MNAR (*Missing Not at Random*):** a ausência depende do próprio valor não observado.

As estratégias de imputação variam entre métodos simples (substituição pela média em distribuições simétricas ou pela mediana em distribuições assimétricas) e métodos complexos baseados em modelos, como o `KNN Imputer` ou `IterativeImputer`.

A limpeza de dados envolve a remoção de duplicações e a adequação de inconsistências. No tratamento de dados desbalanceados (situação em que a classe de interesse é extremamente rara), empregam-se técnicas de *undersampling* (redução aleatória da classe majoritária) e *oversampling* sintético, como o algoritmo **SMOTE (*Synthetic Minority Over-sampling Technique*)**, que cria novas instâncias da classe minoritária por meio de interpolação linear entre vizinhos mais próximos.

A transformação e escalonamento de atributos são etapas fundamentais para algoritmos baseados em métricas de distância (como KNN, SVM e K-Means) ou gradiente descendente. A padronização Z-score (`StandardScaler`, $Z = \frac{X - \mu}{\sigma}$, média 0 e desvio-padrão 1) é sensível a outliers (média e desvio-padrão são influenciados por extremos); para robustez, usar `RobustScaler` (mediana/IQR). O `MinMaxScaler` ($X_{\text{norm}} = \frac{X - X_{\min}}{X_{\max} - X_{\min}}$, que reescala o atributo para o intervalo estrito $[0, 1]$) é o mais sensível.

A codificação de variáveis categóricas utiliza **One-Hot Encoding** para atributos nominais sem hierarquia (criando variáveis binárias *dummy*) e **Ordinal Encoding** para categorias ordenadas. A **seleção de atributos (*feature selection*)** divide-se em métodos **filter** (baseados em propriedades estatísticas intrínsecas, como correlação, informação mútua e qui-quadrado), **wrapper** (que avaliam subconjuntos usando o próprio modelo, como RFE — *Recursive Feature Elimination* — e seleção *forward/backward*) e **embedded** (integrados ao treinamento do algoritmo, como regularização Lasso $L_1$ e importância de atributos em árvores); já a **engenharia de atributos (*feature engineering*)** abrange a extração de componentes de datas/ciclos temporais, termos de interação entre variáveis, *target encoding* (codificação pela média do alvo, exigindo validação cruzada ou suavização para evitar vazamento) e *binning* (discretização de variáveis contínuas em faixas).

A prevenção de vazamento de informação (**Data Leakage**) constitui a regra técnica mais crítica na preparação de dados. O *Data Leakage* ocorre quando informações do conjunto de teste ou do futuro são indevidamente introduzidas no processo de treinamento do modelo, gerando métricas de desempenho otimistas que não se sustentam na implantação em produção. Para evitar o vazamento, a divisão entre os conjuntos de treino e teste deve preceder qualquer operação de pré-processamento. Estatísticas como média, desvio-padrão, limites de MinMax, vocabulários e imputadores devem ser calculados (`fit`) estritamente sobre a partição de treino e posteriormente aplicados (`transform`) às partições de teste e validação.

Em um projeto da CGU focado no desenvolvimento de um modelo preditivo para identificar empresas de fachada em licitações públicas, a base de dados contém 100.000 contratos, sendo apenas 500 associados a empresas irregulares (desbalanceamento de 0,5%). O analista realiza a separação prévia entre treino (80%) e teste (20%). Em seguida, ajusta o `StandardScaler` e o algoritmo SMOTE estritamente na partição de treino. A transformação de escalonamento é então aplicada ao conjunto de teste sem reajustar os parâmetros, garantindo que o modelo seja avaliado sobre dados perfeitamente isolados e imunes ao vazamento de informação.

| Método de Escalonamento | Formulação Matemática | Sensibilidade a Outliers | Limites do Resultado | Algoritmos Beneficiados |
|---|---|---|---|---|
| **Padronização (`StandardScaler`)** | $Z = \frac{X - \mu}{\sigma}$ | Sensível (média e desvio-padrão sofrem com extremos) | Sem limites fixos (Média = 0, Variância = 1) | Regressão Ridge/Lasso, SVM, PCA |
| **Escalonamento Robusto (`RobustScaler`)** | $X_{\text{rob}} = \frac{X - Q_2}{\text{IQR}}$ | Baixa (robusto; usa mediana e IQR) | Sem limites fixos (Mediana = 0, IQR = 1) | Dados com presença severa de outliers |
| **Normalização (`MinMaxScaler`)** | $X_{\text{norm}} = \frac{X - X_{\min}}{X_{\max} - X_{\min}}$ | Muito Alta (o mais sensível; comprime dados normais) | Intervalo rígido $[0, 1]$ | Redes Neurais, Algoritmos de Distância |

**Pegadinhas da CEBRASPE:**
- Recomendar a aplicação de técnicas de sobreamostragem de dados como o SMOTE sobre a totalidade do banco de dados antes de efetuar a divisão aleatória entre os conjuntos de treinamento e teste.
- Sustentar que a padronização $Z$-score transforma qualquer distribuição de dados brutos assimétricos em uma distribuição normal perfeita.
- Afirmar que o algoritmo `KNN Imputer` pode ser aplicado diretamente sobre atributos numéricos de escalas discrepantes sem a necessidade de escalonamento prévio dos dados.

---

## 2. Flashcards de Alta Retenção

- Qual a principal limitação da média aritmética em dados assimétricos? :: A média é altamente sensível a valores discrepantes (outliers), sendo deslocada em direção à cauda da distribuição.
- Como a amplitude interquartil (IQR) é calculada no Boxplot? :: Pela diferença entre o terceiro e o primeiro quartil: $\text{IQR} = Q_3 - Q_1$.
- Quais são as barreiras de outliers leves pelo critério de Tukey? :: Limite Inferior = $Q_1 - 1,5 \times \text{IQR}$ e Limite Superior = $Q_3 + 1,5 \times \text{IQR}$.
- Qual estatística resume o centro de um Boxplot? :: A linha central no interior da caixa representa a mediana ($Q_2$).
- O Coeficiente de Variação (CV) permite comparar grupos de escalas distintas? :: Sim, pois expressa a razão entre o desvio-padrão e a média como uma proporção imune à unidade de medida original.
- O que diferencia a amostragem estratificada da amostragem por conglomerados? :: A estratificada seleciona elementos dentro de todos os estratos (homogêneos); a de conglomerados sorteia blocos inteiros (heterogêneos).
- Por que a variância amostral utiliza o divisor $n-1$? :: Para fornecer um estimador não tendencioso da variância populacional desconhecida.
- O que afirma o Teorema do Limite Central (TLC)? :: Que a distribuição amostral da média aproxima-se de uma distribuição normal à medida que o tamanho da amostra $n$ cresce.
- Como se conceitua formalmente o Intervalo de Confiança de 95%? :: Indica que 95% dos intervalos construídos por amostragens repetidas contêm o verdadeiro parâmetro populacional.
- Quando a distribuição $t$-Student deve substituir a distribuição Normal $Z$? :: Quando a variância populacional é desconhecida e o tamanho amostral é pequeno.
- O que define o Erro Tipo I ($\alpha$) em testes de hipóteses? :: Ocorre ao rejeitar a hipótese nula ($H_0$) quando ela é verdadeiramente correta (Falso Positivo).
- O que define o Erro Tipo II ($\beta$) em testes de hipóteses? :: Ocorre ao não rejeitar a hipótese nula ($H_0$) quando ela é verdadeiramente falsa (Falso Negativo).
- O que representa o poder de um teste estatístico ($1 - \beta$)? :: A probabilidade de rejeitar corretamente a hipótese nula quando a hipótese alternativa é verdadeira.
- Qual a definição formal do $p$-valor? :: É a probabilidade de obter estatística igual ou mais extrema que a observada, dado que $H_0$ é verdadeira.
- Por que a significância estatística difere da relevância prática? :: Porque em grandes amostras ($n$ elevado), diferenças irrisórias atingem $p < 0,05$ sem possuírem impacto real.
- Qual a consequência da heterocedasticidade nos estimadores de MQO? :: Os estimadores continuam não tendenciosos e consistentes, mas perdem a eficiência e invalidam os erros-padrão.
- Qual o benefício do $R^2$ Ajustado em relação ao $R^2$ simples? :: O $R^2$ Ajustado penaliza a adição de regressores irrelevantes que não elevam o poder explicativo real.
- O que exige o pressuposto de Normalidade nos resíduos da regressão? :: Exige que os erros $\varepsilon_i$ sigam distribuição normal $\mathcal{N}(0, \sigma^2)$ para validar os testes $t$ e $F$.
- Qual estatística é utilizada na tabela ANOVA para testar igualdade de médias? :: A estatística de teste $F$, calculada pela razão entre o Quadrado Médio Entre Grupos e Dentro dos Grupos.
- Por que correlação linear de Pearson elevada não prova causalidade? :: Porque mensura apenas a associação conjunta entre variáveis, sem identificar a direção de causa e efeito ou isolar variáveis de confusão.
- Qual a diferença formal entre $P(Y \mid X)$ e $P(Y \mid do(X))$? :: $P(Y \mid X)$ representa a observação preditiva; $P(Y \mid do(X))$ representa a intervenção contrafactual causal.
- O que é o vício de seleção em dados administrativos? :: Distorção ocorrida quando a entrada na base de dados ou tratamento é associada ao próprio desfecho analisado.
- Como o método de Diferenças em Diferenças (DiD) estabelece a causalidade? :: Comparando a variação temporal do grupo tratado com a do controle sob o pressuposto de tendências paralelas.
- Como o método RDD identifica o efeito causal em políticas públicas? :: Comparando unidades situadas imediatamente acima e abaixo de um ponto de corte arbitrário de elegibilidade.
- Quais são os tipos de dados mutáveis fundamentais em Python 3? :: Listas (`list`), dicionários (`dict`) e conjuntos (`set`).
- Quais são os tipos de dados imutáveis fundamentais em Python 3? :: Tuplas (`tuple`), strings (`str`), inteiros (`int`) e flutuantes (`float`).
- Quando o bloco `else` é executado na estrutura `try-except-else-finally`? :: Apenas quando o bloco `try` é finalizado sem que nenhuma exceção seja lançada.
- O que faz a instrução `finally` no tratamento de exceções em Python? :: Executa seu bloco obrigatoriamente, tenha-se ou não lançado exceções, sendo usada para liberação de recursos.
- O que diferencia `copy.copy()` de `copy.deepcopy()` em Python? :: A cópia rasa duplica o container mantendo referências internas; a profunda recria recursivamente todos os objetos.
- O que caracteriza a ausência de dados do tipo MCAR? :: Quando a probabilidade de um dado estar ausente é totalmente aleatória e independente de qualquer variável.
- Como o algoritmo SMOTE trata o desbalanceamento de classes? :: Cria instâncias sintéticas da classe minoritária por interpolação linear entre vizinhos mais próximos.
- Qual a fórmula de transformação da padronização `StandardScaler`? :: $Z = \frac{X - \mu}{\sigma}$, resultando em média 0 e desvio-padrão 1.
- Qual a fórmula de transformação da normalização `MinMaxScaler`? :: $X_{\text{norm}} = \frac{X - X_{\min}}{X_{\max} - X_{\min}}$, comprimindo os dados no intervalo $[0, 1]$.
- O que caracteriza o fenômeno de Data Leakage no pré-processamento? :: O uso de informações do conjunto de teste ou do futuro para ajustar transformadores durante o treinamento.
- Como prevenir o Data Leakage na preparação de matrizes de dados? :: Realizando a divisão de treino e teste antes de qualquer ajuste (`fit`) de escaladores ou imputadores.

---

## 3. Questões Inéditas no Estilo CEBRASPE (Certo/Errado)

**Questão 1**
No âmbito da análise exploratória de dados de contratações públicas, a mediana e a amplitude interquartil são estatísticas de posição e dispersão recomendadas para sintetizar variáveis que apresentam distribuições fortemente assimétricas com presença de valores discrepantes, visto que a média e o desvio-padrão são altamente sensíveis a outliers.
- **Gabarito:** CERTO
- **Justificativa:** O item está correto. A média aritmética e o desvio-padrão não são medidas robustas, pois incorporam diretamente a magnitude de todos os valores da amostragem, sendo fortemente distorcidos por observações extremas ou distribuições assimétricas. Nessas condições, a mediana (que reflete a posição central dos dados ordenados) e a amplitude interquartil ($\text{IQR} = Q_3 - Q_1$, que avalia a dispersão dos 50% centrais dos dados) constituem métricas representativas.

**Questão 2**
Considerando o processo de amostragem em auditorias governamentais, a amostragem estratificada consiste na divisão da população em grupos heterogêneos internamente e homogêneos entre si, procedendo-se posteriormente ao sorteio aleatório de alguns desses grupos inteiros para compor a amostra final de análise.
- **Gabarito:** ERRADO
- **Justificativa:** O item está incorreto por inverter as definições de amostragem estratificada e por conglomerados. Na amostragem estratificada, a população é dividida em estratos homogêneos internamente e heterogêneos entre si, realizando-se o sorteio de elementos dentro de todos os estratos. A descrição fornecida na questão refere-se formalmente à Amostragem por Conglomerados, na qual os grupos são heterogêneos internamente e sorteiam-se os blocos inteiros.

**Questão 3**
Em testes de hipóteses estatísticas aplicados a grandes bases de dados administrativos ($n > 1.000.000$), a obtenção de um $p$-valor inferior a $0,001$ assegura a existência de uma relevância prática e materialidade orçamentária expressiva, autorizando o auditor a concluir pela presença de uma irregularidade com impacto financeiro amplo.
- **Gabarito:** ERRADO
- **Justificativa:** O item está incorreto por confundir significância estatística com relevância prática. Em amostras de tamanho maciço ($n$ elevado), o erro-padrão do estimador tende a zero, fazendo com que desvios irrisórios ou irrelevantes na prática atinjam rejeição da hipótese nula com $p$-valores extremamente baixos ($p < 0,001$). A relevância prática ou materialidade orçamentária deve ser verificada pelo tamanho do efeito (*effect size*), e não apenas pelo valor do $p$-valor.

**Questão 4**
Na regressão linear estimada pelo método de Mínimos Quadrados Ordinários (MQO), a ocorrência de heterocedasticidade nos resíduos viola os pressupostos clássicos do modelo, tornando os estimadores dos coeficientes tendenciosos e inconsistentes.
- **Gabarito:** ERRADO
- **Justificativa:** O item está incorreto. A heterocedasticidade (variância não constante dos resíduos) não causa tendência ou inconsistência nos estimadores de MQO; os coeficientes permanecem imparciais e não tendenciosos. Contudo, a heterocedasticidade destrói a eficiência dos estimadores (deixam de ter a menor variância) e faz com que o cálculo dos erros-padrão fique incorreto, invalidando os testes de hipóteses $t$ e $F$.

**Questão 5**
A utilização de bases de dados administrativos governamentais em substituição a experimentos aleatorizados garante a identificação direta do efeito causal de uma política pública, pois a cobertura censitária dessas bases elimina integralmente o vício de seleção e as variáveis de confusão não observadas.
- **Gabarito:** ERRADO
- **Justificativa:** O item está incorreto. A simples cobertura populacional ou cadastral massiva dos dados administrativos não elimina o vício de seleção nem as variáveis de confusão. Como os dados administrativos derivam de registros passivos e de processos de adesão a programas públicos que dependem de regras ou escolhas dos beneficiários, a inferência causal exige obrigatoriamente a aplicação de métodos quase-experimentais (como DiD, RDD ou PSM) para tratar a ausência de aleatorização.

**Questão 6**
Considere o seguinte código escrito em Python 3:
```python
def processar_dados(lista_valores):
    try:
        resultado = [x / 2 for x in lista_valores]
    except TypeError:
        return "Erro de Tipo"
    else:
        return "Processamento Concluído"
    finally:
        print("Operação Finalizada")
```
Se a função for chamada com o argumento `processar_dados([10, 20, 30])`, a string `"Processamento Concluído"` será retornada e a frase `"Operação Finalizada"` será exibida no console.
- **Gabarito:** CERTO
- **Justificativa:** O item está correto. Como a lista `[10, 20, 30]` contém apenas números válidos para a divisão por 2, nenhuma exceção é lançada no bloco `try`. Consequentemente, o bloco `except` é ignorado, a cláusula `else` é executada (retornando a string `"Processamento Concluído"`) e o bloco `finally` é executado antes da saída final da função, imprimindo a mensagem no terminal.

**Questão 7**
Visando prevenir o vazamento de informação (*Data Leakage*) na preparação de dados para um modelo de aprendizado de máquina, o profissional deve realizar o escalonamento dos atributos (`StandardScaler`) em toda a base de dados antes de efetuar a divisão dos dados entre os conjuntos de treinamento e de teste.
- **Gabarito:** ERRADO
- **Justificativa:** O item está incorreto por inverter o procedimento correto e descrever exatamente a causa do *Data Leakage*. Ao aplicar o `StandardScaler` na base inteira antes do split, as estatísticas de média e desvio-padrão do conjunto de teste vazam para o processo de pré-processamento. O correto é realizar a separação de treino e teste primeiro, ajustar (`fit`) o escalador estritamente nos dados de treino e apenas aplicar a transformação (`transform`) nos dados de teste.

**Questão 8**
O algoritmo SMOTE (*Synthetic Minority Over-sampling Technique*) é uma técnica de pré-processamento para dados desbalanceados que atua duplicando de forma idêntica as instâncias existentes na classe majoritária, reduzindo a variância do modelo final sem alterar a distribuição dos atributos.
- **Gabarito:** ERRADO
- **Justificativa:** O item está incorreto em dois pontos conceituais: primeiro, o SMOTE atua na classe minoritária (e não na majoritária); segundo, o SMOTE não realiza duplicação simples/idêntica de instâncias. Ele cria novas instâncias sintéticas da classe minoritária por meio de interpolação linear entre observações vizinhas mais próximas no espaço de atributos.

---

## 4. Glossário Técnico

- **Amplitude Interquartil ($\text{IQR}$):** Medida de dispersão robusta calculada pela diferença entre o terceiro e o primeiro quartil ($Q_3 - Q_1$).
- **Amostragem Estratificada:** Método probabilístico que divide a população em estratos homogêneos e sorteia amostras dentro de cada um deles.
- **Amostragem por Conglomerados:** Método probabilístico que divide a população em blocos heterogêneos e sorteia os blocos inteiros.
- **ANOVA (Análise de Variância):** Teste estatístico baseado na estatística $F$ utilizado para comparar a igualdade de médias entre três ou mais grupos.
- **Boxplot:** Diagrama visual que representa a distribuição de dados por meio de quartis, mediana e identificação de outliers.
- **Coeficiente de Determinação ($R^2$):** Métrica que quantifica a proporção da variância total da variável resposta explicada pelo modelo de regressão.
- **Coeficiente de Variação ($\text{CV}$):** Medida de dispersão relativa definida pela razão entre o desvio-padrão e a média.
- **Data Leakage:** Vazamento de informações do conjunto de teste ou do futuro para o processo de treinamento do modelo.
- **Diferenças em Diferenças (DiD):** Método quase-experimental para avaliação de impacto causal comparando variações temporais entre tratados e controles.
- **Erro Tipo I ($\alpha$):** Erro inferencial consistente em rejeitar uma hipótese nula que é verdadeiramente verdadeira (Falso Positivo).
- **Erro Tipo II ($\beta$):** Erro inferencial consistente em não rejeitar uma hipótese nula que é verdadeiramente falsa (Falso Negativo).
- **Heterocedasticidade:** Condição na qual a variância dos resíduos de um modelo de regressão não é constante entre as observações.
- **Homocedasticidade:** Pressuposto de que os resíduos de uma regressão possuem variância constante ao longo de todas as observações.
- **Imutabilidade:** Propriedade de objetos em linguagens de programação cujos estados internos não podem ser alterados após a alocação na memória.
- **Normalização ($MinMax$):** Rescalonamento de um atributo para um intervalo estrito entre $0$ e $1$.
- **$p$-valor:** Probabilidade condicional de obter uma estatística amostral igual ou mais extrema do que a observada, dada a veracidade de $H_0$.
- **Padronização ($Z$-score):** Transformação de um atributo para que apresente média $0$ e desvio-padrão $1$.
- **Poder Estatístico ($1 - \beta$):** Probabilidade de um teste estatístico rejeitar corretamente a hipótese nula quando esta for falsa.
- **Regressão Descontínua (RDD):** Método causal que explora pontos de corte arbitrários na regra de elegibilidade a programas públicos.
- **Relevância Prática:** Magnitude real e impacto prático do efeito medido, independentemente do nível de significância estatística.
- **SMOTE:** Técnica que gera dados sintéticos para a classe minoritária por interpolação de vizinhos mais próximos.
- **Teorema do Limite Central (TLC):** Princípio segundo o qual a distribuição amostral das médias aproxima-se da Normal para grandes amostras.
- **Vício de Seleção:** Distorção amostral decorrente de processos não aleatórios de entrada na base de dados ou no tratamento.

---

## 5. Mapa Mental

- **BLOCO 1 — ESTATÍSTICA, PROGRAMAÇÃO E ANÁLISE DE DADOS**
  - **1. Exploração e Descrição de Dados**
    - Tipos de Variáveis e Mensuração
      - Qualitativas (Nominais, Ordinais)
      - Quantitativas (Discretas, Contínuas)
    - Medidas de Posição
      - Média Aritmética (Não robusta, sensível a outliers)
      - Mediana (Medida robusta de tendência central)
      - Quartis e Percentis (Resumo de cinco números)
    - Medidas de Dispersão
      - Variância e Desvio-Padrão ($n-1$ na amostra)
      - Amplitude Interquartil ($\text{IQR} = Q_3 - Q_1$)
      - Coeficiente de Variação ($\text{CV} = \frac{s}{\bar{x}}$)
    - Exploração Visual e Anomalias
      - Histogramas e Distribuição Empírica
      - Boxplot e Critério de Tukey ($1,5 \times \text{IQR}$)
  - **2. Probabilidade e Inferência Estatística**
    - Distribuições de Probabilidade
      - Discretas (Binomial, Poisson)
      - Contínuas (Normal Padrão $Z$, $t$-Student, $F$, Qui-quadrado)
    - Amostragem e Estimação
      - Amostragem Aleatória Simples
      - Amostragem Estratificada (Estratos homogêneos)
      - Amostragem por Conglomerados (Blocos heterogêneos)
      - Teorema do Limite Central (Normalidade da média)
      - Intervalos de Confiança (Conceito de cobertura repetida)
    - Testes de Hipóteses e Erros Inferenciais
      - Hipótese Nula ($H_0$) e Alternativa ($H_1$)
      - Erro Tipo I ($\alpha$) vs. Erro Tipo II ($\beta$)
      - Poder do Teste ($1 - \beta$)
      - $p$-valor ($P(\text{Dados} \mid H_0)$)
      - Significância Estatística vs. Relevância Prática (Tamanho de Efeito)
  - **3. Relações entre Variáveis**
    - Associação e Regressão
      - Correlação Linear de Pearson vs. Monótona de Spearman
      - Regressão Linear por MQO ($Y = \beta_0 + \beta_1 X + \varepsilon$)
      - Pressupostos LINE (Linearidade, Independência, Normalidade, Homocedasticidade)
      - Consequência da Heterocedasticidade (Ineficiência dos estimadores)
      - Ajuste do Modelo ($R^2$ vs $R^2$ Ajustado)
      - ANOVA (Comparação de médias e estatística $F$)
    - Causalidade em Dados Administrativos
      - Associação Preditiva ($P(Y \mid X)$) vs. Inferência Causal ($P(Y \mid do(X))$)
      - Vício de Seleção e Confusão em Registros Públicos
      - Métodos Quase-Experimentais (DiD, RDD, PSM, IV)
      - Validade Interna vs. Validade Externa
  - **4. Programação para Análise (Python 3)**
    - Estruturas de Dados Nativas
      - Mutáveis (`list`, `dict`, `set`)
      - Imutáveis (`tuple`, `str`, `int`, `float`)
    - Controle de Fluxo e Modularização
      - Indentação estrutural e laços (`for`, `while`)
      - Funções, Escopos e Módulos
    - Tratamento de Exceções
      - Estrutura `try-except-else-finally`
      - Execução restrita do bloco `else`
      - Garantia de execução do `finally`
    - Engenharia de Software e Reprodutibilidade
      - Gerenciadores de Contexto (`with open`)
      - Testes Unitários (`pytest`, `unittest`)
  - **5. Preparação, Transformação e Engenharia de Atributos**
    - Limpeza e Dados Ausentes
      - Mecanismos de Ausência (MCAR, MAR, MNAR)
      - Imputação Simples vs. Algorítmica (`KNN Imputer`)
    - Transformação e Escalonamento
      - Padronização ($Z$-score: Média 0, Variância 1)
      - Normalização ($MinMax$: Intervalo $[0, 1]$)
      - Codificação Categórica (One-Hot vs. Ordinal)
    - Desbalanceamento de Classes
      - Undersampling vs. Oversampling Sintético (SMOTE)
    - Prevenção de Vazamento de Informação (Data Leakage)
      - Divisão estrita entre Treino e Teste antes do pré-processamento
      - Ajuste (`fit`) exclusivo na partição de Treino
