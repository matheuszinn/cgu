---
tipo: prova
concurso: "tcu_25_aufc"
arquivo_origem: "Provas Cebraspe/tcu_25_aufc/PROVA OBJETIVA CONHECIMENTOS ESPECIFICOS.pdf"
tags:
  - prova
  - cebraspe
  - cgu-2026
---

# PROVA OBJETIVA CONHECIMENTOS ESPECIFICOS

## CONHECIMENTOS ESPECÍFICOS

_Julgue os próximos itens, relativos a infraestrutura de TI._

**101** ARP é um protocolo stateless que realiza mapeamento dinâmico de um endereço IP para o endereço MAC correspondente, atuando dentro no mesmo domínio de broadcast.

**102** As arquiteturas hiperconvergentes utilizam um modelo de controlador centralizado, o que permite a simplificação do gerenciamento e da escalabilidade ao serem integrados todos os componentes de hardware e software, de forma eficiente, em um sistema único.

**103** Para a garantia de alta performance em ambientes de alta demanda, a fragmentação de disco em sistemas de arquivos tradicionais é resolvida pelo LFS (log-structure file system) com a otimização da performance de leitura e gravação, atenuando-se gargalos de entradas e saídas por meio da melhora da velocidade de gravação, tratando-se todas as escritas como anexações sequenciais a um log.

**104** O processo de hardening para controladores de domínio (domain controllers — DC) envolve uma abordagem em várias camadas na adoção de medidas de segurança contra ataques cibernéticos, como, por exemplo, a aplicação de autenticação multifator (multifactor authenticator — MFA) para todos os acessos administrativos aos DC e a remoção de serviços que não sejam essenciais, reduzindo a superfície de ataque.

**105** O protocolo de roteamento OSPF garante convergência rápida e alta escalabilidade, contudo tem enfrentado desafios de adaptação a novos paradigmas de rede, como a compatibilidade com o IPv6, o que causa o aumento da frequência e o escopo de flooding de LSA (links state advisement) em topologias estáveis.

**106** No padrão IEEE 802.11ax (wi-fi 6), a arquitetura OFDMA (orthogonal frequency-division multiple access) opera múltiplos clientes simultaneamente, sendo ideal para tráfego de baixa largura de banda e alta latência.

**107** Em relação ao modelo OSI, o IPv6 atua diretamente na camada de transporte que gerencia o transporte de dados entre as aplicações, garantindo a entrega confiável dos dados, sem erros, pois os divide em segmentos (com protocolos como TCP e UDP).

_Considerando a ITIL v4, julgue os itens a seguir._

**108** Na ITIL v4, o propósito do gerenciamento de incidente é reduzir a probabilidade e o impacto de incidentes, por meio da identificação das causas reais e potenciais de incidentes e do gerenciamento de soluções alternativas e erros conhecidos.

**109** Com escopo abrangente que inclui todos os ativos físicos e lógicos da organização, o CMDB atende ao princípio foco no valor da ITIL v4, e a utilização de um número maior de itens de configuração (IC) garante continuamente uma análise de impacto mais detalhada e exata.

**110** Em uma aplicação de e-commerce, convém utilizar a estratégia de federação dos dados em CMDB para serviços como pedidos, pagamentos e autenticação, pois replicar dados em um repositório centralizado melhora a precisão e reduz a latência na manutenção dos itens de configuração voláteis.

**111** SVC (service value chain), que não é um processo linear nem rígido, define como atividades e componentes de uma organização atuam para converter a demanda e a oportunidade em valor.

**112** Na ITIL v4, a arquitetura de valor do SVS (service value system) demonstra como os componentes e as atividades de uma organização interagem para criar valor, sendo tais elementos configuráveis, de maneira flexível, para otimizar o alinhamento com as realidades de serviço e a integração dos recursos organizacionais.

_A respeito de bancos de dados e integração com fontes de dados,_

_julgue os próximos itens._

**113** Arquivos do tipo CSV podem ser utilizados para representar informações de tabelas, incluindo os rótulos de suas colunas.

