---
tipo: prova
concurso: "tce_ms_25"
arquivo_origem: "Provas/PDF/tce_ms_25/PROVA OBJETIVA CONHECIMENTOS ESPECIFICOS CARGO 5.pdf"
tags:
  - prova
  - cebraspe
  - cgu-2026
---

# PROVA OBJETIVA CONHECIMENTOS ESPECIFICOS CARGO 5

Nas questões que avaliarem conhecimentos de informática e(ou) tecnologia da informação, a menos que seja explicitamente
informado o contrário, considere que todos os programas mencionados estão em configuração-padrão e que não há restrições de
proteção, de funcionamento e de uso em relação aos programas, arquivos, diretórios, recursos e equipamentos mencionados.

## CONHECIMENTOS ESPECÍFICOS

_Questão 43_

### Questão 41

Julgue os próximos itens, relativos ao Windows Subsystem Linux
(WSL) e ao pacote Microsoft Office.
I
No Windows, o WSL permite a execução de um ambiente
Linux sem a necessidade de dual boot.
II No Excel, ao selecionar a célula B2 e ativar o recurso
Congelar Painéis,
apenas as colunas à esquerda serão
congeladas.
III No PowerPoint, é possível vincular dados de uma planilha do
Excel, de modo que as alterações feitas na planilha são
atualizadas na apresentação.
Assinale a opção correta.
A Apenas o item III está certo.
B Apenas os itens I e II estão certos.
C Apenas os itens I e III estão certos.
E Todos os itens estão certos.

### Questão 42

Durante uma auditoria acerca do uso de recursos
tecnológicos em um órgão público, observou-se que os servidores
utilizam intranet para comunicação interna e navegadores
distintos (Microsoft Edge e Google Chrome) para acesso a
sistemas, além de serviços de email corporativo (Outlook)
integrados a soluções de computação em nuvem.
A partir da situação hipotética precedente, assinale a opção
correta, considerando boas práticas de governança de TI e
conceitos correlatos.
A A utilização de navegadores distintos compromete a
segurança da informação, visto que apenas navegadores
homologados por órgãos de segurança são totalmente livres
de vulnerabilidades.
B A sincronização do Outlook com o Microsoft Cloud torna
inviável o uso de autenticação condicional, disponibilizando
os dados sem controle associado.
C O uso de computação em nuvem exige a substituição imediata
de toda a infraestrutura local, pois modelos híbridos não são
recomendados em ambientes públicos.
D A intranet, diferentemente da Internet, não requer protocolos
comunicação
padronizados,
podendo
operar
com
protocolos proprietários específicos de cada instituição.
E Os navegadores Edge e Chrome operam em ambientes
internos e externos, desde que façam parte da mesma pilha de
protocolos TCP/IP.
A Firewalls são projetados exclusivamente para filtrar tráfego
de rede em servidores, não possuindo aplicação em estações
de trabalho.
B Ransomware é um tipo de worm que utiliza exclusivamente
falhas de hardware para se propagar e criptografar dados.
C Rootkits são utilizados para impedir a propagação de worms,
pois reforçam o sistema operacional com mecanismos nativos
de defesa.
D O modelo 3-2-1 de backup recomenda que sejam feitas três
cópias dos dados, em dois tipos diferentes de mídia, estando
pelo menos uma dessas cópias fora do ambiente físico
principal.
E Antivírus e antispywares modernos utilizam apenas
assinaturas estáticas para detectar ameaças, o que limita sua
eficácia contra malwares desconhecidos.
Espaço livre
D Apenas os itens II e III estão certos.
de
Considerando o contexto das práticas de segurança da
informação em órgãos públicos, assinale a opção correta acerca
de procedimentos de segurança, pragas virtuais, aplicativos de
proteção, backup e armazenamento em nuvem.

### Questão 44


### Questão 45

Considere a seguinte tabela Funcionarios em um banco
de dados relacional de funcionários de uma empresa.
CREATE TABLE Funcionarios (
id INT PRIMARY KEY,
nome VARCHAR(100),
salario DECIMAL(10, 2),
departamento VARCHAR(50)
);
Considere, ainda, que os seguintes dados sejam inseridos
nessa tabela.
INSERT INTO Funcionarios (id, nome,
departamento) VALUES
(1, 'Ana', 3000.00, 'Vendas'),
(2, 'Bruno', 4500.00, 'TI'),
(3, 'Carlos', 3500.00, 'Vendas'),
(4, 'Diana', 5000.00, 'TI'),
(5, 'Elena', 4000.00, 'Financeiro');
salario,
A partir dessas informações, assinale a opção que corresponde à
consulta SQL que retorna o nome do funcionário (ou
funcionários, se houver empate) com o maior salário por
departamento.
A SELECT f1.departamento, f1.nome, f1.salario
FROM Funcionarios f1
WHERE f1.salario = (
SELECT MAX(f2.salario)
FROM Funcionarios f2
GROUP BY f2.departamento
HAVING f2.departamento = f1.departamento
);
B SELECT f1.departamento, f1.nome, f1.salario
FROM Funcionarios f1
WHERE f1.salario = (
SELECT MAX(f2.salario)
FROM Funcionarios f2
);
C SELECT f1.departamento, f1.nome, f1.salario
FROM Funcionarios f1
WHERE f1.salario = (
SELECT MAX(f2.salario)
FROM Funcionarios f2
WHERE f2.departamento = f1.departamento
);
D SELECT departamento, nome, MAX(salario)
FROM Funcionarios
GROUP BY departamento;
E SELECT f1.departamento, f1.nome, f1.salario
FROM Funcionarios f1
WHERE f1.salario = (
SELECT MAX(f2.salario)
FROM Funcionarios f2
GROUP BY f2.departamento
);
Ao não realizar o mapeamento direto do esquema conceitual
global para os esquemas internos locais em um banco de dados
distribuído, busca-se evitar
A a junção, em um único passo, dos critérios de distribuição e
da estratégia de armazenamento.
B a necessidade de duplicar os mesmos dados em todos os nós
do sistema.
C a sobrecarga do diretório de dados global com funções de
mapeamento.
D a ausência de autonomia dos nós na definição de sua estrutura
interna.
E a duplicidade de funções entre o nível externo e o nível
interno.

