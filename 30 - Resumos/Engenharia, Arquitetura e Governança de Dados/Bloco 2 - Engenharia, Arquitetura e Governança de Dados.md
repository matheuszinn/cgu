---
tipo: resumo
disciplina: "Engenharia, Arquitetura e Governança de Dados"
tema: "Bloco 2 — Engenharia, Arquitetura e Governança de Dados (Completo)"
status: novo
data: "2026-11-03"
tags: [resumo, ciencia-de-dados, cgu-2026, cargo-2]
---

# Guia de Estudo Exaustivo: Engenharia, Arquitetura e Governança de Dados — Concurso CGU 2026 (AFFC)

> [!info] MOC: [[Engenharia, Arquitetura e Governança de Dados]]
> Edital nº 1/2026 – CGU – AFFC · **Conhecimentos específicos** · Cargo 2 (TI / Ciência de Dados).

---

## 1. Resumo Estruturado por Subitem

### 1.1 Modelagem e Arquiteturas: Relacional, NoSQL, Multidimensional e Vetorial

**Definição**
A modelagem de dados especifica a estrutura lógica, as regras de armazenamento, os mecanismos de indexação e a integridade informacional exigida por diferentes classes de sistemas computacionais. Os modelos compreendem o padrão Relacional (organizado em tabelas com forte consistência transacional), as alternativas NoSQL (Documental, Chave-Valor, Grafos e Colunar), a abordagem Multidimensional (estruturada especificamente para suporte à decisão em depósitos analíticos) e o modelo Vetorial (desenvolvido para busca semântica sobre representações numéricas densas de dados não estruturados).

**Para que Serve**
Serve para estabelecer os pilares de sustentabilidade, velocidade de acesso, integridade e flexibilidade dos dados em uma organização. No âmbito do controle público, a escolha adequada do modelo garante a auditabilidade estrita de lançamentos financeiros operacionais ou possibilita a rápida identificação de anomalias em grandes volumes de transações administrativas.

**Como Funciona**
- **Modelo Relacional:** Organiza os dados em tabelas (relações) compostas por colunas (atributos) e linhas (tuplas), impondo integridade referencial por meio de chaves primárias (PK) e estrangeiras (FK). Operações atendem às propriedades **ACID** (Atomicidade, Consistência, Isolamento e Durabilidade). A normalização (1FN, 2FN, 3FN, BCNF) é aplicada para eliminar dependências funcionais inadequadas e prevenir anomalias de inserção, alteração e exclusão.
- **Modelo Documental:** Armazena dados em documentos autoexplicativos e sem esquema fixo pré-definido (*schema-on-read* ou *schema-flex*), geralmente utilizando formatos semiestruturados como JSON, BSON ou XML (ex.: MongoDB).
- **Modelo Chave-Valor:** Estrutura os dados em pares simples compostos por um identificador único (chave) e um conteúdo opaco associado (valor). Prioriza baixíssima latência de leitura e escrita em memória (ex.: Redis).
- **Modelo Multidimensional:** Organiza dados históricos segundo esquemas em Estrela (*Star Schema*) ou Floco de Neve (*Snowflake Schema*). Separa os dados em Tabelas Fato (contendo métricas numéricas acumuladas e chaves de contexto) e Tabelas Dimensão (contendo atributos descritivos do negócio).
- **Modelo Vetorial:** Transforma textos, imagens ou áudios em vetores densos de alta dimensão (*embeddings*) por meio de modelos de aprendizado de máquina. A busca e recuperação ocorrem mediante cálculo de proximidade espacial no vetor, utilizando algoritmos de vizinhos mais próximos (HNSW, IVFFlat) e métricas de distância como similaridade de cosseno, distância euclidiana ou produto escalar.

**Exemplo Aplicado ao Setor Público (CGU)**
A Controladoria-Geral da União (CGU) utiliza o modelo relacional normalizado para gerenciar a execução orçamentária do SIAFI; adota bancos documentais NoSQL para armazenar integrais de editais de licitação e contratos em formato JSON; utiliza bancos multidimensionais para construir cubos OLAP de gastos públicos por função de governo; e emprega bancos vetoriais para realizar buscas semânticas de indícios de plágio ou conluio na descrição de itens de planilhas orçamentárias de obras públicas.

**Comparação de Modelos de Dados**

| Característica | Relacional (OLTP) | Multidimensional (OLAP) | Documental (NoSQL) | Vetorial |
|---|---|---|---|---|
| **Objetivo Primário** | Processamento transacional | Consultas analíticas complexas | Flexibilidade e alta escrita | Busca semântica e IA |
| **Abordagem de Esquema** | Schema-on-Write | Schema-on-Write | Schema-on-Read | Vetores densos fixos |
| **Estilo de Normalização** | Alta (3FN / BCNF) | Desnormalizado (Estrela) | Desnormalizado | N/A |
| **Garantia Padrão** | ACID Estrito | Consistência de Leitura | Teorema CAP / BASE | Indexação gráfica vetorial |

**Pegadinhas Típicas da CEBRASPE**
- Afirmar que a 3ª Forma Normal (3FN) elimina toda e qualquer redundância no banco relacional. Isso é falso: a 3FN elimina apenas dependências transitivas; redundâncias oriundas de dependências funcionais sobre chaves candidatas compostas são tratadas pela Forma Normal de Boyce-Codd (BCNF) e formas superiores.
- Trocar o conceito do esquema em Estrela (*Star Schema*) pelo Floco de Neve (*Snowflake Schema*), afirmando que o esquema em Estrela possui tabelas dimensão normalizadas. No *Star Schema*, as dimensões são propositalmente desnormalizadas; a normalização das dimensões é a marca registrada do *Snowflake Schema*.

---

### 1.2 Arquiteturas Analíticas: Data Warehouse, Data Mart, Data Lake, Lakehouse e Data Mesh

**Definição**
São padrões conceituais e tecnológicos voltados à consolidação, processamento, organização e governança de volumes massivos de dados para suportar a inteligência institucional e a ciência de dados.

**Para que Serve**
Permitem integrar repositórios operacionais isolados, viabilizando a fiscalização contínua, o cruzamento de bases administrativas, a detecção de fraudes e a disponibilização de relatórios analíticos de auditoria.

