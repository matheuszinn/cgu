---
tipo: prova
concurso: "CGE_CE_18"
arquivo_origem: "Provas Cebraspe/CGE_CE_18/PROVA OBJETIVA CONHECIMENTOS ESPECIALIZADOS CARGO 3.pdf"
tags:
  - prova
  - cebraspe
  - cgu-2026
---

# PROVA OBJETIVA CONHECIMENTOS ESPECIALIZADOS CARGO 3

CEBRASPE – CGE/CE – Aplicação: 2019
CONHECIMENTOS ESPECIALIZADOS
DESENVOLVIMENTO DE SISTEMAS
DE COMPUTAÇÃO

### QUESTÃO 65

ALTER TABLE dbo.Ordens ADD CONSTRAINT
DFT_Ordens_ordemts DEFAULT(SYSDATETIME()) FOR
ordemts;
Considerando que a ferramenta SonarQube permite analisar código
gerado na linguagem Java e em outras linguagens, assinale a opção
que indica erro que, na análise do código de um sistema de recursos
humanos, pode ser identificado como configuração default dessa
ferramenta.
O código precedente modifica a tabela Ordens (composta
por ordens de venda e ordemts – data/hora do pedido), em um
banco de dados MS-SQL Server.
A método de conexão do banco de dados com tratamento de
erro/exceção ou falha da conexão

### QUESTÃO 61

Após essa modificação, sempre que for inserida uma nova ordem de
venda,
A se não for definido um valor para o campo ordemts, o sistema
invocará a função SYSDATETIME.
B será obrigatório o preenchimento manual do campo ordemts.
C se não for definido um valor para o campo ordemts, este
ficará Null.
D se for definido um valor para o campo ordemts, o banco de
dados retornará erro de dado não permitido.
E se não for definido um valor Null para o campo ordemts, o
banco de dados retornará erro de dado não permitido.

### QUESTÃO 62

O Spring Framework utiliza os chamados controllers, que são
classes mapeadas por meio de annotations e servem para dizer
à aplicação o que exibir quando for requisitada uma página
no navegador. Ao se requisitar uma URL em um sistema
desenvolvido em Spring Framework, a classe @Controller
verificará a URL que foi solicitada, por meio da anotação
A
B
C
D
E
@NodeEntity.
@RequestMapping.
@StartNode.
@Configuration.
@EnableAutoConfiguration.

### QUESTÃO 63

As estruturas básicas que constituem um JSon são
A uma lista de valores e uma coleção de strings/inteiros.
B uma lista de inteiros e uma coleção de pares de strings.
C uma lista de valores ordenados e uma coleção de pares
nome/valor.
D uma lista de strings e uma coleção de pares de booleanos.
E uma lista de booleanos e uma coleção de listas de strings.

### QUESTÃO 64

Nos testes unitários, é possível testar uma classe ou até mesmo um
objeto Java. Nesse contexto, uma classe, para ser testada pelo Junit,
deve se estender a partir de
A
B
C
D
E
Collection.
TestExecution.
TestSetUp.
TestCase.
TestReporter.
B método de retorno de inteiro com tratamento de retorno de
nulo
C método de retorno de nome da base de dados com tratamento
de exceção caso não se estabeleça a conexão ou não se
encontrem dados
D método projetado para verificar uma conexão de banco de
dados e tratar exceção, caso ocorra
E método projetado para verificar a igualdade e que sempre
retorna falso

### QUESTÃO 66

Em uma aplicação de votação online desenvolvida em três camadas
do tipo MVC, o controller é responsável por
A transformar eventos gerados pela view em ações de negócio,
alterando o model.
B transformar eventos gerados pela view em ações temporárias de
negócio.
C manipular a tela com dados de negócio que podem ser
alterados diretamente com o banco de dados.
D manipular o model do sistema responsável pela interface com
o cliente.
E alterar a view do sistema que contém a lógica do negócio.

### QUESTÃO 67

