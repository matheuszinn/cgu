---
tipo: resumo
disciplina: "Arquitetura e Integração de Sistemas"
tema: "Arquiteturas de aplicações"
status: estudando
data: "2026-10-14"
tags: [resumo, arquitetura, cgu-2026]
---

# Resumo: Arquiteturas de aplicações

> [!info] MOC: [[Arquitetura e Integração de Sistemas]]
> Edital nº 1/2026 – CGU – AFFC · **Conhecimentos específicos** · Cargo 4 (TI / Desenvolvimento de Sistemas) · Item 1 — *Arquiteturas de aplicações*.

## Escopo no edital (checklist)

- [x] 1.1 Monolitos, microsserviços e arquiteturas orientadas a eventos.
- [x] 1.2 Distribuição de responsabilidades, acoplamento e dependências.
- [x] 1.3 Desempenho, escalabilidade, segurança e custo.
- [x] 1.4 Escolha de arquitetura conforme restrições.
- [x] 1.5 Aplicações Java com Spring Framework e Spring Boot: organização de componentes, inversão de controle e injeção de dependências.
- [x] 1.6 Configuração e autoconfiguração.
- [x] 1.7 Construção de serviços REST e separação entre apresentação, regras de negócio e acesso a dados.

## Resumo

**Arquitetura de aplicações** é o conjunto de decisões estruturais sobre **quais componentes** existem, **quais responsabilidades** cada um tem e **como eles se comunicam e dependem** uns dos outros. A banca costuma cobrar o *trade-off*: não existe arquitetura "melhor" em abstrato, e sim arquitetura **adequada ao contexto** (complexidade do domínio, tamanho da equipe, requisitos não funcionais e restrições orçamentárias).

Três grandes estilos organizam o item: o **monolito** (uma única unidade implantável, com todos os componentes em um mesmo processo), os **microsserviços** (aplicação decomposta em serviços pequenos, independentes e implantáveis de forma autônoma, comunicando-se por rede — normalmente HTTP/REST ou mensageria) e as **arquiteturas orientadas a eventos (EDA)**, em que produtores publicam eventos e consumidores reagem de forma assíncrona e desacoplada (com variações como *event notification*, *event-carried state transfer*, *event sourcing* e **CQRS**).

A distribuição de responsabilidades e o **acoplamento** são o coração da arquitetura: busca-se **alta coesão** (cada componente faz bem uma coisa) e **baixo acoplamento** (pouca dependência entre componentes). Princípios como **DDD/bounded contexts**, **arquitetura hexagonal (portas e adaptadores)**, **camadas (apresentação–domínio–dados)** e **inversão de dependência** orientam essa divisão. Todo estilo é julgado por **atributos de qualidade** — desempenho, escalabilidade, segurança, disponibilidade, resiliência e **custo** (inclusive o "prêmio do microsserviço": mais complexidade operacional).

A escolha da arquitetura (item 1.4) deriva de **restrições e requisitos não funcionais**: domínios simples favorecem monolito modular; domínios complexos, com times grandes e necessidade de evolução independente, favorecem microsserviços; fluxos de tempo real e alto volume favorecem EDA; aplicações tradicionais com baixa frequência de mudança favorecem **N-tier**.

Em Java, o **Spring Framework** fornece o **contêiner de IoC** que gerencia **beans** e faz **injeção de dependência (DI)**; o **Spring Boot** acrescenta convenção sobre configuração, *starters*, servidor embutido e **autoconfiguração** — que só se aplica quando as condições (classes no *classpath*, ausência de bean do usuário etc.) são satisfeitas, sendo sempre possível **substituir/desligar** a configuração automática. Por fim, **serviços REST** organizam o código em **camadas** (apresentação/controladores → regras de negócio/serviços → acesso a dados/repositórios), mantendo as dependências predominantemente de cima para baixo e usando o estilo REST (REST *architectural style* de Roy Fielding) com seus recursos, representações, verbos e restrições.

## 1. Monolitos, microsserviços e arquiteturas orientadas a eventos (1.1)

### 1.1.1 Monolito

- **Definição (Martin Fowler):** aplicação construída como **uma única unidade** — "um *single logical executable*". Em geral divide-se em três partes: interface (UI/cliente), banco de dados e aplicação servidora; o servidor executa a lógica, acessa o banco e monta as respostas.
- **Características:**
  - Um **único processo** e uma **única base de código**; comunicação interna por **chamadas de método/função em memória** (rápidas e confiáveis).
  - **Uma única implantação**: qualquer alteração exige reconstruir e reimplantar **toda** a aplicação.
  - **Escala horizontal simples**: várias instâncias do mesmo monolito atrás de um balanceador (*cookie-cutter scaling* / réplicas idênticas).
  - **Transações ACID locais** fáceis: uma única transação de banco pode atualizar vários registros de forma atômica → **consistência forte** natural.
- **Vantagens:** simplicidade de desenvolvimento, testes e depuração; implantação única; baixo custo operacional inicial; desempenho de chamadas internas; consistência transacional.
- **Desvantagens (à medida que cresce):** **acoplamento** e erosão da modularidade (risco do **Big Ball of Mud**); ciclos de mudança amarrados (mudar um ponto exige reimplantar tudo); escalabilidade "grossa" (escala-se o aplicativo inteiro e não só a parte quente); dificuldade de adoção de novas tecnologias; *deploy* arriscado e lento.
- **Monolito modular:** monolito bem estruturado, com **fronteiras de módulo explícitas** e internas (pacotes/módulos com interfaces claras). Fowler: é perfeitamente possível ter fortes fronteiras de módulo em um monolito — exige **disciplina**. É a base da estratégia *Monolith First*. No ecossistema Spring, o **Spring Modulith** implementa a ideia de módulos com fronteiras verificáveis.
- **Big Ball of Mud:** antônimo do monolito modular — sistema sem estrutura clara, no qual as dependências se cruzam de forma desordenada.

### 1.1.2 Microsserviços

- **Definição (Lewis & Fowler):** estilo arquitetural que estrutura a aplicação como **um conjunto de serviços pequenos**, cada um **rodando em seu próprio processo**, comunicando-se por **mecanismos leves** (frequentemente API HTTP de recursos), **construídos em torno de capacidades de negócio** e **implantáveis de forma independente** por maquinário de implantação automatizado.
- **Características (as 9 de Fowler):**
  1. **Componentização via serviços** — o componente é a unidade substituível/atualizável de forma independente; serviços são componentes **fora de processo** (comunicação remota), em contraste com **bibliotecas** (chamadas em memória).
  2. **Organização por capacidade de negócio** — serviços em torno de áreas de negócio (*business capabilities*), com times **multifuncionais** (cross-functional), e não divididos por camada técnica (UI, lógica, DBA).
  3. **Produto, não projeto** — o time acompanha o serviço ao longo de todo o seu **ciclo de vida** ("*you build, you run it*"), em vez de entregar e dissolver o time.
  4. ***Smart endpoints and dumb pipes*** — a inteligência fica nos **serviços**; a infraestrutura de comunicação é "burra" (apenas roteia mensagens). Preferem-se protocolos simples (HTTP/REST) e mensageria leve (RabbitMQ, ZeroMQ), em oposição a **ESB** com roteamento, coreografia e transformação sofisticadas.
  5. **Governança descentralizada** — liberdade para escolher linguagens, bibliotecas e *frameworks*; padrões *battle-tested* e amplamente implementados em vez de padrões centrais rígidos.
  6. **Gestão de dados descentralizada** — cada serviço gerencia **seu próprio banco**; admite **polyglot persistence** (bancos diferentes conforme a necessidade). Evita o *integration database* compartilhado, fonte de acoplamento.
  7. **Automação de infraestrutura** — *continuous integration/delivery*, pipelines de build/teste/deploy automatizados; essenciais por causa da quantidade de serviços.
  8. **Design para falha (*design for failure*)** — qualquer chamada remota pode falhar; o cliente deve tratar a falha com elegância. Padrões: **Circuit Breaker**, **Bulkhead**, **Timeout**; testes de caos (*Chaos Monkey/Simian Army*).
  9. **Design evolucionário** — decomposição como ferramenta para controlar mudanças; parte da ideia de **componente substituível** (alguns serviços são descartados em vez de evoluir).
