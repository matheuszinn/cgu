---
tipo: prova
concurso: "inpi_23"
arquivo_origem: "Provas Cebraspe/inpi_23/PROVA OBJETIVA CONHECIMENTOS COMPLEMENTARES CARGOS 9 10 E 11.pdf"
tags:
  - prova
  - cebraspe
  - cgu-2026
---

# PROVA OBJETIVA CONHECIMENTOS COMPLEMENTARES CARGOS 9 10 E 11

## CONHECIMENTOS COMPLEMENTARES

_Acerca de estrutura de dados e algoritmos, julgue os itens a seguir. A passagem de um vetor por valor é mais eficiente que a passagem por parâmetro, considerando aspectos de tempo de processamento e espaço em memória, estando ambas as situações sob as mesmas condições de recursos. Pilhas são tipos de estruturas de dados que permitem a remoção direta de qualquer elemento de sua estrutura. O algoritmo quicksort possui complexidade de tempo de pior caso O(n2), contudo a complexidade de tempo médio desse algoritmo é O(n log n). Os algoritmos de Dijkstra e de Bellman-Ford resolvem o problema de caminhos mais curtos de única origem. Enquanto este aceita arestas de pesos negativos, aquele aceita somente arestas não negativas. Em uma lista circular ordenada, o acesso ao maior elemento possui complexidade de tempo de pior caso O(1). O seguinte pseudocódigo possui complexidade de tempo de pior caso O(2n) para a verificação da existência de um elemento na lista. função BuscaRecursiva(lista, tamanho, elemento) se tamanho < 1 então retorna FALSO se lista[tamanho] == elemento então retorna VERDADEIRO senão BuscaRecursiva(lista, tamanho-1, elemento) fim função Uma árvore binária é classificada como balanceada (AVL) quando as alturas das subárvores da maioria dos nós dessa árvore diferem entre si em apenas uma unidade. As árvores B são caracterizadas por minimizarem os custos de tempo em discos magnéticos e possuírem, no máximo, dois filhos em cada nó._

_Julgue os itens subsequentes, relativos a COBIT 2019 e ITIL v4. No COBIT não há processo específico que vise implementar abordagem de gerenciamento tal que os requisitos de governança corporativa sejam atendidos, e abrangendo componentes de governança como procedimentos, serviços, infraestrutura e aplicativos, pois essa abordagem é considerada princípio norteador no COBIT 2019. O ITIL v4 fornece a orientação acerca do gerenciamento de serviços nas organizações, no entanto, nesse guia não há prática com vistas a formular os objetivos da organização e adotar os cursos de ação de recursos necessários para atingir esses objetivos, diferentemente do COBIT 2019 que lida com essas necessidades estratégicas._

_Considerando a figura a seguir que descreve a cascata de objetivos do COBIT 2019, é correto afirmar que #1 está mais relacionado a motivadores e necessidades das partes interessadas do que à estratégia empresarial. No COBIT 2019, os riscos gerenciados dentro dos limites do compliance da governança da informação e tecnologia são tratados por processo específico no domínio construir, adquirir e implementar._

**63** O ITIL v4 possui prática específica para gerir risco, visando garantir que a organização entenda e lide com os riscos de forma eficaz, pois a gestão de riscos é essencial para o sistema de valor de serviço da organização.

_Julgue os próximos itens, em relação ao PMBOK 7.ª edição._

**64** O plano de gerenciamento dos riscos é um componente do plano de gerenciamento do portfólio que descreve como as atividades de gerenciamento de riscos serão estruturadas e executadas.

**65** Escritório de gerenciamento de projetos é uma estrutura de suporte de entrega de projeto que se concentra em criar equipes de coaching e construir habilidades e capacidades ágeis em toda a empresa.

**66** Um dos domínios de desempenho do projeto, de acordo com o PMBOK 7.ª edição, é a abordagem de desenvolvimento e do ciclo de vida, o qual consiste em fases que conectam a entrega de valor de negócios e as partes interessadas do início ao fim do projeto, facilitando a abordagem de entrega para produzir os produtos entregues pelo projeto.

_Julgue os seguintes itens, relacionados a modelagem de dados._

**67** O modelo lógico pode conter chaves primárias e estrangeiras e pode ser usado em vários bancos de dados, tais como SQL Server, MySql, Oracle e PostgreSql.

**68** Considere-se que uma tabela de nome Produto tenha os atributos cod_cliente, cod_produto, nome_produto, preco e quantidade. Nesse caso, se a chave primária for composta de cod_cliente e cod_produto, a tabela estará na segunda forma normal, pois não possui grupos repetitivos.