No modelo REST de desenvolvimento de web services, o método
HTTP é utilizado para determinar a operação ou o método a ser
executado. A esse respeito, assinale a opção correta.
A O referido modelo impõe uma padronização no formato da
URL a ser utilizada.
B O modelo REST deixa a cargo de quem provê o serviço a
definição da URL a ser utilizada.
C No modelo em questão, os parâmetros devem ser
obrigatoriamente do tipo JSon.
D Os parâmetros do modelo definem a requisição dos métodos a
serem acessados, tornando o acesso automatizado.
E O método TRACE do HTTP não pode ser manipulado pelo
modelo REST.
CEBRASPE – CGE/CE – Aplicação: 2019
GESTÃO E GOVERNANÇA DE
TECNOLOGIA DA INFORMAÇÃO

### QUESTÃO 68

Os web services evoluíram para integrar aplicativos e fornecer
serviços, no entanto apresentam inúmeros riscos de ataques.
O ataque que força a reinicialização do sistema, consumindo todos

### QUESTÃO 71

os recursos, é denominado
Julgue os itens a seguir, relativos ao sistema de gestão de segurança
da informação (SGSI).
A XML injection.
I
B SQL injection.
C DoS attack.
D cross-site scripting.
E invalid types.

### QUESTÃO 69

O gerenciador de conteúdo e de documentos Alfresco possui vasta
biblioteca que pode ser customizada pelo cliente. Acerca desse
assunto, assinale a opção correta.
A O Alfresco desenha fluxogramas por meio da criação de regras
automáticas por usuário e todos os documentos.
B Um documento disponibilizado no portal Alfresco do cliente
possui características não editáveis, o que impede o
gerenciador de documentos de indexar para buscas futuras.
C Um grupo de usuários do portal Alfresco possui acesso apenas
aos documentos originais do sistema.
D Ao acessar o Alfresco na última versão do Firefox, é possível
adicionar folders e seus arquivos, inclusive subdiretórios,
apenas arrastando-os e soltando-os dentro de sua biblioteca.
E Uma pasta de documentos possui regras apenas para os
De acordo com a NBR ISO/IEC 27001, no desenvolvimento e
na implantação do SGSI, os riscos devem ser mensurados e
considerados unicamente a partir da fase de operação.
II De acordo com a NBR ISO/IEC 27001, na operação de
sistemas, a organização deve controlar tanto os processos
terceirizados quanto as mudanças no sistema.
III De acordo com a NBR ISO/IEC 27002, para a segurança física
e ambiental, deve-se adotar uma política de mesa limpa e tela
bloqueada.
Assinale a opção correta.
A
B
C
D
E

### QUESTÃO 72

Segundo a NBR ISO/IEC 27005, a opção de tratamento de risco
que consiste na possibilidade de aceitação do ônus da perda ou do
benefício do ganho associado a determinado risco é denominada
A
B
C
D
E
documentos contidos no diretório raiz do documento, e as
subpastas não herdam essas regras.

### QUESTÃO 70

A Apache ANT é uma biblioteca Java e uma ferramenta de linha de
comando. Em relação ao arquivo build.xml, a ser interpretado
pelo ANT, assinale a opção correta.
A A tag property, no ANT, contém apenas um atributo, que é
denominado name.
B A tag target, no ANT, deve conter um atributo determinado
value, que é único e imutável.
C A tag macrodef, no ANT, contém definições de criação de
diretório.
D Apenas uma tag property representando os arquivos de
configuração deve constar no arquivo build.xml.
E Apenas uma tag project representando o escopo de início e
fim do projeto deve constar no arquivo build.xml.
Apenas o item I está certo.
Apenas o item II está certo.
Apenas os itens I e III estão certos.
Apenas os itens II e III estão certos.
Todos os itens estão certos.
redução do risco.
retenção do risco.
ação de evitar o risco.
compartilhamento do risco.
transferência do risco.

### QUESTÃO 73

