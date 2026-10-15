---
tipo: prova
concurso: "telebras_25"
arquivo_origem: "Provas Cebraspe/telebras_25/PROVA OBJETIVA CONHECIMENTOS ESPECIFICOS CARGO 13.pdf"
tags:
  - prova
  - cebraspe
  - cgu-2026
---

# PROVA OBJETIVA CONHECIMENTOS ESPECIFICOS CARGO 13

## CONHECIMENTOS ESPECÍFICOS

_Julgue os próximos itens, em relação aos modelos de referência OSI e TCP/IP. A camada de enlace é a mais baixa do modelo OSI e funciona como uma interface entre os hosts e os meios de transmissão, como linhas seriais e Ethernet, cujos principais protocolos são SMTP e DNS. O modelo TCP/IP não separa de forma clara os conceitos de serviço, interface e protocolo, o que contraria princípios fundamentais da engenharia de software, que preceituam a distinção entre especificação e implementação._

_No que se refere a tecnologia MPLS, serviço de DNS, protocolo LDAP, FTP, mecanismo de NAT e fundamentos de IPSec, julgue os itens subsequentes. O protocolo FTP, usado para a transferência de arquivos e programas em redes TCP/IP, utiliza o protocolo TCP na camada de transporte e opera por meio das portas 20, destinada à transferência de dados, e 21, responsável pelo controle da comunicação. O modo túnel do IPsec, além de apenas proteger parte dos dados, exige que todos os dispositivos da rede conheçam e configurem o IPsec individualmente, por isso não é utilizado em VPN. A NAT permite que os endereços IP privados possam circular livremente pela Internet pública, utilizada principalmente por servidores globais, cujas três principais faixas privadas são 10.0.0.0/16, 172.32.0.0/8 e 192.168.0.0/24, sendo a faixa 192.168.0.0/24 a mais usada em grandes provedores de Internet. O MPLS, que surgiu para aumentar a velocidade do encaminhamento, reduzindo o processamento necessário nos roteadores, expandiu-se para a flexibilidade de roteamento e o suporte à qualidade de serviço._

**53** O modelo OSI visa promover a padronização internacional dos protocolos de rede e baseia-se na interconexão de sistemas abertos, isto é, sistemas capazes de se comunicar com outros. A camada de aplicação reúne todos os protocolos de alto nível, e, diferentemente do modelo OSI, o TCP/IP não possui camadas específicas de sessão e apresentação, pois suas funções são incorporadas diretamente pelas aplicações. O modelo OSI é estruturado em sete camadas, cada uma com função bem definida e escolhida de modo a facilitar a criação de protocolos padronizados internacionalmente. Na camada internet, que é responsável por integrar todas as redes, atuam dois protocolos principais: o TCP e o UDP. O serviço de DNS é um sistema hierárquico de nomes combinado com um banco de dados distribuído, e sua função principal é mapear nomes de hosts para endereços IP.

_Julgue os próximos itens, relativos a endereçamento IPv4 e suas classes, máscaras de sub-redes e protocolo de roteamento BGP e IPv4. LDAP é um protocolo de aplicação usado para o acesso e manutenção de serviços de diretório distribuídos, sendo utilizado em dados transacionais com Schema rígido. O IPv4, principal protocolo da camada de aplicação da Internet, utiliza datagrama composto pelo tamanho do cabeçalho, que varia entre 5 bytes até 40 bytes. O BGP é um protocolo flexível, e sua complexidade não está no protocolo em si, mas nas políticas de roteamento, que não são padronizadas. Na configuração de redes internas para endereços de classe A, são utilizados endereços de rede 172.16.0.0 e máscara de sub-rede de 255.255.0.0. Antes de 1993, o endereçamento IP utilizava um modelo chamado endereçamento em classes, no qual a classe A era reservada para multicast, o que permitia o envio de datagramas para múltiplos hosts._

_Em relação à comutação por pacotes ou por células, julgue os itens a seguir. A comutação por pacotes não requer mecanismos de controle de congestionamento. No ATM (asynchronous transfer mode), a comutação por células utiliza unidades de dados de tamanho fixo (53 bytes)._

_A respeito de SDN (software defined network), julgue os próximos itens. Protocolos southbound em SDN definem APIs padronizadas para a comunicação entre o plano de controle e o plano de dados. Em uma arquitetura SDN, o plano de controle pode ser logicamente centralizado, mantendo uma visão unificada da rede, entretanto pode ser fisicamente distribuído na rede,_

_considerando aspectos de escalabilidade. Espaço livre_

_Acerca de CSMA/CD e CSMA/CA, julgue os itens subsequentes. O CSMA/CA não elimina a ocorrência de colisões ao empregar mecanismos de escuta do meio e quadros de controle como RTS/CTS. O mecanismo de detecção de colisões do CSMA/CD requer que o tempo de transmissão de um quadro de tamanho mínimo seja oito vezes o tempo de propagação do meio._

