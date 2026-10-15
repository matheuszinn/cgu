---
tipo: prova
concurso: "funpresp_26_jud"
arquivo_origem: "Provas Cebraspe/funpresp_26_jud/PROVA OBJETIVA CONHECIMENTOS ESPECIFICOS EMPREGO 9.pdf"
tags:
  - prova
  - cebraspe
  - cgu-2026
---

# PROVA OBJETIVA CONHECIMENTOS ESPECIFICOS EMPREGO 9

## CONHECIMENTOS ESPECÍFICOS

_Acerca da modelagem estatística de dados, julgue os itens a seguir._

**51** Em séries temporais, a ordem temporal dos dados pode ser ignorada sem prejuízo para a modelagem, desde que a amostra seja grande.

**52** A normalização pode ser útil em etapas de preparação de dados, especialmente quando variáveis estão em escalas muito diferentes.

**53** Testes t e F em regressão linear dependem, em sua formação clássica, da validade da estrutura de variância assumida pelo modelo.

**54** Na regressão linear simples estimada pelo método dos mínimos quadrados ordinários, o coeficiente β1 minimiza a soma dos quadrados dos resíduos.

**55** Em regressões múltiplas, a presença de multicolinearidade perfeita melhora a precisão dos coeficientes, pois aumenta a informação disponível ao modelo.

_Julgue os itens subsequentes, em relação à modelagem de bancos de dados._

**56** Em modelagem de dados, a terceira forma normal exige que todo atributo não-chave seja dependente apenas da chave primária, o que a torna igualmente adequada tanto para sistemas transacionais quanto para ambientes analíticos.

**57** O esquema snowflake apresenta melhor desempenho que o esquema estrela em ambientes OLAP, porque a normalização das dimensões reduz redundância e diminui o tempo de resposta das consultas analíticas.

**58** Em um esquema estrela, a tabela-fato contém, predominantemente, descrições textuais detalhadas dos clientes, enquanto as dimensões armazenam métricas numéricas agregadas.

**59** Em um esquema estrela, toda tabela-fato deve conter pelo menos uma medida numérica, pois sem ela não há como estabelecer relacionamento com as dimensões.

**60** Em um esquema estrela, alterar o grão da tabela-fato implica redefinir o nível de detalhe de cada linha, o que pode exigir revisão das dimensões associadas e impactar a granularidade das análises.

**61** O uso de slowly changing dimensions do tipo 2 em um esquema estrela permite rastrear o histórico de alterações em uma dimensão, inserindo uma nova linha a cada mudança e mantendo as linhas antigas para preservar a consistência das análises históricas.

_A respeito do desenvolvimento de projetos digitais e do machine learning, julgue os itens subsecutivos._

**62** Em regra, em algoritmos de gradient boosting, quanto maior o número de estimadores usados, menor o erro de generalização do modelo, pois cada árvore adicionada corrige os erros residuais da anterior.

**63** Em projetos digitais, o escopo pode ser definido integralmente após a implementação, pois a fase de planejamento é dispensável em metodologias ágeis.

**64** Algoritmos não supervisionados identificam agrupamentos ou estruturas ocultas nos dados sem a necessidade de rótulos prévios, operando exclusivamente sobre as observações.

**65** Em validação cruzada k-fold, o modelo é treinado k vezes, cada vez usando uma partição diferente como conjunto de teste, o que produz uma estimativa mais robusta do erro de generalização do que uma única divisão treino-teste.