### Questão 46

Com base na Lei Geral de Proteção de Dados Pessoais (Lei
n.º 13.709/2018), a disciplina da proteção de dados pessoais tem
como fundamentos
I o desenvolvimento econômico e tecnológico e a inovação.
II a proteção da autodeterminação informativa.
III a inviolabilidade da intimidade, da honra e da imagem.
IV a liberdade de expressão, de informação, de comunicação e
de opinião.
Assinale a opção correta.
A Apenas os itens I, II e III estão certos.
B Apenas os itens I, II e IV estão certos.
C Apenas os itens I, III e IV estão certos.
D Apenas os itens II, III e IV estão certos.
E Todos os itens estão certos.

### Questão 47

No contexto dos algoritmos de classificação em inteligência
artificial, a técnica caracterizada por construir hiperplanos de
separação em espaços de alta dimensão, visando maximizar a
margem entre classes, é denominada
A support vector machine.
B random forest.
C k-nearest neighbors.
D naive Bayes.
E decision tree.

### Questão 48

Em LLM (large language models), como o GPT, o mecanismo
principal que permite gerar um texto coerente e contextualizado é
denominado
A algoritmos de busca por vizinhos mais próximos.
B redes neurais convolucionais.
C modelos de Markov de alta ordem.
D árvores de decisão com bagging.
E redes transformer baseadas em atenção.

### Questão 49

class Funcionario:
def __init__(self, nome, salario):
self.nome = nome
self.salario = salario
def bonus(self):
return self.salario * 0.10
class Gerente(Funcionario):
def bonus(self):
return super().bonus() + 500
func = Funcionario("Ana", 2000)
ger = Gerente("Bruno", 3000)
print(func.bonus())
print(ger.bonus())
print(isinstance(ger, Funcionario))
Considere o código Python precedente. Assinale a opção que
corresponde ao resultado da execução desse código.
A 200.0
300.0
True
B 200.0
500.0
False
C 800.0
500.0
False
D 200.0
800.0
True
E 200.0
800.0
False
Espaço livre

### Questão 50

interface Pagavel {
double calcularPagamento();
}
class Freelancer implements Pagavel {
double horasTrabalhadas;
double valorHora;
Freelancer(double horas, double valor) {
this.horasTrabalhadas = horas;
this.valorHora = valor;
}
}
public double calcularPagamento() {
return horasTrabalhadas * valorHora;
}
class Consultor extends Freelancer {
double bonus;
Consultor(double horas,
double bonus) {
super( horas, valor);
this.bonus = bonus;
}
double
valor,
@Override
public double calcularPagamento() {
return
super.calcularPagamento()
bonus;
}
}
+
public class TestePagamento {
public static void main(String[] args) {
Pagavel f = new Freelancer(40, 50);
Pagavel c = new Consultor(30, 80, 500);
System.out.println(f.calcularPagamento());
System.out.println(c.calcularPagamento());
System.out.println(f instanceof Consultor);
}
}
Considere o código Java 17 acima. Assinale a opção que
corresponde ao resultado da execução do código em apreço no
console.
A 2900.0
2000.0
false
B 2000.0
2900.0
false
C 50
false
D 2000.0
2900.0
true
E 50
true

### Questão 51

Considerando os conceitos de segurança física e segurança
lógica, assinale a opção em que são apresentadas medidas que
correspondem à aplicação simultânea desses dois tipos de
segurança.
A implementação de backups diários em nuvem pública e
criptografia dos dados antes da transmissão
B utilização de senhas complexas e renovação periódica dos
patches de segurança dos servidores
C reforço da estrutura predial contra incêndios e instalação de
nobreaks que mantenham os servidores ativos em caso de
falha elétrica
D instalação de câmeras de vigilância nos corredores e restrição
do acesso a áreas sensíveis por meio de autenticação
biométrica integrada ao controle de login do sistema
E implementação de um firewall de última geração e
monitoramento da rede por meio de sistemas de detecção de
intrusos (IDS)

### Questão 52

Acerca dos métodos de autenticação (senhas, tokens, certificados
e biometria), assinale a opção correta.
A Por não requererem integração com hardware adicional, as
senhas descartáveis (OTP) são menos seguras que as
estáticas.
B Tokens físicos ou virtuais são vantajosos porque podem
fornecer autenticação baseada em algo que o usuário possui, o
que reduz o risco de compartilhamento indevido.
C Certificados digitais têm como principal fraqueza o fato de
dependerem de uma autoridade certificadora, o que
inviabiliza o seu uso em ambientes corporativos.
D A biometria é o método de autenticação recomendável em
todos os casos porque não está sujeita a falhas de leitura nem
a riscos de falsificação.
E Senhas oferecem maior resistência contra ataques de força
bruta que biometria.

### Questão 53

