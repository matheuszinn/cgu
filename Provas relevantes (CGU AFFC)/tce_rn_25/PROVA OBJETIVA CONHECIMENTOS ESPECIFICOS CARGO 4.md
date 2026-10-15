---
tipo: prova
concurso: "tce_rn_25"
arquivo_origem: "Provas Cebraspe/tce_rn_25/PROVA OBJETIVA CONHECIMENTOS ESPECIFICOS CARGO 4.pdf"
tags:
  - prova
  - cebraspe
  - cgu-2026
---

# PROVA OBJETIVA CONHECIMENTOS ESPECIFICOS CARGO 4

## CONHECIMENTOS ESPECÍFICOS

_Julgue os próximos itens, relativos aos dados estruturados e não estruturados, à ingestão e armazenamento de grande quantidade de dados e aos bancos de dados NoSQL. Bancos de dados NoSQL são projetados para garantir, por padrão, consistência forte (strong consistency), priorizando a integridade imediata dos dados em ambientes distribuídos._

**52** Dados estruturados são organizados segundo um esquema rígido previamente definido, enquanto dados não estruturados não possuem modelo predefinido, sendo tipicamente armazenados em formatos como textos livres, imagens e vídeos.

**53** Em arquiteturas de Big Data, dados não estruturados não podem ser indexados ou consultados diretamente, sendo obrigatória sua transformação em dados estruturados antes de qualquer análise.

**54** Em sistemas NoSQL orientados a documentos, como MongoDB, os dados são armazenados em estruturas flexíveis que permitem variação de esquema entre registros de uma mesma coleção. No que diz respeito a projetos e processos de software, julgue os itens a seguir. No catálogo GoF, o padrão de criação Singleton garante que haja somente uma instância para cada classe, com um único ponto de acesso a ela. Enquanto o foco do processo incremental é aprimorar o que já foi entregue, o objetivo do processo iterativo é entregar nova funcionalidade. A primeira etapa de um projeto de software consiste na definição do time que irá trabalhar no desenvolvimento técnico. Na fase de levantamento de requisitos de um projeto, as motivações informais da organização devem ser consideradas pelo gerente do projeto. A ingestão de dados em streaming não é adequada para cenários que exigem alta confiabilidade, pois não permite mecanismos de tolerância a falhas ou reprocessamento de eventos.

**56** Sistemas de armazenamento distribuído, como data lakes, permitem o armazenamento de dados em seu formato bruto, favorecendo abordagens ELT em detrimento de ETL.

_No que se refere a práticas ágeis e a licitação e gerenciamento de requisitos de desenvolvimento, julgue os próximos itens. Um dos objetivos do método Kanban é colocar a maior quantidade possível de itens em andamento, aumentando a capacidade de entrega do time de desenvolvimento. A metodologia Scrum determina que a duração de uma sprint é inalterável, mesmo que todos os itens previstos ainda não estejam finalizados._

_De acordo com o conceito INVEST, as histórias de usuário devem ser independentes, negociáveis, pequenas e testáveis. Na estrutura de um storytelling, o clímax e o desfecho ocorrem no mesmo momento, ao final da narrativa._

_Acerca da integridade referencial, da linguagem de manipulação de dados (DML) e da otimização de performance em larga escala, julgue os itens subsequentes. A instrução UPDATE pode ser utilizada em conjunto com subconsultas correlacionadas para modificar dados com base em valores provenientes de outras tabelas, respeitando as restrições de integridade definidas no banco de dados._

**58** A utilização de índices compostos garante melhoria uniforme de desempenho para qualquer consulta que envolva pelo menos uma das colunas indexadas, independentemente da ordem dos atributos no índice.

**59** O particionamento de tabelas elimina a necessidade de índices secundários, pois a divisão física dos dados já garante acesso eficiente em qualquer tipo de consulta.