_Em relação à manipulação e à limpeza de dados para fins de análise quantitativa e às linguagens de programação adequadas para essa tarefa, julgue os itens que se seguem. Em Python, a biblioteca Plotly gera visualizações baseadas em HTML e JavaScript, o que permite interatividade nativa no navegador, sem dependência de servidor ativo, diferentemente de dashboards construídos com Dash, que requerem um processo servidor em execução para processar as interações do usuário e atualizar componentes reativamente. Em Python, a operação de merge entre dois DataFrames da biblioteca Pandas realiza, por padrão, um inner join, descartando registros sem correspondência em ambas as chaves; quando há valores ausentes nas colunas de junção, essa biblioteca os trata como valores iguais entre si, preservando esses registros no resultado final. Uma instituição pública estruturou a sua nova arquitetura de dados em duas camadas operacionais. A primeira camada é dedicada ao BI (business intelligence) corporativo, operando sobre um data warehouse centralizado, cujos dados estruturados são consumidos por meio de painéis interativos desenvolvidos em Power BI e Tableau, constituindo a base do seu sistema de suporte à decisão (SSD). A segunda camada é voltada para o data analytics avançado, em que cientistas de dados utilizam as linguagens Python e R para extrair insights preditivos e processar grandes volumes de dados não estruturados provenientes de redes sociais e sensores._

_Com base nessa situação hipotética e nos conceitos técnicos de business intelligence, sistemas de suporte a decisão e ferramentas de análise de dados, julgue os itens a seguir. No contexto do sistema de suporte à decisão da arquitetura proposta, as ferramentas de gestão de conteúdo são alocadas na primeira camada com a função técnica de estruturar e modelar os dados relacionais numéricos armazenados no data warehouse. Na segunda camada da arquitetura, a execução de algoritmos preditivos nos processos de data analytics, em linguagens como Python e R, está subordinada ao resultado dos processos de business intelligence. Na primeira camada descrita, o funcionamento dos painéis de business intelligence fundamenta-se na estruturação multidimensional do data warehouse para viabilizar o processamento analítico de dados. Na primeira camada descrita, a operacionalização dos painéis em ferramentas como Power BI e Tableau permite integrar as informações do data warehouse central a múltiplas fontes de dados externas. Na arquitetura estabelecida, a camada voltada ao data analytics caracteriza-se pela natureza focada na análise descritiva e diagnóstica._

_No que se refere às metodologias de inovação e ao desenvolvimento de soluções centradas no usuário, julgue os itens subsequentes._

**73** Na estruturação da transformação digital, o design thinking estabelece que o mapeamento e a adoção de tecnologias disruptivas devem ser o ponto de partida da ideação.

**74** No design de produto, a pesquisa em UX foca em questionar diretamente os usuários acerca das funcionalidades e o projeto das interfaces desejadas.

**75** As métricas de uso na avaliação da experiência do usuário (UX) fornecem dados essenciais para a análise das consequências das ações que os usuários realizam, embora sejam insuficientes para explicar os motivos que as fundamentam.

_Julgue os itens subsequentes, relativos a metodologias ágeis, a ferramentas de gestão de projetos, e a estratégias de comunicação e marketing em ambientes digitais._

**76** A adoção de ferramentas baseadas em quadros ágeis, como o Trello e o Planner, para a gestão de estratégias de comunicação e marketing em mídias digitais parte da premissa de que o escopo das campanhas seja definido de forma completa já na fase de planejamento.

**77** No contexto do marketing em mídias digitais, a adoção de estratégias de segmentação que priorizam nichos específicos de audiência, em detrimento de abordagens massificadas, constitui uma técnica eficaz para direcionar ações e otimizar o engajamento do público-alvo.

**78** No âmbito do framework Scrum, o scrum master atua como a autoridade responsável por distribuir as tarefas técnicas entre os desenvolvedores e monitorar o cumprimento do cronograma diário para garantir o atingimento da meta da sprint.

**79** Na aplicação do método Kanban, a limitação do trabalho em progresso (WIP – work in progress) é uma prática fundamental que visa evitar a sobrecarga da equipe e evidenciar gargalos, promovendo a melhoria contínua do fluxo de entrega de valor.

**80** Na gestão ágil, a metodologia Kanban transcende a gestão visual de tarefas, operando como um sistema para projetar o fluxo de valor, controlar o trabalho em progresso e medir a eficiência técnica.

**81** Nas estratégias de comunicação corporativa, a aplicação técnica do storytelling pressupõe a substituição da exibição exaustiva e neutra de painéis quantitativos em favor de uma narrativa analítica estruturada.

