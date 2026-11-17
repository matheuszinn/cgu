---
tipo: resumo
disciplina: "Operação, Governança e Gestão de Soluções de Dados e IA"
tema: "Bloco 4 — Operação, Governança e Gestão de Soluções de Dados e IA (Completo)"
status: novo
data: "2026-11-03"
tags: [resumo, ciencia-de-dados, cgu-2026, cargo-2]
---

# Material Estratégico de Preparação: Operação, Governança e Gestão de Soluções de Dados e IA (CGU 2026)

> [!info] MOC: [[Operação, Governança e Gestão de Soluções de Dados e IA]]
> Edital nº 1/2026 – CGU – AFFC · **Conhecimentos específicos** · Cargo 2 (TI / Ciência de Dados).

Este relatório técnico e material de estudo aprofundado foi concebido estritamente para a preparação ao cargo de Auditor Federal de Finanças e Controle (AFFC) da Controladoria-Geral da União (CGU), especialidade Ciência de Dados. O escopo abrange a intersecção entre a Ciência de Dados e o arcabouço normativo de controle público, com foco no perfil de cobrança da banca CEBRASPE (itens de Certo/Errado, alta densidade interpretativa, inversão de conceitos e exceções à regra).

A análise disseca o Bloco 4 do edital, fornecendo resumos estruturados, comparações, flashcards, questões comentadas, glossário e mapa mental, tudo fundamentado nas melhores práticas de MLOps, governança digital e na Instrução Normativa SGD/ME nº 94/2022.

---

## 1. Ciclo de Vida e MLOps

O desenvolvimento de modelos de Machine Learning (ML) transita de ambientes isolados de pesquisa para sistemas de produção contínua através das práticas de MLOps. Esta disciplina estende o paradigma de DevOps, incorporando a complexidade inerente aos dados, que são mutáveis e determinam o comportamento do software.

### 1.1 a 1.6: Resumo Estruturado e Aprofundamento

**Definição e Funcionalidade:**
O ciclo de vida em MLOps engloba a ingestão e preparação de dados, treinamento, validação, implantação (*deploy*) e monitoramento. Diferentemente do software tradicional, onde o código é o único artefato versionado, em IA exige-se o versionamento tridimensional: **código** (via Git), **dados** (via DVC - *Data Version Control* ou LakeFS) e **modelos** (via *Model Registries* como MLflow). O registro de experimentos é a prática de catalogar hiperparâmetros, métricas de desempenho (ex.: F1-Score, AUC-ROC) e metadados de cada execução, permitindo rastrear exatamente qual combinação gerou o melhor resultado.

A **reprodutibilidade** é a garantia de que um experimento, ao ser reexecutado com os mesmos dados e código, produzirá o mesmo modelo. Isso é assegurado por meio de contêineres (Docker) que fixam as dependências e o ambiente de execução.

Os pipelines automatizados dividem-se em CI/CD/CT:
- **Integração Contínua (CI):** Testa não apenas o código, mas valida a qualidade e o esquema dos dados entrantes (utilizando ferramentas como *Great Expectations*).
- **Entrega Contínua (CD):** Empacota o modelo validado e o disponibiliza via APIs (arquiteturas REST ou gRPC) para inferência.
- **Treinamento Contínuo (CT):** Gatilhos automáticos que re-treinam o modelo quando ocorre degradação de desempenho ou quando novos dados chegam, reiniciando o ciclo.

A disponibilização por APIs exige estratégias de implantação seguras para permitir reversões (*rollbacks*). O **Blue-Green Deployment** mantém dois ambientes idênticos, trocando o tráfego instantaneamente, enquanto o **Canary Deployment** expõe o novo modelo a uma fração pequena dos usuários (ex.: 5%), monitorando erros antes da liberação total.

O monitoramento é a fase mais crítica em produção, pois os modelos sofrem degradação natural ao longo do tempo (*drift*). Existem dois tipos principais mapeados na literatura e nas ferramentas de MLOps:

| Tipo de Degradação | Definição | Métricas e Testes de Detecção |
|---|---|---|
| **Data Drift (Desvio de Covariável)** | Mudança na distribuição estatística dos dados de entrada ($X$) ao longo do tempo, em relação aos dados de treino. A relação com o alvo não muda. | PSI (*Population Stability Index*), Teste Kolmogorov-Smirnov (KS), Distância de Wasserstein. |
| **Concept Drift (Desvio de Conceito)** | Mudança na relação lógica e matemática entre as variáveis de entrada ($X$) e a variável alvo ($y$). O que era considerado "certo" no passado mudou. | Requer a coleta de novos rótulos reais (*ground truth*) para medir a queda de acurácia, F1-Score ou AUC. |

**Exemplo Aplicado ao Setor Público (CGU):**
A CGU desenvolve um modelo de IA para detectar anomalias e indícios de corrupção em empenhos federais. Se a legislação muda e os gestores passam a registrar empenhos com novas rubricas, a definição do que é anômalo muda; isso é *Concept Drift*. Por outro lado, se o sistema de compras do governo é atualizado e os valores monetários passam a vir em centavos em vez de reais, alterando drasticamente a distribuição estatística da variável, isso é *Data Drift*. A auditoria contínua da CGU exige que o modelo registre experimentos (MLflow) para provar a lisura do modelo escolhido.

**Pegadinhas Típicas da CEBRASPE:**
- **Inversão Drift:** A banca frequentemente troca a definição de *Concept Drift* por *Data Drift*. Lembre-se: Data = muda a distribuição da entrada; Concept = muda a relação com o alvo.
- **Monitoramento sem Rótulos:** Afirmar que o *Concept Drift* pode ser detectado estatisticamente apenas analisando os dados de entrada. É falso; ele exige a comparação com a realidade (*ground truth*) tardia.
- **Deploy e Automação:** Afirmar que o Treinamento Contínuo (CT) força a implantação cega de modelos em produção. Na verdade, o CT treina o modelo, mas a implantação exige portões de qualidade (validação técnica e humana).
- **Reprodutibilidade:** Dizer que o versionamento do código via Git é suficiente para garantir a reprodutibilidade. É incompleto: sem versionar a semente aleatória (*random seed*), os hiperparâmetros e os dados de treino, a reprodutibilidade falha.

### Flashcards: Ciclo de Vida e MLOps

- Versionamento de Dados :: Prática de gerenciar alterações em conjuntos de dados ao longo do tempo, utilizando ferramentas como DVC para garantir reprodutibilidade.
- Versionamento de Modelos :: Gerenciamento do ciclo de vida de artefatos de ML (ex.: MLflow), permitindo transição de estágios (Staging para Production).
- Registro de Experimentos :: O ato de capturar código, ambiente, hiperparâmetros e métricas (ex.: acurácia) para comparar múltiplas execuções de treinamento de forma rastreável.
- Integração Contínua (CI) em ML :: Teste automatizado de código, integração de módulos e validação da qualidade dos dados (Data Quality) a cada novo commit.
- Treinamento Contínuo (CT) :: Pipeline de MLOps que automatiza o retreinamento do modelo com novos dados, geralmente acionado por degradação (drift) ou cronograma.
- Great Expectations :: Biblioteca popular para validação de qualidade de dados (Data Quality), atuando como testes unitários para conjuntos de dados no pipeline.
- Reprodutibilidade :: Capacidade de duplicar exatamente os resultados de um experimento de ML, exigindo controle de código, dados, ambiente (contêineres) e sementes aleatórias.
- API REST / gRPC :: Padrões de arquitetura para disponibilizar modelos como microsserviços, permitindo que outros sistemas consumam inferências via rede.
- Deploy Canary :: Estratégia de implantação de modelos que direciona uma fração diminuta do tráfego para a nova versão, limitando o impacto de falhas.
- Deploy Blue-Green :: Mantém dois ambientes de produção idênticos (apenas um ativo), permitindo reversão (rollback) imediata em caso de erro na nova implantação.
- Data Drift (Covariate Shift) :: Mudança na distribuição estatística dos dados de entrada (features) no ambiente de produção em relação à base de treinamento.
- Concept Drift (Model Drift) :: Alteração na relação entre as entradas e o alvo; o padrão que o modelo aprendeu deixou de ser válido no mundo real.
- Population Stability Index (PSI) :: Métrica para quantificar data drift; compara proporções de categorias/faixas. Valores > 0.2 indicam mudança significativa.
- Kolmogorov-Smirnov (KS) :: Teste estatístico não-paramétrico que mede a distância máxima entre duas funções de distribuição acumulada; altamente sensível a grandes amostras.
- Distância de Wasserstein :: Medida de "esforço" necessário para transformar uma distribuição em outra, eficiente para detectar anomalias complexas sem binarização excessiva.