- **Vantagens:** fronteiras de módulo fortes; **implantação independente** (mudar um serviço não reimplanta o resto); **diversidade tecnológica** (e, sobretudo, **versionamento** independente de bibliotecas); isolamento de falhas; **escalabilidade seletiva** (escala só o serviço sobrecarregado); times autônomos e maior velocidade de entrega; possibilidade de separar e proteger dados sensíveis.
- **Desvantagens / custos:** **sistemas distribuídos são mais difíceis** (chamadas remotas lentas e sujeitas a falha); **consistência eventual** em vez de transações locais; **complexidade operacional** (muitos serviços, monitoramento, *deploy*); depuração entre serviços; **duplicação/coordenação** de contratos; necessidade de maturidade (CD, *devops*).
- **Tamanho do serviço:** "micro" **não** define tamanho. Fowler cita desde times de "duas pizzas" (Amazon, ~uma dúzia de pessoas) até times pequenos mantendo vários serviços. O tamanho ideal está ligado a **fronteiras de negócio**, não a linhas de código.
- **Microsserviços × SOA:** microsserviços lembram SOA, mas SOA significa coisas muito diferentes — frequentemente associada a **ESB** central e a aplicações monolíticas integradas. Alguns consideram microsserviços uma forma de SOA "feita direito"; outros rejeitam o rótulo. Diferenças típicas: serviços menores e mais finos, **dados descentralizados**, governança descentralizada e *smart endpoints* em vez de *smart pipes*.
- **Conway's Law:** "as organizações projetam sistemas que são cópias de suas estruturas de comunicação" (Melvin Conway, 1968). Daí a **Inverse Conway Maneuver**: reorganizar os times para induzir a arquitetura desejada.

### 1.1.3 Estratégia *Monolith First* e o "prêmio do microsserviço"

- **Microservice Premium (Fowler):** microsserviços impõem **custo extra de produtividade** que só se paga em **sistemas complexos**. Diretriz: **não considere microsserviços a menos que o sistema seja complexo demais para um monolito**.
- **Monolith First (Fowler):** quase todos os casos de sucesso de microsserviços **começaram como um monolito** que cresceu e foi decomposto; quase todos os casos que começaram direto como microsserviços **tiveram problemas**. Razões: (a) o **YAGNI** — talvez o produto nem seja útil; (b) é difícil acertar **as fronteiras** dos serviços no começo; refatorar entre serviços é muito mais caro que entre bibliotecas.
- Formas de executar: monolito modular → extrair serviços nas bordas (*peel off*); começar com **poucos serviços grosseiros** e refinar; substituir totalmente o monolito (arquitetura "sacrificial"). Há quem defenda começar já com microsserviços, especialmente em **substituição de sistemas** com domínio bem conhecido e times experientes.

### 1.1.4 Arquiteturas orientadas a eventos (EDA)

- **Definição:** estilo em que **produtores** geram **eventos** (registros de algo que aconteceu), **consumidores** reagem a eles e **canais/brokers** transportam os eventos. Produtores e consumidores são **desacoplados** (o produtor não sabe quem consome) e a entrega é **assíncrona**, em tempo quase real.
- **Evento × comando × mensagem:**
  - **Evento** — fato ocorrido no passado, imutável (ex.: `OrderCreated`); o produtor não espera resposta. É um **fato**, não uma ordem.
  - **Comando** — intenção/ordem direcionada a um destinatário (ex.: `ReserveCredit`); espera ser executada.
  - **Mensagem** — termo genérico que cobre ambos.
  - **Armadilha (Fowler):** usar um evento como **"comando passivo-agressivo"** quando se espera que o destinatário execute uma ação — deveria ser um comando.
- **Padrões de "eventos" (Fowler, 2017):**
  1. **Event Notification** — notificar que algo mudou, com pouca carga (IDs); o receptor decide se busca mais dados. **Baixo acoplamento**, simples, mas o fluxo lógico fica **implícito** (difícil de enxergar/depurar se ninguém documenta a coreografia).
  2. **Event-Carried State Transfer** — o evento **carrega os dados** alterados; o consumidor mantém sua própria cópia e **não precisa consultar** o produtor. Ganha-se resiliência (funciona se a origem cair), menor latência e menos carga na origem; paga-se com **mais dados trafegados, cópias e complexidade** de manter estado.
  3. **Event Sourcing** — em vez de guardar só o **estado atual**, guarda-se a **sequência de eventos** que levou a ele; o **log de eventos é a fonte da verdade** e o estado é derivado por *replay*. Exemplos: controle de versão (o log de commits é o event store). Benefícios: **auditoria forte**, reconstrução de estados passados, *snapshots*. Cuidados: mudança de esquema dos eventos, complexidade, resultados dependentes de sistemas externos, distinção entre *replay* e estado corrente.
  4. **CQRS (Command Query Responsibility Segregation)** — separar o **modelo de escrita** (comandos) do **modelo de leitura** (consultas). Útil em domínios complexos e quando há grandes diferenças entre padrões de leitura e escrita (ex.: muitas leituras, poucas escritas), permitindo escalar/otimizar cada lado separadamente. **Não exige eventos**, mas costuma ser combinado com eles. Fowler alerta: **CQRS adiciona complexidade perigosa** e deve ser usado em **partes específicas** do sistema (um *bounded context*), nunca no sistema inteiro.
- **Topologias (Azure):**
  - **Broker (corretor)** — os componentes **difundem eventos** para todo o sistema; quem se interessa reage. Altamente desacoplado, simples, dinâmico — mas **não há coordenação/orquestração central**, o que dificulta tratamento de erro, reinício e consistência.
  - **Mediator (mediador)** — um **mediador de eventos** controla o fluxo, mantém estado e trata erros/reinício; despacha **comandos** para canais designados (normalmente filas) em vez de difundir. Mais controle e consistência, porém **maior acoplamento** e risco de o mediador ser gargalo/ponto único de falha.
- **Modelos de entrega:**
  - **Publish-subscribe** — a infraestrutura rastreia assinaturas; o evento é entregue a cada assinante; **não é durável** (novos assinantes não veem eventos passados). Ex.: Azure Event Grid; Kafka tem semântica de *log*.
  - **Event streaming** — eventos gravados em **log durável e ordenado por partição**; o cliente lê de qualquer posição e **pode reprocessar** (*replay*). Ex.: Azure Event Hubs, Apache Kafka.
- **Coordenação de fluxos distribuídos:**
  - **Coreografia (choreography)** — cada serviço publica eventos que **disparam** os próximos; sem controlador central. Simples e desacoplada, mas o fluxo global fica difícil de visualizar.
  - **Orquestração (orchestration)** — um **orquestrador** comanda os participantes (envia comandos e recebe respostas). Fluxo explícito e controlado, mas adiciona acoplamento e um componente central.
- **Saga (microservices.io):** uma **transação de negócio que atravessa vários serviços** é implementada como **sequência de transações locais**; cada uma publica evento/mensagem que dispara a próxima. Se uma falhar, disparam-se **transações compensatórias** que desfazem as anteriores. Problemas: **não há rollback automático** (compensações devem ser escritas) e há **falta de isolamento** (a letra "I" do ACID), exigindo contramedidas.
- **Consistência em EDA:** como não se usam **transações distribuídas (2PC)**, a consistência costuma ser **eventual**; exige **idempotência** (evitar efeito duplo de mensagens reentregues), **ordenação** e padrões como **Transactional Outbox** e *event sourcing* para gravar estado e publicar evento atomicamente. Métricas/rastreamento: propagar um **correlation ID** nos eventos e usar *distributed tracing*.

## 2. Distribuição de responsabilidades, acoplamento e dependências (1.2)

### 2.1 Coesão e acoplamento

