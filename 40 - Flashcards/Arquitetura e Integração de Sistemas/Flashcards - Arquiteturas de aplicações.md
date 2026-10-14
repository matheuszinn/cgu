---
tipo: flashcard
disciplina: "Arquitetura e Integração de Sistemas"
tema: "Arquiteturas de aplicações"
data: "2026-10-14"
tags:
  - flashcard
---

# Flashcards: Arquiteturas de aplicações

> Deck baseado no resumo [[Arquiteturas de aplicações - Arquitetura e Integração de Sistemas]].
> Formato: cards de linha única do plugin Spaced Repetition (pergunta e resposta no mesmo parágrafo).

## Conceitos gerais

O que é arquitetura de aplicações? :: O conjunto de decisões estruturais sobre quais componentes existem, quais responsabilidades cada um tem e como eles se comunicam e dependem entre si.

Qual premissa a banca costuma cobrar sobre arquitetura? :: Não existe arquitetura melhor em abstrato; ela deve ser adequada ao contexto (complexidade do domínio, tamanho da equipe, requisitos não funcionais e orçamento).

Quais três estilos organizam o tema e qual o objetivo central da distribuição de responsabilidades? :: Monolito, microsserviços e arquiteturas orientadas a eventos (EDA); busca-se alta coesão (cada componente faz bem uma coisa) e baixo acoplamento (pouca dependência entre componentes).

## Monolito

Qual a definição de monolito segundo Fowler? :: Aplicação construída como uma única unidade implantável ("single logical executable"), com todos os componentes em um mesmo processo; costuma dividir-se em interface (UI), banco de dados e aplicação servidora.

Como é a comunicação e a implantação em um monolito? :: Comunicação interna por chamadas de método/função em memória (rápidas e confiáveis); há uma única implantação, então qualquer alteração exige reconstruir e reimplantar toda a aplicação.

Como o monolito escala e que tipo de transação favorece? :: Escala horizontalmente com instâncias idênticas atrás de um balanceador (cookie-cutter scaling) e favorece transações ACID locais, que dão consistência forte natural.

Quais as vantagens do monolito? :: Simplicidade de desenvolvimento, teste e depuração; implantação única; baixo custo operacional inicial; desempenho das chamadas internas; consistência transacional.

Quais as desvantagens do monolito à medida que cresce? :: Acoplamento e erosão da modularidade, ciclos de mudança amarrados, escalabilidade grossa (escala-se tudo, não só a parte quente), dificuldade de adotar novas tecnologias e deploy lento/arriscado.

Monolito modular × Big Ball of Mud? :: Monolito modular tem fronteiras de módulo explícitas e internas, exigindo disciplina; Big Ball of Mud é o antônimo, um sistema sem estrutura clara com dependências desordenadas (e pode ocorrer em monolito ou em microsserviços).

Qual recurso Spring implementa módulos com fronteiras verificáveis em um monolito? :: Spring Modulith.

## Microsserviços

Qual a definição de microsserviços (Lewis & Fowler)? :: Estilo que estrutura a aplicação como um conjunto de serviços pequenos, cada um rodando em seu próprio processo, comunicando-se por mecanismos leves (geralmente API HTTP), construídos em torno de capacidades de negócio e implantáveis de forma independente.

Biblioteca × serviço como componente? :: Biblioteca é componente em processo (ligada ao programa, chamada em memória); serviço é componente fora de processo (comunicação remota, por web service/RPC).

O que significam organizar por capacidade de negócio e "produto, não projeto"? :: Serviços em torno de áreas de negócio, com times multifuncionais (não por camada técnica); e o time acompanha o serviço por todo o seu ciclo de vida ("you build, you run it").

O que significa "smart endpoints and dumb pipes"? :: A inteligência fica nos serviços e a infraestrutura de comunicação é simples, apenas roteando mensagens — é uma reação ao ESB, com seus roteamentos e transformações centrais.

O que caracteriza governança e gestão de dados descentralizadas? :: Liberdade para escolher linguagens, bibliotecas e frameworks (padrões battle-tested); cada serviço gerencia seu próprio banco, admitindo polyglot persistence e evitando o integration database compartilhado.

O que são automação de infraestrutura e design for failure? :: CD/pipelines automatizados, essenciais por causa da quantidade de serviços; e a premissa de que qualquer chamada remota pode falhar, tratada com Circuit Breaker, Bulkhead, Timeout e testes de caos.

