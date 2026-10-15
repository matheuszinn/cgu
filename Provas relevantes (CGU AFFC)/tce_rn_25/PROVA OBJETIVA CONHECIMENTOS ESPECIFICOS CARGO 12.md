---
tipo: prova
concurso: "tce_rn_25"
arquivo_origem: "Provas Cebraspe/tce_rn_25/PROVA OBJETIVA CONHECIMENTOS ESPECIFICOS CARGO 12.pdf"
tags:
  - prova
  - cebraspe
  - cgu-2026
---

# PROVA OBJETIVA CONHECIMENTOS ESPECIFICOS CARGO 12

## CONHECIMENTOS ESPECÍFICOS

_Julgue os itens a seguir, relativos a cloud computing e virtualização, a conteinerização de aplicações, a endereçamento e protocolos da família TCP/IP e a tecnologias de armazenamento NAS e SAN._

**51** O cabeçalho-base do IPv6 tem tamanho fixo e foi simplificado em relação ao IPv4, com as informações opcionais sendo transferidas para cabeçalhos de extensão.

**52** Em soluções de armazenamento, a arquitetura SAN atua no nível de arquivo, enquanto a arquitetura NAS atua no nível de bloco.

**53** No Kubernetes, um Pod só pode executar um único contêiner, impossibilitando-se o compartilhamento nativo de recursos de rede e armazenamento.

**54** No modelo IaaS, o consumidor pode instalar e gerir os sistemas operativos e as aplicações, mas a infraestrutura física da nuvem continua sob responsabilidade do fornecedor. Sabendo-se que, no contexto da implementação de uma arquitetura de Big Data, o uso de um data lake distribuído para o armazenamento de dados brutos favorece a escalabilidade horizontal e a flexibilidade de esquemas, a adoção de formatos de arquivo colunares, como o Apache Parquet, é uma prática recomendada para otimizar a performance de leitura e reduzir o consumo de armazenamento por meio de técnicas de compressão e codificação eficientes. Um tribunal de contas implementou um data lake para auditoria contínua de contratos administrativos, utilizando ingestão incremental via CDC (change data capture). Os dados são armazenados na tabela contratos_cdc, que contém múltiplas versões de registros ao longo do tempo. A tabela

_Acerca de fundamentos de Linux, de criptografia, de noções de roteamento e switching e de segurança em redes de computadores e dispositivos de proteção, julgue os itens a seguir._

**55** Para assegurar a confidencialidade de um documento por meio de criptografia assimétrica, o remetente deve cifrar a mensagem utilizando sua própria chave privada.

**56** Os firewalls de inspeção de estado mantêm uma tabela dinâmica que registra as conexões ativas, avaliando os pacotes de rede com base no contexto da sessão TCP.

**57** O BGP (border gateway protocol) constitui o principal protocolo de roteamento exterior (EGP) da Internet, funcionando como um protocolo de vetor de caminho (path-vector) para a troca de informações de alcançabilidade entre distintos sistemas autônomos (AS).

**58** No Linux, o comando chmod 754 arquivo.txt concede ao proprietário permissões de leitura e execução quanto ao grupo leitura, escrita e execução, e concede aos demais usuários apenas permissão de leitura.

_A respeito de dados estruturados e não estruturados, de banco de dados NoSQL, de modelagem e normalização de dados e de Big Data, julgue os itens a seguir._

**59** Considere uma tabela em um banco de dados relacional com o esquema R(A, B, C, D), em que {A, B} constitui a chave primária. Considere, também, que não existam dependências parciais, que o atributo C seja determinado pela chave {A, B} e que o atributo D tenha uma dependência funcional em relação a C (C → D). Nesse caso, conclui-se corretamente que a tabela encontra-se na terceira forma normal (3FN).