### Questões CERTO/ERRADO: Ciclo de Vida e MLOps

1. **(CEBRASPE - Inédita / CGU)** Em ecossistemas maduros de MLOps, a ocorrência de *data drift* (desvio de dados) é caracterizada pela modificação na relação matemática entre as variáveis preditoras e a variável resposta, o que exige inexoravelmente a intervenção de especialistas para a coleta de novos rótulos e retreinamento do modelo.
   - **Gabarito:** ERRADO. A questão descreve o *concept drift* (desvio de conceito). O *data drift* ocorre apenas quando há mudança na distribuição das variáveis de entrada (preditoras), mesmo que a relação com a variável resposta (alvo) permaneça inalterada.

2. **(CEBRASPE - Inédita / CGU)** A métrica conhecida como PSI (*Population Stability Index*) é amplamente adotada em ferramentas de observabilidade de ML para mensurar o *data drift*, sendo que valores inferiores a 0,1 indicam estabilidade populacional, ao passo que valores superiores a 0,2 justificam ações de recalibragem ou investigação profunda do modelo.
   - **Gabarito:** CERTO. Esta é a regra de bolso clássica para a interpretação do PSI em MLOps, permitindo que a variação na distribuição das categorias (*bins*) alerte as equipes antes mesmo da queda real na acurácia ser detectada.

3. **(CEBRASPE - Inédita / CGU)** Em uma arquitetura orientada ao Treinamento Contínuo (CT), a esteira de MLOps é configurada para automatizar integralmente não apenas o retreinamento do modelo perante novos dados, mas também a sua implantação imediata e irrestrita no ambiente de produção, visando reduzir o tempo de latência de entrega.
   - **Gabarito:** ERRADO. O Treinamento Contínuo (CT) automatiza o retreinamento e o empacotamento, mas a implantação (CD - *Continuous Delivery/Deployment*) em ambientes críticos de negócios não deve ser cega ou irrestrita. Ela requer "portões de qualidade" (avaliações contra o modelo antigo, testes A/B, *shadow deployment*) para garantir que o novo modelo realmente performa melhor.