De acordo com o PMBOK 5.ª edição, julgue os próximos itens,
relativos a gerenciamento de projetos.
I
O plano de gerenciamento dos custos, além de estabelecer
como os custos do projeto serão gerenciados e controlados,
inclui também o método utilizado para estimar o custo das
atividades.
II A estrutura analítica do projeto (EAP), ainda que não lide com
as entregas, fornece as relações entre todos os componentes do
projeto.
III Controlar os custos do projeto inclui monitorar o andamento do
projeto e gerenciar as mudanças feitas na linha de base de
custos.
Assinale a opção correta.
A
B
C
D
E
Apenas o item I está certo.
Apenas o item II está certo.
Apenas os itens I e III estão certos.
Apenas os itens II e III estão certos.
Todos os itens estão certos.
CEBRASPE – CGE/CE – Aplicação: 2019

### QUESTÃO 74

De acordo com o PMBOK 5.ª edição, há um documento que define
os requisitos para a aprovação de um projeto que influenciarão o
gerenciamento dos custos. Esse documento fornece também um
resumo de orçamento a partir do qual os custos detalhados do
projeto serão desenvolvidos. O referido documento é denominado
A plano de gerenciamento de custos.
B linha de base de custos.
C especificação do escopo do projeto.
D termo de abertura do projeto.
E dicionário da estrutura analítica do projeto.

### QUESTÃO 75

Ao avaliar o funcionamento da central de serviços de
determinado órgão, um analista de TI observou que todos os
chamados recebidos pela central de serviços foram classificados
como incidentes, antes mesmo de qualquer diagnóstico. Verificou
também que, quando possível, alguns incidentes foram resolvidos
pela própria central, no primeiro contato.
Acerca dessa situação, à luz da ITIL v3, é correto afirmar que o
gerenciamento de serviços realizado nesse órgão foi
A compatível com a ITIL, pois todos os chamados devem ser
classificados como incidentes, sem a necessidade de
diagnóstico prévio.
B compatível com a ITIL, pois todo chamado deve ser alterado
de incidente para problema ou requisição, mas somente após
a sua classificação.
C compatível com a ITIL apenas no que se refere ao fato de a
central de serviços não ter realizado diagnósticos dos
chamados recebidos, o que não é de sua competência.
D compatível com a ITIL apenas no que se refere ao fato de a
central de serviços poder resolver incidentes no primeiro
contato, quando possível.
E incompatível com a ITIL, pois não compete à central
classificar chamadas, realizar diagnósticos nem resolver
incidentes.

### QUESTÃO 76

Segundo a ITIL v3, no estágio desenho de serviço, a saída principal
que inclui todas as informações necessárias para gerenciar o ciclo
de vida de um serviço novo ou alterado é o
A pacote de nível de serviço (PNS).
B requisito de nível de serviço (RNS).
C acordo de nível de serviço (ANS).
D procedimento padrão de operação (PPO).
E pacote de desenho de serviço (PDS).

### QUESTÃO 77

Com base no COBIT 5, julgue os itens a seguir.
I
Existe, no domínio Avaliar, Dirigir e Monitorar, processo
destinado a garantir que desempenho, medição e relatórios de
conformidade da TI corporativa sejam transparentes às partes
interessadas.
II
Para cada habilitador no COBIT, é possível definir um
conjunto específico de metas relevantes para apoiar os
objetivos de TI.
III A gestão, diferentemente da governança, visa garantir que as
necessidades das partes interessadas sejam avaliadas a fim de
determinar objetivos corporativos.
Assinale a opção correta.
A Apenas o item I está certo.
B Apenas o item III está certo.
C Apenas os itens I e II estão certos.
D Apenas os itens II e III estão certos.
E Todos os itens estão certos.
Espaço livre
CEBRASPE – CGE/CE – Aplicação: 2019
REDES DE COMPUTADORES

### QUESTÃO 78