**60** No que se refere à tipologia de dados, documentos em HTML são classificados como dados estruturados, uma vez que a utilização de tags de marcação define rigidamente a organização e o esquema dos dados, de forma equivalente à estrutura de tabelas em bancos de dados relacionais.

**61** No que tange aos bancos de dados que oferecem suporte nativo ao tipo JSON, o armazenamento de documentos com estruturas aninhadas constitui um impedimento técnico para a realização de consultas em atributos localizados em níveis hierárquicos profundos, uma vez que a ausência de um esquema rígido (schema) inviabiliza o mapeamento e a recuperação desses dados de forma direta. contratos_cdc tem as colunas a seguir. • id_contrato (identificador do contrato); • valor (valor do contrato); • status (situação do contrato); • data_atualizacao (timestamp da alteração). Um auditor do referido tribunal deseja realizar a seguinte consulta SQL.

**1** SELECT id_contrato, valor, status

**2** FROM ( SELECT *, ROW_NUMBER() OVER ( PARTITION BY id_contrato ORDER BY data_atualizacao DESC ) AS rn FROM contratos_cdc

**9** ) t

**10** WHERE rn = 1 A partir das informações apresentadas e do trecho de código SQL precedente, julgue os itens a seguir. No contexto de uma arquitetura de inteligência da informação para auditoria de dados, a consulta SQL apresentada utiliza a função de janela ROW_NUMBER() para segmentar os registros por contrato e ordená-los cronologicamente de forma decrescente; essa abordagem é eficaz para identificar a versão mais recente de cada contrato em uma tabela de CDC, sob a condição de que a coluna data_atualizacao tenha granularidade suficiente para garantir uma ordenação unívoca, evitando que registros distintos de um mesmo contrato apresentem o exato mesmo marcador temporal. No que concerne à manipulação de dados em larga escala e à organização de consultas SQL, a utilização da CTE (common table expression) apresentada a seguir para encapsular a lógica de ranking é semanticamente equivalente à consulta SQL apresentada, pois ambas as abordagens produzem o mesmo resultado lógico ao isolar a versão mais recente de cada contrato, sob a premissa de que a coluna data_atualizacao permita uma ordenação unívoca para cada id_contrato.

**1** WITH contratos_rankeados AS ( SELECT *, ROW_NUMBER() OVER ( PARTITION BY id_contrato ORDER BY data_atualizacao DESC ) AS rn FROM contratos_cdc

**8** )

**9** SELECT id_contrato, valor, status

**10** FROM contratos_rankeados

**11** WHERE rn = 1 Em arquiteturas de dados que seguem o padrão de medallion architecture, a ingestão de dados provenientes de sistemas transacionais é frequentemente realizada de forma incremental para minimizar o impacto nos bancos de produção. Uma das abordagens comuns utiliza ferramentas de CDC (change data capture) acopladas a sistemas de mensageria para alimentar um data lake ou cloud data warehouse. A esse respeito, julgue o item a seguir. No contexto de arquiteturas de dados modernas para auditoria e inteligência, a implementação de CDC integrada a um modelo ELT permite que os eventos de alteração de dados (DML) sejam ingeridos e persistidos no repositório central em seus formatos semiestruturados originais.

_A respeito de prototipação e de práticas ágeis desenvolvimento de software, julgue os itens a seguir. de No SCRUM, o product owner é o responsável pela gestão do product backlog, inclusive pela definição e pela ordenação dos itens; entretanto, em cenários de alta complexidade com múltiplos stakeholders, essa responsabilidade é compartilhada com o scrum master, a fim de assegurar o alinhamento estratégico e a viabilidade técnica das necessidades do negócio. No contexto de processos de desenvolvimento ágeis, a utilização da prototipação é considerada incompatível com o desenvolvimento incremental, fundamentando-se no fato de que protótipos representam versões necessariamente descartáveis que não agregam valor direto ao incremento do produto final. No que concerne a testes de software, métricas de software, DevOps e integração contínua, julgue os itens a seguir._