O que é design evolucionário e o termo "micro" define o tamanho do serviço? :: Decomposição como ferramenta para controlar mudanças, com componente substituível (alguns serviços são descartados); "micro" não define tamanho, que se liga a fronteiras de negócio, não a linhas de código.

Quais as vantagens dos microsserviços? :: Fronteiras de módulo fortes, implantação independente, diversidade e versionamento tecnológico, isolamento de falhas, escalabilidade seletiva e times autônomos.

Quais os custos dos microsserviços? :: Sistemas distribuídos mais difíceis, consistência eventual, complexidade operacional, depuração entre serviços, coordenação de contratos e necessidade de maturidade em CD e devops.

Microsserviços × SOA tradicional? :: SOA tradicional costuma usar ESB central e governança centralizada; microsserviços usam serviços finos, dados descentralizados e smart endpoints com dumb pipes.

O que diz a Lei de Conway e a Inverse Conway Maneuver? :: A Lei de Conway (1968) diz que as organizações projetam sistemas que copiam suas estruturas de comunicação; a Inverse Conway Maneuver reorganiza os times para induzir a arquitetura desejada.

## Monolith First e Microservice Premium

O que é o Microservice Premium? :: Custo extra de produtividade imposto pelos microsserviços, que só se paga em sistemas complexos; a diretriz é não os considerar a menos que o sistema seja complexo demais para um monolito.

O que diz a estratégia Monolith First e por quê? :: Quase todos os casos de sucesso de microsserviços começaram como monolito (e os que começaram direto tiveram problemas), por causa do YAGNI e da dificuldade de acertar as fronteiras no início, já que refatorar entre serviços é muito mais caro que entre bibliotecas.

## Arquiteturas orientadas a eventos (EDA)

O que é uma arquitetura orientada a eventos (EDA)? :: Estilo em que produtores geram eventos, consumidores reagem a eles e canais/brokers transportam os eventos, com produtores e consumidores desacoplados e entrega assíncrona em tempo quase real.

Evento × comando × mensagem? :: Evento é fato ocorrido no passado e imutável, sem esperar resposta (ex.: OrderCreated); comando é ordem a um destinatário que espera execução (ex.: ReserveCredit); mensagem é o termo genérico que cobre ambos. Armadilha: usar evento como comando passivo-agressivo.

O que é Event Notification? :: Padrão que apenas notifica que algo mudou, com pouca carga (IDs), e o receptor decide se busca mais dados; baixo acoplamento, mas fluxo lógico implícito.

O que é Event-Carried State Transfer? :: O evento carrega os dados alterados e o consumidor mantém sua própria cópia sem consultar o produtor; ganha resiliência e menor latência, mas aumenta dados trafegados, cópias e complexidade.

O que é Event Sourcing? :: Em vez de guardar só o estado atual, guarda-se a sequência de eventos que levou a ele; o log de eventos é a fonte da verdade e o estado é derivado por replay (ex.: o log de commits do controle de versão).

O que é CQRS e qual o alerta de Fowler? :: Separar o modelo de escrita (comandos) do de leitura (consultas), podendo otimizar cada lado; não exige eventos, mas adiciona complexidade perigosa e deve ser usado só em partes específicas (um bounded context), nunca no sistema inteiro.

Topologia broker × mediator em EDA? :: Broker difunde eventos a todo o sistema, sem coordenação central (mais desacoplado, porém difícil para erro, reinício e consistência); mediator centraliza o fluxo, mantém estado e despacha comandos em filas (mais controle, porém maior acoplamento e risco de gargalo/ponto único de falha).

Publish-subscribe × event streaming? :: Pub/sub entrega a assinantes e não é durável (novos assinantes não veem eventos passados); streaming grava em log durável e ordenado por partição, permitindo o replay.

Coreografia × orquestração? :: Coreografia: cada serviço publica eventos que disparam os próximos, sem controlador central; orquestração: um orquestrador comanda os participantes com comandos e respostas.

O que é o padrão Saga e quais seus problemas? :: Transação de negócio que atravessa vários serviços vira sequência de transações locais; se uma falha, disparam-se compensações. Não há rollback automático nem isolamento (a letra "I" do ACID).