No que se refere a phishing, pharming e hoax, assinale a opção
correta.
A O phishing caracteriza-se pelo envio de mensagens enganosas
que simulam comunicações legítimas para a obtenção de
dados confidenciais do usuário.
B O pharming é um golpe baseado em correntes de email que
disseminam boatos ou informações falsas para enganar o
usuário.
C O hoax consiste na captura de senhas e dados bancários por
meio de formulários fraudulentos em sites clonados.
D No furto de identidade, criminosos criam sites falsos que
redirecionam o usuário para páginas aparentemente legítimas
a fim de capturar credenciais de acesso.
E Na fraude de antecipação de recursos, a vítima é induzida a
fornecer informações pessoais em troca de supostos prêmios
inexistentes.

### Questão 54

Em relação ao ransomware e às formas de prevenção e combate a
esse tipo de ataque, assinale a opção correta.
A O uso de backups regulares e atualizados reduz
significativamente o impacto de um ataque de ransomware.
B A melhor forma de se evitar ransomware é desativar
periodicamente os antivírus, para permitir sua atualização sem
interferências.
C Evitar atualizações sistemáticas diminui as chances de
infecção do sistema por ransomware, pois previne conflitos
com softwares de segurança.
D O ransomware atua apenas contra servidores em nuvem, não
afetando dispositivos locais.
E O ataque por ransomware, embora infecte o sistema, não
restringe o acesso a arquivos ou dispositivos.

### Questão 55

Assinale a opção correta a respeito da DMZ (demilitarized zone).
A A implementação de DMZ substitui o uso de IDS/IPS, pois
concentra toda a proteção na configuração de roteadores e
switches.
B A DMZ é implementada exclusivamente em ambientes de
nuvem, não sendo aplicável em data centers locais.
C A DMZ é uma zona de rede que abriga serviços acessíveis
externamente, separando-os da rede interna para reduzir o
impacto de comprometimentos.
D A DMZ consiste em uma rede isolada que impede totalmente
a comunicação entre servidores expostos e a rede interna, o
que elimina a necessidade de regras de firewall.
E A função principal da DMZ é criptografar dados em trânsito
entre clientes e servidores internos de forma a garantir a
confidencialidade.

### Questão 56

Assinale a opção correta no que diz respeito às VPN (virtual
private networks).
A As VPN IPSec operam apenas no modo transporte e garante a
segurança de cabeçalhos e payloads embora não permita
tunelamento entre redes inteiras.
B Uma VPN de acesso remoto garante a confidencialidade
apenas se a rede do usuário final for segura, pois não utiliza
protocolos de criptografia para proteger o tráfego de dados.
C O uso de VPN substitui totalmente a necessidade de firewalls,
já que o túnel criptografado estabelecido por ela impede
qualquer ataque externo.
D As VPN baseadas em SSL/TLS são restritas ao transporte de
tráfego de email corporativo, não suportando aplicações web.
E A VPN do tipo site-to-site estabelece túneis criptografados
entre redes distintas, sendo frequentemente utilizada para
conectar filiais de uma mesma organização.

### Questão 57

No que concerne aos dispositivos de segurança, assinale a opção
correta.
A O firewall local, no host, substitui a necessidade de proxies,
IDS e IPS, já que é suficiente, por si mesmo, para prover
segurança completa em uma rede corporativa.
B O IPS (intrusion prevention system) apenas registra tentativas
de ataque, sem possibilidade de reação em tempo real.
C O proxy garante a confidencialidade do tráfego entre usuários
e servidores, pois utiliza exclusivamente criptografia de ponta
a ponta.
D O firewall tem como função principal analisar o conteúdo de
mensagens de email para identificar vírus e removê-los
automaticamente.
E O IDS (intrusion detection system) monitora o tráfego de rede
para identificar padrões suspeitos ou maliciosos.

### Questão 58


### Questão 61

Assinale a opção correta no que se refere aos sistemas de
criptografia simétricos e assimétricos.
Julgue os próximos itens, relativos aos tipos de planejamento
organizacional e suas características.
A Criptografia assimétrica não oferece segurança para
assinaturas digitais.
B Em sistemas simétricos, são usadas duas chaves diferentes:
uma para criptografia e outra para descriptografia.
C Nos sistemas simétricos, é usada a mesma chave para
criptografia e descriptografia, ao passo que, nos assimétricos,
são utilizadas uma chave pública para criptografia e
uma chave privada para descriptografia.
D Criptografia simétrica não exige troca de chaves entre
remetente e destinatário.
E O tempo de processamento nos sistemas assimétricos é menor
que nos simétricos.
I

### Questão 59

A respeito das normas técnicas ABNT NBR ISO/IEC 27001 e
ABNT NBR ISO/IEC 27002, assinale a opção correta.
A Ambas as normas aplicam-se obrigatoriamente a todas as
instituições educacionais brasileiras.
B A ABNT NBR ISO/IEC 27002 substitui a necessidade de
outras normas de gestão de riscos em TI; a aplicação da
ABNT NBR ISO/IEC 27001 é obrigatória apenas para
universidades públicas.
C A ABNT NBR ISO/IEC 27001 trata de criptografia de dados
acadêmicos; a ABNT NBR ISO/IEC 27002 foca auditoria
financeira.
D A ABNT NBR ISO/IEC 27001 define controles técnicos de
segurança da informação; a ABNT NBR ISO/IEC 27002 trata
exclusivamente da gestão da qualidade em instituições
educacionais.
E A norma ABNT NBR ISO/IEC 27002 fornece diretrizes de
boas práticas de proteção de ativos de informação.

### Questão 60