**Como Funciona**
- **Data Warehouse (DW):** Repositório centralizado contendo dados históricos altamente estruturados e limpos. Utiliza pipelines ETL tradicionais e impõe *schema-on-write*.
- **Data Mart:** Subconjunto focalizado do Data Warehouse, desenhado para atender às necessidades analíticas de um departamento ou processo de negócio específico (ex.: Data Mart de Benefícios Sociais).
- **Data Lake:** Repositório centralizado de armazenamento econômico (geralmente baseado em objetos ou HDFS) que recebe dados estruturados, semiestruturados e não estruturados em seu formato bruto (*raw*), aplicando o padrão *schema-on-read*.
- **Lakehouse:** Arquitetura híbrida moderna que implementa uma camada de armazenamento e gerenciamento aberto (como Delta Lake, Apache Iceberg ou Apache Hudi) sobre o Data Lake. Essa camada confere suporte a transações ACID, versionamento de dados (*time travel*), concorrência e indexação sobre dados em formatos abertos (ex.: Parquet).
- **Data Mesh:** Paradigma sociotécnico descentralizado baseado em quatro pilares essenciais: arquitetura orientada por domínios de conhecimento, dados tratados estritamente como produtos (*data products*), plataforma de infraestrutura federada como autosserviço e governança federada computacional interdominial.

**Exemplo Aplicado ao Setor Público (CGU)**
Na CGU, o Data Lake armazena a totalidade das notas fiscais eletrônicas e registros brutos de diárias de viagem recebidos dos ministérios. A arquitetura Lakehouse consolida esses dados em tabelas delta com garantias ACID para consultas performáticas de auditoria. O Data Mesh permite que a equipe de auditoria da Saúde governando seu próprio domínio publique o "Produto de Dados: Compras de Medicamentos", enquanto a equipe de Pessoal publica o "Produto de Dados: Servidores Ativos", sendo ambos interoperados sob regras federadas globais de anonimização e segurança.

**Comparação de Arquiteturas Analíticas**

| Arquitetura | Estrutura de Dados | Abordagem de Esquema | Organização Operacional | Suporte ACID |
|---|---|---|---|---|
| **Data Warehouse** | Apenas Estruturados | Schema-on-Write | Centralizada / Monolítica | Sim (Nativo) |
| **Data Lake** | Todos os Tipos | Schema-on-Read | Centralizada / Monolítica | Não (Nativo) |
| **Lakehouse** | Todos os Tipos | Híbrido | Centralizada / Monolítica | Sim (Via Camada de Armazenamento) |
| **Data Mesh** | Heterogêneos por Domínio | Descentralizado | Descentralizada por Domínios | Depende da implementação |

**Pegadinhas Típicas da CEBRASPE**
- Representar o Data Mesh como uma ferramenta de software ou uma plataforma tecnológica comprável. O Data Mesh é um paradigma organizacional e de arquitetura sociotécnica.
- Sugerir que o Data Mesh dispensa a existência de governança e padrões de dados devido à descentralização. O Data Mesh exige rigorosamente o pilar de Governança Federada com automação computacional (*governance as code*) para impedir a criação de ilhas isoladas de informação.

---

### 2.1 SQL e Consultas Analíticas: DDL, DML, DCL, TCL, Junções, CTEs e Funções de Janela

**Definição**
Linguagem declarativa padrão para definição, manipulação, controle e consulta analítica avançada sobre dados estruturados mantidos em bancos relacionais e motores distribuídos.

**Para que Serve**
Permite aos auditores extrair dados, realizar junções entre tabelas heterogêneas, aplicar filtros condicionais, construir tabelas temporárias legíveis e aplicar funções analíticas avançadas sem colapsar a estrutura de linhas do conjunto de dados.

**Como Funciona**
- **Divisão Funcional:** DDL (`CREATE`, `ALTER`, `DROP`), DML (`SELECT`, `INSERT`, `UPDATE`, `DELETE`), DCL (`GRANT`, `REVOKE`) e TCL (`COMMIT`, `ROLLBACK`, `SAVEPOINT`).
- **Expressões de Tabela Comuns (CTEs):** Construídas via cláusula `WITH`, criam estruturas temporárias nomeadas que simplificam subconsultas complexas, melhoram a legibilidade do código e viabilizam processamentos recursivos (ex.: navegação em hierarquias organizacionais).
- **Funções de Janela (*Window Functions*):** Computam valores sobre um conjunto de linhas (janela) correlacionadas à linha corrente, preservando a identidade e o número de linhas do resultado original. Utilizam a sintaxe `OVER (PARTITION BY ... ORDER BY ... window_frame)`.
  - `ROW_NUMBER()`: Gera uma sequência inteira e estritamente única de linhas (1, 2, 3, 4...).
  - `RANK()`: Atribui posições ordinais considerando empates, gerando lacunas (*gaps*) nas posições subsequentes (ex.: 1, 2, 2, 4...).
  - `DENSE_RANK()`: Atribui posições ordinais em empates, mantendo a sequência contínua sem deixar lacunas (ex.: 1, 2, 2, 3...).
  - `LAG(coluna, offset)` e `LEAD(coluna, offset)`: Acessam valores de linhas anteriores ou posteriores dentro da partição sem a necessidade de realizar autojunção (*self-join*).

**Exemplo Aplicado ao Setor Público (CGU)**
Uso da função `LAG()` combinada com CTE para identificar pagamentos consecutivos efetuados ao mesmo fornecedor por uma prefeitura em intervalo inferior a 24 horas, sinalizando indícios de fracionamento indevido de despesa para burlar o limite de dispensa de licitação.

**Comparação de Funções de Janela Ordinais**

| Função | Resultado para Empates | Próxima Numeração Pós-Empate Duplo |
|---|---|---|
| `ROW_NUMBER()` | Atribuição distinta arbitrária | Incrementa sequencialmente (+1) |
| `RANK()` | Atribui a mesma ordem aos empatados | Deixa lacuna (ex.: pula de 2 para 4) |
| `DENSE_RANK()` | Atribui a mesma ordem aos empatados | Mantém continuidade (ex.: passa de 2 para 3) |

**Pegadinhas Típicas da CEBRASPE**
- Afirmar que as Funções de Janela reduzem o número de linhas devolvidas pela consulta da mesma forma que a instrução `GROUP BY`. As funções de janela mantêm todas as linhas originais do conjunto de dados.
- Trocar o comportamento de `RANK()` e `DENSE_RANK()`, afirmando que `DENSE_RANK()` gera lacunas na numeração após a ocorrência de valores empatados.

---

### 2.2 Desempenho e Otimização em SQL: Índices, Planos de Execução, Tristate Logic e Duplicações

**Definição**
Conjunto de fundamentos operacionais e semânticos que regem a velocidade de execução de consultas e a exatidão da interpretação de dados ausentes e duplicados pelo otimizador do banco de dados.

**Para que Serve**
Assegura a execução eficiente de consultas sobre bases públicas com bilhões de linhas, evitando o consumo excessivo de memória RAM e recursos de Entrada/Saída (E/S).

**Como Funciona**
- **Índices:** Estruturas de acesso rápido. O índice B-Tree é o padrão para buscas pontuais, ordenação e faixas de valores; o índice Hash serve estritamente para igualdades exatas; índices GIN/GiST atendem a dados estruturados em JSON, array ou coordenadas geográficas.
- **Planos de Execução e Junções Físicas:** O otimizador baseado em custo (CBO) decide os algoritmos de acesso e junção:
  - *Nested Loop Join*: Indicado quando uma das tabelas é muito pequena e a outra possui índice na chave de junção.
  - *Hash Join*: Escolhido para tabelas grandes sem índices, construindo uma tabela hash na memória com a menor relação.
  - *Merge Join (Sort-Merge)*: Exige que ambas as entradas estejam previamente ordenadas pela chave de junção, sendo altamente eficiente para grandes volumes.