**114** No serviço REST, para que o servidor responda adequadamente, ele precisa armazenar o estado da sessão do cliente entre suas requisições.

**115** Bancos de dados relacionais utilizam tabelas bidimensionais, e o MongoDB representa os dados em formato JSON ou XML.

**116** PolyBase é a ferramenta que permite ao Microsoft SQL Server consultar fontes externas como se os dados estivessem armazenados localmente.

_Acerca de data warehouse, data lake, data mesh, CI/CD e ETL,_

_julgue os itens a seguir._

**117** Como data warehouse é não volátil, a etapa intermediária do ETL deve efetuar todos os tratamentos necessários nos dados para melhorar a sua qualidade.

**118** A construção de um data mesh parte do princípio de propriedade de domínio, conforme o qual as equipes de cada domínio assumem a responsabilidade por seus dados.

**119** O pipeline de CI/CD consiste em duas etapas sequenciais: implantação rápida em produção e posterior integração com os demais serviços.

**120** Data warehouse e data lake armazenam dados em seu formato original, porém o data lake, diferentemente do data warehouse, acessa bases externas a uma organização.

_Julgue os próximos itens, relativos a governança de dados e processamento em nuvem._

**121** A governança de dados está relacionada à prevenção de eventos de risco, incluindo a mitigação da reincidência de incidentes já ocorridos.

**122** O serviço de armazenamento S3 da Amazon utiliza contêineres chamados de buckets para guardar arquivos de qualquer tipo e tamanho.

**123** A equipe da governança de dados de uma organização deve estabelecer políticas e diretrizes corporativas para governança dos dados, enquanto cabe à alta administração a atribuição de papéis e responsabilidades.

**124** Na arquitetura PaaS (Platform as a Service) da computação em nuvem, o provedor é o responsável pelos recursos de sistema operacional e pelas aplicações.

_A respeito do Serverless Framework, dos padrões de integração Service Mesh e de paralelismo, julgue os itens a seguir._

_Em relação a GitHub Actions, Grafana e DevSecOps, julgue os itens subsecutivos._

**125** No fluxo padrão do Serverless Framework Dashboard

**132** No DevSecOps, a execução de varreduras automatizadas de CI/CD, as branch deployments permitem que cada commit em uma branch configurada do repositório GitHub seja implantado automaticamente em um stage associado.

**126** Considere que três funções sejam submetidas simultaneamente a um ProcessPoolExecutor, de maneira que uma durma por 8 segundos, outra, por 3 segundos, e a outra, por 2 segundos. Considere, ainda, que, nessa circunstância, o resultado obtido seja o seguinte. segurança é premissa fundamental do pipeline de desenvolvimento e deve ocorrer de forma integrada e contínua ao longo de todo o ciclo de entrega.

**133** O seguinte trecho do arquivo de workflow do GitHub Actions faz que o workflow seja acionado em duas situações distintas: quando uma nova etiqueta é criada no repositório e quando ocorre um push especificamente para a branch main. Sleeping for 8 seconds Done sleeping for 8 seconds Sleeping for 3 seconds Done sleeping for 3 seconds Sleeping for 2 seconds Done sleeping for 2 seconds Total time: ~13 seconds Nessa situação, o tempo total de execução fica próximo de

**8** segundos, pois esse é o tempo da thread mais longa e todas as demais terminam antes disso.

**127** Em um Service Mesh, a implementação das CCC (cross cutting concerns) permanece a cargo de cada microsserviço, cabendo ao control plane redistribuí-las aos proxies.

_Acerca do versionamento de APIs RESTful e do JWT (JSON Web Token), julgue os itens subsequentes._

**128** A decodificação de um JWT envolve transformar o header e o payload em um formato compacto e seguro para URLs, de maneira a permitir que qualquer pessoa leia essas partes sem precisar de uma chave.

**129** No versionamento baseado em datas, a API RESTful utiliza identificadores de calendário diretamente no URI para indicar versões estáveis e não disruptivas.

_Em relação a Docker e ElasticSearch, julgue os itens que se seguem._