Acerca das normas ABNT NBR ISO/IEC 27005 e ABNT NBR
ISO/IEC 15999, assinale a opção correta.
A A ABNT NBR ISO/IEC 27005 foca auditorias financeiras, e a
ABNT NBR ISO/IEC 15999 trata exclusivamente de
criptografia de dados.
B A ABNT NBR ISO/IEC 27005 define métodos de
continuidade de serviços críticos, e a ABNT NBR ISO/IEC
15999 orienta a avaliação de riscos em ativos de informação.
C A ABNT NBR ISO/IEC 27005 substitui a necessidade de
controles de segurança, e a ABNT NBR ISO/IEC 15999 é
aplicável apenas a pequenas empresas.
D Ambas as normas aplicam-se obrigatoriamente a empresas
que lidam com dados pessoais de clientes.
E A ABNT NBR ISO/IEC 27005 fornece diretrizes para
identificação, análise e tratamento de riscos em segurança da
informação, e a ISO/IEC 15999 estabelece processos para a
garantia da continuidade operacional diante de incidentes,
falhas ou desastres.
O planejamento estratégico é voltado para a definição da
estratégia da organização como um todo, de modo a orientar
sua identidade, ações e objetivos globais.
II O planejamento tático desdobra o planejamento estratégico
em metas e iniciativas específicas para cada área de TI,
marketing ou finanças.
III O planejamento operacional consiste em planos de ação que
especificam recursos, prazos, responsáveis e procedimentos.
Assinale a opção correta.
A Apenas o item I está certo.
B Apenas os itens I e II estão certos.
C Apenas os itens I e III estão certos.
D Apenas os itens II e III estão certos.
E Todos os itens estão certos.

### Questão 62

Na preparação do PDTI, o levantamento de leis, planos
estratégicos, normas e políticas para alinhar a TI às diretrizes
legais e organizacionais é contemplado na fase de
A elaboração do plano de trabalho.
B identificação dos documentos de referência.
C identificação de princípios e diretrizes.
D definição da equipe de elaboração.
E descrição da metodologia.

### Questão 63

No PDTI, a etapa de diagnóstico na qual os sistemas são
definidos por acordos de nível de serviço (ANS) e descritos em
catálogos de serviços é denominada
A consolidação do inventário de necessidades.
B necessidades de infraestrutura de TI.
C alinhamento às estratégias da organização.
D necessidades de informação.
E necessidades de serviços de TI.

### Questão 64

Em razão das mudanças no mercado e nas organizações, dos
avanços tecnológicos e das expectativas crescentes sobre geração
de valor, o PMBOK 7.ª edição introduziu mudanças estruturais
na gestão de projetos, tais como
I
foco em processos padronizados e documentação
consistente.
II avaliação de desempenho e de eficiência e mitigação de
riscos.
III foco em princípios, com diretrizes amplas, flexíveis e
aplicáveis a qualquer abordagem.
IV criação de plataforma digital interativa, dinâmica, acessível e
centrada em valor, denominada PMIstandards.
Estão certos apenas os itens
A I e II.
B I e III.
C III e IV.
D I, II e IV.
E II, III e IV.

### Questão 65

No que diz respeito ao gerenciamento de projetos, assinale a
opção que corresponde ao conceito de algo tangível ou
intangível, quantificável e que pode ser tanto um item final como
um componente de um sistema maior.
A portfólio
B produto
C projeto
D resultado
E valor

### Questão 66

Considerando que, conforme consta no ITIL 4, a cadeia de valor
de serviço é o núcleo do SVS (service value system), um modelo
operacional que organiza atividades essenciais, assinale a opção
que apresenta a atividade cujo objetivo é manter bom
relacionamento e compreensão das necessidades das partes
interessadas e cujas entradas incluem demandas, requisitos de
clientes e incidentes.
A obter e construir
B entregar e suportar
C engajar
D planejar
E melhorar

### Questão 67

Acerca dos principais conceitos de gerenciamento de serviço e
com base no ITIL 4, julgue os itens a seguir.
I
Valor é a percepção subjetiva dos benefícios, da utilidade e
da importância de algo, que varia conforme a perspectiva das
partes interessadas.
II Produto é o meio de permitir cocriação de valor, facilitando
resultados desejados sem que o cliente gerencie riscos ou
custos.
III Riscos são eventos incertos que podem gerar perdas ou
dificultar objetivos, e o provedor é responsável por
gerenciá-los em nome do consumidor.
Assinale a opção correta.
A Apenas o item I está certo.
B Apenas os itens I e II estão certos.
C Apenas os itens I e III estão certos.
D Apenas os itens II e III estão certos.
E Todos os itens estão certos.

### Questão 68

O COBIT
I
é um framework voltado para governança e gestão de
informação e tecnologia organizacional.
II abrange toda a tecnologia e processamento de informações
da organização, não se limitando apenas ao setor de TI.
III é uma estrutura técnica de TI cujo objetivo é gerir toda a
tecnologia organizacional.
IV prescreve ou toma decisões sobre TI na escolha da
arquitetura e da gestão de custos.

### Questão 69

De acordo com a Lei de Acesso à Informação (Lei
n.º 12.527/2011), um cidadão tem o direito de obter informações
I
contidas em registros ou documentos, produzidos ou
acumulados por seus órgãos ou entidades.
II relativas às atividades exercidas pelos órgãos e entidades,
inclusive as relativas à sua política, organização e serviços.
III relativas aos resultados de inspeções, auditorias, prestações e
tomadas de contas realizadas pelos órgãos de controle
interno e externo.
Assinale a opção correta.
A Apenas o item II está certo.
B Apenas os itens I e II estão certos.
C Apenas os itens I e III estão certos.
D Apenas os itens II e III estão certos.
E Todos os itens estão certos.