À luz do COBIT, é necessário gerenciar as seguintes tarefas:
I
II
desenvolver e(ou) adquirir soluções de TI;
implementar e integrar as soluções de TI junto aos processos
de negócio;
III realizar mudanças e manutenções em sistemas existentes.
De acordo com os objetivos dos domínios do COBIT 5, é correto
afirmar que as tarefas descritas em
A I e II pertencem ao domínio Construir, Adquirir e Implementar,
e as descritas em III pertencem ao domínio Entregar, Reparar
e Suportar.
B I, II e III pertencem ao domínio Entregar, Reparar e Suportar.
C I pertencem ao domínio Construir, Adquirir e Implementar,
e as descritas em II e III pertencem ao domínio Alinhar,
Planejar e Organizar.
D I, II e III pertencem ao domínio Construir, Adquirir e
Implementar.
E I pertencem ao domínio Alinhar, Planejar e Organizar, as
descritas em II pertencem ao domínio Construir, Adquirir
e Implementar, e as descritas em III pertencem ao domínio
Entregar, Reparar e Suportar.

### QUESTÃO 79

A respeito dos níveis de capacidade e maturidade do MPS.BR,
assinale a opção correta.
A Os níveis de capacidade dos processos são descritos por
atributos de processo (AP) caracterizados pela habilidade
de o processo alcançar os objetivos de negócio.
B Os níveis de capacidade e de maturidade são descritos por
meio de sete letras, do G ao A.
C A organização deve escolher, entre os níveis de capacidade
e de maturidade, qual estratégia adotar, pois não é possível
combinar essas estratégias.
D É possível atingir o nível de maturidade/capacidade E sem
atingir os níveis F ou G.
E Tanto os níveis de capacidade como os de maturidade são
descritos por meio dos nove seguintes pares de números: 1.1,
2.1, 2.2, 3.1, 3.2, 4.1, 4.2, 5.1 e 5.2.

### QUESTÃO 80

Assinale a opção que indica o processo do MPS.BR no qual se
espera que as necessidades, as expectativas e as restrições do
cliente, tanto do produto quanto de suas interfaces, sejam
identificadas.
A
B
C
D
E
gerência de requisitos
gerência de projetos
desenvolvimento de requisitos
validação
verificação

### QUESTÃO 81

Em determinada rede de comunicação, a transmissão tem
como característica o envio de dados caractere a caractere, em que
cada caractere é antecedido de um sinal de início e sucedido de um
sinal de fim.
Nesse caso, a técnica de transmissão de dados em uso é a
A
B
C
D
E
paralela síncrona.
half-duplex assíncrona.
serial assíncrona.
multiponto síncrona.
full-duplex assíncrona.

### QUESTÃO 82

Um pacote de dados em uma rede de comunicação contém
um campo com informação de camadas superiores e pode ser
fragmentado se exceder o tamanho máximo permitido.
Nesse caso, utiliza-se a comutação de
A
B
C
D
E
circuito.
pacote.
célula.
rede.
malha.

### QUESTÃO 83

Em uma rede de comunicação, quando um dispositivo
transmite um sinal, toda a rede fica ocupada; se outro dispositivo
tentar enviar um sinal ao mesmo tempo, ocorrerá uma colisão e a
transmissão deverá ser reiniciada.
Nessa situação, a topologia dessa rede de comunicação é do tipo
A
B
C
D
E
barramento.
anel.
estrela.
árvore.
ponto a ponto.

### QUESTÃO 84

Para reduzir a complexidade de projeto, as redes de comunicação
são normalmente organizadas em camadas ou níveis. A esse
respeito, assinale a opção correta.
A As interfaces entre as camadas devem ser dependentes, de tal
maneira que uma interface não possa ser modificada sem
alteração nas camadas intermediárias.
B As camadas devem ficar isoladas para garantir a dependência
da multiplexação de unidades de dados de protocolo, para que
não ocorram problemas de roteamento.
C O objetivo das camadas consiste em ofertar serviços de
roteamento sem preocupação com a origem e o destino da
comunicação.
D As camadas inferiores devem oferecer certos serviços para as
camadas superiores, isolando os detalhes de como os serviços
oferecidos estão atualmente implementados.
E A camada de mais alto nível deve ser capaz de fazer a
checagem de erros na camada de mais baixo nível.
CEBRASPE – CGE/CE – Aplicação: 2019

### QUESTÃO 85

No endereçamento TCP/IP, para decidir se roteia determinado
pacote, um roteador realiza, entre outras, uma operação algébrica
do tipo