**130** Em um dockerfile de multi-stage build, a execução do comando apresentado a seguir resultará na cópia de quaisquer arquivos do stage builder que corresponderem ao padrão /app/target/*.jar, os quais serão adicionados com o nome/app/app.jar ao stage atual. COPY --from=builder /app/app.jar /app/target/*.jar

**131** Na instalação via Docker, o modelo NER (Named Entity Recognition) pode ser carregado no ElasticSearch por meio da execução do comando eland_import_hub_model dentro da imagem docker do Eland, conforme parâmetros definidos. on: label: types: - created page_build: types: - main

**134** O parâmetro http_addr define a interface em que o Grafana realiza a escuta, sendo um valor equivalente a 127.0.0.1, e expõe o serviço apenas na interface local (localhost), enquanto o http_port, cujo padrão é 8080, especifica a porta de escuta. Espaço livre

_Considerando a linguagem de programação Java e a cobertura SonarQube, julgue os itens a seguir._

**135** A linguagem Java, ao implementar o conceito de nest, permite o acesso a membros private entre nestmates nativamente pela máquina virtual, dispensando o uso de métodos sintéticos.

**136** No trecho de código a seguir, a implementação individualizada do QualityGate permite que o resultado do estágio Quality Gate 1 não interrompa o pipeline, caso o resultado da análise do SonarQube seja FAILED, e que ele prossiga normalmente para a execução do estágio SonarQube analysis 2. pipeline { agent any stages { stage('SonarQube analysis 1') { steps { sh 'mvn clean verify org.sonarsource.scanner.maven:sonarmaven-plugin:sonar' } } stage("Quality Gate 1") { steps { waitForQualityGate abortPipeline: true } } stage('SonarQube analysis 2') { steps { sh 'gradle sonar' } } stage("Quality Gate 2") { steps { waitForQualityGate abortPipeline: true } } } }

_Acerca de gestão de identidade e de acesso, privacidade, segurança por padrão e malware, julgue os itens a seguir._

**137** Backdoors incorporados a campanhas de malware fileless podem estabelecer canais de comando e controle a partir de código que permanece apenas em memória, utilizando mecanismos nativos do sistema para evitar detecção baseada em arquivos.

**138** Em uma arquitetura corporativa que adota SSO via SAML 2.0, o authorization server do fluxo OAuth2 atua como identity provider responsável pela emissão das assertions SAML utilizadas no processo de autenticação entre o usuário e o service provider.

**139** A adoção de privacidade por padrão em um serviço digital legitima que as configurações iniciais favoreçam a coleta ampliada de dados, desde que os mecanismos de segurança por padrão estejam habilitados para proteger essas informações.

**140** Um keylogger fileless depende da instalação prévia de um rootkit no sistema para registrar com sucesso os eventos de teclado, devido à necessidade de persistência em nível de kernel.

_A respeito de controles e testes de segurança para aplicações web, múltiplos fatores de autenticação e soluções para segurança da informação, julgue os itens subsequentes._

**141** Em arquiteturas corporativas, o uso combinado de um proxy e de um SIEM tem potencial para ampliar a capacidade de detecção de atividades anômalas, uma vez que os registros de navegação tratados pelo proxy podem ser correlacionados pelo SIEM a eventos provenientes de firewalls, IDS e controles de acesso.

**142** A validação de segurança realizada no cliente é suficiente para eliminar os riscos de injeção em aplicações web baseadas em APIs REST, desde que o tráfego esteja protegido por TLS.

**143** Em um sistema corporativo, a exigência de senha e de código gerado por aplicativo autenticador atende aos requisitos de múltiplos fatores de autenticação, pois combina um fator de conhecimento e um fator de posse.

**144** O uso de um SIEM devidamente configurado para correlação em tempo real elimina a necessidade de mecanismos de prevenção de um IPS, já que os eventos consolidados permitem bloquear as atividades maliciosas diretamente a partir da análise centralizada.

_No que se refere a frameworks de segurança da informação e a tratamento de incidentes cibernéticos, julgue os itens que se seguem._

**145** No MITRE ATT&CK, as técnicas associadas à fase de exfiltração são classificadas como táticas do domínio Enterprise que representam objetivos estratégicos e substituem a necessidade de técnicas específicas na matriz.

**146** Em um cenário corporativo no qual o framework NIST CSF é utilizado para organização das funções de segurança, a implementação de inventário e controle de ativos prevista nos CIS controls pode apoiar diretamente a função Identify do framework, já que ambos exigem visibilidade consistente de recursos tecnológicos.

**147** Durante o tratamento de um incidente cibernético, a fase de contenção pode incluir o isolamento temporário de ativos afetados, para limitar o impacto do incidente.

_Julgue os itens a seguir, referentes a assinaturas digitais, segurança em nuvens e ataques a redes de computadores._

**148** Em ambientes de nuvem pública, a configuração de controles de acesso baseada em princípio de privilégio mínimo no nível dos serviços gerenciados contribui para reduzir superfícies de ataque.

**149** Em um sistema que utiliza assinatura digital para garantir integridade e autenticidade de documentos, é adequado que a proteção dos dados em trânsito seja apoiada por protocolos como o TLS, enquanto a proteção dos dados em repouso seja realizada por criptografia simétrica.

**150** Em ataques de ARP spoofing, o atacante depende de técnicas de IP spoofing para alterar o mapeamento entre endereços MAC e IP na tabela ARP da vítima.

_Em relação à computação em nuvem e a tecnologias de contêineres, julgue os itens a seguir._

**151** Docker e Kubernetes são software intercambiáveis em qualquer ambiente, pois ambos criam, executam e orquestram contêineres de forma idêntica.

**152** Em arquiteturas serverless, operam servidores físicos, porém a gestão da infraestrutura — incluídos o provisionamento, a manutenção e a escalabilidade — é totalmente abstraída dos desenvolvedores, que focam exclusivamente a lógica da aplicação, permitindo rápida adaptação a demandas variáveis, sem preocupações com recursos subjacentes.

_Acerca de modelos de controle de acesso e das arquiteturas de segurança RBAC (Role-Based Access Control) e Zero Trust,_

_julgue os próximos itens._

**153** Na arquitetura Zero Trust, usuários conectados por VPN corporativa são tratados como confiáveis por padrão, uma vez que, nesse modelo, a confiança é eliminada independentemente da origem da conexão, incluído o perímetro da rede interna, exigindo-se autenticação contínua e validação de acesso a cada recurso.

**154** O modelo RBAC não é eficaz para a implementação do princípio do menor privilégio, pois suas funções tendem a conceder permissões amplas e não limitam o acesso somente ao necessário para tarefas específicas, o que compromete a segurança em ambientes de computação em nuvem.

_Julgue os itens que se seguem, relativos a conceitos, práticas e ferramentas de integração e entrega contínua (CI/CD) e a gestão financeira em ambientes de computação em nuvem (FinOps)._

**155** A prática de FinOps combina pessoas, processos e tecnologias para fornecer visibilidade detalhada e em tempo real dos custos em ambientes de nuvem, possibilitando o controle financeiro eficaz e a tomada de decisão baseada em dados precisos, o que promove a otimização contínua dos gastos e a gestão alinhada às necessidades estratégicas do negócio.

**156** A abordagem CI/CD visa otimizar e acelerar o ciclo de vida do desenvolvimento de software, combinando a integração automática e frequente de alterações ao repositório por meio da integração contínua, com processos automatizados de testes, entrega e implantação que conduzem a mudanças no ambiente de produção, assegurando agilidade e qualidade.

_Julgue os próximos itens, relativos a fundamentos de computação em nuvem, plataformas e serviços em nuvem e armazenamento de dados em computação em nuvem._

**157** A alta disponibilidade em ambientes de nuvem é obtida suficientemente com o uso de múltiplas zonas de disponibilidade dentro de um mesmo data center, sem necessidade de replicação geográfica de dados ou de componentes de sistema.

**158** No armazenamento orientado a objetos, cada informação é organizada como uma unidade autônoma acompanhada de metadados, sendo tal abordagem indicada para grandes volumes de dados não estruturados, como imagens, vídeos, logs e backups.

**159** O AWS IAM (Identity and Access Management) restringe o controle de permissões a configurações gerais aplicadas de maneira uniforme a todos os usuários, sem oferecer mecanismos para detalhamento de acesso por recurso ou por entidade específica.

_Acerca de estratégias de migração de aplicações e de arquiteturas multicloud, julgue os itens subsequentes._

**160** Arquiteturas multicloud caracterizam-se pelo uso simultâneo de serviços de nuvens públicas de diferentes provedores, o que permite maior flexibilidade operacional e reduz a dependência de um único fornecedor.

**161** A estratégia lift and shift envolve a reescrita completa das aplicações antes da migração, de modo a serem explorados integralmente os recursos nativos da nuvem, e prioriza a modernização antes da transferência do ambiente.

_Com base nas normas relativas à computação em nuvem no governo federal, julgue o próximo item._

**162** O uso de computação em nuvem no governo federal deve obedecer à Lei Geral de Proteção de Dados Pessoais (LGPD), com garantia dos direitos fundamentais de titularidade, guarda de registros das operações de tratamento e adoção de responsabilidades compartilhadas entre órgãos e provedores. Segundo relatório da McKinsey de 2024, 78% das organizações entrevistadas afirmam já usar IA em pelo menos uma função de negócio. Apesar do entusiasmo, essa inserção de tecnologia disruptiva implica sérios riscos, como imprecisão dos resultados, quebra de privacidade e violação de propriedade intelectual. Esses riscos são tão evidentes que, segundo o mesmo estudo, cerca de 27% dos entrevistados afirmam que 100% dos resultados da IA generativa são revisados por humanos antes do uso. Ainda, o relatório aponta que não há uma propensão a abordar riscos relacionados à precisão ou explicabilidade dos resultados da IA. Ivette Luna. Da predição à compreensão: o papel da explicabilidade na implementação de IA em políticas públicas. In: Jornal da UNICAMP, 29 de setembro de 2025. Internet: <jornal.unicamp.br> (com adaptações).

_No que se refere a ética, transparência e responsabilidade no uso de IA, julgue os próximos itens._

**163** Explicabilidade e interpretabilidade tratam do desafio de entender como os modelos de aprendizado de máquina funcionam, devido especialmente à natureza de “caixa-preta” de muitos modelos, que pode tornar difícil ou impossível a capacidade de explicar uma previsão ou decisão.

**164** Há discriminação algorítmica quando um sistema de IA usa, para uma tomada de decisão, sem justificativa válida, a informação de que alguém pertence a um grupo social (ou características que funcionam como proxies), de modo a gerar desvantagens sistemáticas para esse grupo em contextos em que esse critério não deveria influenciar a decisão.

**165** Explicabilidade diz respeito às propriedades internas do modelo de IA que permitem compreender como ele funciona.

_Acerca de aplicações do processamento de linguagem natural (PNL) e da teoria de sistemas multiagentes, julgue os itens subsequentes._

**166** Emergência é uma propriedade-chave de sistemas multiagentes que deve ser intencionalmente projetada pelo desenvolvedor como parte central do comportamento coletivo desejado para os agentes inteligentes.

**167** Modelos supervisionados de reconhecimento de entidades nomeadas dependem de textos previamente anotados com categorias como pessoa, organização e local para que o algoritmo aprenda a identificar esses tipos de informação em novos textos.

**168** Modelos de PLN como transformers eliminam a necessidade de pré-processamento do texto, pois operam diretamente sobre o texto original.

**169** Sistemas multiagentes são adequados para problemas que exigem solução distribuída, autonomia local e coordenação entre entidades independentes, como logística, simulação social e controle de tráfego.

**170** O Word2Vec é um modelo de aprendizado profundo que utiliza redes neurais com várias camadas e mecanismos de atenção para aprender representações distribuídas de palavras a partir de grandes corpora textuais.

_Em relação a MLOps (machine learning operations), julgue os itens a seguir._

**171** A orquestração em MLOps concentra-se principalmente na etapa de treinamento dos modelos, não tendo relação direta com o deploy nem com o monitoramento de serviços em produção.

**172** MLOps é um conjunto de práticas de engenharia que padronizam, automatizam e monitoram o ciclo de vida de modelos de aprendizado de máquina com o objetivo de garantir reprodutibilidade, escalabilidade, governança e operação contínua dos sistemas de IA.

**173** A construção de um repositório estruturado de versionamento e governança de modelos é uma prática recomendada em MLOps para garantir rastreabilidade, controle de implantação e execução segura de rollbacks. O Conselho Nacional de Justiça (CNJ) e a Universidade de Brasília (UnB) desenvolvem, no âmbito do Programa Justiça 4.0, um modelo de IA que irá permitir a verificação automática de precedentes qualificados. A partir do texto da petição inicial, o modelo será capaz de identificar os precedentes qualificados dos tribunais superiores e listá-los em ordem decrescente de similaridade, até o limite mínimo de 70% de correspondência. O modelo adota o método não supervisionado, que consiste no aprendizado de máquina de forma mais autônoma a partir da inclusão de novos dados, que não precisam ser categorizados previamente. Vanessa Maeji. Parceria com a UnB desenvolve modelo de IA de verificação automática de precedentes qualificados. In: Agência CNJ de Notícias, 24 de junho de 2023. Internet: <www.cnj.jus.br> (com adaptações). Tendo o texto como referência inicial, julgue os itens subsecutivos, a respeito de aprendizado de máquina.

**174** O aprendizado por reforço é essencialmente uma forma de aprendizagem não supervisionada, pois seu objetivo principal é descobrir padrões ocultos e agrupamento nos dados, sem uso de rótulos; nesse paradigma, a recompensa funciona como um critério secundário de avaliação.

**175** A aprendizagem por reforço se diferencia da aprendizagem supervisionada, pois se baseia em feedback avaliativo, em vez de exemplos rotulados ou especificação da ação correta por um supervisor externo, para julgar a qualidade das ações.

**176** Modelos preditivos dispensam validação em um conjunto separado de dados porque a acurácia calculada durante o treinamento já representa a capacidade real do modelo de prever eventos futuros. No que diz respeito às etapas da contratação de soluções de TI na administração pública, julgue os itens a seguir.

**177** O estudo técnico preliminar pode substituir o termo de referência na contratação de alguns tipos de serviços que envolvam soluções de TI.

**178** A etapa inicial do processo de contratação de soluções de TI na administração pública consiste na elaboração do termo de referência.

_Julgue os seguintes itens, a respeito de tipos de soluções e modelos de serviço._

**179** Denomina-se fábrica de software um modelo de contratação com foco na produção contínua de sistemas e normalmente remunerado por ponto de função.

**180** No que se refere à contratação sob demanda de software, os direitos patrimoniais do código-fonte desenvolvido devem ser cedidos à administração pública.

**181** No modelo SaaS (Software as a Service), fica sob a responsabilidade do contratante a gestão de infraestrutura e do sistema operacional no qual o software é executado.

_A respeito de governança, fiscalização e gestão de contratos, riscos e controles em contratações, julgue os itens que se seguem._

**182** A responsabilização do licitante que der causa à inexecução parcial do contrato ocorrerá apenas na esfera judicial.

**183** Acordos de níveis de serviços, também denominados SLA (service level agreement), podem ser utilizados para medição do desempenho de contratos.

**184** As sanções administrativas aplicáveis ao responsável por infrações em licitações e contratos incluem advertência, multa, impedimento de licitar e declaração de inidoneidade.

**185** O reequilíbrio econômico-financeiro poderá ser concedido de forma automática sempre que houver aumento de custos do contratado.

**186** A administração pública contratante goza de total discricionariedade para definir, em edital, o valor das multas aplicáveis em função do cometimento de infrações administrativas pelo contratado, de acordo com o impacto da penalidade para a instituição.

_Julgue os itens subsequentes com base na Lei n.º 14.133/2021, na Lei Geral de Proteção de Dados Pessoais (LGPD), no Decreto n.º 10.024/2019 e na Instrução Normativa SGD/ME n.º 94/2022._

**187** Em regra, para os órgãos da administração pública federal direta, é obrigatória a adoção do pregão na forma eletrônica para a aquisição de bens e contratação de serviços comuns.

**188** Em geral, sustentabilidade e acessibilidade são temas a serem considerados, espontânea e opcionalmente, pelo fornecedor, todavia, em se tratando de segurança da informação, sua observância é obrigatória.

**189** No que tange ao tratamento de dados pessoais em contratos de TI, o controlador e o operador devem manter o registro das operações de tratamento de dados pessoais que realizarem, além de adotar medidas de segurança contra acessos não autorizados a tais dados.

**190** Na fase de planejamento da contratação de soluções de TIC, devem ser considerados os requisitos técnicos e não funcionais, que devem ser formalizados no termo de referência.

_Julgue os itens a seguir, a respeito de gerenciamento de serviços conforme a ITIL v4._

**191** No modelo das quatro dimensões do gerenciamento de serviços da ITIL v4, a dimensão “parceiros e fornecedores” é primariamente responsável por garantir que as práticas de gerenciamento sejam adequadamente combinadas e sequenciadas para criar fluxos de valor eficazes, atuando como o ponto focal para a integração de recursos externos e internos necessários à entrega de valor.

**192** A aplicação consistente do princípio orientador “progredir iterativamente com feedback” é intrinsecamente suportada pelo componente cadeia de valor do serviço (service value chain — SVC) no sistema de valor do serviço (SVS) da ITIL v4, uma vez que cada uma das seis atividades da SVC pode ser vista como um ciclo de feedback no qual as saídas de uma atividade se tornam insumos para a próxima ou para o consumo, o que permite melhorias contínuas e ajustes incrementais em cada etapa.

_Julgue os próximos itens, relativos à governança de TI de acordo com o COBIT 2019._

**193** O modelo de core do COBIT 2019 é composto por quarenta objetivos de governança e gestão, organizados em cinco domínios que representam áreas distintas de responsabilidade e alinhamento com o ciclo de vida da gestão e governança da organização.

**194** O COBIT 2019 define governança como a responsabilidade de garantir que as necessidades das partes interessadas (stakeholders), as condições e as opções sejam avaliadas para determinar objetivos organizacionais equilibrados e acordados, estabelecendo a direção por meio de priorização e tomada de decisão e monitorando o desempenho e a conformidade com a direção e os objetivos acordados.

**195** A estrutura do COBIT 2019 estabelece que o objetivo principal da gestão (management) é a avaliação do sistema de governança, enquanto a governança se concentra na realização de atividades para o atingimento dos objetivos da organização e na implementação de soluções acordadas.

_A respeito de metodologias ágeis, julgue os próximos itens._

**196** No desenvolvimento orientado a testes (TDD, na sigla em inglês), o ciclo de trabalho segue a ordem vermelho-verderefatorar (red-green-refactor), sendo vermelho a etapa que consiste em escrever o código de produção necessário para que o teste, criado na fase anterior, passe a funcionar corretamente.

**197** No desenvolvimento orientado ao domínio (DDD, na sigla em inglês), o contexto delimitado (bounded context) busca estabelecer a regra de que toda a lógica de negócio do sistema deve ser implementada em um único modelo coeso e global para garantir a consistência de todos os termos e definições de domínio.

**198** A reunião diária do scrum (daily scrum) é um evento de inspeção e adaptação obrigatório para a equipe, devendo ser utilizada pelo scrum master como o momento principal para que ele defina as tarefas do dia para cada membro do development team e para que solucione os impedimentos reportados.

**199** O desenvolvimento orientado ao comportamento (BDD, na sigla em inglês) estende o conceito do desenvolvimento orientado a testes, focando a colaboração e a comunicação entre desenvolvedores e stakeholders, por meio da definição de especificações executáveis escritas em linguagem ubíqua no formato Gherkin.

**200** O sistema Kanban utiliza como indicador chave de desempenho a métrica lead time, que é o tempo total gasto por uma unidade de trabalho desde o momento de seu compromisso (commitment) até a sua entrega final (delivery), sendo essencial para a previsão e otimização do fluxo de valor. Espaço livre