**68** Em um pipeline de CI/CD, a eficácia da integração contínua fundamenta-se na execução automatizada de builds e testes, visando assegurar que o código integrado ao ramo principal (main branch) permaneça em um estado tecnicamente implantável, de modo a mitigar riscos de instabilidade a cada nova alteração.

**69** No âmbito das técnicas de teste de software, os testes funcionais e os testes de aceitação compartilham o objetivo de confirmar o cumprimento dos requisitos, divergindo, entretanto, em seu propósito primordial: enquanto o teste funcional visa verificar a conformidade do comportamento do sistema em relação às suas especificações técnicas (caixa-preta), o teste de aceitação busca validar a prontidão do produto para o uso, avaliando-o sob a ótica das necessidades de negócio e dos critérios de aceitação estabelecidos pelos usuários finais.

**70** Com base na métrica de análise de pontos de função (APF), conforme as diretrizes que estabelecem o cálculo do fator de ajuste (VAF), considere que um sistema tenha 120 pontos de função não ajustados (UFP) e que a soma das

**14** características gerais do sistema (GSC) seja igual a 30. Nessa situação, o total de pontos de função ajustados (PFA) será exatamente igual a 114.

_No que se refere a autenticação por meio de certificados e de biometria, julgue os itens a seguir._

**71** Sistemas de autenticação biométrica modernos armazenam, por definição, a imagem biométrica bruta capturada do usuário, pois a verificação de identidade exige a comparação direta entre a imagem original cadastrada e a nova amostra coletada.

**72** A autenticação baseada em certificados digitais no padrão X.509 utiliza criptografia de chave pública, em que o usuário comprova a posse da chave privada correspondente ao certificado durante o processo de autenticação, e o servidor é capaz de validar a assinatura utilizando a chave pública contida no certificado.

_Acerca de worms e de rootkits, julgue os itens que se seguem._

**73** Um rootkit é um tipo de malware cuja principal função é integrar múltiplos computadores comprometidos em uma botnet controlada remotamente por um servidor de comando e controle (C2).

**74** Um worm é um tipo de malware capaz de se propagar pela rede explorando vulnerabilidades em serviços ou em sistemas, sem depender da execução de um arquivo hospedeiro por um usuário. No que diz respeito a segurança da informação, a exploração de falhas e a buffer overflow, julgue os itens subsequentes.

**75** Em linguagens de programação compiladas, a ocorrência de buffer overflow é impedida pelo próprio modelo de gerenciamento de memória dessas linguagens, que realiza automaticamente a verificação de limites (bounds checking) em operações de leitura e de escrita em buffers.

**76** Um ataque de buffer overflow baseado em pilha (stack-based buffer overflow) pode permitir a execução de código arbitrário quando dados excedentes sobrescrevem o endereço de retorno armazenado na pilha de execução, redirecionando o fluxo do programa para instruções controladas pelo atacante. Com relação a sistemas criptográficos simétricos e assimétricos,

_julgue os itens subsecutivos._

**77** O compartilhamento prévio de chaves secretas entre as partes que desejam se comunicar não é necessário em criptografias simétricas.

**78** Na criptografia assimétrica, para garantir a confidencialidade de uma mensagem, o remetente deve utilizar a chave pública do destinatário para cifrar os dados, permitindo, dessa maneira, que apenas a chave privada correspondente seja capaz de realizar a decifração. No que concerne à governança corporativa de TI, à gestão de riscos de TI e à gestão de serviços de TI, julgue os itens a seguir,

_considerando os principais frameworks e as normas aplicáveis._

**79** O COBIT 2019 é projetado para fornecer uma abordagem flexível e integrada para design e implementação de governança de TI, incluindo processos como managed data, managed projects e managed assurance, em uma abordagem em cascata de metas.