**60** Em ambientes de alta concorrência, a definição de restrições de chave estrangeira garante que operações de inserção e de atualização ocorram com menor custo computacional, pois o SGBD utiliza essas restrições para simplificar as verificações de consistência. A integridade referencial garante que valores de chave estrangeira em uma tabela correspondam a valores válidos de chave primária em outra tabela, evitando a existência de registros órfãos. A execução de comandos DML, como UPDATE e DELETE, sem cláusula WHERE pode resultar em operações em massa que afetam toda a tabela, podendo comprometer a integridade lógica dos dados.

_A respeito de testes e métricas de software e de DevOps, julgue os itens subsequentes. O uso de mocks é recomendado para testes de unidade, mas deve ser evitado para testes de integração, para garantir a comunicação com todos os serviços acessados. Throughput e Velocity são duas métricas de software que identificam a quantidade absoluta de itens entregues em determinado período de tempo. O processo de deployment blue/green utiliza dois ambientes de produção com as mesmas configurações, o que permite um método de implantação de baixo risco. Sob o mesmo namespace, diversos contêineres Docker podem ser executados e interagir entre si, com compartilhamento local de dados._

_Julgue os itens a seguir, a respeito de bancos de dados relacionais, modelagem dimensional e análise de dados. Em um data warehouse, o armazenamento orientado à transação não necessita de múltiplas operações de entrada e saída para carregar dados no banco de dados. É chamado de esquema estrela o conjunto formado por uma tabela de fatos, várias tabelas de dimensão e chaves estrangeiras que relacionam dados da tabela de fatos aos dados das tabelas de dimensão._

_Acerca de técnicas para pré-processamento de dados, CRISP-DM, análise de grupamento, detecção de anomalias e regras de associação, julgue os próximos itens._

**77** No contexto de regras de associação, o conceito de confiança refere-se à expectativa de que um dado, grupo ou banco de dados atue da maneira esperada em dada situação.

**78** O k-means é um algoritmo iterativo de agrupamento baseado em centroides, isto é, ele divide um conjunto de dados em grupos semelhantes com base na distância entre seus centroides.

**79** Em mineração de dados, dado ruidoso é aquele cujo valor está fora do domínio do atributo.

**80** Na metodologia CRISP-DM, a preparação dos dados serve para limpá-los, tratando valores ausentes, outliers e inconsistências.

**81** Uma anomalia é um valor discrepante, ou seja, um valor que se localiza significativamente distante dos valores considerados normais.

_No que se refere à classificação da mineração de dados, à mineração de texto, à modelagem preditiva e à visualização e análise exploratória de dados, julgue os itens subsecutivos._

**82** Histograma é uma representação da distribuição dos dados de certa base, conforme um ou mais atributos desses dados, por meio de um gráfico de barras.

**83** Enquanto um falso positivo é um erro do tipo 2, um falso negativo é um erro do tipo 1.

**84** Em um processo de mineração de texto, a tokenização é o processo de dividir textos longos em palavras individuais, removendo-se espaços e pontuação, para fins de identificação da frequência de termos ou da estrutura de uma frase em um grande volume de documentos.

**85** Modelos de regressão linear são métodos estocásticos para modelagem da relação entre variáveis aleatórias e uma função polinomial.

_Julgue os itens que se seguem, a respeito de ferramentas de apoio à análise de dados._

**86** Considere o seguinte código em Python. Com relação ao aprendizado de máquina, à IA generativa e às redes neurais e deep learning, julgue os próximos itens. Modelos de IA generativa, como os baseados em arquiteturas transformer, são capazes de produzir novos dados a partir de padrões aprendidos durante o treinamento. Em modelos de deep learning, o overfitting ocorre quando o modelo possui baixa capacidade de representação, sendo raro em redes neurais profundas com muitos parâmetros. Redes neurais profundas diferenciam-se das redes neurais rasas principalmente pela presença de múltiplas camadas ocultas, permitindo maior capacidade de representação. Em algoritmos de aprendizado de máquina, a validação cruzada (cross-validation) é utilizada para aumentar o conjunto de treinamento ao duplicar os dados disponíveis, elevando assim a capacidade de generalização do modelo.