### Questão 70

Conforme a Lei de Acesso à Informação (Lei n.º 12.527/2011), é
concedido acesso irrestrito às informações quando os dados
forem relativos a
A inteligência, investigação ou fiscalização em andamento.
B segurança, vida e saúde da população.
C violações de direitos humanos cometidas por agentes
públicos.
D relações internacionais e negociações diplomáticas.
E estabilidade econômica, financeira ou monetária.

### Questão 71

Considerando-se que a Instrução Normativa SGD/SEDGG/ME
n.º 94/2022 determina, entre outras providências, a criação de
diversos documentos durante todo o processo de contratação de
bens e serviços de TIC, é correto afirmar que, na fase de gestão
do contrato, deve ser produzido(a)
I
a ata da reunião inicial (kick-off) com pautas mínimas
obrigatórias.
II a ordem de serviço/ordem de fornecimento (OS/OF) contendo
elementos mínimos para formalização de demandas.
III o mapa de gerenciamento de riscos (MGR).
Assinale a opção correta.
A Apenas o item I está certo.
B Apenas o item II está certo.
C Apenas os itens I e III estão certos.
D Apenas os itens II e III estão certos.
E Todos os itens estão certos.

### Questão 72

Estão certos apenas os itens
Segundo a Instrução Normativa SGD/SEDGG/ME n.º 94/2022, o
responsável por confeccionar e assinar o termo de recebimento
provisório (TRP) a ser produzido durante a fase de gestão do
contrato de soluções de TIC, quando da entrega do objeto
constante na OS/OF, é o
A I e II.
B I e IV.
C II e III.
D I, III e IV.
E II, III e IV.
A fiscal administrativo do contrato.
B gestor do contrato.
C fiscal setorial do contrato.
D fiscal requisitante do contrato.
E fiscal técnico do contrato.

### Questão 73


### Questão 75

Segundo a Instrução Normativa SGD/SEDGG/ME n.º 94/2022,
na fase de gestão do contrato de soluções de TIC, existem
diversas responsabilidades/atribuições inerentes aos integrantes
da equipe de gestão do contrato, tais como as listadas a seguir.
I
formalizar
demandas
de
correção
à
contratada,
por
comunicação oficial pertinente
II verificar regularidades fiscais, trabalhistas e previdenciárias,
para fins de pagamento
III avaliar a qualidade dos serviços/bens conforme os critérios de
aceitação, em conjunto entre fiscais
IV autorizar o faturamento com base no termo de recebimento
definitivo (TRD)
V
coordenar os atos preparatórios à prorrogação, alteração,
reequilíbrio, pagamento, sanções e extinção
Compete, respectivamente, ao fiscal requisitante, ao fiscal
administrativo e ao gestor do contrato o que se apresenta nos itens
A I, II e IV.
B I, II e V.
C I, III e V.
D II, III e IV.
E III, IV e V.
No âmbito da Lei n.º 14.133/2021, o planejamento e a fiscalização
dos contratos de TI devem estar de acordo com regras que tratam
da matriz de riscos, da alocação de responsabilidades e da
manutenção do equilíbrio econômico-financeiro. Conforme essa
lei, a matriz de riscos em contratos de TI
A autoriza o contratado a revisar unilateralmente os preços do
sempre
que
houver
alteração
cambial
ou
inflacionária.
B serve exclusivamente para registrar falhas de execução
verificadas
Com base nas informações precedentes, assinale a opção em que
é apresentado um conjunto de providências e registros
compatíveis com o início e o acompanhamento da gestão de um
contrato de TIC, conforme a referida instrução normativa.
A centralizar aceite no gestor; arquivar o mapa de riscos após a
seleção; trocar OS por atas; e admitir reunião informal
B tratar a ata sem assinaturas; permitir ordens verbais iniciais;
limitar riscos a mudanças de escopo; e usar apenas email
C deixar a contratada indicar o gestor; dispensar OS em serviços
contínuos; e registrar riscos apenas em plano de continuidade
D designar gestor e equipe; registrar reunião inicial em ata;
emitir OS; e manter mapa de riscos atualizado
E reabrir documento de formalização da demanda (DFD) e
estudo técnico preliminar (ETP) sem motivação; atualizar
riscos semestralmente; usar email como OS; e substituir ata
por relatório

### Questão 76


### Questão 74

contrato
A Instrução Normativa SGD/SEDGG/ME n.º 94/2022,
que disciplina a gestão dos contratos de soluções de TIC,
determina providências formais no início da execução,
instrumentos padronizados para o encaminhamento de demandas
e atualização contínua do gerenciamento de riscos, de modo a
garantir rastreabilidade, responsabilização e conformidade ao
modelo de execução aprovado.
durante
a
fiscalização
do
contrato
pela
administração.
C substitui a necessidade de manutenção do mapa de
gerenciamento de riscos previsto em normas infralegais de
contratações de TIC.
D permite que a administração transfira integralmente ao
contratado todos os riscos da execução contratual, inclusive
os de caso fortuito ou força maior.
E estabelece a alocação objetiva de riscos entre a administração
e o contratado, fixando responsabilidades e impactos
econômico-financeiros previstos.
Determinado órgão da administração pública precisa
estimar o valor de referência para a contratação de serviços de
manutenção de equipamentos de informática, e o gestor da
contratação opta, com base na Instrução Normativa SEGES/ME
n.º 65/2021, por utilizar diferentes parâmetros de pesquisa de
preços, respeitando prioridades e prazos definidos.
Nessa situação hipotética, para atender corretamente aos
parâmetros estabelecidos na referida instrução normativa, o
gestor deve
A adotar como regra a média aritmética simples das propostas
obtidas diretamente com fornecedores, sendo desnecessária
sua justificativa.
B utilizar exclusivamente propostas de fornecedores sem
considerar sua validade temporal, desde que constem em
papel timbrado.
C usar preços divulgados em catálogos de fabricantes e
distribuidores como parâmetro prioritário, como em qualquer
contratação de TIC.
D consultar o painel de preços do governo federal e contratações
similares realizadas pela administração nos últimos 12 meses,
adotando a mediana como valor estimado.
E basear-se em anúncios de jornais especializados de
tecnologia, ainda que publicados há mais de 24 meses, se
acompanhados de três cotações distintas.