4. **(CEBRASPE - Inédita / CGU)** O teste de Kolmogorov-Smirnov (KS) é um método paramétrico focado em variáveis categóricas, empregado na detecção de *drift* para mensurar o esforço necessário de transformação entre uma distribuição antiga e uma nova distribuição de dados.
   - **Gabarito:** ERRADO. A questão apresenta três erros técnicos. Primeiro, o teste KS é não-paramétrico. Segundo, ele é primariamente utilizado para variáveis contínuas, avaliando a distância máxima entre as funções de distribuição acumulada (e não categóricas). Terceiro, o conceito de "esforço de transformação" refere-se à Distância de Wasserstein (*Earth Mover's Distance*).

5. **(CEBRASPE - Inédita / CGU)** O processo de rastreamento de linhagem de dados (*data lineage*) e registro de experimentos em ferramentas como MLflow garante a governança e a reprodutibilidade de soluções analíticas, registrando metadados que conectam diretamente o código executado aos conjuntos de dados transformados e aos hiperparâmetros aplicados na construção do artefato final de IA.
   - **Gabarito:** CERTO. Este é o propósito central das ferramentas de registro de experimentos e linhagem em MLOps: fornecer uma trilha de auditoria completa, possibilitando que um cientista de dados ou auditor da CGU reverta ou reproduza o exato contexto de treinamento de uma rede neural ou árvore de decisão.

---

## 2. Sustentação de Soluções Analíticas

A sustentação transcende a disponibilidade de infraestrutura. Ela integra a alocação eficiente de recursos físicos (CPUs, Memória, GPUs) aos requisitos operacionais (latência, *throughput*) e à proteção rigorosa dos dados institucionais, impactando a escolha estratégica de arquitetura.

### 2.1 a 2.4: Resumo Estruturado e Aprofundamento

**Definição e Funcionalidade:**
A dicotomia entre serviços gerenciados (Nuvem Pública) e operação própria (*Datacenter on-premise*) afeta diretamente o fluxo de caixa, a agilidade técnica e o grau de dependência. Modelos de IA modernos, particularmente Redes Neurais Profundas (*Deep Learning*) e *Large Language Models* (LLMs), demandam aceleradores de hardware (GPUs para processamento matricial e TPUs). O treinamento requer vastas quantidades de memória de vídeo (VRAM) e taxa de transferência, enquanto a inferência foca na latência mínima.

O **Custo Total de Propriedade (TCO)** é a bússola financeira dessa sustentação. Em operações próprias, o **CapEx** (*Capital Expenditure* - compra de máquinas) é altíssimo, com um **OpEx** (*Operational Expenditure*) focado em energia e refrigeração. Em Nuvem, converte-se tudo em OpEx (pagamento por uso). A nuvem também embute custos invisíveis que podem destruir orçamentos governamentais, notavelmente os **Egress Costs** (tarifas cobradas quando se retira dados do provedor de nuvem).

A **observabilidade** eleva o monitoramento reativo a um diagnóstico proativo. Ela se sustenta em três pilares:
- **Métricas:** Dados quantitativos agregados (ex.: uso de CPU, requisições por segundo).
- **Logs:** Registros detalhados de eventos específicos gerados pelo código.
- **Traces (Rastreamento Distribuído):** Caminho percorrido por uma requisição ao longo de múltiplos microsserviços.

No campo da segurança e continuidade, o Controle de Acesso baseado em funções (RBAC) e o princípio do menor privilégio são fundamentais. Um desafio crítico em MLOps é a **proteção de segredos** (chaves de API, senhas de banco de dados). Eles jamais devem constar em código-fonte (*hardcoded*). A sustentação exige a implementação de **Secret Managers** (como HashiCorp Vault ou Azure Key Vault), que injetam as credenciais dinamicamente. A continuidade baseia-se em redundância, tolerância a falhas e estratégias de *Disaster Recovery*.

| Requisito Analítico | Implicações na Sustentação e Arquitetura |
|---|---|
| **Processamento (CPUs vs. GPUs)** | CPUs são eficientes para processamento sequencial e ETL; GPUs são mandatórias para treinamento paralelo massivo (Deep Learning). |
| **Armazenamento** | Modelos e Data Lakes requerem armazenamento de objeto escalável (ex.: Amazon S3, MinIO) que desatrele armazenamento de computação. |
| **Latência vs Throughput** | Inferência em tempo real (ex.: predição de fraude no clique) exige baixa latência. Inferência em lote (ex.: gerar relatórios noturnos) exige alto throughput (vazão). |

**Exemplo Aplicado ao Setor Público (CGU):**
A CGU decide migrar a hospedagem de seu sistema analítico de riscos de licitações para a Nuvem (SaaS/PaaS). A sustentação financeira analisada via TCO revelou que manter GPUs físicas subutilizadas 80% do tempo era um mau uso do dinheiro público (alto CapEx ocioso). Porém, na nuvem, a CGU precisa aplicar proteção estrita de segredos: o modelo na nuvem não guarda a senha do banco de dados confidencial da CGU; ele a acessa via um cofre seguro. Além disso, foi elaborado um Plano de Continuidade de Negócios para garantir que, caso a nuvem caia, as auditorias não parem.

**Pegadinhas Típicas da CEBRASPE:**
- **CapEx vs OpEx:** Afirmar que a migração para a computação em nuvem reduz despesas operacionais (OpEx) às custas do aumento de investimentos de capital (CapEx). A afirmativa é inversa.
- **Ofuscação de Senhas:** Afirmar que chaves de API e senhas devem ser "criptografadas e enviadas no repositório de código" para garantir a segurança em repositórios privados. Falso, exige-se o uso de Vaults / Secret Managers dinâmicos.
- **Observabilidade vs Monitoramento:** Tentar limitar a observabilidade ao mero acompanhamento do estado de servidores (CPU/RAM). Observabilidade foca na capacidade de investigar o estado interno e entender as causas raízes de falhas usando métricas, logs e traces.

### Flashcards: Sustentação de Soluções Analíticas

- Serviços Gerenciados (Cloud) :: Infraestrutura de TI onde o provedor abstrai hardware, patching e rede, convertendo aquisição física (CapEx) em pagamento por uso (OpEx).
- Operação Própria (On-Premise) :: Hospedagem local que garante total controle dos dados e soberania, mas exige altos investimentos iniciais e equipe técnica de manutenção profunda.
- GPU (Graphics Processing Unit) :: Acelerador de hardware essencial para treinamento de redes neurais devido à sua arquitetura focada em paralelismo massivo de cálculos matriciais.
- TCO (Total Cost of Ownership) :: Métrica que calcula o impacto financeiro global de uma solução de TI, englobando aquisição, manutenção, energia, licenças, depreciação e descarte.
- Egress Costs :: Taxas cobradas por provedores de nuvem para a transferência ou extração de dados para fora de sua infraestrutura.
- Observabilidade :: Capacidade de inferir o estado interno de um sistema complexo a partir de suas saídas externas, utilizando o tripé: logs, métricas e rastreamentos (traces).
- Latência :: Tempo de atraso entre o envio de uma requisição para a API de inferência do modelo e o recebimento da predição. Crítico em sistemas de tempo real.
- Throughput (Vazão) :: Quantidade de dados ou inferências processadas em um determinado intervalo de tempo. Crítico em processamento em lote (batch).
- Secret Manager (Cofre de Segredos) :: Ferramenta de infraestrutura utilizada para armazenar e injetar dinamicamente senhas e chaves de API, evitando que sejam expostas em repositórios de código.
- Continuidade de Negócios :: Planejamento estratégico que inclui tolerância a falhas, redundância e Disaster Recovery para manter a operação em caso de incidentes graves.

### Questões CERTO/ERRADO: Sustentação de Soluções Analíticas

1. **(CEBRASPE - Inédita / CGU)** Ao decidir entre a sustentação de um modelo de aprendizado profundo (*Deep Learning*) em infraestrutura local (operação própria) ou na contratação de serviços gerenciados em nuvem pública, o cálculo do TCO (*Total Cost of Ownership*) deve computar as despesas operacionais, sendo os altos investimentos iniciais com a aquisição de GPUs classificados exclusivamente como CapEx (*Capital Expenditure*).
   - **Gabarito:** CERTO. No modelo de operação própria (*on-premise*), a compra inicial de infraestrutura pesada (servidores e GPUs) entra no balanço como despesa de capital (CapEx). A nuvem, por outro lado, elimina grande parte desse CapEx, deslocando-o para OpEx (despesas operacionais recorrentes e elásticas).

2. **(CEBRASPE - Inédita / CGU)** Nos pipelines modernos de inferência analítica conteinerizada, a proteção de segredos criptográficos, tais como chaves privadas e tokens de API, deve ser garantida mediante a ofuscação (criptografia estática) de seus valores diretamente no código-fonte, dispensando infraestruturas adicionais de gerenciamento e reduzindo a latência da aplicação.
   - **Gabarito:** ERRADO. Em nenhuma hipótese de sustentação segura é admitido o armazenamento de credenciais (*hardcoding*), mesmo que ofuscadas, no código-fonte ou no sistema de versionamento. O padrão ouro de sustentação exige o uso de gerenciadores de segredos (*Secret Managers* ou *Vaults*) acoplados a políticas de IAM para injetar credenciais dinamicamente em tempo de execução.

3. **(CEBRASPE - Inédita / CGU)** A observabilidade difere do monitoramento tradicional de infraestrutura porque, enquanto o monitoramento sinaliza se um sistema está funcionando ou falhando através de alertas reativos predefinidos, a observabilidade permite às equipes investigar o comportamento dinâmico e localizar a causa raiz da falha em sistemas distribuídos, comumente baseando-se em métricas, logs estruturados e rastreamentos (*traces*).
   - **Gabarito:** CERTO. Essa é a exata distinção doutrinária e de arquitetura entre monitoramento (foco no que está quebrado, focado em painéis reativos) e observabilidade (foco na capacidade sistêmica de responder "por que está quebrado" a partir de dados instrumentados internamente, utilizando *logs, metrics e traces*).

4. **(CEBRASPE - Inédita / CGU)** Diferentemente de um processador central (CPU) que executa instruções predominantemente sequenciais otimizadas para processamento geral, os aceleradores de hardware como GPUs (Unidades de Processamento Gráfico) e TPUs (Unidades de Processamento de Tensores) são essenciais para sustentar o treinamento de redes neurais devido à sua arquitetura projetada para computação paralela massiva em matrizes e tensores.
   - **Gabarito:** CERTO. As redes neurais dependem da multiplicação de grandes matrizes, operações que são incrivelmente aceleradas pelos milhares de núcleos paralelos presentes em GPUs e TPUs, justificando os altos requisitos operacionais e de sustentação dessas tecnologias.

5. **(CEBRASPE - Inédita / CGU)** Ao migrar data lakes governamentais para a computação em nuvem, a avaliação de sustentação de custos dispensa a estimativa da tarifa de transferência externa (*egress costs*), uma vez que serviços em nuvem pública tarifam apenas o processamento de CPU e o armazenamento inativo de objetos, mantendo o tráfego de dados gratuito como fomento tecnológico.
   - **Gabarito:** ERRADO. Os *egress costs* (cobranças pela transferência de dados para fora da nuvem) constituem um dos "custos ocultos" mais altos e perigosos no TCO em nuvem. A saída de dados nunca é gratuita nos grandes provedores, e ignorá-los em ETPs de migração é um erro crasso de dimensionamento.

---

## 3. Governança e Responsabilidade

A implementação de IA no setor público está condicionada não apenas ao rigor tecnológico, mas principalmente ao alinhamento com a Constituição, o Estatuto do Servidor e os direitos dos cidadãos. Isso exige o mapeamento da rastreabilidade da decisão e o respeito imperativo à Lei Geral de Proteção de Dados (LGPD) e normativas emergentes.

### 3.1 a 3.5: Resumo Estruturado e Aprofundamento

**Definição e Funcionalidade:**
A Governança de IA requer a formalização de papéis (desenvolvedores, proprietários do modelo, especialistas em conformidade) por meio de instrumentos como a **Matriz RACI**. A rastreabilidade das decisões exige que as organizações justifiquem algoritmos discriminatórios ou enviesados. A **ABNT NBR ISO/IEC 42001** (Sistema de Gestão de IA) e a **ISO/IEC 23894** (Orientação para Gestão de Riscos) estabelecem as bases internacionais normatizadas de como a alta administração estrutura essa governança, desde a política ética até a operação.

No cenário legal brasileiro, o impacto de automações que processam dados pessoais deve ser relatado através do **Relatório de Impacto à Proteção de Dados Pessoais (RIPD)**. O **Artigo 20 da LGPD** é um pilar: ele confere ao titular dos dados o direito de solicitar a revisão de decisões tomadas unicamente com base em tratamento automatizado. Contudo, a lei atual não determina taxativamente que tal revisão deva ser feita exclusivamente por ser humano, embora seja fortemente recomendada.

Já o **Projeto de Lei nº 2338/2023 (Marco Legal da IA)** propõe regulação baseada em riscos:
- **Risco Excessivo:** Sistemas cujo uso é expressamente vedado/proibido (ex.: armas autônomas, uso de técnicas subliminares nocivas).
- **Alto Risco:** Sistemas que impactam direitos (ex.: crédito, saúde, avaliações, justiça). Exigem avaliação de impacto prévia e aqui sim, a revisão humana torna-se um direito expresso.

No âmbito do SISP (Governo Federal), a Secretaria de Governo Digital (SGD/MGI) instituiu a **Autoavaliação de Impacto Ético (AIE)**, ferramenta em que gestores classificam o projeto e garantem aderência a princípios como explicabilidade e supervisão. Para a transparência, utiliza-se a **Ficha do Sistema de IA**, prestando contas de limitações e lógicas à sociedade.

| Elemento de Governança | Mecanismo de Prevenção / Tratamento |
|---|---|
| **Vieses e Discriminação** | Adoção de métricas de equidade (Fairness) no ciclo de vida (ISO 42001) e representatividade na amostragem; não utilizar variáveis sensíveis ilicitamente. |
| **Uso Fora da Finalidade** | Aplicação estrita da finalidade e minimização de dados conforme LGPD; rastreabilidade de acessos (Logs). |
| **Limites da Automação** | Sistemas de apoio à decisão vs Decisão Autônoma. Aplicação de Human-in-the-Loop (revisão contínua), Human-on-the-Loop (supervisão intermitente) ou Human-in-Command. |

**Exemplo Aplicado ao Setor Público (CGU):**
A CGU pretende usar Machine Learning para ranquear servidores civis quanto à probabilidade de irregularidade disciplinar. Como esse sistema lida com dados sensíveis e toma decisões que afetam o direito do servidor (Alto Risco), a CGU aciona a governança: elabora o RIPD, aplica a AIE, publica a Ficha do Sistema e, essencialmente, garante que a IA atue apenas como recomendação, não como decisão final punitiva. Caso o sistema aplique punições sozinho, o servidor poderia recorrer ao Art. 20 da LGPD para exigir revisão.

**Pegadinhas Típicas da CEBRASPE:**
- **Exigência de Revisão "Humana" na LGPD Atual:** Cuidado: A palavra "humana" (ou pessoa natural) foi vetada no Art. 20 da LGPD antes da sanção. A revisão é obrigatória, mas a LGPD atual permite, na literalidade da lei, que seja feita por outra máquina. A revisão estritamente "humana" aparece no PL 2338/2023. A CEBRASPE brinca com esse detalhe.
- **Tecnologia Proibida:** O PL 2338 baseia-se em risco, não proíbe a tecnologia (ex.: Redes Neurais), mas o uso (ex.: manipulação de crianças).
- **Certificação ISO 42001:** Afirmar que a obtenção da ISO 42001 afasta ou dispensa as sanções e controles da LGPD. Errado; são complementares. A ISO ajuda a demonstrar conformidade, mas não substitui a lei.

### Flashcards: Governança e Responsabilidade

- Matriz RACI em IA :: Matriz de responsabilidades organizacionais dividida em Responsible (Responsável), Accountable (Autoridade), Consulted (Consultado) e Informed (Informado).
- Art. 20 da LGPD :: Assegura o direito à revisão de decisões tomadas unicamente por meio de tratamento automatizado de dados que afetem interesses (sem, contudo, exigir revisão humana expressa no texto atual).
- PL 2338/2023 :: Projeto do Marco Legal da IA no Brasil; institui regulação baseada em categorias de impacto: Risco Excessivo, Alto Risco e outros usos.
- Sistemas de Risco Excessivo :: Usos de IA inaceitáveis/proibidos pelo PL 2338, como exploração de vulnerabilidades e armas autônomas fora do controle humano.
- RIPD (Relatório de Impacto à Proteção de Dados Pessoais) :: Documento exigido pela LGPD contendo a descrição dos processos de tratamento que geram risco às liberdades civis, com medidas de mitigação.
- AIE (Autoavaliação de Impacto Ético) :: Framework orientativo da SGD/MGI para avaliar riscos éticos em projetos de IA no governo federal.
- Ficha de Sistema de IA :: Artefato público de governança que documenta limites técnicos, vieses, finalidade e lógica processual para a transparência à sociedade.
- ISO/IEC 42001 :: Norma ABNT que estabelece diretrizes e requisitos certificáveis para o Sistema de Gestão de IA (Artificial Intelligence Management System).
- Discriminação Algorítmica :: Produção de resultados tendenciosos devido ao aprendizado em bases de dados enviesadas, violando princípios da LGPD e diretrizes de Direitos Humanos.
- Human-in-the-Loop (HITL) :: Paradigma de governança que exige intervenção direta e contínua de um humano no ciclo de predição do modelo para aprovar decisões críticas.

### Questões CERTO/ERRADO: Governança e Responsabilidade

1. **(CEBRASPE - Inédita / CGU)** Considere que a CGU esteja implementando uma plataforma de triagem automatizada baseada em IA para negar imediatamente benefícios sociais aos cidadãos com suspeita de irregularidade. Em consonância com a Lei Geral de Proteção de Dados Pessoais (LGPD) vigente, os cidadãos afetados detêm o direito potestativo de solicitar a revisão dessas decisões automatizadas, restando à CGU a obrigação inafastável de submeter tal revisão unicamente à avaliação manual e exaustiva por um auditor humano (pessoa natural), sendo vedado o uso de outra automação nesse grau de recurso.
   - **Gabarito:** ERRADO. Cuidado absoluto: embora o projeto de lei PL 2338/2023 preveja a "revisão humana", a redação vigente do caput do Art. 20 da LGPD assegura o direito à revisão de decisões unicamente automatizadas, mas o termo "por pessoa natural" foi suprimido (vetado) do texto legal em 2019. Assim, estritamente à luz da LGPD vigente, a revisão humana não é uma obrigação inafastável, podendo a revisão ser executada por sistema distinto.

2. **(CEBRASPE - Inédita / CGU)** Em observância à publicação da ABNT NBR ISO/IEC 42001, que orienta o Sistema de Gestão de IA, a obtenção de certificação por entidade credenciada é legalmente compulsória para todos os órgãos do Sistema de Administração dos Recursos de Tecnologia da Informação (SISP) que realizem processamento de grandes volumes de dados (*Big Data*).
   - **Gabarito:** ERRADO. A norma ABNT NBR ISO/IEC 42001 (e sua respectiva certificação) é de adoção voluntária e não compulsória por lei; ela constitui um guia de melhores práticas e sistema de gestão. As obrigações no setor público advêm de instruções normativas, portarias governamentais (como a Portaria SGD 6.618/2024 sobre AIE) e da LGPD.

3. **(CEBRASPE - Inédita / CGU)** O Projeto de Lei nº 2338/2023 (Marco Legal da Inteligência Artificial), alinhado a frameworks internacionais, assenta-se sobre uma modelagem regulatória baseada em riscos (*Risk-Based Approach*), não proibindo a tecnologia de IA *per se*, mas estabelecendo gradações rigorosas conforme o contexto de aplicação e o impacto da decisão sobre direitos fundamentais.
   - **Gabarito:** CERTO. Perfeita definição da abordagem do PL 2338. A regulação proposta não é orientada à ferramenta tecnológica (ex.: banir redes neurais), e sim ao seu impacto. Aplicações de "alto risco" exigem forte governança, enquanto "risco excessivo" é proibido e "baixo risco" tem apenas obrigações de transparência.

4. **(CEBRASPE - Inédita / CGU)** O uso da Ficha de Sistema de IA, conforme diretrizes da SGD/MGI, exime a entidade pública da elaboração de Relatório de Impacto à Proteção de Dados Pessoais (RIPD), já que ambos os documentos atendem de forma redundante e integral aos mesmos princípios técnicos e finalidades da Lei Geral de Proteção de Dados.
   - **Gabarito:** ERRADO. Os documentos possuem finalidades distintas e são complementares, não excludentes. O RIPD é uma obrigação legal decorrente da LGPD, focado nos impactos aos direitos e garantias das pessoas naturais afetadas pelo processamento dos dados. A Ficha de Sistema de IA atende a diretrizes de governança técnica (AIE), visando publicizar capacidades, limites técnicos, e mitigar riscos éticos mais amplos que privacidade.

5. **(CEBRASPE - Inédita / CGU)** Para evitar que uma solução baseada em Machine Learning infira equivocadamente perfis de indivíduos através de "vieses ocultos" (*proxies*), é dever institucional estabelecer medidas de prevenção e tratamento de discriminação algorítmica, as quais devem abranger desde a fase de coleta equitativa e avaliação dos dados de treinamento até a implementação de métricas de justiça (*fairness*) na validação dos resultados.
   - **Gabarito:** CERTO. A mitigação da discriminação algorítmica não ocorre apenas no momento da inferência; é um princípio sistêmico que impõe a governança ao longo de todo o ciclo de vida do dado, expurgando assimetrias desde a aquisição e garantindo amostragem representativa antes mesmo do treinamento da IA.

---

## 4. Gestão de Produtos de Dados

A transição da mentalidade de "projeto com fim específico" para a visão de "produto contínuo" é vital em Ciência de Dados, pois os produtos evoluem e degradam. Na esfera pública, este produto tem dupla função: atender aos cidadãos e gerar auditoria/conformidade, alinhando-se aos grandes documentos governamentais.

### 4.1 a 4.6: Resumo Estruturado e Aprofundamento

**Definição e Funcionalidade:**
O ciclo de vida do produto inicia-se no alinhamento do **problema público**. Não se desenvolve um produto de dados porque a tecnologia é nova; desenvolve-se porque existe uma ineficiência mensurável. As funcionalidades geradas (modelos de predição, análises) formam o **Backlog do Produto**, organizado por priorização baseada em valor de negócio e mitigação de risco.

Para que um incremento seja aceito, usam-se **Critérios de Aceitação** rigorosos e indicadores (KPIs). Ex: *"O modelo deve acertar predições de lavagem de dinheiro com F1-Score mínimo de 0.90 em base de teste não vista, respeitando latência de 2 segundos"*.

Frameworks ágeis ditam o ritmo dessa entrega:
- **Scrum:** Prescritivo. Define Papéis (*Product Owner*, *Scrum Master*, *Developers*). Trabalha por iterações de tempo fixo (Sprints de 1 a 4 semanas). Utiliza métricas como o *Velocity* (quanto a equipe consegue entregar por Sprint).
- **Kanban:** Fluxo Contínuo, sem Sprints obrigatórias. Foca puramente em identificar gargalos limitando a quantidade de trabalho em andamento (*WIP limits*). É muito útil em equipes de MLOps lidando com demandas rotineiras, chamados e manutenção. Métricas: *Lead Time* (tempo do pedido à entrega) e *Throughput* (vazão).

Na estrutura pública, o produto deve se articular com a arquitetura maior:
- **PDTIC (Plano Diretor de TI e Comunicação):** Nível Tático. Vigência mínima de 2 anos. Trata do orçamento, infraestrutura e governança interna de TI.
- **Plano de Transformação Digital (PTD):** Nível finalístico e estratégico. Orienta a modernização de serviços focados na melhoria da experiência do cidadão e do serviço público.
- **Plano de Dados Abertos (PDA):** Nível de Transparência Ativa. Regulamenta como o órgão tratará e publicará seus acervos em formato legível por máquina (ex.: CSV, JSON), fomentando controle social.

O produto falha se não houver **Comunicação dos Resultados e Incertezas**. Modelos não fornecem "verdades absolutas"; fornecem probabilidades. Omitir a margem de erro na tomada de decisão pública é um equívoco que viola o princípio de revisão e explicabilidade.

| Característica | Scrum | Kanban |
|---|---|---|
| **Frequência de Entrega** | Ao final de cada Sprint de tempo delimitado. | Contínua (assim que o item estiver pronto). |
| **Limitação do Trabalho** | Indireta (determina-se o que cabe na Sprint). | Direta (limita-se estritamente as tarefas na coluna - WIP). |
| **Estrutura de Papéis** | Rígida e obrigatória (PO, SM, Dev). | Nenhuma predefinição obrigatória. |

**Exemplo Aplicado ao Setor Público (CGU):**
A CGU cria o produto "Alice" (Analisador de Licitações e Contratos). O problema público é a corrupção; o produto é o modelo de IA. A equipe ágil adota o Scrum, estabelecendo Sprints de 2 semanas. Eles priorizam a análise de superfaturamento antes do conluio, pois o ROI público é maior. Para atender ao PDA, parte das metodologias e metadados de resultados classificados como "baixíssimo risco" são expostos em transparência ativa. Ao notificar um auditor de um alerta gerado pela "Alice", a interface informa: "Probabilidade de fraude de 87% (Margem de Incerteza ±5%)", comunicando claramente o caráter estocástico da IA.

**Pegadinhas Típicas da CEBRASPE:**
- **Kanban exige Sprint:** Afirmar que "No desenvolvimento de produtos com Kanban, a priorização ocorre rigorosamente antes de cada Sprint de quinze dias". Errado, Kanban usa fluxo contínuo.
- **Certeza do Modelo:** A assertiva dirá que "uma boa comunicação requer que as margens de erro sejam suprimidas pelo Cientista de Dados para que os gestores tenham segurança técnica ao agir". Erradíssimo. Incerteza deve ser visualizada.
- **Esfera do PDTIC:** Confundir PDTIC com PTD. PDTIC organiza os recursos, TI, orçamentos e tática (Plano Diretor). O PTD foca nos serviços digitais entregues à sociedade.

### Flashcards: Gestão de Produtos de Dados

- Problema Público :: A ineficiência, falha de serviço ou carência social que justifica o empenho de orçamento público para o desenvolvimento do produto.
- Produto de Dados :: Conjunto de ativos, modelos e engenharia que gera valor contínuo baseado no consumo inteligente de informações, possuindo gestão de ciclo de vida permanente.
- Critérios de Aceitação :: Condições preestabelecidas que uma funcionalidade (história de usuário) do modelo deve cumprir para que o Product Owner a considere "Pronta" (DoD).
- Scrum :: Framework ágil iterativo (com ciclos chamados Sprints) com papéis definidos e ritos rígidos (Planning, Daily, Review, Retrospective).
- Kanban :: Metodologia baseada na visualização e fluxo de valor contínuo; sua regra central é limitar o trabalho em andamento (WIP limits) para não sobrecarregar a equipe.
- WIP (Work In Progress) Limit :: Princípio do Kanban que proíbe puxar novos trabalhos enquanto a coluna do fluxo atual (ex.: testes de modelo) já estiver em sua capacidade máxima de itens.
- PDTIC :: O Plano Diretor de Tecnologia da Informação e Comunicação é o principal norteador tático de ações, metas e orçamento de TI em órgãos públicos.
- Plano de Dados Abertos (PDA) :: Documento que orienta as ações de transparência ativa do ente, definindo cronograma e formatação técnica para publicação de bases ao acesso público.
- Plano de Transformação Digital (PTD) :: Instrumento da Estratégia de Governo Digital, voltado para a oferta de serviços públicos digitalizados, automatizados e centrados na experiência do cidadão.
- Comunicação de Incertezas :: Diretriz que exige que analistas forneçam intervalos de confiança ou probabilidades de erro junto aos resultados da IA para não iludir o tomador de decisão (Cegueira da Automação).

### Questões CERTO/ERRADO: Gestão de Produtos de Dados

1. **(CEBRASPE - Inédita / CGU)** Em contraste com as metodologias em cascata, o framework Scrum atua no gerenciamento do ciclo de vida de soluções de dados através de entregas incrementais; todavia, por ser altamente adaptativo a escopos voláteis, ele abole totalmente a definição de papéis e a prescrição de rituais temporais fixos nas equipes de Ciência de Dados.
   - **Gabarito:** ERRADO. O Scrum é um framework leve, mas extremamente prescritivo quanto às suas regras, eventos e papéis. Ele define obrigatoriamente a existência do Product Owner, Scrum Master e Developers, e exige ciclos de tempo fixo (*timeboxes*) através das Sprints e rituais obrigatórios (Planning, Daily, Review, Retrospective).

2. **(CEBRASPE - Inédita / CGU)** Na construção de um produto de IA preditivo, a articulação com o Plano de Dados Abertos (PDA) do órgão impõe que o governo publique periodicamente as bases de treinamento exauridas de dados pessoais para viabilizar controle social, ao passo que o Plano Diretor de Tecnologia da Informação e Comunicação (PDTIC) garantirá as diretrizes táticas, orçamentárias e de governança interna da TI para a sustentação dessa plataforma.
   - **Gabarito:** CERTO. Os conceitos de PDTIC e PDA estão perfeitamente delineados. O PDTIC traça a direção tática e as dotações orçamentárias (internas) da TI por no mínimo dois anos, enquanto o PDA instrumentaliza a política de transparência ativa (disponibilização externa em formatos abertos, excluindo-se as informações sensíveis).

3. **(CEBRASPE - Inédita / CGU)** A gestão do trabalho em equipes de MLOps fundamentada na metodologia Kanban exige a paralisação do fluxo contínuo a cada duas semanas para se proceder ao fechamento e faturamento dos artefatos produzidos (limitação por iteração).
   - **Gabarito:** ERRADO. A principal característica que distingue o Kanban do Scrum é exatamente o foco no fluxo contínuo, sem a exigência de iterações de tempo fixo (Sprints). O Kanban controla o sistema limitando o trabalho em andamento (*WIP limits*), e não dividindo o tempo em blocos preestabelecidos.

4. **(CEBRASPE - Inédita / CGU)** A definição dos "Critérios de Aceitação" para a entrega de um modelo de linguagem natural em uma Controladoria Pública deve especificar não apenas os limites de latência e os limiares métricos mínimos de detecção de fraudes em ambientes de homologação, mas também representar claramente as expectativas da área de negócio em relação ao problema público a ser mitigado.
   - **Gabarito:** CERTO. Os critérios de aceitação compõem a "Definição de Pronto" (*Definition of Done*) para itens de valor. Eles estabelecem a ponte entre os requisitos funcionais/técnicos exigidos pela engenharia (latência) e o alcance dos objetivos gerenciais propostos (problema público atacado).

5. **(CEBRASPE - Inédita / CGU)** Durante a comunicação dos resultados de um modelo preditivo a tomadores de decisão não-técnicos, como juízes ou auditores seniores, as margens de erro e os graus de incerteza da ferramenta matemática devem ser ocultados, uma vez que a exposição da estocasticidade do algoritmo tende a invalidar a aceitação gerencial do produto de dados.
   - **Gabarito:** ERRADO. Um dos grandes riscos da inteligência artificial nas esferas de auditoria e jurídica é a "Cegueira da Automação" (*Automation Bias*). A comunicação efetiva de produtos analíticos exige a representação clara das incertezas, probabilidades, falsos positivos e limitações para que o decisor exerça uma supervisão humana informada.

---

## 5. Contratação e Controle de Soluções

A terceirização ou aquisição de infraestrutura para IA no Governo Federal baseia-se na **Lei nº 14.133/2021** (Nova Lei de Licitações) e na fundamental **Instrução Normativa SGD/ME nº 94/2022** (que revogou a antiga IN 01/2019). Esta norma impõe um rito altamente engessado para mitigar fraudes e desperdícios.

### 5.1 a 5.7: Resumo Estruturado e Aprofundamento

**Definição e Funcionalidade:**
O Planejamento da Contratação de TIC segue estritamente três documentos basilares, que operam em sequência (obrigatoriamente via ETP Digital):
- **DFD (Documento de Formalização da Demanda):** Instrumento embrionário onde a área requisitante apenas expõe o "problema", a justificativa e as estimativas muito iniciais.
- **ETP (Estudo Técnico Preliminar):** É aqui que as equipes levantam soluções do mercado, estimam o volume necessário e realizam o cálculo do Custo Total de Propriedade (TCO) comparativo. É o ETP que compara se vale a pena desenvolvimento próprio, aquisição de mercado ou adoção de SaaS em Nuvem, culminando em uma declaração objetiva de "Viabilidade da Contratação".
- **TR (Termo de Referência):** O ETP provou o "quê" e o "por quê". O TR consolida as regras do jogo: especifica tecnicamente o serviço exato, modelos de penalidades, cronogramas de entrega e os Acordos de Nível de Serviço (SLA).

**O Mapa de Gerenciamento de Riscos (MGR):**
Corre paralelamente a essas fases (planejamento, seleção e execução). Não deve ser confundido com os mapas gerais de auditoria ou avaliações de impacto ético (RIPD).

**Contratação Direta (Lei 14.133):**
- **Inexigibilidade (Art. 74):** Competição é inviável. Exemplos: consultoria ultraespecializada (notória especialização) para arquitetar sistemas de IA onde ninguém mais no país detém a tecnologia ou fornecedor unicamente exclusivo.
- **Dispensa (Art. 75):** A Competição é viável (existem várias empresas de desenvolvimento), mas, por economia processual (baixo valor) ou emergência/calamidade pública, a lei dispensa a licitação.

**Fiscalização e Pagamento:**
A IN 94/2022 revolucionou a TI governamental ao **vedar expressamente o pagamento por mera alocação de postos de trabalho ou horas** sem atrelamento a resultados e vedar subordinação da terceirizada. A fiscalização remunera **entregas verificáveis**, medidas por pontuação de função, *story points* certificados, ou Acordos de Nível de Serviço (SLA).

**Propriedade e Continuidade (Vendor Lock-in):**
Contratos de fábricas de software ou nuvem para o Governo impõem que a Propriedade Intelectual de códigos elaborados sob encomenda e todos os modelos pertencem inequivocamente à Administração. Para evitar dependência tecnológica (*Vendor Lock-in*), todo TR de nuvem e desenvolvimento precisa prever o **Plano de Saída (Plano de Transição)**: obriga a contratada a passar conhecimento e realizar extração (*dump*) irrestrito dos dados no fim do contrato.

**Pesquisa de Preços (IN SEGES/ME 65/2021):**
Proíbe firmar contratos baseados unicamente em propostas verbais. Privilegia as cotações extraídas do Painel de Preços e contratações pretéritas de outros órgãos. Rejeitam-se valores anômalos (*outliers*) em cálculos de média, mediana e menor preço.

| Fases de Contratação (IN 94/2022) | Responsáveis Típicos e Produtos Gerados |
|---|---|
| **Planejamento** | Área Demandante (DFD). Equipe de Planejamento (ETP, MGR e TR). |
| **Seleção de Fornecedores** | Agente de Contratação / Pregoeiro (Edital, Avaliação, Adjudicação). |
| **Gestão do Contrato** | Fiscais Técnico, Requisitante e Administrativo; Gestor de Contrato (Recebimento, Pagamento por Entregas). |

**Exemplo Aplicado ao Setor Público (CGU):**
A CGU pretende monitorar as redes sociais governamentais para medir sentimento. Elabora o DFD. No ETP, ao comparar a contratação de desenvolvimento próprio (horas internas) com a contratação de um serviço SaaS de IA, comprova viabilidade econômica no SaaS. O TR define um SLA de 99,5% de disponibilidade e, para evitar o risco cibernético (Lei 14.133), impõe na Matriz de Riscos severas multas caso a contratada descumpra a LGPD.

**Pegadinhas Típicas da CEBRASPE:**
- **Pagamento por hora:** Afirmar que "para garantir qualidade, os contratos de desenvolvimento de IA do governo devem remunerar baseados no total de horas logadas pelos programadores, exercendo controle direto de ponto". Ocorre o oposto: a IN proíbe subordinação e foca na medição da "entrega verificável" (resultado).
- **Dispensa x Inexigibilidade:** Misturar as definições. "Inviabilidade de competição caracteriza dispensa". (Inviabilidade gera Inexigibilidade).
- **ETP no TR:** Afirmar que a análise TCO comparativa entre "fazer no governo ou comprar fora" acontece na etapa do Termo de Referência. (Essa decisão estrutural ocorre no Estudo Técnico Preliminar - ETP).

### Flashcards: Contratação e Controle

- DFD (Documento de Formalização da Demanda) :: Documento simplificado emitido pela área requisitante detalhando a necessidade institucional e iniciando o fluxo do processo de aquisição de TIC.
- ETP (Estudo Técnico Preliminar) :: Artefato obrigatório do planejamento no qual se analisam alternativas de mercado, viabilidade, TCO comparativo e dimensionamento de TIC.
- TR (Termo de Referência) :: Documento exaustivo que descreve minunciosamente as exigências técnicas da solução escolhida e compila as regras operacionais (SLAs) para instruir o edital licitatório.
- IN SGD/ME 94/2022 :: Norma imperativa que regula o processo de aquisição e fiscalização de Tecnologia da Informação pelos órgãos membros do SISP no Executivo Federal, sucedânea da antiga IN 01/2019.
- Pagamento por Entregas Verificáveis :: Diretriz que veda a remuneração por mera disposição/alocação de mão de obra de TI, ancorando o pagamento à comprovação do atendimento de especificações ou níveis de serviço.
- Plano de Saída (Exit Plan) :: Previsão contratual que impõe, no encerramento da vigência, a migração irrestrita de acervos, metadados e transferência tecnológica de volta ao ente estatal, atenuando o vendor lock-in.
- TCO (Custo Total de Propriedade) no ETP :: Cálculo que exige integrar despesas iniciais (CapEx), gastos correntes prolongados (OpEx) e riscos implícitos por todo o ciclo projetado de utilidade da solução comparada.
- Pesquisa de Preços (IN 65/2021) :: Metodologia de aferição orçamentária prévia que prioriza consultas a bases transacionais da Administração e dispensa preços nitidamente discrepantes (outliers) para formar a mediana/média.
- Inexigibilidade de Licitação :: Modalidade de compra autorizada quando comprovada a inviabilidade material ou mercadológica da competição, como no caso de objeto estritamente singular.
- Dispensa de Licitação :: Modalidade de aquisição onde a competição mercadológica é viável na prática, mas o dispositivo legal consente não realizá-la, por critério de emergência ou módico valor financeiro.

### Questões CERTO/ERRADO: Contratação e Controle

1. **(CEBRASPE - Inédita / CGU)** Segundo as regras estabelecidas pela Instrução Normativa SGD/ME nº 94/2022, o processo de contratação de software e serviços em nuvem exige a constituição de uma Equipe de Planejamento, à qual incumbe a tarefa preliminar de formalizar a análise comparativa entre soluções de mercado e dimensionar o Custo Total de Propriedade (TCO) diretamente no Documento de Formalização da Demanda (DFD).
   - **Gabarito:** ERRADO. A assertiva atribui funções do Estudo Técnico Preliminar (ETP) ao Documento de Formalização da Demanda (DFD). O DFD é o instrumento sucinto de origem que demonstra a necessidade. É no âmbito do ETP que a equipe técnica avalia e justifica as opções do mercado, efetuando, assim, a análise comparativa de soluções e a computação do TCO.

2. **(CEBRASPE - Inédita / CGU)** Em conformidade com a nova Lei de Licitações (Lei nº 14.133/2021) e jurisprudência vinculada de controle externo, caso a CGU pretenda contratar um especialista para desenhar arquiteturas inéditas de Machine Learning para as quais exista inequivocamente apenas uma consultoria de notória especialização capaz no território, o processo será justificado mediante Inexigibilidade de Licitação, motivada pela patente inviabilidade fática de competição.
   - **Gabarito:** CERTO. A questão correlaciona adequadamente as premissas da inexigibilidade de licitação insculpidas no art. 74 da Lei 14.133/2021. Diante da singularidade do objeto e da constatação clara de "notória especialização" com ausência de competição prática, aplica-se a inexigibilidade, restando a dispensa àquelas condições onde existe rivalidade ofertante, mas o montante não a justifica.

3. **(CEBRASPE - Inédita / CGU)** Nos contratos administrativos regidos para serviços de Fábrica de Software e Sustentação de Infraestrutura em Ciência de Dados, o pagamento em proveito da contratada deverá processar-se pautado na medição do fornecimento exclusivo das horas despendidas pela força de trabalho dos profissionais (programadores e analistas), cabendo à CGU atestar o relógio de ponto destes para exercer fiscalização subordinativa de excelência.
   - **Gabarito:** ERRADO. Esta tese contraria incisivamente os pilares operacionais da gestão de TIC do Governo Federal (IN SGD/ME nº 94/2022). O normativo é claro ao vedar estabelecer subordinação técnica com trabalhadores terceirizados, bem como é explicitamente vedada a remuneração pautada tão somente no provimento das horas ou por postos de trabalho; o faturamento deve ocorrer pautado em entregas verificáveis (resultados, pontos de função, índices de SLA) devidamente avaliadas pelos fiscais do contrato.

4. **(CEBRASPE - Inédita / CGU)** No que tange à dependência tecnológica, em processos de contratação de recursos de armazenamento e modelos de processamento analítico em Nuvem Pública, as áreas técnicas são obrigadas a redigir e estipular obrigações através de um "Plano de Saída" no Termo de Referência, garantindo de antemão estratégias de descontinuidade amigável e repatriação de acervos sem a incidência de bloqueios mercadológicos arbitrários (*vendor lock-in*) no ocaso contratual.
   - **Gabarito:** CERTO. Exigência pétrea da mitigação de riscos governamentais, o plano de transição (ou de saída) obriga e vincula juridicamente que o fornecedor assegure a interoperabilidade, a extração universal em formatos irrestritos e colabore na migração dos dados sistêmicos para outra solução, inibindo as amarras de exclusividade lesivas do *vendor lock-in*.

5. **(CEBRASPE - Inédita / CGU)** Em levantamentos preliminares e na pesquisa sistemática de preços (IN 65/2021), a identificação de disparidades evidentes com valores superlativamente incompatíveis (*outliers*) deve ser reavaliada mediante adoção exata das metodologias matemáticas, suprimindo os valores distorcidos da composição amostral para o apuramento justo do menor preço, média ou mediana aplicável à estimativa de gastos do edital.
   - **Gabarito:** CERTO. É diretriz basilar da pesquisa mercadológica pública que os gestores façam análise crítica (*outliers*), desconsiderando cotações com preços impraticavelmente diminutos (inexequíveis) ou desarrazoadamente inflacionados face aos padrões correntes das aquisições estatais equivalentes, expurgando as margens ilógicas visando orçar a licitação por parâmetros da modicidade.

---

## Glossário

- **API (Application Programming Interface):** Ponto de acesso em rede utilizado em MLOps (via REST ou gRPC) para consumir predições de um modelo isolado na nuvem.
- **CapEx (Capital Expenditure):** Despesas concentradas em investimentos iniciais pesados, como aquisições definitivas de clusters físicos (CPUs/GPUs).
- **DFD (Documento de Formalização da Demanda):** O preâmbulo do processo de aquisições no qual o setor atesta e fundamenta o problema organizacional ou ineficiência enfrentada.
- **Egress Costs:** As incidências financeiras cumulativas de rede provocadas pela remessa volumosa de dados hospedados num Data Lake público para um repositório alheio.
- **ETP (Estudo Técnico Preliminar):** Momento preparatório no qual equipes diagnosticam a exata viabilidade técnica, definem as alternativas do setor privado, dimensionam necessidades e apuram o TCO.
- **Kanban:** Arcabouço operacional focado no balanceamento e na extração desobstruída do valor, que atua restringindo a carga laboral paralela (*Work In Progress*), dispensando Sprints.
- **MLflow:** Plataforma basilar em sistemas modernos que rastreia os ensaios, empacota os algoritmos e hospeda o ciclo dos modelos em produção (*Model Registry*).
- **OpEx (Operational Expenditure):** Classificação do dispêndio contínuo com taxas, pagamentos mensais (SaaS/PaaS) e utilidades, típico da terceirização via Cloud Computing.
- **TR (Termo de Referência):** A "bula" licitatória confeccionada para definir padrões técnicos, métricas restritivas do serviço (SLA), multas e obrigações da fiscalização estatal.
- **Wasserstein (Distância de):** Cálculo robusto na gestão de data drift capaz de quantificar o nível exato de esforço matemático necessário para igualar as curvas das distribuições originais e novas.

---

## Mapa Mental

- **Bloco 4: Operação, Governança e Gestão de Dados/IA (CGU)**
  - **1. Ciclo de Vida e MLOps**
    - Versionamento Dimensional: Dados (DVC), Código (Git), Modelos (MLflow Registry).
    - Pipelines Estruturados: CI (Código e Qualidade de Dados), CD (Deploy Contínuo), CT (Retreinamento).
    - Estratégias de Disponibilização API: Blue-Green vs Canary Deployment (Exposição Gradual).
    - Anomalias (Drift):
      - Data Drift: Desvio estatístico nas variáveis de entrada (Usa PSI, Teste KS, Wasserstein).
      - Concept Drift: Modificação relacional entre Variável Independente e Alvo (Exige Ground Truth e recálculo de acurácia).
  - **2. Sustentação de Soluções**
    - Arquiteturas: Contratação de Serviços em Nuvem (Managed Services) vs Operação em Datacenter (On-Premise).
    - Balanço Econômico: Investimento Bruto (CapEx) vs Custo Variável/Assinaturas (OpEx).
    - Ameaças: Vendor Lock-in e Tarifas Invisíveis na Nuvem (Ex.: Egress Costs).
    - Observabilidade: Além de checar servidores (Monitoramento). Envolve Métricas, Traces, e Logs.
    - Segurança Estrutural: Gerenciadores Dinâmicos de Segredos (Vaults), RBAC, Não usar senhas no código (Hardcoded).
  - **3. Governança e Direitos Civis**
    - Parâmetros e Normas: NBR ISO/IEC 42001 (Sistema de Gestão de IA).
    - Painel do SISP (Governo): AIE (Autoavaliação de Impacto Ético), Matriz de Papéis (RACI) e Ficha Transparente do Sistema.
    - LGPD (Art. 20): Direito perpétuo à Revisão de Decisão Automatizada que restrinja direitos.
    - Regulação Iminente (PL 2338/23 - Marco da IA):
      - Risco Excessivo: Aplicações ilícitas/vedadas.
      - Alto Risco: Avaliação algorítmica profunda, previsão de Revisão expressamente Humana.
  - **4. Gestão Ágil e Produto**
    - Guias Federativos: PDTIC (Tático e TI), PTD (Serviços e Cidadão), PDA (Transparência Ativa, formatos abertos).
    - Framework Scrum: Entregas fixadas pelo relógio (Timeboxed Sprints), Papéis impositivos.
    - Metodologia Kanban: Foco puramente direcional na Vazão, Limitando o trabalho em andamento (WIP) nas colunas do quadro.
  - **5. Contratos na Administração Pública (Lei 14.133 / IN 94)**
    - Fases de Planejamento:
      - DFD: Levantamento do problema.
      - ETP: Investigação das alternativas, TCO Comparativo, Viabilidade técnica.
      - TR: Construção contratual, exigências operacionais e imposição do Nível de Serviço.
    - Contratação Direta: Inexigibilidade (Falta fática de competição) vs Dispensa (Pequena urgência ou valor delimitado).
    - Fiscalização Operacional: Exigência imperiosa de Pagamento por Resultados/Entregas Verificáveis.
    - Blindagem (Continuidade): Oposição ao Lock-in exigindo da empresa um Plano de Saída (Devolução plena dos códigos encomendados e dos bancos de dados).