- **Lógica Tri-Valorada (*Tristate Logic*):** Comparações com o valor `NULL` resultam em `UNKNOWN` (Desconhecido). A avaliação de `NULL = NULL` ou `NULL <> NULL` produz `UNKNOWN`. Na cláusula `WHERE`, apenas registros com avaliação estritamente `TRUE` são retornados.
- **Subconsultas com `NOT IN` e Nulos:** A instrução `WHERE coluna NOT IN (SELECT sub_coluna FROM tabela_b)` retornará zero linhas se a subconsulta contiver pelo menos um único valor `NULL`, devido à resolução lógica de `AND UNKNOWN`.
- **Contagem e Agregação:** `COUNT(*)` computa o número total de linhas da tabela. `COUNT(coluna)` computa apenas as linhas em que a referida coluna seja diferente de `NULL`.

**Exemplo Aplicado ao Setor Público (CGU)**
Na verificação do cadastro de servidores federais, se um auditor consultar `SELECT COUNT(cpf) FROM servidores`, a contagem ignorará os registros com CPF nulo. Para mensurar a totalidade exata de registros na base, exige-se o uso de `COUNT(*)`.

**Pegadinhas Típicas da CEBRASPE**
- A CEBRASPE afirma que a criação irrestrita de índices melhora o desempenho global do banco de dados. Isso é falso: embora acelere consultas de leitura (`SELECT`), a manutenção dos índices penaliza o desempenho de escrita (`INSERT`, `UPDATE`, `DELETE`).
- Afirmar que a expressão `WHERE campo NOT IN (1, 2, NULL)` é equivalente a `WHERE campo <> 1 AND campo <> 2`. O resultado da primeira é sempre vazio caso nenhum valor seja `TRUE`, enquanto a segunda opera normalmente sobre os valores declarados.

---

### 3.1 Ingestão e Integração de Dados: ETL vs ELT, Batch, Streaming, Contratos e Formatos

**Definição**
Processos, arquiteturas e especificações destinadas à extração, movimentação, harmonização e validação da consistência de dados oriundos de fontes heterogêneas.

**Para que Serve**
Garante o fluxo automatizado e contínuo de dados administrativos entre os sistemas de origem nos órgãos governamentais e os repositórios analíticos de controle.

**Como Funciona**
- **ETL vs ELT:** No ETL, a transformação dos dados ocorre em uma área intermediária (*Staging Area*) em servidor dedicado antes da carga no destino. No ELT, os dados brutos são carregados diretamente no repositório final de destino (ex.: Lakehouse), que utiliza seu próprio poder computacional de grande escala para efetuar as transformações.
- **Processamento Batch vs Streaming:** Batch efetua a carga de volumes acumulados em intervalos definidos (ex.: processamento diário). Streaming efetua o processamento contínuo registro a registro com baixíssima latência (ex.: Apache Kafka, Apache Flink).
- **Estratégias de Carga:** Carga Completa (*Full Load*) sobrescreve todo o repositório destino; Carga Incremental identifica e move apenas os registros novos ou modificados a partir da última execução (via marcas de tempo ou *Change Data Capture* - CDC).
- **Contratos de Dados (*Data Contracts*):** Acordos formais, versionados e computacionalmente verificáveis estabelecidos entre produtores e consumidores de dados, definindo esquemas, regras de qualidade, semântica e SLAs.
- **Formatos de Arquivo:**
  - *CSV / JSON / XML*: Formatos textuais orientados à linha. Verbosos, de leitura lenta e sem suporte nativo a metadados de otimização analítica.
  - *Apache Parquet*: Formato colunar binário e compactado. Armazena metadados avançados por grupo de linhas (*row groups*), suportando *predicate pushdown* e *column pruning*.
- **Idempotência e Repetição de Processamento:** Garantia de que a execução repetida do mesmo pipeline de ingestão produza o mesmo estado final no banco de dados, sem duplicar dados.

**Exemplo Aplicado ao Setor Público (CGU)**
Ingestão contínua em formato Parquet das emissões de Notas Fiscais Eletrônicas da Receita Federal para o Data Lakehouse da CGU via pipeline ELT incremental idempotente.

**Comparação de Formatos e Abordagens de Ingestão**

| Característica | Formato CSV / JSON | Formato Apache Parquet |
|---|---|---|
| **Organização Física** | Orientado a Linha (Texto) | Orientado a Coluna (Binário) |
| **Suporte Analytic OLAP** | Baixo (Leitura total do arquivo) | Altíssimo (Column Pruning) |
| **Eficiência de Compressão** | Baixa | Elevada |
| **Leitura por Motores SQL** | Requer parsing textual dispendioso | Leitura vetorial direta com Pushdown |

**Pegadinhas Típicas da CEBRASPE**
- Tentar induzir o candidato ao erro afirmando que a abordagem ELT descarta a fase de transformação. A fase de transformação continua sendo realizada; apenas o momento e o ambiente computacional de execução foram alterados.
- Afirmar que os pipelines de ingestão orientados a evento (*streaming*) garantem atomicidade e consistência estrita sem a necessidade de implementar padrões de idempotência ou tratamento de mensagens duplicadas.

---

### 4.1 a 4.4 Processamento Distribuído: Particionamento, Paralelismo, Movimentação e Data Skew

**Definição**
Técnicas de arquitetura de software distribuído (ex.: Apache Spark) que dividem a carga de computação e armazenamento de grandes volumes de dados (*Big Data*) entre múltiplos nós trabalhando em paralelo num aglomerado (*cluster*).

**Para que Serve**
Supera as limitações físicas de memória RAM e processamento de computadores individuais, viabilizando o cruzamento massivo de tabelas governamentais em tempo hábil.

**Como Funciona**
- **Particionamento e Paralelismo:** Os dados são divididos em blocos lógicos chamados partições. O nó mestre (*Driver*) distribui tarefas (*tasks*) executadas simultaneamente pelos nós trabalhadores (*Executors*) sobre cada partição.
- **Movimentação de Dados (*Shuffle*):** Ocorre quando o sistema precisa reorganizar os dados entre diferentes nós da rede para satisfazer operações globais como `JOIN`, `GROUP BY` ou `DISTINCT`. É a operação mais custosa em termos de tráfego de rede e E/S.
- **Broadcast Join (*Map-Side Join*):** Técnica de otimização em que a menor tabela do cruzamento é copiada integralmente para a memória RAM de todos os nós executores, eliminando totalmente a necessidade de realizar o *shuffle* da tabela grande.
- **Escalabilidade e Resiliência:** Escalabilidade Horizontal (*scale-out*) adiciona novos nós ao cluster. A tolerância a falhas no Apache Spark se baseia no Grafo Acíclico Dirigido (DAG) e na linhagem das transformações: se um nó falha, o sistema recomputa apenas as partições perdidas a partir do histórico de transformações.
- **Assimetria de Dados (*Data Skew*):** Ocorre quando a chave de particionamento distribui o volume de registros de forma desproporcional entre os nós do aglomerado. Um ou poucos nós sobram com um volume desmesuradamente maior de trabalho (*stragglers*), gerando estouro de memória (*Out Of Memory* - OOM) e paralisando a finalização da consulta.