O que a consistência em EDA exige e para que serve o correlation ID? :: Sem 2PC, usa-se consistência eventual, idempotência (contra mensagens reentregues), ordenação e padrões como Transactional Outbox e event sourcing para gravar estado e publicar evento atomicamente; o correlation ID propaga o rastreamento e viabiliza o distributed tracing.

## Distribuição de responsabilidades, coesão e acoplamento

O que são coesão e acoplamento e o que se deseja? :: Coesão é o grau em que os elementos de um módulo fazem uma coisa só (deseja-se alta); acoplamento é o grau de dependência entre módulos (deseja-se baixo). Mudanças que acontecem juntas ficam no mesmo módulo.

Ordem de força do acoplamento, do mais fraco ao mais forte? :: Por parâmetros de dados, por estrutura de dados, por interface, por estado global e por conteúdo (acesso a internals); o acoplamento temporal (depender de estar ativo ao mesmo tempo) é crítico em sistemas distribuídos.

O que são Ca, Ce e a instabilidade I (métricas de Martin)? :: Ca (afferent) é quantas classes externas dependem do módulo; Ce (efferent) é de quantos módulos ele depende; I = Ce dividido por (Ca mais Ce), com 0 = estável e 1 = instável; componentes estáveis devem ser abstratos (SDP/SAP).

O que é DDD e o que são bounded contexts? :: Dividir o domínio em contextos delimitados, cada um com sua linguagem ubíqua e seu modelo; há correlação natural entre fronteira de contexto e fronteira de serviço/módulo.

O que acontece com granularidade inadequada e o que é responsabilidade única? :: Serviço muito grande dá baixa coesão e acoplamento alto; muito pequeno gera excesso de comunicação e nano-serviços (o critério é a capacidade de negócio); cada componente deve ter uma razão para mudar, evitando o objeto de Deus.

## Camadas e arquitetura hexagonal

Quais as três camadas do Presentation-Domain-Data Layering e qual a direção das dependências? :: Apresentação (UI), domínio/regras de negócio e acesso a dados (persistência); as dependências vão de cima para baixo (apresentação depende do domínio, que depende dos dados).

Como desacoplar o domínio do banco e quais as vantagens das camadas? :: Com um mapper/adapter entre domínio e dados (hexagonal/portas e adaptadores); as camadas reduzem o escopo de atenção, permitem múltiplas apresentações, possibilitam substituir implementações e melhoram a testabilidade.

Camada (layer) × tier (nível físico)? :: Camada é separação conceitual/lógica; tier é separação física/implantação. As três camadas podem rodar numa máquina ou ser distribuídas em tiers separados.

Qual o anti-padrão de times por camada e como organizar sistemas grandes? :: Separar times por camada (front-end, back-end, DBA) cria fricção e afasta do usuário — os desenvolvedores não precisam ser full-stack, mas os times devem ser; em sistemas grandes, o nível mais alto de módulos deve ser orientado a domínio, com camadas dentro de cada módulo.

O que é a arquitetura hexagonal (Cockburn, 2005)? :: O aplicativo deve funcionar sem UI e sem banco, centralizando a relação dentro × fora, em que o código do interior não vaza para o exterior.

Portas × adaptadores e primárias × secundárias? :: Portas são interfaces que definem a conversa com o exterior; adaptadores são suas implementações tecnológicas (GUI, teste, banco SQL, mock). Portas primárias (driving) dirigem a aplicação; secundárias (driven) são dirigidas por ela.

Enuncie o Dependency Inversion Principle e seu uso. :: Módulos de alto nível não devem depender de baixo nível; ambos dependem de abstrações; abstrações não dependem de detalhes; detalhes dependem de abstrações. É o que torna adaptadores substituíveis e baseia a injeção de dependência no Spring.

## Desempenho, escalabilidade, disponibilidade, segurança e custo

Latência × throughput × jitter × utilização? :: Latência é o tempo de resposta de uma operação; throughput é a quantidade de operações por unidade de tempo; jitter é a variação da latência; utilização é a fração do recurso em uso.

Como a distribuição afeta o desempenho e como mitigar? :: Chamadas remotas são muito mais lentas que em memória e encadear serviços soma latências; mitiga-se com maior granularidade (menos chamadas) e assincronismo/paralelismo (N chamadas concorrentes custam o tempo da mais lenta).

O que dizem as Fallacies of Distributed Computing? :: Premissas falsas como: a rede não é confiável nem instantânea, a topologia muda, a banda não é infinita, a latência não é zero e o transporte não é gratuito.