### QUESTÃO 88

Com relação à tecnologia de rede Gigabit Ethernet, assinale a
opção correta.
A Gigabit Ethernet é um protocolo sem compatibilidade com os
A OU lógico entre o endereço IP de origem e a máscara de rede
do destino.
padrões anteriores da família Ethernet e foi projetado para
B OU lógico entre o endereço IP de destino e a sua máscara
de rede.
B No caso do padrão 1000Base-X, se emprega a codificação
C E lógico entre o endereço IP de origem e a máscara de rede
do destino.
D E lógico entre o endereço IP de origem e a sua máscara
de rede.
E E lógico entre o endereço IP de destino e a sua máscara
de rede.

### QUESTÃO 86

No modelo OSI, é função da camada física
funcionar com fibra óptica e com par trançado.
8b/10b, em que, para cada 8 bits de dados, são usados10 bits
para a transmissão.
C No Gigabit Ethernet com transmissão em fibra óptica
monomodo, a distância de enlace é limitada em 30 km.
D O padrão Gigabit Media-Independent Interface permite a
qualquer transceptor se conectar ao controlador, desde que isso
ocorra no padrão 1000Base-X.
E No padrão 1000Base-T, são utilizados apenas 2-níveis PAM
(pulse amplitude modulation).

### QUESTÃO 89

A estabelecer e liberar conexões, além de definir a sequência de
pinos de conectores e suas respectivas funções.
B realizar a fragmentação das mensagens fim a fim, quando
necessário.
C realizar o controle de congestionamento entre hosts.
O protocolo de segurança relacionado ao WPA2 é utilizado em uma
rede sem fio no padrão
A IEEE 802.11k, em conjunto com o algoritmo AES para
criptografia.
D quebrar os dados de entrada em quadros, bem como criar e
reconhecer as fronteiras dos quadros.
B IEEE 802.11n, em conjunto com o algoritmo blowfish para
E gerenciar o diálogo de uma forma ordenada para determinado
serviço solicitado.
C IEEE 802.11i, em conjunto com o algoritmo AES para

### QUESTÃO 87

A respeito das características da arquitetura cliente-servidor, julgue
os itens a seguir.
I
Nessa arquitetura, por padrão, deve existir comunicação de um
cliente com outros clientes.
II Um servidor deve ser capaz de atender solicitações de
múltiplos clientes de maneira simultânea.
III Do lado do processo servidor, os serviços não podem ser
distribuídos.
IV Em termos de implementação, normalmente o processo do lado
servidor é mais complexo que o processo do lado cliente.
criptografia.
criptografia.
D IEEE 802.11b, em conjunto com o algoritmo RC4 para
criptografia.
E IEEE 802.11p, em conjunto com o algoritmo blowfish para
criptografia.

### QUESTÃO 90

Dois roteadores, A e B, são ligados fisicamente por um
mesmo enlace. O roteador A é responsável pelo encaminhamento
de pacotes destinados à rede C, que tem endereçamento 10.1.1.0/25,
e o roteador B é responsável pelo encaminhamento de pacotes
destinados à rede D, que tem endereçamento 10.1.1.128/25.
Considerando essas informações, assinale a opção que apresenta o
Estão certos apenas os itens
endereço de broadcast da rede C e da rede D, respectivamente.
A I e II.
A 10.1.1.1 e 10.1.1.129
B I e III.
C II e IV.
B 10.1.1.127 e 10.1.1.254
C 10.1.1.126 e 10.1.1.255
D I, III e IV.
D 10.1.1.127 e 10.1.1.255
E II, III e IV.
E 10.1.1.1 e 10.1.1.254
CEBRASPE – CGE/CE – Aplicação: 2019
SEGURANÇA DA INFORMAÇÃO

### QUESTÃO 91

A política de segurança da informação de uma organização deve ter
como objetivo prover
A regras para a criação de processos ligados ao negócio.
B controle sobre os processos de tecnologia da informação.
C metodologia para a implantação de soluções de segurança da
informação.
D recursos financeiros para proteger as informações da
organização contra ações maliciosas.
E orientações embasadas nos requisitos do negócio da
organização, em conformidade com as leis e regulamentações.