**Exemplo Aplicado ao Setor Público (CGU)**
Durante a auditoria das folhas de pagamento dos municípios, ao realizar a junção da base de servidores com a base do Cadastro Único utilizando o CPF como chave, a presença de milhões de registros com o CPF zerado (`00000000000`) faz com que o Spark envie todas essas linhas para um único nó por hash, causando uma paralisia no processamento decorrente de *data skew*.

**Comparação de Funções de Redimensionamento em Spark**

| Função | Envolve Shuffle de Rede? | Uso Indicado |
|---|---|---|
| `coalesce(n)` | Não (Combina partições no mesmo nó) | Apenas para REDUZIR a quantidade de partições |
| `repartition(n)` | Sim (Redistribuição total por Hash) | Para AUMENTAR partições ou eliminar Data Skew |

**Pegadinhas Típicas da CEBRASPE**
- Afirmar que o comando `coalesce()` no Spark deve ser aplicado para resolver o problema de assimetria de dados (*Data Skew*) aumentando o número de partições. O `coalesce()` não realiza *shuffle* e serve exclusivamente para diminuir partições; a redistribuição equilibrada exige o uso de `repartition()` ou adição de *salting* (sufixo aleatório à chave).
- Confundir a tolerância a falhas de um cluster de Big Data com a replicação física total e contínua do estado dos nós trabalhadores.

---

### 5.1 a 5.5 Qualidade, Rastreabilidade e Conciliação de Dados

**Definição**
Práticas, frameworks, padrões de validação e técnicas estatísticas aplicadas para mensurar, monitorar, unificar e garantir a acurácia, confiabilidade e rastreabilidade da informação analítica.

**Para que Serve**
Assegura que as análises de auditoria e os relatórios de irregularidades produzidos pela CGU estejam fundamentados em dados corretos, incontestáveis e devidamente auditáveis.

**Como Funciona**
- **Metadados, Catálogo e Linhagem (*Data Lineage*):** O catálogo indexa os metadados organizacionais e técnicos. A linhagem rastreia o histórico completo do dado, registrando sua origem, todas as transformações sofridas nos pipelines e as tabelas finais consumidas.
- **Dimensões da Qualidade de Dados:**
  - *Completude*: Medida da ausência de valores ausentes ou nulos em campos obrigatórios.
  - *Consistência*: Ausência de contradições lógicas em dados armazenados em diferentes bases.
  - *Validade*: Conformidade com regras de formato, tipo, sintaxe ou domínios previstos.
  - *Unicidade*: Ausência de duplicidades indesejadas para a mesma entidade real.
  - *Acurácia*: Grau de conformidade entre o dado registrado e o valor real do evento no mundo físico.
  - *Atualidade (Timeliness)*: Tempestividade do dado em relação ao momento da ocorrência do fato.
- **Record Linkage (Vinculação de Registros):**
  - *Determinístico*: Vincula registros por meio da igualdade exata de uma chave primária compartilhada (ex.: CPF).
  - *Probabilístico (Método Fellegi-Sunter)*: Avalia pares de registros através da comparação de múltiplos atributos incompletos ou com erros de digitação (nome, data de nascimento, endereço). Calcula matrizes de probabilidade ($m$-probabilities e $u$-probabilities) resultando num peso logarítmico de evidência de correspondência (*match*).
- **Riscos de Correspondência:** Falsos Positivos (vincular pessoas distintas como se fossem a mesma) causam séria injustiça administrativa e imputações indevidas. Falsos Negativos (deixar de vincular registros da mesma pessoa) ocultam fraudes e acúmulos ilícitos de cargos públicos.

**Exemplo Aplicado ao Setor Público (CGU)**
Aplicação do *Record Linkage* Probabilístico via algoritmo de Fellegi-Sunter para unificar os cadastros de beneficiários de programas sociais federais com folhas de pagamento estaduais e municipais, identificando fraudes mesmo quando o nome do beneficiário foi grafado com pequenos erros de digitação nas bases municipais.

**Comparação de Métodos de Record Linkage**

| Critério | Linkage Determinístico | Linkage Probabilístico (Fellegi-Sunter) |
|---|---|---|
| **Requisito de Chave** | Chave única perfeita exata (ex.: CPF) | Múltiplos atributos parciais / imperfeitos |
| **Sensibilidade a Grafia** | Nula (Qualquer divergência falha) | Alta (Métricas como Jaro-Winkler, Levenshtein) |
| **Custo Computacional** | Baixo ($O(N)$ com índices) | Elevado ($O(N \times M)$, exige técnicas de blocking) |
| **Risco Principal** | Elevado índice de Falsos Negativos | Risco de Falsos Positivos em limiares baixos |

**Pegadinhas Típicas da CEBRASPE**
- Confundir Completude com Acurácia. Um atributo pode estar 100% preenchido (máxima completude), porém contendo informações totalmente falsas ou errôneas (baixa acurácia).
- Afirmar que a unificação de bases de dados populacionais por meio de técnicas probabilísticas independe de estratégias de blocagem (*blocking*). Sem o *blocking*, o custo computacional de comparar todos os registros com todos os outros inviabiliza o processamento em bases governamentais massivas.

---

### 6.1 a 6.5 Compartilhamento, Proteção de Dados e LGPD

**Definição**
Conjunto de salvaguardas técnicas, administrativas, legais e arquiteturais destinadas a gerenciar o ciclo de vida dos dados, assegurando a privacidade dos titulares nos termos da Lei Geral de Proteção de Dados Pessoais (LGPD - Lei nº 13.709/2018).

**Para que Serve**
Permite o cumprimento dos mandamentos institucionais de transparência e controle social (Lei de Acesso à Informação - LAI) sem violar as garantias fundamentais de privacidade e proteção aos dados pessoais dos cidadãos.