- **Coesão** = grau em que elementos de um módulo pertencem juntos (fazem uma coisa só). Quer-se **alta coesão**.
- **Acoplamento** = grau de dependência entre módulos. Quer-se **baixo acoplamento**.
- **Objetivo arquitetural:** combinar **alta coesão** com **baixo acoplamento**; "mudanças que acontecem juntas ficam no mesmo módulo" (modularidade dirigida pelo padrão de mudança). Se dois serviços mudam sempre juntos, provavelmente deveriam ser um só.
- **Tipos/força de acoplamento:** de mais fraco para mais forte — por **parâmetros de dados**, por **estrutura de dados**, por **interface**, por **estado global**, por **conteúdo** (acesso a internals). Acoplamento **temporal** (componentes dependem de estarem ativos ao mesmo tempo) é crítico em sistemas distribuídos.
- **Acoplamento aferente/efetente (métricas de Martin):**
  - **Ca — Afferent coupling:** quantas classes externas dependem deste módulo (responsabilidade).
  - **Ce — Efferent coupling:** de quantos módulos este depende.
  - **Instabilidade I = Ce / (Ca + Ce)**: 0 = estável (muitos dependem dele, ele depende de poucos); 1 = instável. **Componentes estáveis devem ser abstratos** (SDP/SAP — Stable Dependencies Principle / Stable Abstractions Principle).

### 2.2 Distribuição de responsabilidades

- **DDD — Domain-Driven Design:** dividir o domínio em **bounded contexts** (contextos delimitados), cada um com sua **linguagem ubíqua** (*ubiquitous language*) e seu modelo. Há correlação natural entre **fronteira de contexto** e **fronteira de serviço/módulo**.
- **Conway's Law / Inverse Conway Maneuver:** a estrutura do software tende a espelhar a comunicação da organização; pode-se reorganizar times para obter a modularização desejada.
- **Granularidade:** serviço/módulo muito **grande** → baixa coesão e acoplamento alto; muito **pequeno** → excesso de comunicação e "nano-serviços". O critério é a **capacidade de negócio**, não a contagem de linhas.
- **Responsabilidade única:** cada componente deve ter **uma razão para mudar**. Evitar o **objeto de Deus** / classes responsáveis por tudo.

### 2.3 Camadas, camadas lógicas × tiers físicos

- **Presentation–Domain–Data Layering (Fowler):** as aplicações de informação são comumente separadas em **três camadas**:
  - **Apresentação (UI):** lida com requisições/HTTP e renderização/resposta.
  - **Domínio / regras de negócio:** validações e cálculos; o "coração".
  - **Acesso a dados (persistência):** como armazenar/recuperar dados (banco, serviços remotos).