### Questão 77


### Questão 80

No ciclo de vida das contratações de soluções de TI, a fase de
gestão do contrato é essencial para a garantia de que o objeto
contratado seja entregue conforme os requisitos técnicos e
administrativos estabelecidos. Na gestão de contratos de TI, é
atribuição típica do gestor e da equipe de fiscalização do contrato
A Instrução Normativa SEGES/ME n.º 65/2021 dispõe sobre
regras e parâmetros para a pesquisa de preços nas contratações
públicas, inclusive para bens e serviços de TI, estabelecendo
prioridades, prazos e fontes oficiais de consulta. Segundo essa
instrução normativa, entre as fontes priorizadas de pesquisa de
preços estão
A conduzir a análise jurídica do edital e do contrato, emitindo
parecer vinculante para a administração.
B acompanhar a execução, emitir ordens de serviço, registrar
reuniões em ata e atualizar o mapa de riscos.
C aprovar a pesquisa de preços como referência de valor
estimado, fixando os parâmetros estatísticos a serem
utilizados.
D elaborar o estudo técnico preliminar e o termo de referência,
articulando-os ao Plano Diretor de Tecnologia da Informação
e Comunicação.
E definir a modalidade de licitação e homologar o resultado,
mediante decisão final da autoridade competente.
A as contratações similares da administração nos últimos
12 meses, adotando-se a mediana.
B as cotações em jornais de grande circulação, válidas até
24 meses da data de sua publicação.
C as propostas de fornecedores, aceitas sem exigência de prazo
de validade específico.
D os preços de sites de comércio eletrônico, cujo uso dispensa
justificativa formal.
E os catálogos de fabricantes de informática, que sempre
substituem as demais fontes.

### Questão 78

A Lei n.º 14.133/2021 apresenta inovações relevantes sobre
garantias em contratos administrativos, incluindo contratos de
obras, serviços e fornecimentos de bens de TI. A esse respeito,
julgue os itens subsequentes.
I
Em contratos de obras e serviços de grande vulto, a
administração poderá exigir garantia de até 30% do valor
inicial, desde que prevista no edital e justificada
tecnicamente.
II A referida lei não menciona a modalidade seguro-garantia,
prevendo apenas caução em dinheiro ou títulos da dívida
pública.
III A garantia prestada pelo contratado deve ser restituída após a
execução do contrato e o recebimento definitivo do objeto.
Assinale a opção correta.
A Apenas o item I está certo.
B Apenas o item II está certo.
C Apenas os itens I e III estão certos.
D Apenas os itens II e III estão certos.
E Todos os itens estão certos.

### Questão 79

Segundo a Instrução Normativa SGD/SEDGG/ME n.º 94/2022,
um dos documentos da fase de planejamento da contratação de
soluções de TIC é o
A ato de fiscalização contratual (AFC), que institui formalmente
o gestor e a equipe de fiscalização do contrato antes do
planejamento.
B relatório de execução orçamentária (REO), que demonstra a
conformidade fiscal da unidade requisitante.
C termo de execução preliminar (TEP), que detalha as sanções
aplicáveis ao fornecedor em caso de inadimplemento.
D documento de oficialização da demanda (DOD), que
apresenta a matriz de responsabilidades da execução
contratual.
E estudo técnico preliminar (ETP), que justifica a necessidade
da contratação e avalia alternativas de solução.

### Questão 81

Durante a fase interna da aquisição de bens de tecnologia da
informação, a indicação de marca pode ser excepcionalmente
considerada válida quando
A estiver fundamentada em pesquisa de mercado que aponte
maior participação da marca no setor.
B for recomendada por fornecedor que já atende a outros órgãos
públicos.
C estiver prevista em contrato anterior firmado com o mesmo
fornecedor.
D estiver formalmente justificada, em decorrência da
necessidade de padronização do objeto.
E for baseada em preferência do gestor responsável pela área
requisitante.

### Questão 82

Assinale a opção correta quanto aos modelos de adjudicação.
A A adjudicação global é obrigatória nas contratações cujo
objeto envolva serviços contínuos.
B É recomendada a adjudicação global quando se deseja
contratar diversos fornecedores para diferentes partes do
objeto.
C Quando demonstrada a inviabilidade da adjudicação por item,
poderá ser adotado o critério de julgamento de menor preço
por grupo de itens, desde que evidenciada sua vantagem
técnica e econômica.
D É vedada a adjudicação por grupo em processos que
envolvam bens de consumo duráveis.
E A adjudicação por grupo é utilizada quando os itens possuem
características técnicas distintas e não se relacionam entre si.

### Questão 83