_Julgue os próximos itens, relativos às MLOps, interpretabilidade de modelos e ao viés algorítmico. Em pipelines de MLOps, a automação de testes, de monitoramento e de re-treinamento contínuo contribui para a confiabilidade e para a escalabilidade dos sistemas de ML. A mitigação de viés em modelos de IA pode envolver técnicas como balanceamento de dados, regularização e avaliação de métricas de equidade. Modelos altamente interpretáveis, como árvores de decisão simples, tendem a apresentar menor transparência em comparação a modelos complexos, como redes neurais profundas._

_Julgue os itens subsequentes, relativos a padrões arquiteturais e padrões de projeto. Diferentemente das arquiteturas tradicionais de N camadas, a arquitetura de microsserviços se baseia na descentralização da gestão de dados, em que cada serviço deve, idealmente, possuir sua própria base de dados, de forma a garantir a independência de implantação e o baixo acoplamento. A adoção de uma estratégia de camadas fechadas (closed layers) permite que a camada de apresentação acesse diretamente os serviços da camada de dados quando houver necessidade de otimização de performance, desde que a camada de negócio permaneça inalterada. No padrão arquitetural MVC (model-view-controller), o componente controller atua como um intermediário que interpreta as entradas enviadas pelo usuário e coordena as atualizações necessárias no model, de forma a permitir que a lógica de negócio e o estado dos dados permaneçam independentes da interface de apresentação. import numpy as np S = np.array([45, 55]) U = np.array([[12, 22, 33], [45, 55, 66]]) print((U.T + S).T) A execução desse código resultará no erro a seguir. NameError: name 'T' is not defined O PROC SQL integra o software Base SAS e pode ser usado com qualquer conjunto de dados SAS._

**88** Considere o trecho de código a seguir, em linguagem R.

**1** m <- matrix(1:9, nrow = 3, ncol = 3, byrow = TRUE)

**2** result <- rowMeans( m)+colMeans( m)

**3** print(result) A execução desse trecho de código terá o seguinte resultado. [1] 6 10 14 Em tabelas dinâmicas de planilhas eletrônicas, a área de valores corresponde à área em que se devem colocar os campos em que se pretende efetuar cálculos como soma, contagem de valores, média aritmética, entre outros. à

**100** No padrão de projeto abstract factory, a inclusão de uma nova categoria de objeto em uma família de produtos já existente prescinde da alteração da interface da fábrica abstrata e de suas subclasses concretas.

_Acerca de integração de sistemas, serviços web e arquiteturas modernas, julgue os itens que se seguem._

**101** No que se refere ao desenvolvimento de soluções mobile baseadas em padrões W3C, a arquitetura de uma PWA (progressive web app) utiliza service workers para atuar como um proxy de rede programável de forma a permitir que o usuário mobile acesse funcionalidades críticas da aplicação mesmo em cenários de latência elevada ou ausência de conectividade.

**102** O framework gRPC adota o formato JSON como padrão nativo de serialização de dados, o que assegura a interoperabilidade direta com navegadores web.

**103** Nas arquiteturas cloud native, o isolamento provido pelo uso de containers permite que falhas em serviços individuais sejam mitigadas pela substituição automática das instâncias comprometidas.

_Julgue os itens seguintes, relativos a COBIT 2019, ISO 31000, COSO e ITIL v4._

**104** A ISO 31000:2018 promove uma compreensão compartilhada dos riscos, e suas diretrizes ajudam a incorporar o gerenciamento de riscos na governança, estratégia, planejamento, processos de relatórios, políticas, valores e cultura de uma organização.

**105** O COBIT 2019 contribui para que as organizações atinjam seus objetivos de negócios por meio de uma gestão de TI eficaz, entretanto, como não inclui estruturas de auditoria com vistas ao controle de governança de TI, faz-se necessária a utilização da COSO no que diz respeito a aspectos concernentes à auditoria.

**106** A prática de gerenciamento de continuidade de serviço do ITIL v4 fornece estrutura para a construção de resiliência organizacional com a capacidade de produzir uma resposta em caso de desastre, visando garantir que a disponibilidade e o desempenho de um serviço sejam mantidos em níveis suficientes após um evento súbito não planejado que cause danos ou perdas graves.