- **Direção das dependências:** em geral **de cima para baixo** — a apresentação depende do domínio, que depende do acesso a dados.
- **Inversão para desacoplar o domínio:** pode-se inserir um **mapper/adapter** entre domínio e dados para que o **domínio não dependa do banco** (*Hexagonal Architecture / Ports and Adapters*).
- **Vantagens da separação em camadas:** reduzir o escopo de atenção; permitir **múltiplas apresentações** sobre a mesma lógica; possibilitar **substituição** de implementações; **testabilidade** (costuras/*seams* para testes, *test doubles*).
- **Camadas lógicas ≠ tiers físicos:** pode-se rodar as três camadas numa única máquina (monolito) ou distribuí-las em *tiers* separados (apresentação no browser + BFF, domínio em servidor, banco em outro). "Camada" é conceitual; "tier" é implantação física.
- **Anti-padrão:** separar **times por camada** (time de front-end, time de back-end, time de DBA). Fowler: "desenvolvedores não precisam ser *full-stack*, mas **os times devem ser**"; fronteiras de time por camada criam fricção e afastam do usuário.
- **Quando a aplicação cresce:** o corte em camadas funciona em granularidade **pequena**; em sistemas grandes, o **nível mais alto** de módulos deve ser **orientado a domínio**, com camadas **dentro** de cada módulo.

### 2.4 Arquitetura hexagonal (Ports & Adapters) e inversão de dependência

- **Hexagonal (Alistair Cockburn, 2005):** o aplicativo deve funcionar **sem UI e sem banco**, para permitir testes automatizados, operar em modo *headless* (só API) e integrar-se a outros programas. Centraliza a relação **dentro × fora**: o código do **interior** não pode "vazar" para o **exterior**.
- **Portas (ports):** interfaces que definem a **conversa** com o exterior (ex.: porta de UI, porta de banco). **Adaptadores (adapters):** implementações tecnológicas de uma porta (GUI, teste, arquivo, banco SQL, *mock*).
- **Portas primárias (driving) × secundárias (driven):** primárias **dirigem** a aplicação (usuário, teste, HTTP); secundárias são **dirigidas** por ela (banco, mensageria). O "hexágono" é só uma forma de desenhar vários adaptadores simétricos em torno do núcleo.
- **Dependency Inversion Principle (Robert C. Martin):** "módulos de alto nível não devem depender de módulos de baixo nível; ambos devem depender de **abstrações**; abstrações não devem depender de detalhes; detalhes devem depender de abstrações." É o que torna os adaptadores substituíveis (mock ↔ real) e baseia a injeção de dependência no Spring.
- **Layered vs Hexagonal:** camadas enfatizam UI/armazenamento separados; portas e adaptadores enfatizam **interior × exterior** e a **substituibilidade** das tecnologias externas.

## 3. Desempenho, escalabilidade, segurança e custo (1.3)

### 3.1 Desempenho (performance)

- **Latência** = tempo de resposta de uma operação; **throughput** = quantidade de operações por unidade de tempo; **jitter** = variação da latência; **utilização** = fração do recurso em uso.
- **Distribuição custa desempenho:** chamadas **remotas** são muito mais lentas que chamadas **em memória**. Encadear serviços (A→B→C→…) **soma** latências; mitigar com (a) **maior granularidade** (menos chamadas) e (b) **assincronismo/paralelismo** (N chamadas concorrentes custam o tempo da **mais lenta**, não a soma).
- **Fallacies of Distributed Computing:** a rede não é confiável, nem instantânea, a topologia muda, a banda não é infinita, a latência não é zero, o transporte não é gratuito, a rede é homogênea (falso), etc.
- **Boas práticas:** cache (reduz latência média), *content delivery*/CDN, chamadas assíncronas, *batching*, granularidade dos serviços, evitar *chatty* (conversa fiada) entre serviços.

### 3.2 Escalabilidade

- **Vertical (escala para cima / scale up):** aumentar recursos de uma máquina (CPU, RAM). Simples, sem mudar arquitetura, mas tem **limite físico** e pontos únicos de falha.
- **Horizontal (escala para fora / scale out):** adicionar **instâncias**; exige balanceamento de carga, aplicação **sem estado** (*stateless*) ou estado compartilhado. Quase sempre preferida em nuvem.
- **Elasticidade:** capacidade de escalar **automaticamente** conforme a demanda (mais nuvem que escalabilidade pura); ligada ao *autoscaling*.
- **Escala seletiva × cookie-cutter:** microsserviços, em tese, permitem escalar **só o serviço quente**; Fowler alerta que **não** são muitos os relatos convincentes de que isso seja mais eficiente que replicar o aplicativo inteiro (escala *cookie-cutter*). Rode réplicas idênticas e balanceie.
- **Escalabilidade exige:** estado fora da aplicação (banco/cache/sessão distribuída), idempotência, particionamento (sharding), *stateless*, e cuidado com o **banco** como gargalo.

### 3.3 Disponibilidade, confiabilidade e resiliência

- **Disponibilidade** = fração de tempo no ar (ex.: "nove" tradicionais – 99,9% ≈ 8h46 de indisponibilidade/ano). **SLA/SLO/SLI** = acordo, objetivo e indicador de nível de serviço.
- **Confiabilidade** = probabilidade de funcionar corretamente por um período. **Resiliência** = capacidade de se recuperar de falhas.
- **Multiplicação de indisponibilidade:** em **chamadas síncronas** encadeadas, a indisponibilidade do sistema ≈ **produto** das indisponibilidades dos componentes (torna-se pior que o pior componente). Mitigar com **assincronismo** ou gestão de indisponibilidade. Regra da Guardian: **ao menos uma chamada síncrona por requisição**; Netflix construiu assincronia na "malha" da API.
- **Padrões de resiliência:** **Circuit Breaker** (abre o circuito após falhas, evita sobrecarregar o serviço em pane), **Bulkhead** (isola recursos para conter falhas), **Timeout**, **Retry com backoff exponencial**, **fallback/degradação graciosa**.
- **Teorema CAP (Brewer):** em sistema distribuído, sob **partição de rede (P)**, é preciso escolher entre **consistência (C)** e **disponibilidade (A)**. Muitos sistemas de microsserviços optam por **AP + consistência eventual**. **ACID × BASE:** BACID = Atomicidade, Consistência, Isolamento, Durabilidade (transações clássicas); BASE = Basically Available, Soft state, Eventually consistent.

### 3.4 Segurança

- **Princípios:** **defesa em profundidade** (várias camadas de controle), **privilégio mínimo** (*least privilege*), **negação por padrão** (*deny by default*), **segregação de funções**, **fail-safe defaults**, **não confiar em entrada externa** (*zero trust*).
- **Superfície de ataque cresce com a distribuição:** mais serviços = mais endpoints, mais tráfego leste-oeste (entre serviços), mais credenciais. Boas práticas: proteger **todo** o tráfego entre serviços (mTLS), autenticação/autorização em cada serviço (ou no *gateway*), **tokens** e escopos, **gestão de segredos** (não embutir em código), criptografia em repouso e em trânsito.
- **Isolamento por serviço:** permite separar **dados sensíveis** e aplicar controles mais rigorosos a eles; um *breach* em um serviço deve ter impacto limitado (princípio do menor privilégio e *bulkhead*).
- **Riscos clássicos (OWASP):** injeção (SQL/command), quebra de autenticação/sessão, exposição de dados sensíveis, XXE, quebra de controle de acesso (incluindo **permissões excessivas**), má configuração de segurança, XSS, desserialização insegura, uso de componentes vulneráveis, logs/monitoramento insuficientes.
- **Em EDA:** eventos costumam ser **visíveis a vários componentes** (não só ao consumidor); incluir só o necessário no *payload* ("assume breach"). Cuidado com **instruções maliciosas em conteúdo externo** e com *prompt injection* quando há IA (tema do item 4, mas vale o princípio de sanitizar entradas).

### 3.5 Custo

- **TCO (Total Cost of Ownership):** não só infraestrutura, mas **desenvolvimento, operação, monitoramento, treinamento, dívida técnica**.
- **Custo do microsserviço:** mais máquinas/serviços, mais *deploy*, mais observabilidade, **mais pessoas qualificadas e mais tempo**. O *Microservice Premium* é, essencialmente, **custo**.
- **Modelo de nuvem:** **pay-as-you-go** (paga pelo consumo), elástico; reduz investimento inicial (CAPEX → OPEX), mas exige controle de gastos (custo de egresso de dados, recursos ociosos, *over-provisioning*).
- **Trade-off central:** arquitetura mais sofisticada só se justifica se o **benefício (requisitos não funcionais atendidos)** superar o **custo e a complexidade**.
- **FinOps (boa prática):** dimensionar recursos, autoscaling, desligar ambientes ociosos, escolher serviços gerenciados quando reduzirem esforço operacional, medir e otimizar continuamente.

## 4. Escolha de arquitetura conforme restrições (1.4)

### 4.1 Arquitetura é um conjunto de decisões condicionadas

- **Restrição (constraint)** = limitação que orienta o *design*: o estilo define quais elementos podem existir e quais relações são permitidas — isso "dá forma" à arquitetura. Ao aderir às restrições, certas propriedades desejáveis **emergem**.
- **Exemplo (microsserviços), restrições:** cada serviço tem **uma responsabilidade**; serviços são **independentes**; **dados são privados** do serviço dono (não se compartilha banco). Ao respeitá-las, ganham-se: implantação independente, isolamento de falhas, atualizações mais frequentes e adoção mais fácil de novas tecnologias.
- **Ordem de raciocínio (Azure):** (1) identificar a **natureza do problema**; (2) definir **drivers de negócio** e **características arquiteturais / requisitos não funcionais**, **priorizando-os**; (3) escolher o estilo; (4) **medir, validar e refinar** continuamente. Mudar de rumo depois costuma ser **caro** → vale investir mais na definição inicial.

### 4.2 Estilos comuns e quando usar (Azure Architecture Styles)

| Estilo | Gerenciamento de dependências | Tipo de domínio ideal |
| --- | --- | --- |
| **N-tier** | Camadas horizontais por sub-rede | Domínio de negócio tradicional; baixa frequência de mudanças |
| **Web-Queue-Worker** | Front-end e *workers* separados por mensageria assíncrona | Domínio relativamente simples com tarefas pesadas/longas |
| **Microsserviços** | Serviços decompostos **funcionalmente** (vertical) que se chamam por APIs | Domínio **complicado**; alta frequência de atualizações |
| **Orientada a eventos** | Produtor/consumidor; visão independente por subsistema | IoT e sistemas em tempo real |
| **Big data** | Divide grande conjunto de dados em pedaços; processamento paralelo | Análise em lote e em tempo real; ML |
| **Big compute** | Alocação de dados para milhares de núcleos | Domínios intensivos em CPU (simulação, HPC) |

- **N-tier:** divide em **camadas lógicas e tiers físicos**; cada camada só chama a de baixo. Boa para migrar aplicações legadas; a horizontalidade dificulta mudanças sem afetar várias partes (menor agilidade).
- **Web-Queue-Worker:** front-end web + fila + *worker* de segundo plano; ideal para cargas pesadas assíncronas; escalável separadamente; cuidado para não virar monólito.
- **Escolha = equilíbrio:** o estilo não exige tecnologia específica, mas algumas tecnologias se encaixam melhor (ex.: contêineres para microsserviços).

### 4.3 Fatores de decisão (checklist)

- **Complexidade do domínio** (o maior fator): sistema simples → monolito modular; complexo → microsserviços.
- **Tamanho e distribuição da equipe:** times grandes/distribuídos favorecem serviços com fronteiras fortes (Conway).
- **Frequência de mudanças / velocidade de entrega:** alto → serviços e CD.
- **Requisitos não funcionais priorizados:** tempo de mercado (maintainability, testability, reliability), orçamento apertado (feasibility e simplicidade), latência, escala, disponibilidade.
- **Maturidade técnica e cultural:** microsserviços/EDA exigem **CD, observabilidade, devops**; sem isso, o resultado piora.
- **Restrições regulatórias/segurança** e **custo**.
- **Práticas:** atenção a **limites da orientação geral** ("depende"); evitar "arquitetura por moda"; começar simples e evoluir (evolutiva); documentar decisões (**ADRs**).

### 4.4 Consequências de escolher mal

- **Complexidade desnecessária** (microsserviços em domínio simples) → queda de produtividade, mais risco, mais custo.
- **Simplicidade excessiva** (monolito grande sem modularidade) → **Big Ball of Mud**, dependências mal gerenciadas, estrutura que se degrada.
- **Microsserviços "de mentira":** quando os serviços precisam ser implantados **em conjunto**, não é, de fato, uma arquitetura de microsserviços.

## 5. Aplicações Java com Spring Framework e Spring Boot (1.5)

### 5.1 Visão geral

- **Spring Framework:** *framework* Java baseado no princípio de **Inversão de Controle (IoC)**; seu **contêiner de IoC** gerencia objetos (**beans**) e suas dependências (**injeção de dependência — DI**).
- **Spring Boot:** *framework* de convenção sobre o Spring que simplifica a criação de aplicações autônomas (servidor web embutido, *starters*, configuração externa e **autoconfiguração**), permitindo rodar com `main` e um JAR executável.

### 5.2 Inversão de Controle (IoC) e Injeção de Dependência (DI)

- **Definição (Spring/versão oficial):** **DI é uma forma especializada de IoC**, na qual os objetos definem suas dependências apenas por **argumentos de construtor**, **argumentos de método de fábrica** ou **propriedades** definidas após a construção. O **contêiner IoC injeta** essas dependências quando cria o bean.
- **É "inversão"** porque o bean **não controla** a criação/localização de suas dependências (não faz `new` nem usa *Service Locator*); quem controla é o contêiner.
- **Service Locator × DI:** no *Service Locator*, o objeto **pede** a dependência a um localizador (dependência oculta do localizador); na **DI**, as dependências são **fornecidas de fora** (preferível: transparência, testabilidade).
- **Formas de DI:**
  - **Por construtor (recomendada):** permite `final` (imutável), garante dependências obrigatórias, facilita testes; o Spring Boot **recomenda injeção por construtor**.
  - **Por *setter*:** dependência opcional/ajustável após construção.
  - **Por campo (`@Autowired` em atributo):** menos recomendada (dificulta testes, esconde dependências e fere imutabilidade).
- **`@Autowired`:** instrui o contêiner a resolver/injetar a dependência. Se houver **mais de um construtor**, é preciso marcar o usado. Com **um** construtor, a injeção é implícita (não precisa de `@Autowired`).
- **Desempate de candidatos:** `@Primary` (preferência), `@Qualifier` (nome qualificado), ou nomes de bean; ambíguo → erro.
- **`@Value`:** injeta valores de propriedades. **`@Resource`** e anotações **JSR-330** (`@Inject`, `@Named`) também são suportadas.

### 5.3 Contêiner IoC: `BeanFactory` × `ApplicationContext`

- **`BeanFactory`:** interface base; mecanismo avançado de configuração e gerência de objetos.
- **`ApplicationContext`** (subinterface de `BeanFactory`, **superconjunto**): adiciona integração com **AOP**, manipulação de **recursos de mensagem** (i18n), **publicação de eventos** e contextos específicos (ex.: `WebApplicationContext`). É o contêiner usado na prática.
- **Bean:** objeto **instanciado, montado (assembled) e gerenciado** pelo contêiner. Beans e suas dependências são descritos nos **metadados de configuração** (anotações Java, XML, etc.).

### 5.4 Configuração do contêiner

- **Configuração baseada em Java (preferida no Boot):** classes anotadas com **`@Configuration`**; métodos **`@Bean`** definem beans; **`@Import`** importa outras classes de configuração; **`@ImportResource`** carrega XML legado.
- **Configuração por anotações + varredura:** **`@ComponentScan`** varre o *classpath* procurando componentes; **estereótipos** são especializações de `@Component`:
  - **`@Component`** — componente genérico.
  - **`@Service`** — serviço/regra de negócio.
  - **`@Repository`** — acesso a dados (também traduz exceções de persistência para `DataAccessException`).
  - **`@Controller` / `@RestController`** — camada web.
  - **`@Configuration`** — classe de configuração.
  - Todos são **registrados automaticamente como beans**.
- **Escopos de bean (`@Scope`):**
  - **`singleton`** (padrão) — uma instância por contêiner.
  - **`prototype`** — nova instância a cada requisição ao contêiner.
  - **`request`**, **`session`**, **`application`**, **`websocket`** — escopos web.
- **Ciclo de vida:** *callbacks* **`@PostConstruct`** (após injeção) e **`@PreDestroy`** (antes de destruir); interfaces `InitializingBean`/`DisposableBean`; `@Lazy` para atrasar a criação.
- **Herança de definição de bean**, **`depends-on`**, e **pontos de extensão do contêiner** (`BeanPostProcessor`, `BeanFactoryPostProcessor`) permitem customização avançada.
- **`@ConfigurationProperties`** liga propriedades externas a objetos Java tipados (configuração **type-safe**).

### 5.5 Spring Boot: organização de componentes

- **Classe principal:** recomenda-se colocá-la em um **pacote raiz acima das demais classes**. A anotação **`@SpringBootApplication`** (na classe `main`) define implicitamente o **"pacote de busca"** base para varredura de componentes e entidades.
- **`@SpringBootApplication`** equivale a **três** anotações:
  - **`@SpringBootConfiguration`** — permite registrar beans adicionais/importar configurações (variação de `@Configuration`, ajuda a detecção em testes).
  - **`@EnableAutoConfiguration`** — habilita a **autoconfiguração**.
  - **`@ComponentScan`** — habilita a varredura de componentes a partir do pacote da aplicação.
  - Deve-se usar **apenas um** `@SpringBootApplication`/`@EnableAutoConfiguration` (na classe principal).
- **Pacote "default" (sem declaração `package`) é desencorajado:** faz o Boot ler **todas** as classes de **todos** os JARs (scan amplo); usar nomes de pacote no padrão invertido (ex.: `com.exemplo.projeto`).
- **Estrutura recomendada (por funcionalidade/domínio):**

```
com
 +- exemplo
     +- minhaapp
         +- MinhaApp.java
         +- cliente
         |   +- Cliente.java
         |   +- ClienteController.java
         |   +- ClienteService.java
         |   +- ClienteRepository.java
         +- pedido
             +- Pedido.java
             +- PedidoController.java
             +- PedidoService.java
             +- PedidoRepository.java
```

- O Spring Boot **não exige** layout específico, mas essas são boas práticas. Para **impor** fronteiras por domínio, existe o **Spring Modulith** (aplicações modulares *domain-driven* sobre Spring Boot).

### 5.6 AOP e teste (contexto útil)

- **Spring AOP:** permite separar **interesses transversais** (transações, segurança, log, cache) via **aspectos** e **proxies**; é a base de anotações como `@Transactional` e `@Cacheable`.
- **Testes:** `Spring TestContext`, `@SpringBootTest`, **`MockMvc`/`WebTestClient`** para a camada web, **`@MockitoBean`** para *mocks*, **Testcontainers** para integrações reais; *test slices* para carregar só parte do contexto.

## 6. Configuração e autoconfiguração (1.6)

### 6.1 Configuração externa (externalized configuration)

- **Princípio (12-factor / fator III — Config):** **separar estritamente configuração de código**. Configuração é tudo que **varia entre implantações** (endereços de banco, credenciais, hostname). O teste decisivo: o **código poderia ser aberto** sem comprometer credenciais.
- **Na 12-factor:** config deve ficar em **variáveis de ambiente** (linguagem/OS-agnósticas, sem risco de *commit* acidental). Observação: a **configuração interna** da aplicação (como os módulos são ligados/`beans`) **não** é "config" 12-factor — fica no código.
- **No Spring Boot:** arquivos **`application.properties`** ou **`application.yml`**, além de variáveis de ambiente, argumentos de linha de comando, `SPRING_APPLICATION_JSON`, etc.
- **Ordem de precedência (resumo):** linha de comando > variáveis de ambiente/JNDI > propriedades de sistema > arquivos de perfil > arquivos de aplicação > `@PropertySource` > padrões. (O que vem antes **sobrescreve** o de depois.)
- **Perfis (`spring.profiles.active`):** grupos de configuração por ambiente (ex.: `dev`, `test`, `prod`); documentados como recurso do Boot.
- **Placeholders e `@Value` / `@ConfigurationProperties`:** injetam e vinculam valores de forma tipada.
- **`@ConfigurationPropertiesScan`**: registra automaticamente classes anotadas com `@ConfigurationProperties`.

### 6.2 Autoconfiguração

- **Definição (Spring Boot):** "a autoconfiguração tenta **configurar automaticamente** a aplicação Spring com base nos **JARs no *classpath***". Ex.: se o HSQLDB está no *classpath* e o usuário **não** criou nenhum bean de conexão, o Boot autoconfigura um banco em memória.
- **Como habilitar:** adicionar **`@EnableAutoConfiguration`** ou **`@SpringBootApplication`** a uma classe `@Configuration` (a classe principal).
- **Não invasiva / substituível:** a qualquer momento pode-se **definir configuração própria para substituir** parte da automática. Ex.: se você define seu próprio bean `DataSource`, o suporte padrão a banco embutido **se retira** (*backs away*).
- **Como funciona (criando sua própria autoconfiguração):**
  - Classes anotadas com **`@AutoConfiguration`** (que é meta-anotada com `@Configuration`).
  - Usam **`@Conditional`** para decidir quando se aplicar; as mais comuns:
    - **`@ConditionalOnClass` / `@ConditionalOnMissingClass`** — presença/ausência de **classes** no *classpath*.
    - **`@ConditionalOnBean` / `@ConditionalOnMissingBean`** — presença/ausência de **beans**; `@ConditionalOnMissingBean` permite ao usuário **sobrescrever** os padrões.
    - **`@ConditionalOnProperty` / `@ConditionalOnBooleanProperty`** — com base em **propriedades**.
    - **`@ConditionalOnResource`** — com base em **recursos**.
    - **`@ConditionalOnWebApplication` / `@ConditionalOnNotWebApplication`**; **`@ConditionalOnWarDeployment`**.
    - **`@ConditionalOnExpression`** — expressão **SpEL**.
  - Descoberta: o Boot lê o arquivo **`META-INF/spring/org.springframework.boot.autoconfigure.AutoConfiguration.imports`** (uma classe por linha) empacotado no JAR. Autoconfigurações **só** são carregadas por esse arquivo e **nunca** por varredura de componentes.
  - **Ordenação:** `before`/`after`/`beforeName`/`afterName` em `@AutoConfiguration`, ou `@AutoConfigureBefore`/`@AutoConfigureAfter`, ou `@AutoConfigureOrder`.
  - **Substituição/depreciação:** arquivo **`...AutoConfiguration.replacements`** mapeia classe antiga → nova.
  - **Cuidado com a ordem:** `@ConditionalOnBean`/`@ConditionalOnMissingBean` só devem ser usados em autoconfigurações (que carregam **depois** dos beans do usuário).
- **Depurar/inspecionar:** iniciar com **`--debug`** gera o **relatório de condições** (*conditions report*) no console — mostra **quais** autoconfigurações foram aplicadas e **por quê**.
- **Desligar autoconfigurações específicas:**
  - `@SpringBootApplication(exclude = {DataSourceAutoConfiguration.class})` (ou `excludeName` se a classe não estiver no *classpath*).
  - Propriedade **`spring.autoconfigure.exclude`**.
  - Exclusões podem ser definidas por anotação **e** por propriedade.
- **Starters:** pacotes de dependências "opinativos" (ex.: `spring-boot-starter-web`, `-data-jpa`, `-security`) que trazem as bibliotecas necessárias e a autoconfiguração associada.
- **Observação prática:** a autoconfiguração do Boot define a **infraestrutura**; a **configuração funcional** (quais módulos existem e como interagem) é decisão do desenvolvedor.

## 7. Construção de serviços REST e separação em camadas (1.7)

### 7.1 O que é REST (Roy Fielding, 2000)

- **REST = Representational State Transfer:** **estilo arquitetural** para sistemas distribuídos hipermídia, **não** um protocolo nem um padrão. Descrito na tese de Roy Fielding; HTTP é sua instanciação mais comum.
- **Restrições arquiteturais (derivação):**
  1. **Cliente–servidor** — separação de interesses (UI × dados); componentes evoluem independentemente.
  2. **Sem estado (stateless)** — cada requisição contém **toda** a informação necessária; **estado de sessão fica no cliente**. Ganha-se visibilidade, confiabilidade e escalabilidade; paga-se com mais dados repetidos por requisição.
  3. **Cache** — respostas podem ser marcadas como **cacheáveis**; reduz latência e interações.
  4. **Interface uniforme** — restrição central, subdividida em: **identificação de recursos**; **manipulação de recursos por meio de representações**; **mensagens autodescritivas**; **HATEOAS** (*Hypermedia as the Engine of Application State*).
  5. **Sistema em camadas** — cada componente só "enxerga" a camada imediata; permite *proxies*, *gateways* e balanceadores; adiciona latência.
  6. **Code-on-demand (opcional)** — o cliente pode baixar e executar código (ex.: scripts) para estender funcionalidade.
- **Elementos de dados:** **recurso** (qualquer coisa nomeável; alvo conceitual de uma referência), **identificador de recurso** (URI/URL/URN), **representação** (bytes + metadados; ex.: HTML, JSON), **metadados** e **dados de controle** (`If-Modified-Since`, `Cache-Control`).
- **Recurso × representação:** o recurso é o conceito; o cliente troca **representações** dele. O mesmo recurso pode ter várias representações (JSON, XML — **negociação de conteúdo** via `Accept`/`Content-Type`).
- **REST na prática (uso coloquial):** serviços HTTP que expõem **recursos em URIs**, usam **verbos HTTP** com semântica e são **stateless**. A banca costuma tratar as duas coisas (estilo arquitetural × API HTTP "RESTful").
- **Richardson Maturity Model:** nível 0 (POX — um só endpoint, *tunnel*), 1 (**recursos**/URIs), 2 (**verbos HTTP** + códigos de status), 3 (**HATEOAS**/controles hipermídia).

### 7.2 Recursos, verbos, status e boas práticas

- **Recursos e URIs:** usar **substantivos** no plural (ex.: `/clientes`, `/clientes/{id}`), evitar verbos na URI. Aninhamento com critério.
- **Verbos HTTP e propriedades:**
  - **GET** — recupera; **seguro** (não altera estado) e **idempotente** (repetir tem o mesmo efeito).
  - **HEAD** — como GET, sem corpo.
  - **POST** — cria/reprocessa; **não idempotente** (em geral); não seguro.
  - **PUT** — substitui o recurso completo; **idempotente**.
  - **PATCH** — atualização **parcial**; idempotência **não garantida**.
  - **DELETE** — remove; **idempotente**.
  - **OPTIONS** — métodos suportados/*preflight* CORS.
- **Códigos de status (famílias):** **1xx** informativo; **2xx** sucesso (200 OK, **201 Created** + `Location`, 202 Accepted, 204 No Content); **3xx** redirecionamento (301, 302, 304 Not Modified); **4xx** erro do cliente (400 Bad Request, **401 Unauthorized**, **403 Forbidden**, 404 Not Found, **405 Method Not Allowed**, **409 Conflict**, 422 Unprocessable Entity, **429 Too Many Requests**); **5xx** erro do servidor (**500 Internal Server Error**, **503 Service Unavailable**, 504 Gateway Timeout).
- **Boas práticas:** usar status corretos; paginação/filtros/ordenação via *query params* (não no corpo do GET); representações em JSON; **versionamento** (URI, header ou media type — usar como **último recurso**, preferindo serviços **tolerantes** a mudanças/*Tolerant Reader*); *idempotência* (chaves de idempotência em POST quando necessário); **caching** com `ETag`/`Cache-Control`; **HATEOAS**; segurança (TLS, autenticação/autorização); limites de taxa; *timeouts*.
- **Contratos e evolução:** *Consumer-Driven Contracts*; evitar quebrar consumidores; adicionar campos é geralmente seguro; remover/renomear não.

### 7.3 Separação em camadas no Spring (apresentação / negócio / dados)

- **Três camadas (regra de dependência de cima para baixo):**
  - **Apresentação (web):** **`@RestController`/`@Controller`** + `@RequestMapping`/`@GetMapping`/`@PostMapping`/…; faz a **tradução HTTP ↔ objetos** (`@RequestBody`, `@ResponseBody`, `@PathVariable`, `@RequestParam`, `@RequestHeader`, `ResponseEntity`); **não** contém regra de negócio; delega ao serviço.
  - **Regras de negócio (serviço):** **`@Service`**; validações, cálculos, **orquestração**, **transações** (`@Transactional`); depende de repositórios por **interfaces**; não conhece HTTP.
  - **Acesso a dados (persistência):** **`@Repository`** (ou **Spring Data JPA** com interfaces `Repository`/`JpaRepository`); isola o banco; traduz exceções.
- **Injeção e dependência:** o controlador recebe o **serviço** por construtor; o serviço recebe o **repositório** por construtor. É o **Dependency Inversion Principle** aplicado — as camadas dependem de **abstrações**.
- **DTO × Entidade:** expor **DTOs** na API em vez de entidades JPA (evita vazamento do modelo de dados, problemas de *lazy loading*/serialização e acoplamento do contrato à base).
- **Tratamento de exceções:** **`@ExceptionHandler`** / **`@RestControllerAdvice`** para respostas de erro padronizadas (ex.: `ProblemDetail`/RFC 7807).
- **Validação:** Bean Validation (`@Valid`, `@NotNull`, `@Size`…) na borda, com validações de negócio no serviço.
- **Configuração:** `application.properties`/`.yml`; `@ConfigurationProperties`; perfis por ambiente.
- **Testes por camada:** unidade no domínio/serviço (mocks), `MockMvc`/`WebTestClient` na web, integração com Testcontainers no repositório.
- **Pitfall:** colocar lógica de negócio no **controlador** (viola a separação e dificulta testes); acessar o **repositório direto do controlador** (pula a camada de negócio); entidade JPA retornada crua na API.