Assinale a opção que apresenta um elemento obrigatório do
termo de referência para a contratação de bens e serviços.
A cronograma de capacitação de usuários finais após entrega
dos bens
B definição do objeto, incluídos sua natureza, os quantitativos, o
prazo do contrato e, se for o caso, a possibilidade de sua
prorrogação
C previsão de plano de comunicação entre as partes para
acompanhamento do projeto
D cláusula que determine o foro de eleição para dirimir
eventuais controvérsias
E dispositivo que preveja a correção monetária incidente sobre
o valor contratual

### Questão 84


### Questão 87

Em relação à execução indireta (terceirização) de contratos
administrativos na área de tecnologia da informação, assinale a
opção correta, de acordo com a Lei n.º 14.133/2021.
Acerca da solicitação e da análise de amostras no âmbito dos
A Durante a vigência do contrato de terceirização, os
empregados da empresa contratada ficam subordinados à
administração pública.
B A administração pública pode, mediante justificativa expressa
e atendidos os requisitos legais, contratar mais de uma
empresa ou instituição para executar o mesmo serviço.
C Uma vez que a contratação dos funcionários é incumbência
da empresa terceirizada, não se aplicam aos contratos de
execução indireta as regras da Lei n.º 14.133/2021 que
buscam obstar o nepotismo.
D Serviços que envolvam tomada de decisão ou posicionamento
institucional nas áreas de planejamento, coordenação,
supervisão e controle devem preferencialmente ser objeto de
terceirização.
E Nos contratos de execução indireta, ocorre a transferência,
para o terceiro contratado, da responsabilidade pela realização
de atos administrativos ou pela tomada de decisão.
A Segundo o TCU, o edital de licitação deve contemplar as

### Questão 85

São legitimadas a apresentar impugnações e pedidos de
esclarecimentos na fase externa de processo licitatório para
aquisição de bens e serviços de tecnologia da informação
A somente pessoas físicas administradoras de empresas que
seriam prejudicadas pelo edital.
B quaisquer pessoas, sem restrições.
C somente empresas da área de tecnologia da informação.
D somente empresas que seriam prejudicadas pelo edital.
E somente pessoas físicas administradoras de empresas da área
de tecnologia da informação.

### Questão 86

Com pertinência à análise de documentação na aquisição de bens
e serviços de tecnologia da informação (TI), assinale a opção
correta, conforme a Lei n.º 14.133/2021.
A Deve-se exigir a comprovação dos documentos relativos à
regularidade fiscal de todos os licitantes no momento do
julgamento das propostas.
B A apresentação de atestados que demonstrem a capacidade
operacional dos licitantes deve ser exigida para todas as
parcelas da aquisição de bens e serviços de TI.
C As sociedades empresárias estrangeiras devem atender à
exigência de registro ou inscrição na entidade profissional
competente, podendo fazê-lo por meio da apresentação do
referido registro no país de origem.
D Nas contratações de projetos ou de serviços técnicos
especializados de TI, inclusive naquelas cujo objeto envolva
atividade de pesquisa e desenvolvimento de caráter científico
e tecnológico, é obrigatória a apresentação de documento de
cessão de todos os direitos patrimoniais para a administração
pública.
E Após a entrega dos documentos para habilitação de licitante, é
permitida a complementação de informações acerca dos
documentos já apresentados, desde que essa complementação
seja necessária para apurar fatos existentes à época da
abertura do certame.
processos licitatórios, assinale a opção correta.
condições de entrega da amostra ou de realização da prova de
conceito (data, horário e local), os procedimentos para o
exame da amostra (roteiro detalhado da avaliação), bem como
os critérios objetivos para a sua aceitação.
B É vedado à administração pública oferecer protótipo do objeto
pretendido para a exigência de amostras, mesmo que haja
previsão expressa no edital de licitação.
C As amostras do objeto que se pretende contratar somente
podem ser exigidas dos licitantes após a fase de julgamento
das propostas.
D A administração pública pode exigir amostras de todos os
licitantes de um certame para realizar análise e avaliação da
conformidade das propostas, mediante homologação de
amostras ou outros testes que sejam de seu interesse.
E As amostras fornecidas pelo licitante provisoriamente
vencedor devem ser analisadas pela administração pública,
sendo vedado o seu encaminhamento a outra instituição.

### Questão 88

No que concerne às condições de recebimento e aceite do objeto
de contrato firmado com a administração pública, é correto
afirmar, de acordo com a Lei n.º 14.133/2021 (Lei de Licitações e
Contratos Administrativos), que o recebimento
A definitivo referente a compras deve ser realizado, mediante
termo detalhado, por comissão designada pela autoridade
competente, com verificação posterior do atendimento das
exigências contratuais.
B definitivo exclui a responsabilidade civil pela solidez e
segurança da obra ou serviço, bem como a responsabilidade
ético-profissional pela perfeita execução do contrato, nos
limites estabelecidos pela lei ou pelo contrato.
C definitivo de projeto de obra pela administração não exime o
projetista da responsabilidade objetiva por todos os danos
causados por falha de projeto.
D provisório referente a contratação de serviços deve ser
realizado pelo responsável por acompanhar os serviços, de
forma sumária, de modo que se certifique o atendimento das
exigências contratuais.
E provisório referente a compras deve ser realizado, de forma
sumária, por servidor designado pela autoridade competente,
com verificação posterior da conformidade do material com
as exigências contratuais.

### Questão 89