**69** Em uma modelagem dimensional, os elementos tabelas fato (para os dados que são métricas) e tabelas dimensões (para os dados descritivos) são opcionais, por exemplo, em um data warehouse.

**70** Os bancos de dados na nuvem podem seguir modelos de dados SQL e NoSQL; as suas principais desvantagens em relação ao banco de dados local são a privacidade e a segurança.

**71** O fato de haver um campo de chave estrangeira com o valor NULL não viola a restrição de chave estrangeira. ALUNOS(ID,Nome,Endereço,Cidade,UF) DISCIPLINA(Cod_disciplina, Nome_diciplina, Carga_horaria)

_Considerando que as tabelas precedentes façam parte de um banco de dados relacional, julgue os itens subsequentes._

**72** O comando a seguir está sintaticamente correto em PostgreSql. select count(_) total, Cidade, UF from ALUNOS group by Cidade, UF having nome like 'maria%' and count(_) > 5 order by count(_) desc;

_Julgue os itens a seguir, a respeito de gerência de riscos e sistema de gestão de continuidade de negócios (SGCN). A seguir, é apresentado um exemplo de comando DDL. DELETE TABLE DISCIPLINA WHERE Carga_horaria > 3; O comando DML a seguir está correto, pois a cláusula WHERE é opcional. UPDATE ALUNOS SET Cidade=’Curitiba’, UF=’PR’; A gestão de continuidade de negócios envolve prioritariamente os processos de análise de impacto no negócio, avaliação de risco e plano de contingência. No gerenciamento de riscos, devem ser considerados os contextos externo e interno da organização, incluindo-se o comportamento humano e os fatores culturais locais. Em uma organização, as mudanças no contexto interno organizacional são os fatores responsáveis pela eliminação completa dos riscos ou alteração de sua configuração. Na etapa de identificação de riscos, devem ser incluídos todos os riscos, com exceção dos das fontes que não estão sob seu controle, apontando-se as fontes de risco, áreas de impacto, as causas e possíveis consequências tangíveis ou intangíveis. Em um SGCN, a organização deve estabelecer as partes da organização a serem incluídas no sistema._

_Julgue os próximos itens, relativos a conceitos de ameaça, vulnerabilidade e impacto em sistemas de informação. São exemplos de vulnerabilidade em segurança da informação nas empresas públicas brasileiras: falhas humanas; malware; ransomware e spyware._

**88** O impacto de um incidente de segurança da informação diz respeito às consequências de determinado evento que acomete a segurança dos ativos.

_Julgue os itens a seguir, que tratam de computação em nuvem._

**75** Dos principais modelos de serviços de computação em nuvem, a infraestrutura como serviço (IaaS) é aquele que oferece o nível mais alto de controle sobre os recursos de TI, sendo, ainda, o mais semelhante aos recursos tradicionais de TI no local.

**76** Em computação em nuvem, a escalabilidade atende às demandas repentinas na carga de trabalho por um pequeno período, enquanto a elasticidade atende a um aumento estático da carga de trabalho.

_Acerca dos componentes centrais da arquitetura em nuvem,_

_julgue os itens subsequentes._

**77** Na computação em nuvem, as plataformas de front-end contêm a infraestrutura do cliente, como recursos de computação, armazenamento e mecanismos de segurança.

**78** Uma zona de disponibilidade (AZ) é um conjunto de data centers de regiões distintas cuja finalidade é a de disponibilizar uma coleção de recursos em uma localização geográfica.

**79** Na computação em nuvem, uma região envolve a disponibilização de uma coleção de recursos em uma localização geográfica que pode afetar características como a latência, a qual será menor quanto mais próximo à região estiverem os clientes.

_Julgue os itens seguintes, a respeito das características gerais de identidade, privacidade, conformidade e segurança na nuvem._

**80** A segurança da nuvem é compartilhada entre os provedores de serviço e os clientes, e as competências de cada um variam de acordo com o tipo de serviço oferecido; na plataforma como serviço (PaaS), por exemplo, os clientes são responsáveis por proteger tudo que está relacionado ao sistema operacional.

**81** SASE (Secure Access Service Edge) é uma arquitetura de rede que, entre outros componentes, possui o acesso à rede zero-trust, o qual verifica as identidades dos usuários e confirma a segurança do dispositivo antes de conceder acesso às aplicações autorizadas.