**Como Funciona**
- **Minimização e Princípio do Menor Privilégio:** O tratamento de dados deve se limitar ao mínimo necessário para atingir as finalidades públicas legítimas. O acesso é estritamente controlado por políticas de privilégios baseadas em papéis (*Role-Based Access Control* - RBAC).
- **Segregação de Ambientes:** Separação física e lógica entre os ambientes de Desenvolvimento, Homologação e Produção. O uso de dados pessoais de produção em ambientes de desenvolvimento ou teste é vedado, exigindo técnica de mascaramento ou dados sintéticos.
- **Retenção e Descarte:** Dados pessoais devem ser eliminados após o término de seu tratamento, autorizada a conservação apenas para hipóteses legais como o cumprimento de obrigação legal/regulatória ou estudo por órgão de pesquisa.
- **Anonimização vs Pseudonimização:**
  - *Anonimização*: Processo irreversível que utiliza meios técnicos razoáveis e disponíveis na ocasião, pelo qual o dado perde a possibilidade de associação direta ou indireta a um indivíduo. O dado anonimizado **NÃO É CONSIDERADO DADO PESSOAL** nos termos da LGPD (Art. 12).
  - *Pseudonimização*: Processo no qual o dado perde a possibilidade de associação direta a um indivíduo senão pelo uso de informação adicional, mantida separadamente em ambiente seguro. O dado pseudonimizado **CONTINUA SENDO DADO PESSOAL** e permanece submetido às regras e sanções da LGPD.
- **Equilíbrio Transparência vs Privacidade:** A abertura de bases públicas deve ser efetuada mediante aplicação de técnicas de anonimização (como $k$-anonimato ou privacidade diferencial), assegurando a utilidade analítica dos dados abertos sem permitir a reidentificação dos indivíduos.

**Exemplo Aplicado ao Setor Público (CGU)**
Ao publicar microdados no Portal da Transparência referentes ao recebimento de auxílios assistenciais por cidadãos em situação de vulnerabilidade, a CGU aplica técnicas de anonimização para ocultar atributos identificadores indiretos que permitam a reidentificação dos beneficiários na comunidade local.

**Comparação na LGPD: Anonimização vs Pseudonimização**

| Característica | Anonimização (Art. 5º, XI / Art. 12) | Pseudonimização (Art. 5º, XI) |
|---|---|---|
| **Reversibilidade** | Irreversível (por meios razoáveis) | Reversível (com chave/informação adicional) |
| **Status Perante a LGPD** | NÃO é dado pessoal | É DADO PESSOAL |
| **Aplicação da Lei** | Isento da LGPD (salvo se reidentificado) | Integralmente submetido às regras da LGPD |
| **Guarda da Informação** | Destruição permanente de vínculos | Separação física da chave de associação |

**Pegadinhas Típicas da CEBRASPE**
- Assertivas afirmando que a pseudonimização é equiparada à anonimização pela LGPD e desobriga o órgão público de aplicar as medidas de proteção previstas na lei. A pseudonimização é apenas uma medida de segurança; o dado continua sendo considerado dado pessoal.
- Afirmar que o direito de acesso à informação pública (LAI) autoriza a divulgação ampla e irrestrita de dados pessoais sensíveis mantidos por órgãos públicos. Exige-se o correto sopesamento de direitos e a devida proteção de privacidade.

---

## 2. Flashcards

- Qual é a garantia central fornecida pelos bancos de dados relacionais OLTP? :: Garantir o cumprimento estrito das propriedades ACID (Atomicidade, Consistência, Isolamento e Durabilidade) nas transações.
- Em qual forma normal são eliminadas as dependências funcionais transitivas em um modelo relacional? :: Na 3ª Forma Normal (3FN).
- O que diferencia o modelo NoSQL Chave-Valor dos demais modelos NoSQL? :: O armazenamento simples de pares identificador-conteúdo otimizado para leituras e escritas de altíssima velocidade em memória.
- Qual é a diferença de normalização entre os esquemas Star Schema e Snowflake Schema no modelo multidimensional? :: O Star Schema mantém suas tabelas dimensão desnormalizadas, enquanto o Snowflake Schema aplica a normalização às tabelas dimensão.
- Para qual finalidade principal são utilizados os bancos de dados vetoriais? :: Para armazenamento de vetores densos (embeddings) e realização de buscas semânticas por similaridade estatística em aplicações de IA.
- Qual é a abordagem de esquema adotada nativamente pelos repositórios do tipo Data Lake? :: Abordagem Schema-on-Read.
- Qual é a definição essencial da arquitetura Data Lakehouse? :: Camada que adiciona transações ACID, versionamento e governança sobre dados armazenados em Data Lakes de baixo custo.
- Quais são os quatro pilares fundamentais da arquitetura Data Mesh? :: Responsabilidade por domínios, dados como produtos, plataforma de infraestrutura de autosserviço e governança federada.
- Quais instruções SQL pertencem à linguagem de controle de dados (DCL)? :: `GRANT` e `REVOKE`.
- Como a função `RANK()` trata valores empatados em uma consulta SQL analítica? :: Atribui o mesmo valor ordinal aos empatados e pula as posições ordinais subsequentes gerando lacunas.
- Como a função `DENSE_RANK()` trata valores empatados em uma consulta SQL analítica? :: Atribui o mesmo valor ordinal aos empatados e mantém a numeração contínua sem deixar lacunas.
- Qual a finalidade das funções analíticas de janela `LAG()` e `LEAD()` em SQL? :: Acessar valores de linhas anteriores ou posteriores dentro da janela de partição sem realizar auto-junção.
- Qual cláusula SQL deve ser obrigatoriamente utilizada para filtrar resultados de funções agregadas pós agrupamento? :: A cláusula `HAVING`.
- Qual é o resultado da avaliação lógica da expressão `NULL = NULL` em SQL? :: `UNKNOWN` (Desconhecido), em decorrência da lógica tri-valorada.
- O que acontece ao executar `WHERE coluna NOT IN (SELECT sub_coluna FROM tabela)` se a subconsulta contiver um valor `NULL`? :: A consulta inteira não retornará nenhuma linha.
- Qual a diferença entre a execução de `COUNT(*)` e `COUNT(coluna)` em SQL? :: `COUNT(*)` conta todas as linhas da tabela, enquanto `COUNT(coluna)` descarta linhas contendo valor nulo na coluna.
- Em que consiste o algoritmo de junção física Hash Join em motores analíticos SQL? :: Algoritmo que constrói uma tabela hash na memória com a menor relação para realizar o cruzamento rápido com a maior relação.
- Qual a diferença estrutural entre as abordagens ETL e ELT? :: No ETL as transformações ocorrem em servidor intermediário antes da carga; no ELT os dados são carregados brutos e transformados no destino.
- Por que o formato Apache Parquet é recomendado para workloads analíticos OLAP? :: Porque é colunar, altamente compactado e suporta predicate pushdown e column pruning.
- O que é um Contrato de Dados (Data Contract) em engenharia de dados? :: Um acordo formal e automatizado de validação do esquema, semântica e qualidade dos dados entre produtores e consumidores.
- O que define o conceito de Idempotência em pipelines de ingestão de dados? :: A capacidade de executar o pipeline repetidas vezes produzindo exatamente o mesmo estado final no repositório.
- O que significa a ocorrência de Shuffle em um framework de processamento distribuído como o Spark? :: Significa a movimentação física de dados entre diferentes nós da rede para reorganização global.
- Como o Broadcast Join otimiza cruzamentos em processamento distribuído? :: Copia integralmente a tabela menor para a memória de todos os nós executores, eliminando o shuffle da tabela grande.
- O que caracteriza o fenômeno de Data Skew em um aglomerado de processamento distribuído? :: A distribuição desproporcional de dados entre as partições do cluster, sobrecarregando nós executores específicos.
- Qual a diferença de comportamento entre `coalesce()` e `repartition()` no Apache Spark? :: `coalesce()` reduz partições fundindo-as localmente sem shuffle; `repartition()` executa shuffle completo podendo aumentar ou diminuir partições.
- O que é o histórico de linhagem de dados (Data Lineage) na governança de dados? :: Mapeamento auditável que rastreia todo o fluxo do dado desde sua origem até a camada final de consumo.
- Como a dimensão de "Completude" difere da dimensão de "Acurácia" na qualidade de dados? :: Completude mede a presença física do dado (ausência de nulos); acurácia mede se o dado cadastrado retrata o fato real.
- O que caracteriza o modelo de Fellegi-Sunter no contexto de Record Linkage? :: Abordagem probabilística que utiliza pesos de concordância/discordância sobre atributos parciais para unir registros.
- Qual a função da estratégia de blocagem (blocking) na vinculação probabilística de registros? :: Reduzir o número de comparações de pares dividindo a base em blocos contendo atributos em comum.
- Como a LGPD trata juridicamente os dados anonimizados em seu Artigo 12? :: Os dados anonimizados não são considerados dados pessoais, ficando fora do escopo da LGPD salvo se reidentificados.
- Por que a pseudonimização não retira a incidência da LGPD sobre uma base de dados? :: Porque a pseudonimização é reversível com o uso de informação adicional, mantendo o status de dado pessoal.
- O que diz o Princípio da Minimização no tratamento de dados pessoais? :: Exige que o tratamento seja limitado ao estritamente necessário para o cumprimento das finalidades públicas informadas.