_Julgue os próximos itens, referentes a SCRUM, PMBOK 7.ª edição e planejamento estratégico de TI._

**107** Um KPI (key performance indicator) é um valor mensurável que se relaciona com metas, objetivos e estratégias específicas que ajudam a avaliar o desempenho de tarefas em uma organização.

**108** De acordo com o Guia SCRUM (versão 2020), a sprint planning inicia a sprint ao definir o plano de trabalho do que será realizado na sprint, na qual, para cada para cada item do product backlog selecionado, o product owner planeja o trabalho e a forma necessária para criar um incremento que atenda à definição de pronto.

**109** Conforme o disposto no PMBOK 7.ª edição, o domínio de desempenho da entrega trata das atividades e funções associadas a riscos, que incluem aspectos afetos à incerteza e suas implicações, sendo a capacidade de antecipar ameaças e de compreender as consequências dos problemas um dos objetivos esperados da execução desse domínio.

**110** Considere que as fases que compõem o processo de elaboração de certo plano diretor de TIC (PDTIC) sejam preparação, diagnóstico e planejamento. Considere, ainda, que se pretenda realizar a análise dos ambientes interno e externo da TIC por meio do método SWOT. Nesse caso, a atividade pretendida deve ser executada na fase de diagnóstico e, para o ambiente interno, podem ser analisados a qualidade dos processos e serviços providos e o nível de satisfação dos usuários com os serviços prestados.

_Julgue os itens a seguir, que se referem à cibersegurança e continuidade de negócios, ao disposto na Lei Geral de Proteção de Dados Pessoais (LGPD), e à governança de dados por meio da metodologia do DAMA-DMBoK._

**111** De acordo com o DAMA‐DMBoK, a modelagem de dados é o processo de descoberta, análise e delimitação dos requisitos de dados de forma iterativa, podendo incluir modelo conceitual, lógico e físico, de forma a representar e comunicar esses requisitos de dados.

**112** A função recuperar do CSF (Cybersecurity Framework) do NIST visa apoiar a capacidade de contenção dos efeitos de incidentes de cibersegurança, incluindo, entre outras ações, o gerenciamento de incidente, que, por sua vez, abrange análise e mitigação do incidente.

**113** Consoante disposto na norma ABNT NBR ISO/IEC 27002:2022, anonimização consiste na alteração irreversível de dados pessoais de forma tal que o titular dos dados não pode mais ser identificado direta ou indiretamente; consoante o disposto na LGPD, anonimização consiste na utilização de meios técnicos por meio dos quais um dado perde a possibilidade de associação, direta ou indireta, a um indivíduo.

_A respeito de gestão de contratação de soluções de TI, julgue os próximos itens._

**114** Ao final do contrato, os módulos implementados serão de propriedade da empresa contratada, que poderá repassar, mediante compensação financeira, os direitos de propriedade intelectual para o contratante.

**115** Na administração estadual, o gestor de contrato pode ser auxiliado, no cumprimento das atribuições do cargo, por recursos terceirizados.

**116** A menos que esteja expresso de forma diferente no edital, os testes e demais provas exigidos por normas técnicas são de responsabilidade do contratante, quando entidade pública.

_No que se refere à legislação aplicável à contratação de bens e serviços de TI, julgue os itens seguintes._

**117** Estão entre os critérios de julgamento no modelo de licitação por concorrência: menor preço, melhor técnica, maior retorno econômico.

**118** Para fins de obtenção de preço estimado, a Instrução Normativa SEGES/ME n.º 65/2021 estipula como único método o cálculo da média a partir de um conjunto de três ou mais preços.

**119** Nos termos da Instrução Normativa SGD/ME n.º 94/2022, na renovação de centro de dados, deve-se priorizar a contratação de serviços em nuvem.

**120** Em contratações que envolvam recursos de cooperação estrangeira, serão admitidas condições decorrentes de acordos internacionais desde que aprovadas pelo presidente da República.