## Detalhes que merecem destaque

- **Fowler × definição de monolito:** "monolito" **não** significa necessariamente código ruim; é só uma aplicação construída como **unidade única**. O antônimo de qualidade é o **Big Ball of Mud**, que pode ocorrer em monolito **ou** em microsserviços.
- **Componente (Fowler):** unidade de software **independentemente substituível e atualizável**. **Biblioteca** = componente **em processo** (chamada em memória); **serviço** = componente **fora de processo** (chamada remota).
- **"Smart endpoints and dumb pipes"** é uma reação ao **ESB**: colocar a inteligência nas pontas e manter o barramento simples. ESB é associado a SOA tradicional, não a microsserviços.
- **Dados descentralizados:** cada serviço **dono do seu banco**; comunicação entre serviços **só via API**, proibindo o *integration database* compartilhado (fonte de acoplamento).
- **ACID × consistência distribuída:** monolito permite transação local; microsserviços usam **consistência eventual**, **saga** e **compensações**; 2PC é desaconselhado ("2PC is not an option").
- **As "três coisas difíceis" da computação:** invalidação de cache, nomes (e *off-by-one*). Referência clássica de Fowler (*TwoHardThings*).
- **Falácias da computação distribuída** e **multiplicação de indisponibilidade** em chamadas síncronas: quanto mais serviços, maior o impacto.
- **Conway's Law (1968):** a arquitetura copia a estrutura de comunicação da organização. **Inverse Conway Maneuver:** reorganizar times para obter a arquitetura desejada.
- **Fallback de arquitetura:** "arquitetura não é binária" — monolito e microsserviços são **regiões** de um espaço arquitetural, com muitas soluções intermediárias (modular monolith, poucos serviços grosseiros).
- **Spring / IoC:** *"the process is fundamentally the inverse... of the bean itself controlling the instantiation or location of its dependencies"*. `ApplicationContext` é **superconjunto** de `BeanFactory` e é o contêiner usado na prática.
- **Injeção por construtor** permite `final` (imutabilidade) — recomendação oficial do Spring Boot.
- **`@SpringBootApplication` = `@SpringBootConfiguration` + `@EnableAutoConfiguration` + `@ComponentScan`** — decorar o "trio" (a banca adora).
- **Autoconfiguração só se aplica se as condições casarem** e **cede** ao usuário (`@ConditionalOnMissingBean`); pode ser **inspecionada** (`--debug`) e **excluída** (`exclude`/`spring.autoconfigure.exclude`).
- **Descoberta de autoconfiguração:** arquivo `META-INF/spring/org.springframework.boot.autoconfigure.AutoConfiguration.imports`. Autoconfiguração **nunca** é alvo de component scan.
- **`@ConditionalOnClass`** usa **ASM** para ler metadados, permitindo referenciar classes que **não** estão no *classpath*; na composição de meta-anotações, deve-se usar `name` (String).
- **REST de Fielding (6 restrições) × "REST" coloquial (JSON/HTTP):** a banca pode cobrar o conceito original. **Sem estado (stateless)** e **interface uniforme** são as mais cobradas; **code-on-demand é opcional**.
- **Idempotência:** GET, PUT e DELETE são **idempotentes**; POST **não**; PATCH **não garantido**. Segurança: GET/HEAD/OPTIONS são **seguros**.
- **RMM (Richardson):** nível 3 = **HATEOAS**; nível 2 = verbos/códigos; nível 1 = recursos; nível 0 = POX.
- **12-factor:** config **fora do código**, em **variáveis de ambiente**; a configuração **interna** (como beans se ligam) pertence ao código, não é "config".
- **Fronteira de contexto (DDD) ↔ fronteira de serviço:** boa correspondência ajuda a modularidade; refatorar entre serviços é **muito mais caro** que entre bibliotecas.