---

## 3. Questões Inéditas no Estilo CEBRASPE (Certo/Errado)

### Bloco 1 — Modelagem e Arquitetura de Dados

**01.** O modelo de dados relacional atende primordialmente às necessidades de processamento de transações analíticas de grande porte (OLAP), uma vez que a rigorosa normalização das tabelas até a 3ª Forma Normal elimina as despesas de computação de junções em consultas analíticas complexas.
- **Gabarito:** ERRADO
- **Justificativa:** O modelo relacional altamente normalizado atende primordialmente ao processamento transacional operacional (OLTP). Na verdade, o excesso de normalização aumenta o custo computacional de junções (JOINs) em consultas analíticas de grande volume (OLAP). Por este motivo, ambientes analíticos utilizam modelagem multidimensional desnormalizada (como o Star Schema) ou bancos de dados orientados a colunas.

**02.** O Data Lakehouse combina recursos característicos do Data Lake, como o armazenamento em formatos abertos e de baixo custo, com garantias transacionais ACID, controle de versionamento e suporte a indexações típicas do Data Warehouse.
- **Gabarito:** CERTO
- **Justificativa:** A assertiva define corretamente o conceito de Lakehouse, que sobrepõe uma camada de gerenciamento aberto (ex.: Delta Lake ou Apache Iceberg) ao Data Lake para garantir transações ACID e alto desempenho OLAP sem exigir o confinamento dos dados em bancos proprietários.

**03.** No paradigma Data Mesh, a descentralização do armazenamento e o protagonismo atribuído às equipes de domínio eliminam a necessidade de implementação de diretrizes e padrões de governança global de dados.
- **Gabarito:** ERRADO
- **Justificativa:** O Data Mesh apoia-se compulsoriamente no pilar de Governança Federada Computacional. A descentralização por domínios exige regras globais automatizadas de interoperabilidade, segurança, qualidade e privacidade; a ausência de governança global converteria a arquitetura em silos ilegíveis de informação.

### Bloco 2 — SQL e Consultas Analíticas

**04.** Ao contrário da instrução `GROUP BY`, que agrega as linhas resultantes alterando a granularidade do conjunto de dados, as Funções de Janela (*Window Functions*) executam seus cálculos analíticos preservando o número total de linhas da consulta original.
- **Gabarito:** CERTO
- **Justificativa:** Esta é a característica distintiva central das funções de janela em SQL. Enquanto o `GROUP BY` colapsa as linhas agrupadas em uma única linha explicativa por grupo, as funções de janela atribuem o valor calculado a cada uma das linhas originais da partição mantendo a granularidade intacta.

**05.** Em consultas analíticas SQL, a aplicação das funções de janela `RANK()` e `DENSE_RANK()` resulta no mesmo arranjo numérico ordinal quando o conjunto de dados processado não apresenta registros com valores empatados.
- **Gabarito:** CERTO
- **Justificativa:** Na ausência de empates, ambas as funções geram uma sequência estritamente contínua e sequencial (1, 2, 3, 4...). A divergência comportamental ocorre apenas em situações de empate, nas quais `RANK()` pula as numerações subsequentes e `DENSE_RANK()` mantém a sequência sem deixar lacunas.

**06.** No padrão SQL, uma consulta contendo a cláusula `WHERE campo NOT IN (SELECT sub_campo FROM tabela_b)` resultará na avaliação correta dos registros da tabela principal mesmo que a subconsulta retorne registros contendo o valor `NULL`.
- **Gabarito:** ERRADO
- **Justificativa:** De acordo com a Lógica Tri-Valorada (*Tristate Logic*), a presença de um único valor `NULL` no conjunto retornado pelo `NOT IN` faz com que todas as comparações de igualdade/diferença sejam convertidas em `UNKNOWN`. Como a cláusula `WHERE` exige obrigatoriamente um resultado `TRUE` para filtrar os dados, a consulta falhará em retornar qualquer linha.

### Bloco 3 — Ingestão e Integração de Dados

**07.** A arquitetura de integração baseada em ELT (*Extract, Load, Transform*) diferencia-se do modelo ETL tradicional por eliminar o processamento de transformação de dados, uma vez que a carga dos dados brutos é efetuada diretamente no repositório final de destino.
- **Gabarito:** ERRADO
- **Justificativa:** A abordagem ELT não elimina o processo de transformação de dados. O processo de transformação continua sendo fundamental; contudo, a sua execução é transferida para o ambiente interno do motor analítico do destino (ex.: Data Warehouse em nuvem ou Lakehouse), aproveitando seu imenso poder de processamento distribuído após o carregamento dos dados brutos.