Escala vertical × horizontal × elasticidade? :: Vertical (scale up) aumenta recursos de uma máquina e tem limite físico; horizontal (scale out) adiciona instâncias e exige balanceamento e aplicação stateless; elasticidade é escalar automaticamente conforme a demanda.

O que é escala seletiva e o que a escalabilidade exige? :: Microsserviços, em tese, escalam só o serviço quente, mas Fowler alerta que não há muitos relatos de que isso supere replicar o aplicativo inteiro (cookie-cutter); escalar exige estado fora da aplicação, idempotência, sharding, stateless e cuidado com o banco como gargalo.

Disponibilidade × confiabilidade × resiliência e o que é a multiplicação de indisponibilidade? :: Disponibilidade é a fração de tempo no ar (SLA/SLO/SLI), confiabilidade é a probabilidade de funcionar por um período e resiliência é se recuperar de falhas; em chamadas síncronas encadeadas, a indisponibilidade do sistema é aproximadamente o produto das dos componentes, ficando pior que o pior componente.

O que é o Teorema CAP e o que é BASE? :: Sob partição de rede (P), escolhe-se entre consistência (C) e disponibilidade (A); muitos microsserviços optam por AP com consistência eventual (BASE = Basically Available, Soft state, Eventually consistent), em contraste com o ACID.

Quais são os padrões de resiliência? :: Circuit Breaker (abre o circuito após falhas), Bulkhead (isola recursos), Timeout, Retry com backoff exponencial e fallback/degradação graciosa.

Quais os princípios de segurança e como a distribuição afeta a segurança? :: Defesa em profundidade, privilégio mínimo, negação por padrão, segregação de funções, fail-safe defaults e zero trust; a distribuição amplia a superfície de ataque (mais endpoints, tráfego leste-oeste e credenciais), mitigada com mTLS, autenticação por serviço ou gateway, tokens/escopos, gestão de segredos e criptografia em repouso e em trânsito.

O que é o TCO, o custo do microsserviço e o que é FinOps? :: TCO é o custo total de propriedade (infraestrutura, desenvolvimento, operação, monitoramento, treinamento e dívida técnica); o custo do microsserviço é o Microservice Premium; o modelo pay-as-you-go converte CAPEX em OPEX e FinOps dimensiona recursos, usa autoscaling, desliga ambientes ociosos e mede/otimiza continuamente.

## Escolha de arquitetura conforme restrições

O que é uma restrição (constraint) e quais restrições definem microsserviços? :: Limitação que orienta o design, definindo quais elementos existem e quais relações são permitidas; em microsserviços: cada serviço tem uma responsabilidade, serviços são independentes e os dados são privados do dono (não se compartilha banco).

Qual a ordem de raciocínio para escolher arquitetura (Azure) e o maior fator? :: Identificar a natureza do problema; definir e priorizar drivers de negócio e requisitos não funcionais; escolher o estilo; medir, validar e refinar continuamente. O maior fator é a complexidade do domínio (simples favorece monolito modular; complexo favorece microsserviços).

Estilo ideal para domínio tradicional com baixa frequência de mudanças? :: N-tier, que divide em camadas lógicas e tiers físicos e é boa para migrar aplicações legadas.

Estilo ideal para domínio simples com tarefas pesadas/longas? :: Web-Queue-Worker, com front-end web, fila assíncrona e worker de segundo plano.

Estilo ideal para domínio complicado com alta frequência de atualizações? :: Microsserviços.

Estilo ideal para IoT e sistemas em tempo real? :: Orientada a eventos.

Big data × big compute? :: Big data divide um grande conjunto de dados em pedaços com processamento paralelo (lote, tempo real e ML); big compute aloca dados para milhares de núcleos (intensivo em CPU, simulação/HPC).

O que a maturidade técnica exige e o que são microsserviços "de mentira"? :: Exige CD, observabilidade e devops, senão o resultado piora; recomenda-se começar simples e evoluir, evitar arquitetura por moda e documentar decisões com ADRs. Serviços que precisam ser implantados em conjunto não são, de fato, microsserviços.

## Spring Framework e Spring Boot (IoC e DI)

O que são o Spring Framework e o Spring Boot? :: O Framework é um framework Java baseado em IoC, cujo contêiner gerencia beans e suas dependências (DI); o Boot é convenção sobre o Spring, com servidor embutido, starters, configuração externa e autoconfiguração, rodando com main e um JAR executável.