_Acerca dos conceitos de segurança da informação, julgue os itens a seguir._

**82** O princípio da disponibilidade garante que somente usuários previamente autorizados possam alterar informações armazenadas em um sistema.

**83** A confidencialidade está associada à prevenção do acesso não autorizado à informação.

_No que se refere aos tipos de ataques na perspectiva de segurança da informação, julgue os próximos itens._

**84** O tipo de ataque em que um agente malicioso captura uma comunicação válida e a retransmite posteriormente é denominado replay attack.

**85** Ataques DDoS caracterizam-se pela exploração única de vulnerabilidades de autenticação para obtenção de acesso privilegiado ao sistema-alvo.

_Considerando técnicas de controle de acesso e seus respectivos mecanismos, julgue os itens que se seguem._

**86** A assinatura digital com uso de nonce garante a confidencialidade da mensagem transmitida.

**87** O controle de acesso baseado em papéis (RBAC) associa permissões a funções organizacionais, permitindo que usuários herdem privilégios conforme os papéis que lhes são atribuídos.

_No que se refere a não repúdio, julgue os itens subsecutivos._

**88** O não repúdio visa impedir que uma entidade negue, posteriormente, a autoria de uma ação ou o envio/recebimento de uma mensagem previamente realizada.

**89** Em criptografia assimétrica, a cifragem de uma mensagem com a chave pública do destinatário é suficiente para garantir não repúdio acerca do envio da mensagem.

_Julgue os itens a seguir, relativos a controle de acesso._

**90** No modelo de controle de acesso mandatório (MAC), as permissões são definidas unicamente pelo proprietário do recurso e são independentes de políticas centrais de classificação.

**91** No controle de acesso discricionário (DAC), um usuário com permissões adequadas pode, em determinadas implementações, delegar o acesso a objetos sob sua responsabilidade. No que diz respeito aos fundamentos e às características de segurança física e de segurança lógica, julgue os itens subsequentes.

**92** A segmentação lógica de redes por VLAN reduz a superfície de exposição entre grupos de ativos, mas não supre, por si só, a necessidade de controles adicionais, como mecanismos de filtragem e políticas de controle de tráfego.

**93** O princípio de defesa em profundidade aplicado à segurança física pode envolver camadas sucessivas de proteção, como perímetro controlado, autenticação de acesso e monitoramento ambiental.

**94** Em ambientes de alta criticidade, a implementação de CCTV suprime a necessidade de controles complementares de acesso físico, por permitir monitoramento contínuo das instalações.

_Acerca do tratamento de dados pessoais no poder público, julgue os itens seguintes._

**95** No setor público, haja vista que a publicidade é a regra geral disposta na Lei de Acesso à Informação (LAI), os órgãos e entidades ficam desobrigados de realizar a análise de riscos ou de adotar salvaguardas sobre os dados pessoais cuja divulgação decorra do interesse público.

**96** A infração às normas da LGPD por agente público pode ensejar a sua responsabilização administrativa de forma pessoal e autônoma, com fundamento na Lei de Introdução às Normas do Direito Brasileiro (LINDB).

**97** Visando à execução de políticas públicas, os órgãos estatais devem manter os dados pessoais tratados em formato interoperável e estruturado, observando os princípios de proteção à privacidade dos titulares.

**98** Diferentemente do princípio da transparência, que exige uma postura ativa do controlador de disponibilizar as informações independentemente de solicitação do titular, o princípio do livre acesso foca na obrigatoriedade de o agente fornecer mecanismos para que o titular possa solicitar e consultar informações sobre o tratamento de seus próprios dados.

**99** A base legal do legítimo interesse pode ser aplicada para fundamentar o tratamento de dados pessoais sensíveis.

_Em relação à Lei n.º 13.709/2018 (Lei Geral de Proteção de Dados Pessoais - LGPD), julgue os itens a seguir._

**100** De acordo com a LGPD, os agentes de tratamento devem adotar medidas de segurança para proteger os dados pessoais contra acessos não autorizados e situações acidentais de destruição ou perda.