**80** No ITIL v4, a prática de gestão de incidentes requer gerenciamento de riscos, uma vez que as ações tomadas ao tentar diagnosticar e resolver incidentes podem levar a riscos graves, significativos tanto para o provedor de serviços quanto para o consumidor do serviço.

**81** A ISO 31.000 enfoca os aspectos relativos aos princípios da gestão de riscos de TI, não abordando aspectos como estrutura e processo de gestão de riscos, que devem ser gerenciados pelas organizações com base no COSO (Committee of Sponsoring Organizations of the Treadway Commission).

_No que se refere ao planejamento estratégico de TI, julgue os itens que se seguem._

**82** O mapa estratégico de uma organização é estruturado de acordo com o balanced scorecard, em quatro perspectivas tradicionais: financeira; clientes; processos internos; e aprendizado e crescimento. Essas perspectivas são genéricas como modelo base e podem ser adaptadas à realidade da organização, que pode incluir e(ou) renomear perspectivas.

**83** O Plano Diretor de Tecnologia da Informação (PDTI) é um instrumento de planejamento anual, que estabelece diretrizes e premissas para o uso das tecnologias da informação e comunicação (TIC) na instituição, sendo revisado e alterado ao final de cada exercício. No que tange à cibersegurança, ao acesso à informação e à proteção de dados pessoais em organizações públicas, julgue os itens seguintes.

**84** Na função proteger (PR) do Cybersecurity Framework (CSF) do NIST, são utilizadas salvaguardas para gerenciar os riscos de segurança cibernética da organização, incluindo-se o gerenciamento de identidade, autenticação e controle de acesso a informações físicas e ativos lógicos, assim como ações relacionadas às identidades e credenciais dos usuários.

**85** A Lei Geral de Proteção de Dados Pessoais determina que o titular dos dados pessoais tem direito de obter do controlador tanto o bloqueio quanto a eliminação de dados desnecessários ou tratados em desconformidade com a referida lei.

**86** De acordo com a Lei de Acesso à Informação, é dever do Estado garantir o direito de acesso à informação íntegra, sendo a integridade definida como a qualidade da informação coletada na fonte, com o máximo de detalhamento possível, sem modificações.

_No que se refere à gestão de contratação de serviços e soluções de TI na administração pública, julgue os itens a seguir. Nas soluções de TIC compostas apenas por fornecimento de bens, de acordo com o estabelecido na Instrução Normativa SGD/ME n.º 94/2022, é indispensável a realização de reunião inicial registrada em ata, por integrar o início da execução contratual._

_De acordo com o disposto na Instrução Normativa SGD/ME n.º 94/2022, no modelo de gestão do contrato, devem constar, quando possível, as situações em que haverá suspensão da participação da contratada em licitações e impedimento para contratar com a administração._

_Com base na legislação aplicável à contratação de bens e serviços de TI e suas alterações, julgue os itens a seguir. Nos termos da Instrução Normativa SGD/ME n.º 94/2022, o órgão ou entidade deverá publicar, em sítio eletrônico de fácil acesso, o estudo técnico preliminar da contratação e o termo de referência no prazo de 30 dias contados da assinatura do contrato. Na pesquisa de preços, conforme as disposições da Instrução Normativa SEGES/ME n.º 65/2021, devem ser priorizadas a composição de custos unitários em sistemas oficiais de governo e as contratações similares feitas pela administração pública, com justificativa nos autos em caso de impossibilidade. Segundo o disposto na Lei n.º 14.133/2021, os trabalhos relativos a assessorias, controle de qualidade e tecnológico incluem-se entre os serviços técnicos especializados de natureza predominantemente intelectual. Compete ao gestor do contrato, de acordo com o disposto na Instrução Normativa SGD/ME n.º 94/2022, anotar, no histórico de gerenciamento do contrato, todas as ocorrências relacionadas à execução contratual bem como confeccionar e assinar o termo de recebimento definitivo. A concorrência é, conforme disposto na Lei n.º 14.133/2021, a modalidade de licitação para contratação de bens e serviços especiais e de obras e serviços comuns e especiais de engenharia, cujo critério de julgamento poderá ser, entre outros, o de melhor técnica ou conteúdo artístico._