**08.** O formato de arquivo Apache Parquet favorece o processamento de consultas analíticas OLAP devido à sua estrutura binária orientada a colunas, que possibilita a aplicação de técnicas de *column pruning* e *predicate pushdown*.
- **Gabarito:** CERTO
- **Justificativa:** O formato Parquet lê estritamente as colunas solicitadas pela consulta (*column pruning*) e consulta os metadados internos para ignorar a leitura de grupos de linhas que não atendem aos filtros da consulta (*predicate pushdown*), otimizando radicalmente a E/S de disco e o desempenho.

### Bloco 4 — Processamento Distribuído

**09.** No processamento distribuído executado pelo Apache Spark, o problema de *Data Skew* refere-se à alocação desproporcional de dados entre as partições físicas do cluster, o que pode sobrecarregar tarefas específicas e provocar falhas do tipo *Out Of Memory*.
- **Gabarito:** CERTO
- **Justificativa:** O *Data Skew* (assimetria) é o principal problema de desempenho em clusters distribuídos. Quando os dados são distribuídos por uma chave muito concentrada (ex.: nulos), uma partição acumula grande volume de registros, tornando seu nó executor um gargalo (*straggler*) suscetível a erros de estouro de memória.

**10.** Em uma aplicação Spark, a chamada do método `coalesce(n)` em um DataFrame deve ser preferida ao uso de `repartition(n)` quando o objetivo for aumentar o número de partições para redistribuir dados assimétricos por meio de um *full shuffle*.
- **Gabarito:** ERRADO
- **Justificativa:** O método `coalesce()` não realiza *shuffle* de rede e destina-se exclusivamente à redução do número de partições através da fusão de partições locais no mesmo nó. Para aumentar o número de partições ou forçar uma redistribuição total por *shuffle* visando eliminar a assimetria, o método obrigatório é o `repartition()`.

### Bloco 5 — Qualidade e Rastreabilidade de Dados

**11.** No método de vinculação probabilística de registros de Fellegi e Sunter, a ocorrência de concordância em um atributo populacional muito raro confere um peso de evidência superior para a confirmação do vínculo do que a concordância em um atributo bastante frequente.
- **Gabarito:** CERTO
- **Justificativa:** O algoritmo de Fellegi-Sunter calcula os pesos de concordância logarítmica de forma inversamente proporcional à frequência daquele atributo na população total. A coincidência em um atributo raro (ex.: um sobrenome muito atípico) apresenta poder discriminatório superior ao de uma coincidência em um atributo muito comum (ex.: o sobrenome "Silva").

**12.** A dimensão da qualidade de dados referente à completude assegura que os registros cadastrados estejam em estrita conformidade com a realidade do mundo real, dispensando auditorias adicionais de acurácia.
- **Gabarito:** ERRADO
- **Justificativa:** A assertiva confunde Completude com Acurácia. A completude atesta apenas a ausência de dados nulos/ausentes (ou seja, o campo foi preenchido). A acurácia é a propriedade que atesta se o valor preenchido retrata fielmente o fato real. Um campo "Data de Nascimento" pode estar 100% completo, mas conter datas fictícias, falhando no teste de acurácia.

### Bloco 6 — Compartilhamento e Proteção de Dados (LGPD)

**13.** Segundo o que dispõe a Lei Geral de Proteção de Dados Pessoais (LGPD - Lei nº 13.709/2018), o dado pessoal submetido à técnica de pseudonimização deixa de ser categorizado como dado pessoal, ficando desvinculado dos direitos dos titulares e das obrigações legais impostas ao controlador.
- **Gabarito:** ERRADO
- **Justificativa:** Segundo o Art. 5º da LGPD, o dado pseudonimizado CONTINUA SENDO DADO PESSOAL, haja vista que a associação ao indivíduo pode ser reconstruída mediante o uso de informação adicional mantida separadamente pelo controlador. Apenas o dado submetido a processo irreversível de anonimização (Art. 12) deixa de ser considerado dado pessoal sob a lei.

**14.** A segregação rígida de ambientes computacionais impede a utilização direta de dados pessoais reais mantidos em bases de produção durante a fase de testes e desenvolvimento de novas ferramentas de auditoria.
- **Gabarito:** CERTO
- **Justificativa:** O princípio da privacidade por padrão (*Privacy by Default*) e as diretrizes de governança exigem a segregação absoluta entre ambientes de Produção, Homologação e Desenvolvimento. Para alimentar ambientes de teste, os dados de produção devem passar obrigatoriamente por mascaramento, anonimização ou geração de dados sintéticos.

---

## 4. Glossário Técnico

- **ACID:** Conjunto de propriedades transacionais (Atomicidade, Consistência, Isolamento, Durabilidade) que garante a confiabilidade absoluta em bancos de dados relacionais.
- **Anonimização:** Processo técnico irreversível no qual o dado perde a capacidade de associação direta ou indireta a um indivíduo, desvinculando-o da LGPD.
- **Acurácia:** Dimensão de qualidade que estabelece o grau de conformidade entre o dado armazenado e o evento factual do mundo real.
- **BASE:** Filosofia de consistência eventual adotada por bancos NoSQL em oposição ao rigor do modelo ACID.
- **Broadcast Join:** Técnica de otimização em clusters distribuídos que envia uma tabela pequena para a memória RAM de todos os nós executores, eliminando o shuffle da tabela grande.
- **Column Pruning:** Capacidade dos motores SQL analíticos de ler unicamente as colunas referenciadas na consulta, ignorando as colunas desnecessárias do arquivo colunar.
- **Completude:** Dimensão de qualidade que avalia a presença física de dados, medindo o percentual de ausência de valores nulos ou faltantes.
- **CTE (Common Table Expression):** Estrutura temporária de dados declarada pela cláusula `WITH` para simplificar e organizar subconsultas SQL complexas.
- **Data Contract:** Acordo formal e automatizado contendo especificações técnicas de esquema, semântica e qualidade entre produtores e consumidores de dados.
- **Data Lineage:** Mapeamento e rastreabilidade visual e auditável de todo o ciclo de vida e transformações sofridas pelo dado desde a origem até o consumo.
- **Data Mesh:** Paradigma sociotécnico descentralizado focado na governança por domínios de negócio e oferta de dados como produtos.
- **Data Skew:** Distribuição assimétrica de dados entre as partições de um aglomerado distribuído, acarretando gargalos de processamento.
- **DENSE_RANK():** Função analítica de janela SQL que atribui a mesma posição a registros empatados e prossegue a numeração sem deixar lacunas.
- **ELT:** Arquitetura de integração onde os dados brutos são extraídos e carregados diretamente no destino para posterior transformação analítica interna.
- **Embeddings:** Representações vetoriais densas de dados não estruturados geradas por modelos de inteligência artificial para busca semântica por proximidade.
- **Fellegi-Sunter:** Modelo formal estatístico de vinculação probabilística de registros baseado em matrizes de probabilidade de concordância de atributos.
- **Idempotência:** Propriedade de pipelines de dados em que execuções sucessivas com os mesmos dados produzem exatamente o mesmo resultado sem duplicidades.
- **Lakehouse:** Arquitetura híbrida que insere uma camada de suporte transacional ACID e indexação sobre arquivos de Data Lakes de baixo custo.
- **Predicate Pushdown:** Otimização na qual os filtros da consulta SQL são executados diretamente na camada de armazenamento do arquivo (ex.: Parquet), evitando leituras desnecessárias de blocos.
- **Pseudonimização:** Processo no qual o dado perde a identificação direta mas permanece como dado pessoal sujeito à LGPD por ser reidentificável mediante chave externa.
- **RANK():** Função analítica de janela SQL que atribui a mesma posição a valores empatados, gerando lacunas na numeração dos registros subsequentes.
- **Record Linkage:** Conjunto de métodos determinísticos e probabilísticos para unificar registros referentes à mesma entidade em bases heterogêneas.
- **Schema-on-Read:** Abordagem em que o esquema lógico dos dados só é aplicado no momento da leitura da consulta analítica (típico de Data Lakes).
- **Schema-on-Write:** Abordagem onde o esquema estrutural é obrigatoriamente validado antes da gravação física dos dados no banco (típico de Data Warehouses).
- **Shuffle:** Processo de transferência e reorganização de dados através das conexões de rede entre os múltiplos nós de um cluster distribuído.
- **Star Schema:** Modelo multidimensional com uma tabela fato desnormalizada central conectada a tabelas dimensão não normalizadas.
- **Tristate Logic:** Lógica tri-valorada do padrão SQL na qual a presença de nulos produz resultados computados como `TRUE`, `FALSE` ou `UNKNOWN`.