## Comparações que a banca costuma cobrar (certo/errado)

| Conceito A | Conceito B | Diferença-chave |
| --- | --- | --- |
| Monolito | Microsserviços | Monolito = **uma unidade implantável**/processo único; microsserviços = **vários serviços independentemente implantáveis** comunicando por rede |
| Biblioteca (componente em processo) | Serviço (componente fora de processo) | Biblioteca: ligada ao programa, chamada **em memória**; serviço: **remoto**, comunicação por web service/RPC |
| Monolito (padrão) | Big Ball of Mud | Monolito só diz que é **unidade única**; Big Ball of Mud = sistema **desestruturado**, dependências emaranhadas (pode haver em ambos os estilos) |
| Microsserviços | SOA tradicional | Microsserviços: serviços finos, dados descentralizados, *smart endpoints*; SOA tradicional: frequentemente **ESB** central e governança centralizada |
| Orquestração | Coreografia | Orquestração = **controlador central** comanda; coreografia = serviços **reagem a eventos** sem coordenador |
| Publicar-assinar (pub/sub) | Event streaming | Pub/sub: entrega a assinantes, **não durável**; streaming: **log durável e ordenado**, com **replay** |
| Event Notification | Event-Carried State Transfer | Notification: só avisa, receptor **busca** dados; State Transfer: evento **carrega** os dados, receptor mantém cópia |
| Event Sourcing | CQRS | Event Sourcing: **fonte da verdade é o log de eventos**; CQRS: **separa modelos de leitura e escrita** (não exige eventos) |
| Consistência forte (ACID) | Consistência eventual (BASE) | ACID: transação atômica/local; BASE: **disponibilidade** priorizada, estados divergem por um tempo |
| 2PC | Saga | 2PC: transação **distribuída** atômica (bloqueante, pouco usado); Saga: **sequência de transações locais** + **compensações** |
| Consistência (C) | Disponibilidade (A) — em CAP | Sob **partição (P)**, trade-off: forte consistência **ou** disponibilidade |
| Escala vertical | Escala horizontal | Vertical = **máquina maior** (*scale up*); horizontal = **mais instâncias** (*scale out*) |
| Latência | Throughput | Latência = **tempo** de uma operação; throughput = **quantidade** por unidade de tempo |
| Camada (layer) | Tier (nível físico) | Camada = **separação lógica**; tier = **separação física**/implantação |
| Inversão de Controle (IoC) | Injeção de Dependência (DI) | IoC = princípio geral de **o contêiner controlar** a criação; DI = **forma especializada** de IoC (construtor/setter/propriedades) |
| BeanFactory | ApplicationContext | ApplicationContext é **subinterface/superconjunto** de BeanFactory, com AOP, i18n, eventos e contextos web |
| `@Configuration` + `@Bean` | `@Component` + `@ComponentScan` | `@Bean` = define bean **por método**; `@Component` (+) = bean descoberto por **varredura** |
| `singleton` | `prototype` | Singleton = **uma instância** por contêiner (padrão); prototype = **nova instância** a cada solicitação |
| Autoconfiguração | Configuração do usuário | Autoconfiguração **cede** à configuração explícita do usuário (`@ConditionalOnMissingBean`); só se aplica se as **condições** casarem |
| `@ConditionalOnClass` | `@ConditionalOnMissingBean` | Por **classe no classpath** × por **ausência de bean** já definido |
| Serviço REST | Estilo REST (Fielding) | REST é um **estilo arquitetural** (6 restrições); "serviço REST" é a **implementação** HTTP/recursos |
| GET / PUT / DELETE | POST | GET/PUT/DELETE são **idempotentes**; POST em geral **não** é (idempotência de PATCH não é garantida) |
| 401 Unauthorized | 403 Forbidden | 401 = **não autenticado**; 403 = autenticado, mas **sem permissão** |
| Web layer | Service layer | Web = **tradução HTTP**/DTOs; Service = **regras de negócio**/transações |