_Acerca de arquiteturas serverless e event-driven, de balanceamento de cargas e de autoescalonamento, julgue os itens a seguir. Em infraestruturas com balanceadores de carga, o autoescalonamento horizontal consiste em aumentar dinamicamente a capacidade computacional de uma instância já existente, enquanto o balanceador distribui requisições entre múltiplas instâncias dessa mesma máquina virtual. Em arquiteturas event-driven serverless, a execução de funções é interrompida por eventos publicados por serviços produtores e modificada por consumidores de forma desacoplada, sendo incomum a utilização de mecanismos de mensageria ou de streams para intermediar a entrega desses eventos. Com relação a monitoramento, logging e tracing, julgue os itens que se seguem. Em plataformas de observabilidade em nuvem, serviços de monitoramento coletam apenas métricas numéricas de infraestrutura, enquanto registros de logs e dados de tracing devem ser armazenados e analisados por ferramentas externas independentes do fabricante e especializadas em regras de negócio segundo o que o auditor determina._

**97** Em sistemas distribuídos, o tracing distribuído permite acompanhar o percurso completo de uma requisição por múltiplos serviços, registrando a sequência de chamadas entre componentes e o tempo gasto em cada etapa do processamento.

_A respeito da norma NIST SP 800-53 e da Lei Geral de Proteção de Dados Pessoais (LGPD), julgue os itens subsecutivos. É estabelecido na LGPD que dados pessoais sensíveis incluem informações acerca da origem racial ou étnica, da convicção religiosa, da opinião política, de dados referentes à saúde ou à vida sexual e de dados genéticos ou biométricos vinculados a uma pessoa natural._

**99** O controle de acesso definido no NIST SP 800-53 estabelece requisitos de segurança destinados à restrição de acesso lógico a sistemas e recursos, com base em políticas organizacionais previamente definidas.

_Acerca de modelagem dimensional, do CRISP-DM e do uso de banco de dados relacionais na análise de dados, julgue os itens a seguir._

**100** A junção externa (LEFT, RIGHT ou FULL OUTER JOIN) garante que todos os registros de pelo menos uma das tabelas sejam preservados no resultado de uma consulta, mesmo na ausência de correspondência na outra tabela.

**101** No modelo de referência CRISP-DM, a fase de preparação de dados ocorre estritamente após a conclusão da fase de modelagem, com o objetivo de formatar as saídas preditivas geradas.

**102** O esquema estrela é caracterizado por uma tabela de fatos central conectada a múltiplas tabelas de dimensão altamente normalizadas, e visa otimizar o uso de espaço de armazenamento.

_Julgue os próximos itens, a respeito de visualização e análise exploratória de dados, de linguagens e ferramentas de apoio à análise de dados e de técnicas e tarefas de mineração de dados._

**103** A técnica de lematização (lemmatization) reduz palavras à sua raiz por meio de regras heurísticas, frequentemente resultando em formas que não constituem palavras válidas no dicionário do idioma original.

**104** O boxplot (diagrama de caixa) é uma ferramenta de visualização que possibilita identificar a mediana, a dispersão dos dados e a presença de valores atípicos (outliers) em uma distribuição.

**105** No ecossistema Python, a biblioteca Pandas oferece a estrutura DataFrame, projetada para manipulação eficiente de dados tabulares bidimensionais com eixos rotulados para linhas e colunas.

_Julgue os itens a seguir, relativos a conceitos e técnicas de aprendizado de máquina, IA generativa, redes neurais e deep learning._

**106** As redes adversárias generativas (GANs) operam com duas redes neurais — o gerador e o discriminador —, que colaboram cooperativamente para minimizar a mesma função de perda, produzindo dados sintéticos indistinguíveis dos reais.