### QUESTÃO 92

Assinale a opção que indica mecanismo que, em uma rede de
comunicação sem fio, apresenta maior nível de criptografia de
dados.
A
B
C
D
E
WPA-2 (wi-fi protected access-2)
WEP (wired equivalent privacy)
HTTP (hypertext transfer protocol)
FTP (file transfer protocol)
SMTP (simple mail transfer protocol)

### QUESTÃO 93

Após o envio de um email pelo emissor a determinado
destinatário, ocorreu uma ação maliciosa e o email foi lido por
terceiro.
Nessa situação, a ação maliciosa é do tipo
A
B
C
D
E
sniffing.
spoofing.
brute force.
defacement.
denial of service.

### QUESTÃO 94

Para proteger a comunicação em uma organização que possui várias
redes internas de computadores interligadas entre si e também à
Internet contra ações maliciosas no tráfego dos dados, o mecanismo
a ser utilizado é o
A
B
C
D
E
registro de logs.
antispam.
firewall.
antispyware.
controlador de domínio.

### QUESTÃO 95

De acordo com NBR ISO/IEC 27001, em um sistema de gestão de
segurança da informação (SGSI), o escopo é definido na fase
A
B
C
D
E
analisar.
estabelecer.
implementar.
manter.
melhorar.

### QUESTÃO 96

À luz da NBR ISO/IEC 27001, assinale a opção que indica o
controle que orienta as organizações quanto à asseguração da
eficácia da sua política de segurança da informação.
A
B
C
D
E
segregação de funções
contato com autoridades
políticas para a segurança da informação
análise crítica das políticas para segurança da informação
metodologia de segurança da informação

### QUESTÃO 97

De acordo com a NBR ISO/IEC 27001, é necessário assegurar que
as partes externas e os funcionários que estejam ligados à
organização entendam suas responsabilidades e fiquem aderentes
à conformidade dos papéis para os quais foram selecionados. Nesse
contexto, um treinamento de segurança da informação com a
finalidade de conscientização deve ser aplicado
A
B
C
D
E
antes da fase de contratação.
durante a fase de contratação.
em eventual mudança de contratação.
no encerramento da contratação.
em processo disciplinar.

### QUESTÃO 98

Em uma organização em que se processam dados pessoais
sensíveis, existe a preocupação com o manuseio dos dados pelos
empregados, para que não aconteçam vazamentos de dados
e exposição indevida de pessoas. Segundo a NBR ISO/IEC 27002,
para assegurar que as referidas informações pessoais recebam o
nível adequado de proteção, deve-se utilizar como controle
A
B
C
D
E
o descarte de mídias.
o uso aceitável de ativos.
o gerenciamento de chaves.
o provisionamento para acesso de usuário.
a classificação da informação.

### QUESTÃO 99

Com fundamento na NBR ISO/IEC 27001 e na
NBR ISO/IEC 27005, uma organização decidiu implantar um
sistema de gestão de segurança da informação (SGSI), a fim de
apoiar o processo de gestão dos riscos, os quais foram listados
de acordo com o escopo estabelecido para o SGSI.
Nessa situação, após os riscos serem listados, deve ser executada a
fase de
A definir contexto dos riscos.
B valorar os ativos.
C tratar os riscos.
D definir critérios de aceitação dos riscos.
E compartilhar os riscos.
CEBRASPE – CGE/CE – Aplicação: 2019

### QUESTÃO 100

Determinada organização pretende realizar uma mudança nos seus recursos de tecnologia da informação, criando ambientes
diferentes para desenvolvimento, teste e produção de software, o que afetará a segurança da informação.
Considerando o disposto na NBR ISO/IEC 27001, assinale a opção que indica o controle que deve ser aplicado pela organização nessa
situação.
A registro de eventos
B gestão de mudanças
C gestão de capacidade
D gestão de vulnerabilidades técnicas
E restrições quanto à instalação de softwares
Espaço livre