## Pegadinhas e erros comuns

> Cuidado com termos absolutos ("sempre", "nunca", "só", "exclusivamente") e com a troca de pares de conceitos — marcas típicas da Cebraspe.

- Dizer que **monolito = código ruim**. Monolito é apenas **unidade única de implantação**; qualidade é outra coisa (o problema é o **Big Ball of Mud**).
- Afirmar que microsserviços são **sempre** mais escaláveis/baratos/rápidos. Fowler: existe o **Microservice Premium**; só se paga em **sistemas complexos**.
- Trocar **microservice × SOA**: SOA tradicional costuma usar **ESB** com inteligência no barramento; microsserviços defendem *smart endpoints and dumb pipes*.
- Dizer que microsserviços **exigem** uma linguagem única ou um **banco único compartilhado** — é o contrário: **diversidade** e **banco por serviço**.
- Confundir **coreografia** (sem coordenador) com **orquestração** (coordenador central).
- Achar que **saga** dá rollback automático. **Não dá** — exige **transações compensatórias** e sofre com **falta de isolamento** (letra "I" do ACID).
- Achar que **event sourcing** e **CQRS** são a mesma coisa. São padrões distintos (CQRS não exige eventos).
- Dizer que em CAP é possível ter **os três** (C, A, P) simultaneamente. Sob partição, escolhe-se C **ou** A.
- Confundir **latência** com **throughput**, ou **escala vertical** com **horizontal**.
- Confundir **camada** (lógica) com **tier** (físico).
- Achar que **REST é um protocolo/padrão**. REST é **estilo arquitetural**; HTTP é sua principal instância. E **HATEOAS** é nível 3 do RMM.
- Dizer que **POST é idempotente**. Não é (em geral). GET/PUT/DELETE são.
- Trocar **401** (não autenticado) por **403** (sem autorização).
- Esquecer que **code-on-demand é restrição opcional** do REST.
- Dizer que o **Spring exige XML**. O Boot favorece **configuração Java**; XML é legado (`@ImportResource`).
- Achar que **injeção por campo** é a recomendada. A recomendação é **por construtor**.
- Confundir **IoC** com **DI**: DI é uma **forma especializada** de IoC.
- Dizer que `ApplicationContext` e `BeanFactory` são iguais. `ApplicationContext` é **superconjunto**.
- Trocar as **três** anotações que `@SpringBootApplication` agrega: é `@SpringBootConfiguration` + `@EnableAutoConfiguration` + `@ComponentScan` (não é `@Configuration` + `@EnableWebMvc` etc.).
- Dizer que a **autoconfiguração sempre se aplica** ou que **não pode ser sobrescrita**. Ela é **condicional** e **não invasiva** (cede ao usuário).
- Esquecer que o **pacote "default"** (sem `package`) é **desencorajado** e faz o scan ler **todos** os JARs.
- Confundir o **escopo `singleton`** (padrão, uma instância por contêiner) com o **padrão de projeto Singleton** (uma instância por JVM/máquina).
- Dizer que **config 12-factor** inclui a configuração **interna** (como beans se ligam). Não: só o que **varia entre deploys**.
- Achar que **versionar API** é a primeira opção em microsserviços. Fowler recomenda evitar e preferir **tolerância a mudanças**.
- Dizer que a **camada de apresentação pode acessar o repositório direto**, pulando o serviço — viola a separação em camadas.
- Esquecer que **GET não deve alterar estado** (deve ser **seguro**).