_Considerando a legislação acerca de privacidade e proteção de dados, julgue os itens a seguir. O responsável pela transmissão, comutação ou roteamento de dados tem o dever de tratar de forma isonômica quaisquer pacotes de dados, e a eventual ocorrência de discriminação ou degradação no tráfego desses pacotes será regulamentada nos termos das atribuições conferidas ao Congresso Nacional pelo inciso IV do art. 84 da Constituição Federal de 1988, ouvidos o Comitê Gestor da Internet e a Agência Nacional de Telecomunicações. As entidades privadas sem fins lucrativos que tenham recebido recursos públicos para a realização de ações de interesse público estão subordinadas, no que couber, à Lei n.º 12.527/2011 (Lei de Acesso à Informação). O acesso às informações de interesse público exige a necessária solicitação do interessado, que deve ser dirigida ao gestor máximo do órgão detentor dessa informação. Para efeitos da Lei de Acesso à Informação (Lei n.º 12.527/2011), documento é considerado como a unidade física de registro de informações, utilizada para materializar conhecimento. A proteção dos dados pessoais, que visa garantir a privacidade das pessoas, está prevista na Lei n.º 13.709/2018 (Lei Geral de Proteção de Dados Pessoais – LGPD) e na Lei n.º 12.965/2014 (Marco Civil da Internet). A proteção de dados pessoais é um dos princípios elencados na Política Nacional de Segurança da Informação (Decreto n.º 9.637/2018). É permitido o tratamento de dados pessoais durante estudos realizados por órgãos de pesquisas, sendo obrigatória a anonimização desses dados. Entre os serviços prestados pelo INPI, estão o registro de marca, o de patente e o de programa de computador. Considere que as empresas Alfa, Beta e Gama tenham solicitado, cada uma, apenas um dos serviços citados, que os serviços tenham sido diferentes para cada empresa e que haja prazos para as solicitações serem respondidas, sendo estes diferentes para cada tipo de serviço. Além disso, considere verdadeira cada proposição a seguir. I “A empresa Beta fez uma solicitação de registro de patente.” II “A solicitação de marca é respondida em 15 dias.” III “A solicitação da empresa Gama será respondida em 10 dias.” Essas informações estão logicamente reunidas na tabela-verdade a seguir. Note que, se o relacionamento entre o elemento da linha e o da coluna for verdadeiro, a letra V aparecerá no cruzamento da relação. A letra F indica que o relacionamento é falso. serviço prazo registro registro de registro programa de de dias dias dias de marca patente computador Alfa F F V F empresa Beta Gama F V_

**10** dias F V F F prazo 15 dias

**30** dias F A partir dessa situação hipotética, bem como considerando a tabela-verdade precedente e seu completo preenchimento, julgue os itens que se seguem.

**96** A proposição “A solicitação da empresa Beta será atendida no prazo de 30 dias, e a empresa Alfa solicitou o registro de programa de computador.” é verdadeira.

**97** A proposição “A empresa Alfa solicitou o registro de programa de computador.” é verdadeira.

_Acerca de contagem, probabilidade e teoria de conjuntos, julgue os itens a seguir._

**98** Considerando-se que os pedidos de registro de patentes diariamente recebidos pelo INPI tenham um número de protocolo e que um atendente disponha de 6 números de protocolo para registrar 3 pedidos, é correto afirmar que esse atendente terá 15 maneiras diferentes de protocolar os pedidos.

**99** Suponha que, em uma amostra de 250 processos protocolados no INPI por variadas empresas, tenha-se verificado que havia 150 pedidos de registro de patente, 120 pedidos de registro de marca e 110 pedidos de registro de programa de computador: 50 pedidos eram de registro de patente e de programa de computador; 90 pedidos eram de registro de patente e de marca; 40 pedidos eram de registro de marca e de programa de computador; e 30 pedidos eram de registro de patente, de marca e de programa de computador. Com base nessa situação hipotética, é correto concluir que a quantidade de processos em que se pedia somente o registro de patente é igual a 40 e que a quantidade de processos em que se pedia somente o registro de marca é igual a 20.

**100** Considere que, em 2019, a Diretoria de Patentes (DIRPA) do INPI tenha iniciado um projeto de combate ao backlog (fila de solicitações), para a redução da quantidade de pedidos de patente de invenção, que, em agosto de 2019, havia cerca de

**149** mil pedidos de patente e que, em novembro de 2023, havia cerca de 4.200 pedidos restantes. Nesse caso, a probabilidade de um pedido de patente ainda ter aguardado atendimento ao término do mês de novembro de 2023 é inferior a 3%. Espaço livre