**107** No aprendizado supervisionado, o modelo é treinado com um conjunto de dados rotulados, no qual a saída ou o resultado desejado para cada observação já é conhecido previamente.

**108** As redes neurais convolucionais (CNNs) são arquiteturas especializadas no processamento de dados com topologia de grade, como imagens, destacando-se pelo uso de camadas de agrupamento (pooling) para reduzir a dimensionalidade espacial das representações. Com relação ao processamento de linguagem natural (PLN) e à arquitetura e engenharia de sistemas de IA, julgue os itens a seguir.

**109** No contexto de MLOps, o fenômeno de concept drift refere-se à degradação do desempenho de um modelo em produção causada exclusivamente por alterações no código-fonte do modelo durante o deploy.

**110** A arquitetura transformer transformou profundamente o processamento de linguagem natural ao substituir redes neurais recorrentes (RNNs) por mecanismos de atenção, acelerando assim a análise sequencial de textos longos.

_Acerca dos tipos de auditoria e das normas de auditoria, julgue os itens que se seguem._

**111** O conceito de risco de auditoria na auditoria financeira, conforme a ISSAI 200, refere-se à probabilidade de o auditor ser processado judicialmente por erros em seu relatório, independentemente de as demonstrações financeiras conterem ou não distorções relevantes.

**112** Na auditoria de conformidade, o trabalho do auditor pode ser realizado sob duas perspectivas: a de atestação, em que o responsável pela gestão declara a conformidade e o auditor verifica essa declaração; ou a de reporte direto, na qual o próprio auditor avalia o objeto e relata a conformidade diretamente aos usuários.

**113** A auditoria operacional deve abster-se de emitir recomendações propositivas ao final do relatório, limitandose a apontar as falhas de eficiência encontradas, a fim de garantir a neutralidade do tribunal de contas e evitar interferência no mérito administrativo do órgão auditado.

_Em relação ao planejamento da auditoria governamental, julgue os itens seguintes._

**114** A utilização da amostragem não estatística é considerada pela ISSAI 100 falha técnica grave que prejudica a validade das conclusões do relatório, uma vez que a referida norma exige a aplicação de métodos probabilísticos em todos os testes de conformidade do setor público.

**115** A matriz de planejamento é o instrumento que organiza as questões de auditoria, os respectivos procedimentos de coleta e análise de dados, as fontes de informação e as possíveis limitações, servindo como roteiro estruturado para a fase de execução.

**116** Na definição do escopo da auditoria, são estabelecidos os limites do trabalho, incluindo-se o período de tempo abrangido, as unidades administrativas e os processos específicos que serão submetidos ao exame do auditor.

_Julgue os itens subsequentes, relativos à execução e ao monitoramento da auditoria do setor público._

**117** O monitoramento de uma auditoria operacional deve ser considerado concluído e o processo deve ser arquivado após o gestor auditado protocolar o plano de ação, uma vez que a responsabilidade pela implementação das melhorias sugeridas é exclusiva da administração, cessando a jurisdição do órgão de controle sobre o caso.

**118** A técnica de revisão analítica consiste na conferência aritmética detalhada de cálculos de impostos e somas de documentos fiscais, com o propósito de atestar a exatidão matemática de processos de liquidação da despesa pública.

**119** Caso os testes de observância revelem que os controles internos da entidade são ineficazes para prevenir ou detectar distorções relevantes, o auditor deve, por imposição normativa, abster-se de realizar testes substantivos e deve declarar a impossibilidade de emitir opinião sobre o objeto, sob pena de vício na caracterização dos achados.

**120** A circularização, também denominada confirmação externa, consiste na obtenção de resposta escrita direta de um terceiro independente sobre informações relativas a saldos ou transações, sendo considerada técnica de alta confiabilidade por originar-se de fonte externa à entidade auditada. Espaço livre