## Notas atômicas relacionadas

```dataview
LIST FROM "20 - Notas"
WHERE disciplina = this.disciplina
  AND contains(tema, this.tema)
SORT file.name ASC
```

## Fontes

- https://martinfowler.com/articles/microservices.html (James Lewis & Martin Fowler — definição e características de microsserviços; monolito; Conway; SOA; dados descentralizados; design for failure)
- https://martinfowler.com/articles/microservice-trade-offs.html (Martin Fowler — trade-offs de microsserviços: fronteiras de módulo, distribuição, consistência eventual, implantação independente, complexidade operacional, diversidade tecnológica)
- https://martinfowler.com/bliki/MonolithFirst.html (Martin Fowler — estratégia "Monolith First")
- https://martinfowler.com/bliki/MicroservicePremium.html (Martin Fowler — Microservice Premium e fator complexidade)
- https://martinfowler.com/bliki/PresentationDomainDataLayering.html (Martin Fowler — camadas apresentação–domínio–dados; camada × tier; anti-padrão de times por camada)
- https://martinfowler.com/articles/201701-event-driven.html (Martin Fowler — Event Notification, Event-Carried State Transfer, Event Sourcing e CQRS)
- https://martinfowler.com/bliki/CQRS.html (Martin Fowler — CQRS: quando usar e riscos)
- https://microservices.io/patterns/data/event-driven-architecture.html (Chris Richardson — Event-driven architecture e consistência entre serviços)
- https://microservices.io/patterns/data/saga.html (Chris Richardson — padrão Saga: coreografia, orquestração, compensações, falta de isolamento)
- https://learn.microsoft.com/en-us/azure/architecture/guide/architecture-styles/ (Microsoft Azure Architecture Center — estilos de arquitetura, restrições e tabela de gerenciamento de dependências por domínio)
- https://learn.microsoft.com/en-us/azure/architecture/guide/architecture-styles/event-driven (Microsoft Azure — EDA: topologias broker e mediator, pub/sub × streaming, desafios, correlation ID)
- https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm (Roy T. Fielding, 2000 — REST: restrições, recursos, representações, conectores)
- https://alistair.cockburn.us/hexagonal-architecture/ (Alistair Cockburn — Hexagonal / Ports & Adapters; DIP)
- https://docs.spring.io/spring-framework/reference/core/beans/introduction.html (Spring Framework — introdução ao contêiner IoC, definição de DI, BeanFactory × ApplicationContext, beans)
- https://docs.spring.io/spring-framework/reference/core/beans.html (Spring Framework — capítulo do contêiner IoC)
- https://docs.spring.io/spring-boot/reference/using/structuring-your-code.html (Spring Boot — organização do código, pacote default, classe principal, Spring Modulith)
- https://docs.spring.io/spring-boot/reference/using/spring-beans-and-dependency-injection.html (Spring Boot — beans, injeção por construtor, estereótipos, @ComponentScan)
- https://docs.spring.io/spring-boot/reference/using/auto-configuration.html (Spring Boot — autoconfiguração, substituição, exclusão, --debug)
- https://docs.spring.io/spring-boot/reference/using/using-the-springbootapplication-annotation.html (Spring Boot — @SpringBootApplication e suas três anotações)
- https://docs.spring.io/spring-boot/reference/using/configuration-classes.html (Spring Boot — classes de configuração, @Import, @ImportResource)
- https://docs.spring.io/spring-boot/reference/features/developing-auto-configuration.html (Spring Boot — criar autoconfiguração, @AutoConfiguration, condições, imports file, ordenação)
- https://docs.spring.io/spring-modulith/reference/index.html (Spring Modulith — aplicações modulares domain-driven sobre Spring Boot)
- https://12factor.net/config (The Twelve-Factor App — Fator III: Config em variáveis de ambiente)
- https://aws.amazon.com/pt/compare/the-difference-between-monolithic-and-microservices-architecture (AWS — comparação monolito × microsserviços, quando usar cada um)