O que é injeção de dependência (definição oficial) e por que é uma "inversão"? :: É uma forma especializada de IoC em que os objetos definem suas dependências por argumentos de construtor, argumentos de método de fábrica ou propriedades pós-construção, cabendo ao contêiner injetá-las. É inversão porque o bean não controla a criação/localização de suas dependências (não faz new nem usa Service Locator).

Service Locator × DI e formas de DI? :: No Service Locator o objeto pede a dependência a um localizador (dependência oculta); na DI ela é fornecida de fora (transparência e testabilidade). A forma recomendada pelo Boot é por construtor (permite final, garante obrigatórias e facilita testes); setter serve para opcionais e a injeção por campo é desaconselhada.

Para que servem @Autowired e como desempatar candidatos? :: @Autowired instrui o contêiner a injetar a dependência (com um único construtor é implícita; com vários é preciso marcar o usado); candidatos se desempatam com @Primary, @Qualifier ou nomes de bean, e ambiguidade gera erro. @Value injeta valores de propriedades, e @Resource/JSR-330 (@Inject, @Named) também são suportados.

BeanFactory × ApplicationContext e o que é um bean? :: BeanFactory é a interface base do contêiner; ApplicationContext é sua subinterface/superconjunto, adicionando AOP, i18n, publicação de eventos e contextos web. Bean é o objeto instanciado, montado e gerenciado pelo contêiner, descrito nos metadados de configuração.

Como configurar beans com Java e quais são os estereótipos? :: Classes com @Configuration, métodos @Bean, @Import (outras configurações) e @ImportResource (XML legado); @ComponentScan varre o classpath. Estereótipos: @Component, @Service, @Repository (traduz exceções para DataAccessException), @Controller/@RestController e @Configuration — todos viram beans.

Quais são os escopos de bean e como o singleton difere do padrão de projeto? :: singleton (padrão, uma instância por contêiner), prototype (nova instância a cada requisição), request, session, application e websocket. O escopo singleton é uma instância por contêiner Spring; o padrão de projeto Singleton é uma instância por JVM/máquina.

Para que servem @PostConstruct, @PreDestroy e @ConfigurationProperties? :: @PostConstruct e @PreDestroy são callbacks de ciclo de vida (após a injeção e antes de destruir); @ConfigurationProperties liga propriedades externas a objetos Java tipados (config type-safe).

## Configuração e autoconfiguração no Spring Boot

Onde colocar a classe principal e por que o pacote "default" é desencorajado? :: Em um pacote raiz acima das demais classes; @SpringBootApplication define o pacote base de busca. O pacote default (sem package) faz o Boot ler todas as classes de todos os JARs (scan amplo), devendo-se usar nomes no padrão invertido (ex.: com.exemplo.projeto).

Quais três anotações @SpringBootApplication agrega? :: @SpringBootConfiguration, @EnableAutoConfiguration e @ComponentScan; deve-se usar apenas uma classe com @SpringBootApplication ou @EnableAutoConfiguration.

O que é autoconfiguração e ela sempre se aplica? :: Tentar configurar automaticamente a aplicação com base nos JARs do classpath (ex.: HSQLDB no classpath sem bean de conexão gera banco em memória); ela é condicional e não invasiva, cedendo à configuração do usuário (se você define seu DataSource, o padrão de banco embutido se retira).

Quais condições comuns a autoconfiguração usa? :: @ConditionalOnClass/@ConditionalOnMissingClass (classe no classpath), @ConditionalOnBean/@ConditionalOnMissingBean (bean, permitindo ao usuário sobrescrever padrões), @ConditionalOnProperty, @ConditionalOnResource, @ConditionalOnWebApplication e @ConditionalOnExpression (SpEL).

Como o Boot descobre, depura e exclui autoconfigurações? :: Lê o arquivo META-INF/spring/org.springframework.boot.autoconfigure.AutoConfiguration.imports e nunca as varre com component scan; --debug gera o relatório de condições; exclusões usam @SpringBootApplication(exclude)/excludeName ou a propriedade spring.autoconfigure.exclude.

O que são starters e o que é configuração funcional? :: Starters são pacotes de dependências "opinativos" (ex.: spring-boot-starter-web, -data-jpa, -security) com bibliotecas e autoconfiguração; a autoconfiguração define a infraestrutura e a configuração funcional (quais módulos existem e como interagem) é decisão do desenvolvedor.