---

## 5. Mapa Mental Hierárquico

- **Engenharia, Arquitetura e Governança de Dados**
  - **1. Modelagem e Arquiteturas Analíticas**
    - 1.1 Modelagem de Dados
      - Relacional: OLTP, Garantias ACID, Normalização (1FN a BCNF), Integridade Referencial
      - NoSQL: Documental (JSON/BSON), Chave-Valor, Grafos, Teorema CAP, Garantias BASE
      - Multidimensional: OLAP, Tabelas Fato e Dimensão, Star Schema vs Snowflake Schema
      - Vetorial: Embeddings, Busca Semântica por Proximidade (HNSW, Distância de Cosseno)
    - 1.2 Padrões de Arquiteturas Analíticas
      - Data Warehouse: Schema-on-write, centralizado, dados puramente estruturados
      - Data Mart: Subconjuntos analíticos especializados por departamento
      - Data Lake: Schema-on-read, dados estruturados, semiestruturados e não estruturados
      - Data Lakehouse: Camada transacional ACID sobre Data Lake, suporte a versionamento (Time Travel)
      - Data Mesh: Paradigma sociotécnico, Domínios, Dados como Produtos, Autosserviço, Governança Federada
  - **2. SQL e Consultas Analíticas**
    - 2.1 Fundamentos e Expressões Avançadas
      - Divisão SQL: DDL, DML, DCL, TCL
      - Estruturação: CTEs (`WITH`), Agregações, Filtros (`WHERE` vs `HAVING`)
      - Funções de Janela: Sintaxe `OVER (PARTITION BY ... ORDER BY ...)`, `ROW_NUMBER()`, `RANK()` (com lacunas), `DENSE_RANK()` (sem lacunas), `LAG()` e `LEAD()`
    - 2.2 Otimização e Semântica de Execução
      - Índices: B-Tree, Hash, GIN/GiST
      - Planos de Execução: Sequential Scan, Index Scan, Nested Loop, Hash Join, Merge Join
      - Lógica Tri-Valorada (Tristate Logic): Tratamento de `NULL` (`UNKNOWN`), `NOT IN` com `NULL`, `COUNT(*)` vs `COUNT(coluna)`
  - **3. Ingestão e Integração de Dados**
    - 3.1 Paradigmas, Formatos e Padrões
      - Arquitetura: ETL (transforma fora) vs ELT (transforma no repositório final)
      - Frequência: Lote (Batch) vs Fluxo em Tempo Real (Streaming)
      - Estratégia: Carga Completa (Full Load) vs Carga Incremental (CDC)
      - Governança de Ingestão: Idempotência, Repetição de Processamento, Contratos de Dados (Data Contracts)
      - Formatos: Orientados a Linha (CSV, JSON, XML) vs Orientados a Coluna (Apache Parquet com Predicate Pushdown e Column Pruning)
  - **4. Processamento Distribuído**
    - 4.1 Execução Paralela e Arquitetura de Aglomerado
      - Conceitos: Particionamento físico, Tarefas (Tasks), Nós Executores, Movimentação de Rede (Shuffle)
      - Otimizações: Broadcast Join (Map-Side Join) para tabelas assimétricas pequenas
    - 4.2 Escalabilidade, Resiliência e Desempenho
      - Escalabilidade: Vertical (Scale-Up) vs Horizontal (Scale-Out)
      - Tolerância a Falhas: DAG (Grafo Acíclico Dirigido), Recomputação por Linhagem
      - Assimetria (Data Skew): Nó arrastado (straggler), Erros de Memória (OOM), Resolução via `repartition()` e Salting
  - **5. Qualidade, Rastreabilidade e Conciliação**
    - 5.1 Rastreabilidade e Métricas de Qualidade
      - Metadados, Catálogos Corporativos, Linhagem de Dados (Data Lineage)
      - Dimensões: Completude, Consistência, Validade, Unicidade, Acurácia, Atualidade
    - 5.2 Unificação de Entidades e Bases Administradas
      - Perfilamento, Deduplicação, Enriquecimento e Conciliação de Fontes
      - Record Linkage Determinístico: Igualdade exata por Chave Única (CPF/CNPJ)
      - Record Linkage Probabilístico: Método Fellegi-Sunter ($m$/$u$ probabilities, pesos logarítmicos, técnicas de blocking)
      - Gestão de Riscos: Falsos Positivos vs Falsos Negativos no controle público
  - **6. Compartilhamento e Proteção de Dados (LGPD)**
    - 6.1 Segurança Arquitetural e Operacional
      - Minimização de Dados, Menor Privilégio (RBAC), Segregação de Ambientes (Dev/Staging/Prod)
      - Retenção e Descarte Seguro de Informações
    - 6.2 Privacidade e Legislação (Lei nº 13.709/2018)
      - Anonimização: Irreversível, dado deixa de ser dado pessoal (Art. 12)
      - Pseudonimização: Reversível via informação adicional, dado CONTINUA sendo pessoal
      - Técnicas: $k$-anonimato, prevenção a ataques de reidentificação por linkagem
      - Conflito Normativo: Ponderação entre Transparência Pública (LAI) e Proteção à Privacidade (LGPD)