_Em relação ao funcionamento dos padrões Fast Ethernet e Gigabit Ethernet, julgue os itens a seguir. Para auxiliar a detecção de colisão em meio compartilhado, o padrão Gigabit Ethernet introduz o carrier extension, que estende a duração da transmissão até um tamanho lógico mínimo de 512 bytes, sem alterar o tamanho real do quadro de dados._

**74** O padrão Fast Ethernet (100 Mb/s) altera o formato do quadro Ethernet, incluindo o tamanho mínimo de 62 bytes e o máximo de 2.500 bytes. No que concerne a características técnicas de equipamentos switches, julgue os itens a seguir. Em um processo de comutação em switches, o método store-and-forward faz o switch iniciar o envio do quadro antes de recebê-lo totalmente.

**76** Um switch que utiliza o protocolo STP pode eliminar loops na camada 3.

_Acerca de conceitos e fundamentos de SD-WAN, julgue os itens a seguir. SD-WAN impede a criação de túneis dinâmicos (overlays), de maneira a garantir a qualidade de serviço._

**78** Em uma rede SD-WAN, as decisões de encaminhamento de pacotes são baseadas em uma variedade de critérios definidos por políticas, os quais podem incluir endereços IP de destino, mas não se limitam a eles.

_Acerca dos protocolos 802.1q e ARP (Address Resolution Protocol), julgue os itens que se seguem. ARP é suscetível a ataques de envenenamento de cache, nos quais um atacante pode inserir um endereço MAC falso associado a um endereço IP legítimo na tabela ARP de um host._

**80** ARP é um protocolo de camada de rede que permite a um host descobrir o endereço IP de um host de destino com base apenas no endereço MAC do destino dado.

**81** O campo FCS (frame check sequence) original é alterado ao se inserir o tag VLAN de 4 bytes em um Frame Ethernet conforme 802.1q.

**82** O VID (VLAN identifier), no protocolo 802.1q, pode assumir valores de 0 a 4095, sendo o VID 4095, em particular, reservado pelo padrão em si.

_Acerca de segurança física e lógica, criptografia e antivírus,_

_julgue os itens a seguir. Em um datacenter corporativo, o controle biométrico com registro de eventos cumpre, suficientemente, o requisito de não repúdio de acesso físico, quando considerado no domínio da segurança física._

**84** Em um ambiente corporativo, a utilização de criptografia simétrica em modos de operação com autenticação associada confere confidencialidade e integridade aos dados protegidos.

**85** Em um ambiente computacional, a utilização de algoritmos criptográficos robustos para proteção de dados em repouso garante a confidencialidade lógica das informações, por permitir o controle das autorizações de acesso ao conteúdo armazenado. Em um datacenter, a adoção de criptografia assimétrica para cifrar diretamente arquivos de backup armazenados em disco atende simultaneamente aos requisitos de confidencialidade e de eficiência operacional, por viabilizar proteção criptográfica adequada sem impacto relevante no processamento.

**87** Em uma estação de trabalho corporativa, um sistema antivírus que realiza inspeção em tempo real do comportamento de processos é capaz de identificar a execução de código malicioso previamente desconhecido, a partir da correlação de padrões de ações típicas de malware, como injeção de código em outros processos e persistência não autorizada no sistema.

_Em relação a sistemas de detecção de intrusão, segurança de servidores e de sistemas operacionais, certificação digital e políticas de segurança, julgue os itens seguintes._

**88** Em um contexto organizacional, a definição formal de uma política de controle de acesso alinhada a normas internacionais reconhecidas é suficiente para que os sistemas implementem corretamente a segregação de privilégios, ainda que não existam procedimentos técnicos de provisionamento, revisão e revogação de acessos.

**89** A verificação de uma assinatura digital baseada em certificado X.509 permite comprovar a integridade do conteúdo assinado e a vinculação da chave pública ao titular do certificado, desde que a cadeia de certificação e o estado de revogação sejam devidamente validados.

**90** Em servidores corporativos, a aplicação regular de atualizações de segurança do sistema operacional elimina a necessidade de medidas adicionais de endurecimento (hardening) e de ajustes de configuração.

**91** Em uma rede corporativa segmentada, um sistema de detecção de intrusão baseado em rede, quando implementado e posicionado no perímetro, é eficaz para identificar tentativas de intrusão realizadas por meio de tráfego criptografado entre hosts internos.

_Acerca de procedimentos de segurança e da gestão da segurança da informação, julgue os próximos itens._

**92** Conforme a norma ISO 27001, no tratamento de riscos, a seleção e a implementação de controles de segurança da informação são formalmente justificadas por meio da declaração de aplicabilidade, que registra os controles adotados e excluídos e suas respectivas motivações.

**93** Nos documentos que formalizam os procedimentos de segurança, as políticas de segurança são traduzidas em instruções operacionais verificáveis, o que viabiliza a execução consistente dos controles técnicos e organizacionais e a geração de evidências objetivas para auditoria e avaliação de conformidade.