O que diz o fator III (Config) do 12-factor e qual a ordem de precedência no Spring? :: Separar estritamente configuração de código, deixando em variáveis de ambiente o que varia entre implantações (a configuração interna dos beans pertence ao código); precedência: linha de comando > variáveis de ambiente/JNDI > propriedades de sistema > arquivos de perfil > arquivos de aplicação > @PropertySource > padrões.

## REST

O que é REST (Fielding, 2000)? :: Representational State Transfer é um estilo arquitetural para sistemas distribuídos hipermídia, não um protocolo nem um padrão; HTTP é sua instanciação mais comum.

Quais as seis restrições REST? :: Cliente–servidor, sem estado (stateless), cache, interface uniforme, sistema em camadas e code-on-demand (opcional).

O que caracteriza a restrição sem estado? :: Cada requisição contém toda a informação necessária e o estado de sessão fica no cliente; ganha visibilidade, confiabilidade e escalabilidade, ao custo de repetir mais dados.

Em que se subdivide a interface uniforme e o que é HATEOAS? :: Identificação de recursos, manipulação por representações, mensagens autodescritivas e HATEOAS (Hypermedia as the Engine of Application State), em que a navegação é guiada por controles hipermídia.

Recurso × representação e elementos de dados do REST? :: O recurso é o conceito nomeável e o cliente troca representações (JSON, XML) via negociação de conteúdo; os elementos de dados são recurso, identificador (URI/URL/URN), representação (bytes mais metadados), metadados e dados de controle.

Quais os níveis do Richardson Maturity Model? :: 0 (POX, um só endpoint/tunnel), 1 (recursos/URIs), 2 (verbos HTTP mais códigos de status) e 3 (HATEOAS).

Quais verbos são seguros e quais são idempotentes? :: GET é seguro e idempotente, e HEAD/OPTIONS também são seguros; PUT e DELETE são idempotentes, POST em geral não é e a idempotência do PATCH não é garantida. PUT substitui o recurso completo e PATCH é parcial.

O que significam os status 401 e 403 e quais as famílias de status? :: 401 Unauthorized é não autenticado e 403 Forbidden é autenticado sem permissão; as famílias são 1xx informativo, 2xx sucesso (200, 201 Created, 204), 3xx redirecionamento (301, 302, 304), 4xx erro do cliente (400, 401, 403, 404, 409, 422, 429) e 5xx erro do servidor (500, 503, 504).

Boas práticas de URIs e versionamento REST? :: Usar substantivos no plural (ex.: /clientes, /clientes/{id}) e evitar verbos; versionar por URI, header ou media type apenas como último recurso, preferindo serviços tolerantes a mudanças (Tolerant Reader) e Consumer-Driven Contracts.

## Serviços REST e separação em camadas no Spring

Qual a responsabilidade da camada de apresentação? :: Com @RestController/@Controller, fazer a tradução HTTP ↔ objetos (@RequestBody, @PathVariable, @RequestParam, @RequestHeader, ResponseEntity), sem regra de negócio, delegando ao serviço.

Qual a responsabilidade da camada de negócio? :: Com @Service, fazer validações, cálculos, orquestração e transações (@Transactional), dependendo de repositórios por interfaces e sem conhecer HTTP.

Qual a responsabilidade da camada de acesso a dados? :: Com @Repository (ou Spring Data JPA), isolar o banco, fornecer as operações de persistência e traduzir exceções.

Como as camadas se injetam e por que expor DTOs? :: O controlador recebe o serviço por construtor e o serviço recebe o repositório por construtor (Dependency Inversion Principle); DTOs evitam vazar o modelo de dados e problemas de lazy loading/serialização.

Para que serve @RestControllerAdvice e quais os pitfalls da separação? :: Padroniza respostas de erro via @ExceptionHandler (ex.: ProblemDetail/RFC 7807); pitfalls: lógica de negócio no controlador, controlador acessando repositório direto e retorno de entidade JPA crua.

O que é Spring AOP e como testar por camada? :: AOP separa interesses transversais (transações, segurança, log, cache) via aspectos e proxies, base de @Transactional e @Cacheable; testa-se com @SpringBootTest/MockMvc/WebTestClient, @MockitoBean e Testcontainers.