**101** A LGPD estabelece um tempo máximo — padrão e obrigatório — pelo qual os dados pessoais podem ficar armazenados por qualquer empresa ou setor.

**102** A organização que realiza o tratamento de dados pessoais deve restringir a coleta ao mínimo indispensável para o alcance da finalidade proposta, sendo-lhe vedado o tratamento de dados que se revelem excessivos ou desproporcionais ao objetivo do serviço.

**103** No ambiente virtual, considera-se lícita a coleta do consentimento do titular por meio de caixas de seleção (checkboxes) previamente marcadas, desde que seja garantido ao usuário o direito de desmarcá-las em caso de discordância.

**104** Além de atuar como um controle de segurança dissuasivo, a auditoria automatizada viabiliza o cumprimento da obrigação legal imposta pela LGPD aos agentes de manter o registro da ampla variedade de operações que constituem o tratamento de dados pessoais.

**105** Com base nas disposições da LGPD para a coleta de dados via web, a revogação do consentimento por parte do titular invalida retroativamente as operações de tratamento de dados que foram realizadas sob o amparo da autorização anterior.

_A respeito dos princípios do privacy by design, julgue os itens subsequentes._

**106** De acordo com o princípio da privacidade como configuração padrão (privacy by default), as medidas de proteção aos dados do indivíduo devem ser aplicadas de forma automática pelo sistema, sem a necessidade de qualquer ação proativa por parte do usuário.

**107** O princípio da funcionalidade total (soma positiva) do privacy by design estabelece que a segurança tecnológica e a eficiência de um negócio exigem, em cenários complexos, o sacrifício parcial da privacidade do usuário.

_Julgue os próximos itens, relativos aos conceitos e aos principais tipos e modelos de inteligência artificial (IA)._

**108** Em arquiteturas transformer utilizadas em grandes modelos de linguagem (LLMs), o mecanismo de atenção realiza processamento sequencial dos tokens durante o treinamento do modelo.

**109** A inteligência artificial simbólica baseia-se predominantemente em regras lógicas e na representação explícita do conhecimento para resolver problemas computacionais.

**110** O aprendizado por reforço caracteriza-se pela inexistência de mecanismos de recompensa durante o treinamento do agente inteligente.

**111** Redes neurais artificiais profundas são estruturas computacionais inspiradas no funcionamento biológico do cérebro humano e podem conter múltiplas camadas ocultas.

**112** Sistemas especialistas são exemplos de IA fraca, projetados para executar tarefas específicas dentro de um domínio delimitado.

_Acerca do armazenamento de Big Data, do pipeline de dados e dos conceitos de data lake, julgue os itens subsequentes._

**113** Em pipelines de dados, a etapa de transformação pode incluir limpeza, padronização e enriquecimento dos dados processados.

**114** Data lake é uma arquitetura destinada ao armazenamento exclusivo de dados estruturados, previamente organizados em tabelas relacionais.

**115** Em ambientes de Big Data, sistemas distribuídos de armazenamento permitem o processamento de grandes volumes de dados em múltiplos nós computacionais.

**116** Em pipelines de dados, a etapa de ingestão corresponde ao processo de eliminação permanente dos dados de origem após o carregamento no ambiente analítico.

**117** O armazenamento orientado a objetos é incompatível com data lakes devido à natureza dos dados armazenados. Com relação aos sistemas de arquivos distribuídos e aos sistemas de indexação, julgue os próximos itens.

**118** Em projetos de ciência de dados, sistemas de arquivos distribuídos permitem armazenar grandes volumes de dados utilizados em treinamento de modelos analíticos e de aprendizado de máquina.

**119** Em ambientes analíticos de ciência de dados, índices compostos podem apresentar melhor desempenho em consultas multidimensionais quando a ordem dos atributos indexados possui aderência aos padrões de filtragem utilizados nas consultas.

**120** Sistemas de indexação impedem variações de desempenho em consultas analíticas, independentemente do volume de dados armazenados. Espaço livre