**94** De acordo com a Instrução Normativa n.º 4/2020 do Gabinete de Segurança Institucional (GSI), no processo de autorização de operação de um sistema de informação em órgão da administração pública federal, a aceitação do risco residual é responsabilidade da área de tecnologia da informação do órgão.

**95** No âmbito da gestão da segurança da informação, a priorização de controles com base em riscos prescinde da definição prévia de objetivos estratégicos de segurança, uma vez que a análise de riscos orienta diretamente a tomada de decisão gerencial.

_No que se refere a auditoria e conformidade, à elaboração de planos de continuidade, ao gerenciamento de riscos de acordo com a norma ISO 27005 e ao gerenciamento de serviços conforme o ITIL 4, julgue os itens subsequentes. Na elaboração de um plano de continuidade de serviços de tecnologia da informação, o inventário de ativos tecnológicos é a principal base para a definição das estratégias de continuidade._

**97** No modelo ITIL 4, a gestão de segurança da informação compõe o sistema de valor de serviço e é aplicada de forma integrada às práticas e à cadeia de valor, com foco na proteção da confidencialidade, integridade e disponibilidade dos serviços ao longo de seu ciclo de vida.

**98** Em uma auditoria de segurança da informação, a verificação da conformidade de um controle de gestão de acessos ocorre por meio do cotejo entre evidências objetivas de sua execução operacional (por exemplo, registros de concessão, revisão e revogação de privilégios) e critérios de auditoria previamente definidos.

**99** Consoante a ISO 27005, o gerenciamento de riscos de segurança da informação fundamenta-se em critérios de risco definidos e na avaliação sistemática de ameaças, vulnerabilidades e impactos, orientando decisões de tratamento e aceitação de riscos.

_Julgue os itens a seguir, referentes à gerência de projetos._

**109** O PMBOK v7 organiza o gerenciamento de projetos em três grupos de processos.

**110** O PMBOK v7 estabelece doze áreas de conhecimento para o gerenciamento de projetos.

_Acerca de ataques a redes e aplicações, julgue os itens que seguem._

**111** Ataques do tipo APT têm como principal objetivo a extorsão financeira por meio da criptografia de dados.

**112** Ataques de amplificação exploram serviços como DNS e NTP para gerar respostas maiores que as requisições originais.

**113** O IP spoofing consiste na alteração do endereço IP de origem para mascarar a identidade do atacante.

**114** Ataques DDoS caracterizam-se pelo uso de múltiplas origens para sobrecarregar recursos de um sistema alvo.

_No que se refere a sistemas de backup, julgue os itens a seguir._

**115** A adoção de políticas de backup elimina a necessidade de soluções de alta disponibilidade.

**116** O backup full (completo) armazena todos os dados modificados desde o último backup incremental realizado.

_A respeito do protocolo SNMP e de listas de acesso, julgue os itens subsecutivos._

_Julgue os itens a seguir acerca de cloud computing._

**100** Em firewalls e proxies, listas de controle de acesso são sistema operacional das máquinas virtuais do cliente.

**118** No modelo SaaS, o cliente faz uso das aplicações sem necessidade de administrar servidores ou sistemas operacionais.

**119** O modelo PaaS fornece um ambiente gerenciado para desenvolvimento e implantação de aplicações. avaliadas de forma ordenada, de modo que a primeira regra compatível com os atributos do tráfego determina a ação aplicada.

**101** O modelo de segurança baseado em usuários introduzido na versão 3 do protocolo SNMP provê confidencialidade e integridade às mensagens de gerenciamento, coexistindo, de forma automática e transparente, com mecanismos de autenticação baseados em comunidades adotados nas versões anteriores.

_Acerca da convergência de rede, julgue os itens a seguir._

**102** O protocolo RTP garante entrega confiável e retransmissão de pacotes perdidos em chamadas VoIP.

**103** O codec G.711 é amplamente utilizado em VoIP por aplicar compressão de dados, oferecendo maior qualidade de áudio e menor consumo de banda.

**104** Projetos de telefonia IP devem considerar parâmetros de qualidade como latência, jitter, perda de pacotes e largura de banda.

**105** A convergência de rede permite transportar voz, vídeo e dados sobre a mesma infraestrutura TCP/IP, mantendo diferenciação lógica dos serviços.

_A respeito dos temas videoconferência e qualidade de serviços,_

_julgue os itens subsequentes._

**106** O H.323 é um protocolo responsável por sinalização, controle e transporte de mídia em videoconferência.

**107** O protocolo SIP é utilizado para sinalização de sessões multimídia, não realizando transporte de mídia.

**108** O uso de multicast associado ao IGMP reduz o tráfego de rede ao evitar múltiplas transmissões unicast para os mesmos receptores.

**117** No modelo IaaS, o provedor é responsável pela gestão do

_Julgue o item a seguir, referente às legislações pertinentes à área de engenharia._

**120** O sistema CONFEA-CREA é responsável pela fiscalização e regulamentação do exercício profissional da engenharia no Brasil. Espaço livre