No que se refere à aplicação das penalidades e sanções
administrativas decorrentes de irregularidades em licitações e
execuções contratuais, assinale a opção correta.
A A prescrição da aplicação das sanções de impedimento de
licitar e contratar, bem como da sanção de declaração de
inidoneidade para licitar e contratar, ocorrerá em 10 anos,
contados da ciência da infração pela administração.
B A sanção de advertência deve ser aplicada exclusivamente em
face do cometimento de infração que tenha dado causa à
inexecução parcial do contrato e tenha resultado em grave
dano à administração, quando não se justificar a imposição de
penalidade mais grave.
C A sanção de impedimento de licitar e contratar, quando
aplicada, impedirá o sancionado de licitar ou contratar no
âmbito da administração pública direta e indireta de todos os
entes federativos, pelo prazo máximo de 3 anos.
D A sanção de declaração de inidoneidade para licitar ou
contratar, quando aplicada pelo Poder Executivo estadual, é
de competência exclusiva do governador de estado, e
impedirá o sancionado de licitar ou contratar no âmbito da
administração pública direta e indireta do ente federativo que
a aplicar, pelo prazo máximo de 6 anos.
E A sanção de multa, única que pode ser aplicada
cumulativamente com as demais, poderá ser aplicada ao
responsável por qualquer das infrações administrativas
previstas na Lei de Licitações e Contratos Administrativos.

### Questão 90

No que se refere à formalização de aditivos contratuais, assinale a
opção correta.
A A formalização do termo aditivo é, em todos os casos,
condição para a execução, pelo contratado, das prestações
determinadas pela administração pública no curso da
execução do contrato.
B Na formalização de termo aditivo destinado à prorrogação de
vigência de contrato com vigência inicial de doze meses, a
administração não é obrigada a verificar a regularidade fiscal
e a idoneidade do contratado.
C Em contratações por escopo com conclusão predefinida, o
prazo de vigência deverá ser prorrogado, mediante
formalização de termo aditivo, quando o objeto não for
concluído no período firmado no contrato.
D É dispensada a celebração de termo aditivo para registrar
variação de valor contratual decorrente de reajuste de preços
previstos no próprio contrato, podendo tal registro ser
realizado por apostila.
E É legal a celebração de termo aditivo com efeitos retroativos
para permitir o pagamento de serviços efetivamente prestados
em contratos com vigência expirada.

### Questão 91


### Questão 92

O principal objetivo da 5.ª forma normal é a
A eliminação de dependências parciais.
B garantia de que todos os valores em uma tabela sejam
atômicos.
C eliminação de dependências multivaloradas.
D eliminação de redundâncias e anomalias de junção em tabelas
que registram múltiplos relacionamentos multivalorados.
E garantia de que não haja grupos de valores repetidos em uma
única célula.

### Questão 93

Entre as diversas características do banco de dados MariaDB,
ressalta-se a de
A agrupamento de threads na Enterprise Edition.
B uso do componente validate_password.
C suporte de criptografia de log temporário e criptografia de log
binário.
D uso de InnoDB e AES na criptografia de dados em repouso.
E armazenamento de relatórios JSON como objetos binários.

### Questão 94

O CRUD, que representa as quatro operações básicas em um
SGBD, é um exemplo de
A data control language.
B not only structured query language.
C data manipulation language.
D data definition language.
E structured query language.

### Questão 95

Conceitua-se curadoria de metadados como
A a utilização de recursos de classe empresarial para usá-los
adequadamente, como gerenciamento de identidade, acesso e
recursos principais, por meio de APIs REST.
B uma possibilidade de ter opções flexíveis de pesquisa e
filtragem para permitir que os usuários encontrem
rapidamente conjuntos relevantes de dados para ciência,
análise ou engenharia de dados.
C uma forma pela qual especialistas no assunto possam
contribuir com conhecimento de negócios na forma de um
glossário de negócios corporativos, marcas, associações,
anotações definidas pelo usuário, classificações, avaliações,
entre outros.
D a aplicação de técnicas de IA e aprendizado de máquina nos
metadados coletados.
E a consolidação de metadados técnicos de uma variedade de
ativos de dados conectados, incluindo armazenamento de
objetos, bancos de dados autônomos e sistemas locais.

### Questão 96

Quando toda coluna não-chave de uma tabela depende
diretamente da chave primária, considera-se que essa tabela está,
no mínimo, na
Em um banco de dados, a instrução CREATE TABLE é um
exemplo de
A 1.ª forma normal.
B 2.ª forma normal.
C 3.ª forma normal.
D 4.ª forma normal.
E 5.ª forma normal.
A SQL.
B DML.
C DDL.
D DCL.
E NoSQL.

### Questão 97

Considerando uma tabela ALUNO com cem registros, a instrução SELECT * FROM ALUNO LIMIT 20 OFFSET 90 apresentará os
registros
A de 21 a 90.
B de 81 a 90.
C de 91 a 100.
D de 71 a 90.
E de 81 a 100.

### Questão 98

Na modelagem dimensional, é objetivo da operação de fragmentação
A rotacionar o cubo OLAP ao longo de uma de suas dimensões.
B criar um subcubo menor a partir de um cubo OLAP.
C resumir os dados para atributos específicos.
D criar uma exibição bidimensional do cubo OLAP.
E aprofundar na hierarquia de conceitos e extrair os detalhes necessários.

### Questão 99

Em um SGBD relacional, a restrição que garante que todos os valores em uma coluna sejam distintos entre si e que permite valor
NULL é denominada
A cardinalidade.
B chave primária.
C índice.
D chave única.
E chave estrangeira.

### Questão 100

A arquitetura de um banco de dados pode ser dividida em diferentes níveis, e o nível que foca na percepção da comunidade de
usuários e não em usuários individuais é o
A físico.
B interno.
C de armazenamento.
D externo.
E conceitual.
Espaço livre
