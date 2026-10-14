---
tipo: resumo
disciplina: "Arquitetura e Integração de Sistemas"
tema: "Comunicação e consistência"
status: estudando
data: "2026-10-14"
tags: [resumo, arquitetura, cgu-2026]
---

# Resumo: Comunicação e consistência

> [!info] MOC: [[Arquitetura e Integração de Sistemas]]
> Edital nº 1/2026 – CGU – AFFC · **Conhecimentos específicos** · Cargo 4 (TI / Desenvolvimento de Sistemas) · Item 3 — *Comunicação e consistência*.

## Escopo no edital (checklist)

- [x] 3.1 Mensageria, eventos e persistência.
- [x] 3.2 Falhas, repetição de requisições, idempotência e consistência.
- [x] 3.3 Integração entre sistemas e coordenação de operações.
- [x] 3.4 Evolução de contratos e migração de esquemas.

## Resumo

**Comunicação e consistência** trata de como sistemas trocam informação e como mantêm dados coerentes quando não existe uma única transação ACID sobre uma única base. O fio condutor é:

1. **Mensageria, eventos e persistência (3.1)** — a comunicação assíncrona por mensagens/eventos e a forma de persistir estado e eventos. Distinguem-se estilos síncronos (RPC/REST, acoplamento temporal) de assíncronos (mensageria, desacoplamento, buffer). Padrões de evento (notificação, transferência de estado, *event sourcing*, CQRS) e de persistência distribuída (*transactional outbox*, CDC, banco por serviço).
2. **Falhas, repetição, idempotência e consistência (3.2)** — em rede qualquer chamada pode falhar ou ser entregue duas vezes; logo, toda operação retentável precisa ser **idempotente**. Garantias de entrega (*at-most-once*, *at-least-once*, *exactly-once*) e como obter o **efeito** exatamente-uma-vez com chaves de idempotência. Modelos de consistência (forte × eventual), CAP/PACELC, ACID × BASE e padrões de resiliência (retry, *circuit breaker*, *bulkhead*, DLQ).
3. **Integração entre sistemas e coordenação de operações (3.3)** — como compor operações que atravessam serviços: **2PC/XA** (bloqueante e pouco escalável) versus **Saga** (transações locais + compensações), em **coreografia** ou **orquestração**; padrões de integração (Hohpe/Woolf) e coordenação (process manager, consensus, locks).
4. **Evolução de contratos e migração de esquemas (3.4)** — mudar interfaces, APIs e schemas sem quebrar consumidores: compatibilidade *backward/forward/full/transitive*, *schema registry*, versionamento de API, *consumer-driven contracts*, *tolerant reader* e o padrão *expand–contract* (*parallel change*).

O tema é uma variação do problema central de sistemas distribuídos: **não há transação única nem entrega garantida de forma absoluta**; a solução é compor padrões (mensageria confiável + idempotência + compensação + evolução compatível) e assumir **consistência eventual** onde antes havia atomicidade.

## 1. Mensageria, eventos e persistência

### 1.1 Estilos de integração

Hohpe e Woolf (*Enterprise Integration Patterns*, 2003) catalogam quatro estilos clássicos de integração:

- **Transferência de arquivos (File Transfer):** sistemas trocam arquivos; baixo acoplamento, mas lento e sem sincronia.
- **Banco de dados compartilhado (Shared Database):** todos acessam o mesmo esquema; simples, porém forte acoplamento e acoplamento de esquema (anti-padrão em microsserviços).
- **Invocação remota de procedimentos (RPC/REST/gRPC):** chamada síncrona; acoplamento **temporal** (ambos precisam estar no ar ao mesmo tempo).
- **Mensageria (Messaging):** comunicação assíncrona por mensagens; maior desacoplamento e resiliência.

**Comunicação síncrona** (request/response): o chamador **bloqueia** aguardando a resposta; latência somada, falha em cascata, acoplamento temporal. **Comunicação assíncrona**: o emissor publica e segue; o broker faz o *buffer*. Prós: desacoplamento, absorção de picos, resiliência a indisponibilidade do consumidor. Contras: **consistência eventual**, maior complexidade de rastreamento, duplicatas, ordenação.

### 1.2 Mensageria: conceitos e componentes

- **Message Channel:** canal por onde as mensagens trafegam.
  - **Point-to-Point Channel (fila):** cada mensagem é consumida por **um** consumidor. Vários consumidores formam **Competing Consumers** (balanceamento de carga e escalabilidade horizontal).
  - **Publish-Subscribe Channel (tópico):** a mensagem é entregue a **todos** os assinantes (fan-out). Assinantes duráveis (*durable subscriber*) recebem mesmo offline.
- **Message:** cabeçalho (metadados: roteamento, correlação) + corpo (payload). Tipos: **Command Message** (instrui a fazer algo), **Document Message** (transfere dados), **Event Message** (notifica que algo aconteceu).
- **Message Broker:** intermediário que roteia, entrega e pode persistir mensagens. **Message Bus:** backbone comum de integração.
- **Message Endpoint / Messaging Gateway:** como o app se conecta ao canal. Consumo **event-driven** (callback) ou **polling**.
- **Message Router / Content-Based Router / Message Filter / Recipient List:** roteamento e seleção por conteúdo.
- **Message Translator / Normalizer / Canonical Data Model:** tradução de formatos; o *canonical data model* reduz o número de tradutores (N×(N−1) → 2N).
- **Dead Letter Channel (DLQ):** canal para mensagens que não puderam ser processadas (venenosas, *poison messages*). **Invalid Message Channel** para mensagens inválidas.
- **Guaranteed Delivery:** persistência de mensagens no broker para não perdê-las em queda.
- **Correlation Identifier:** associa resposta a requisição (Request-Reply assíncrono). Não confundir com chave de idempotência.
- **Message Sequence / Resequencer:** ordenar mensagens. **Message Expiration**: descarte por tempo (TTL). **Format Indicator**: indica o formato do payload.
- **Transactional Client**: o produtor participa de transação para enviar de forma confiável.

### 1.3 Filas (queue-based) × logs (log-based)

Duas famílias de brokers:

| Aspecto | **Queue-based (ex.: RabbitMQ)** | **Log-based (ex.: Apache Kafka)** |
| --- | --- | --- |
| Modelo | Fila; mensagem **removida após ack** | Log *append-only*; mensagem **retida** por tempo/tamanho |
| Roteamento | "Broker inteligente": exchanges (direct, topic, fanout, headers), bindings, routing keys | "Pipe burro": consomem por tópico/partição |
| Replay/consumo repetido | Não (consumido = removido), salvo requeue/DLQ | **Sim**: offset permite reler do início |
| Ordenação | Por fila | **Por partição** (não global) |
| Escalabilidade | Boa | Muito alta (partições + grupos de consumidores) |
| Uso típico | Tarefas, RPC assíncrono, roteamento flexível | Streaming, event sourcing, log de eventos, replay |

- **Kafka:** *topics* divididos em **partições**; cada partição é um log ordenado; consumidores organizam-se em **consumer groups** e cada partição é atribuída a um consumidor do grupo; o progresso é o **offset**. A mensagem **não é apagada ao ser consumida** (retenção por tempo/tamanho) — isso permite **replay**, *event sourcing* e múltiplos consumidores independentes.
- **RabbitMQ:** a mensagem é removida após **ack**; usa **nack/requeue**, **prefetch (QoS)**, **dead-letter exchange (DLX)**; exchanges roteiam por *routing key*/*binding*. Bom para roteamento complexo e baixa latência.

### 1.4 Garantias de entrega

- **At-most-once (no máximo uma vez):** não reenvia; **pode perder** mensagem. Ex.: `acks=0`, dispara e esquece.
- **At-least-once (no mínimo uma vez):** reenvia em falha; **pode duplicar**. É a garantia **típica** de brokers com ack.
- **Exactly-once (exatamente uma vez):** sem perda e sem duplicata. Do ponto de vista de **transporte**, é **impossível** de garantir de forma absoluta (problema dos dois generais / *two generals*). O que se obtém na prática é **efeito exatamente-uma-vez** combinando entrega *at-least-once* + **consumidor idempotente**.

**Kafka e EOS (exactly-once semantics):**
- **Produtor idempotente** (`enable.idempotence=true`, padrão desde Kafka 3.0): o broker atribui **Producer ID (PID)** + **número de sequência** por lote/partição; reenvios do mesmo lote são **deduplicados** pelo broker. Garante exatamente-uma-vez **por partição** e **por sessão** do produtor.
- **Produtor transacional** (`transactional.id`): escreve **atomicamente** em várias partições/tópicos; o `transactional.id` identifica a sessão lógica, com **epoch** para *fencing* de produtores zumbis. O ciclo é `initTransactions()` → `beginTransaction()` → `send()` → `commitTransaction()`/`abortTransaction()`.
- **Read-process-write:** `sendOffsetsToTransaction()` grava os **offsets do consumidor** na mesma transação das escrita de saída; consumidores com `isolation.level=read_committed` só leem transações confirmadas (ignoram abortadas).
- **Kafka Streams:** `processing.guarantee=exactly_once_v2`. Custo: **mais latência e menor throughput** que *at-least-once*.
- EOS cobre **Kafka → Kafka**; escritas em **sistemas externos** exigem cooperação do destino ou idempotência.

### 1.5 Padrões orientados a eventos (Martin Fowler)

Fowler separa quatro significados de "event-driven":

1. **Event Notification (notificação de evento):** envia um evento avisando que algo mudou, **sem** carregar o estado. Baixo acoplamento e simples; o consumidor precisa voltar à fonte para obter dados. Problema: o **fluxo lógico** fica implícito e difícil de depurar.
2. **Event-Carried State Transfer:** o evento **carrega o estado** necessário. Consumidores mantêm **cópias locais**, ganhando **disponibilidade** e **latência** (não chamam a fonte). Custo: **duplicação de dados** e **consistência eventual**.
3. **Event Sourcing:** todas as mudanças de estado são gravadas como uma **sequência de eventos** (o **event log** é a **fonte da verdade**; o estado é **derivado**). Permite *rebuild* completo, *temporal query* (ver o estado no passado), *replay*, correção por eventos retroativos e **snapshots** para desempenho. Cuidados: evolução de schema dos eventos, efeitos colaterais externos no replay (usar *gateways* que suprimem envios), ordenação e identificadores estáveis.
4. **CQRS (Command Query Responsibility Segregation):** usar **modelos diferentes** para **escrita (command)** e **leitura (query)**; escalar leitura e escrita independentemente, frequentemente com *read models*/projeções atualizadas por eventos (**consistência eventual**). Fowler alerta: **não** usar em todo o sistema e só onde há ganho real — é complexo.

> **Comando × evento:** um **comando** expressa **intenção** e é endereçado a um destinatário; um **evento** expressa **fato ocorrido** e é **publicado** (broadcast) a quem interessar. Confundir os dois leva a acoplamento indevido.

### 1.6 Persistência: banco por serviço, outbox e CDC

- **Banco por serviço (Database per Service):** cada serviço possui seu banco; elimina acoplamento por esquema, mas cria o problema de **consistência entre serviços** (base do padrão Saga).
- **Dual write problem:** salvar no banco **e** publicar no broker são **duas** operações (dois sistemas) — não são atômicas. Se o banco commita e o broker falha (ou o processo cai no meio), **o evento se perde** e o fluxo trava; ou publica sem persistir.
  - **Transactional Outbox:** o serviço grava a mensagem em uma **tabela outbox** **na mesma transação local** que atualiza as entidades. Um **message relay** separado lê a outbox e publica no broker. Assim, "publicar" fica condicionado ao commit. O relay é **at-least-once** → o consumidor precisa ser **idempotente**.
  - Implementações do relay: **Polling Publisher** (consulta a tabela) e **Transaction Log Tailing** (ler o *transaction log* do banco = **CDC**, ex.: **Debezium**).
  - **Inbox / Idempotent Consumer:** o consumidor registra IDs de mensagens já processadas e ignora duplicatas.
- **Change Data Capture (CDC):** captura **mudanças de linhas** no log transacional do banco e as transmite. Diferente de **event sourcing**: o CDC registra **o que mudou no banco** (estado), enquanto o event sourcing registra **eventos de domínio** (intenção/semântica de negócio). CDC é útil para replicação, read models e para o *relay* da outbox.
- **Projeções / read models / materialized views / persistência poliglota:** derivar views otimizadas para leitura a partir de eventos; aceitam consistência eventual.

## 2. Falhas, repetição de requisições, idempotência e consistência

### 2.1 Tipos de falha em sistemas distribuídos

- **Falha de rede:** timeouts, mensagens perdidas, partições (o *split-brain*).
- **Crashes de processo/nó:** a operação pode ter sido aplicada e a resposta perdida.
- **Falha parcial:** parte do sistema funciona e parte não; o chamador **não sabe** se a operação ocorreu.
- **Duplicatas:** por *retry* do produtor ou reentrega do broker.
- **Ordem:** mensagens podem chegar fora de ordem (garantia de ordem só **por partição**/fila).
- **Problema dos dois generais / two generals:** é **impossível**, por troca de mensagens sobre canal não confiável, garantir acordo e entrega *exactly-once* absoluta — daí a necessidade de idempotência e de aceitar eventual consistência.

### 2.2 Retry (repetição de requisições)

- Repetir é necessário porque falhas transitórias são comuns — mas o *retry* **cria duplicatas** se a primeira tentativa foi aplicada.
- Regras: repetir apenas **erros transitórios** (timeout, 5xx, conexão); **não** repetir erros permanentes (4xx de validação, autorização).
- **Exponential backoff + jitter:** esperar de forma crescente e aleatória para evitar **retry storm** / **thundering herd** (todos repetindo ao mesmo tempo).
- **Retry budget / limite** de tentativas e **timeouts**.
- Toda operação retentável **deve ser idempotente** — caso contrário, repetir duplica efeitos (cobrança em dobro).

### 2.3 Idempotência

- **Definição:** operação **idempotente** produz o **mesmo resultado** se executada uma ou várias vezes: `f(x) = f(f(x))`. Não significa "executar uma vez", e sim que **repetir não altera** o estado final.
- **Métodos HTTP:** `GET`, `HEAD`, `PUT`, `DELETE` são **idempotentes** (por definição). `POST` **não** é (cada envio pode criar recurso). `PATCH` **não** é necessariamente. `GET/HEAD` também são **seguros** (não alteram estado).
- **Como implementar:**
  - **Chave de idempotência** (*idempotency key*): o cliente envia um identificador único (ex.: cabeçalho `Idempotency-Key`, como no Stripe). O servidor **armazena** o resultado por chave e, em repetição, devolve o **mesmo resultado** sem reprocessar.
  - **Deduplicação explícita** (guardar IDs processados / tabela *inbox*) ou **semântica idempotente** (operações naturalmente idempotentes, ex.: `SET status = X`, *upsert*, restrição de unicidade).
  - **Idempotent Receiver** (EIP): "projete o receptor para receber a mesma mensagem com segurança"; alcançado por (1) *de-duping* explícito ou (2) semântica idempotente.
- **Padrão central:** *at-least-once* **+ idempotência = efeito exatamente-uma-vez**.

### 2.4 Modelos de consistência

- **ACID** (transação local): Atomicidade, Consistência, Isolamento, Durabilidade.
- **BASE** (típico de sistemas distribuídos/NoSQL): *Basically Available*, *Soft state*, *Eventual consistency*.
- **Consistência forte:** toda leitura enxerga a escrita mais recente (exige coordenação; maior latência).
- **Consistência eventual:** as réplicas convergem **com o tempo**, se cessarem as escritas. Modelos intermediários: *read-your-writes*, *monotonic reads*, *causal consistency*.
- **C do ACID ≠ C do CAP:** no ACID, "consistência" = **integridade de restrições/invariantes**; no CAP, "consistência" = *linearizability* (cada leitura vê a última escrita).
- **Teorema CAP (Brewer):** sob **partição de rede (P)**, um sistema distribuído escolhe entre **consistência (C)** e **disponibilidade (A)**. Como partições são inevitáveis, sistemas reais são **CP** ou **AP**. Não significa "escolher 2 de 3 sempre".
- **PACELC:** **se** há partição (P), escolhe-se A × C; **senão** (E), escolhe-se **latência (L) × consistência (C)** — cobre o trade-off mesmo sem partição.

### 2.5 Padrões de resiliência (Cloud Design Patterns)

- **Retry** (com backoff) e **Circuit Breaker** (abre após falhas, evita cascata; estados fechado → aberto → meio-aberto).
- **Bulkhead** (isolar recursos por compartimento, evitar falha total), **Timeout**, **Throttling** (limitar taxa).
- **Queue-Based Load Leveling** (fila absorve picos), **Competing Consumers** (escala consumidores).
- **Dead Letter Queue / Dead Letter Channel** (mensagens não processáveis vão para DLQ para análise).
- **Compensating Transaction** (desfazer efeitos já confirmados — base da Saga).
- **Health Endpoint Monitoring**, **Leader Election**.
- **Cache-Aside**, **Materialized View** (leitura).

## 3. Integração entre sistemas e coordenação de operações

### 3.1 Compondo operações entre serviços

Em **banco por serviço**, uma regra de negócio pode atravessar vários bancos e **não** há transação ACID única. Opções:

- **Two-Phase Commit (2PC/XA):**
  - **Fase 1 (prepare/vote):** o coordenador pede a cada participante que prepare e vote. Os recursos ficam **bloqueados**.
  - **Fase 2 (commit/rollback):** se todos votam "sim", confirma; se algum vota "não", aborta em todos.
  - Problemas: é **bloqueante** (locks mantidos), o **coordenador é ponto único de falha** (cai → participantes ficam bloqueados/incertos), **não escala** e muitos bancos NoSQL/cloud **não** suportam XA. Por isso, **não** é adequado a microsserviços.
- **Saga (Garcia-Molina & Salem, 1987):** decompõe a transação longa em uma **sequência de transações locais** `T1..Tn`, cada uma **commitada imediatamente** em seu serviço. Se `Ti` falha (violação de regra), executa-se a **cadeia de transações compensatórias** `C(i-1)..C1` para desfazer **semanticamente** o que foi feito.
  - **Compensação ≠ rollback:** `T` já foi commitada e visível; desfazer é uma **nova** transação com efeito oposto (ex.: `charge` → `refund`, que fica no extrato). Ações **não compensáveis** (enviar e-mail) devem ficar **depois do pivot**.
  - Categorias de passos: **compensável** (pode ser desfeito), **pivot** (ponto de não retorno) e **retentável** (após o pivot, garante-se concluir).
  - **Não há isolamento (falta o "I" do ACID):** estados intermediários são visíveis → anomalias (*dirty reads*, *lost updates*). Contramedidas de isolamento: **semantic lock** (ex.: pedido em `PENDING` age como trava), **commutative updates**, **pessimistic view**, **reread value**, **version files**.
  - Requisitos: passos e compensações **idempotentes**; compensar em **ordem inversa**; estado do saga **durável**; se a compensação falhar, *retry with backoff* → escalar para intervenção humana (incidente operacional).
  - **Saga × consenso:** saga resolve **fluxo longo com compensação semântica** (abdica de isolamento); **consensus** (Raft/Paxos/etcd) resolve **ordem global sobre um estado único**. São coisas diferentes e podem coexistir.
- **TCC (Try-Confirm-Cancel):** meio-termo; *Try* reserva recursos, *Confirm* efetiva, *Cancel* libera. Explicita a reserva.
- **API Composition:** para **leituras**, um agregador consulta vários serviços e compõe a resposta (não é transação).

### 3.2 Coreografia × orquestração (coordenação de sagas)

- **Coreografia (choreography):** **não** há controlador central; cada serviço publica/consome **eventos** e reage.
  - Prós: baixo acoplamento, sem ponto único de falha, bom para fluxos **simples (2–4 passos)**.
  - Contras: a lógica fica **espalhada** e implícita; **difícil depurar/observar** ("onde travou?"); risco de dependência cíclica; testes de integração difíceis; resiliência global (timeouts/retries) mais difícil.
- **Orquestração (orchestration):** um **orquestrador** (máquina de estados) central comanda os participantes e dispara compensações.
  - Prós: lógica em **um só lugar**, estado explícito e consultável, melhor observabilidade, fácil adicionar passos, sem ciclos, compensação **mais rápida e determinística**.
  - Contras: orquestrador vira **ponto de falha** e hub de acoplamento; risco de virar "monólito distribuído"; toda etapa passa por ele.
- **Regra prática:** **coreografia** para fluxos simples e times/autonomia; **orquestração** para fluxos complexos (branching, compensações condicionais, visibilidade). Muitos sistemas reais são **híbridos**.
- Ferramentas/engines: **Temporal, Camunda/Zeebe, AWS Step Functions, Azure Durable Functions, Axon, Eventuate**.
- **Confiabilidade end-to-end:** Saga **depende** de (a) **transactional outbox + CDC** (o evento não se perde) e (b) **idempotência** (duplicata não faz mal). Sem esse par, ou o saga trava, ou um passo roda duas vezes.
- **Cliente síncrono sobre fluxo assíncrono:** responder só ao fim do saga, **polling** (`GET /orders/{id}`) ou **webhook/websocket**.
- **Padrões de coordenação (EIP):** **Process Manager** (roteia passos de um processo longo), **Routing Slip** (lista de passos), **Scatter-Gather** (dispara e agrega), **Aggregator** (combina respostas), **Splitter** (divide).

## 4. Evolução de contratos e migração de esquemas

### 4.1 Contratos e suas formas de mudança

Um **contrato** é a interface observável: assinatura de API (REST/gRPC), campos de payload, schema de mensagens ou esquema de tabela. Mudanças podem ser:

- **Backward-compatible (compatível com versões anteriores):** consumidores **novos** conseguem ler dados **antigos**.
- **Backward-incompatible (quebra):** exige versionamento ou migração coordenada.

### 4.2 Compatibilidade de schema (Avro/Protobuf/JSON Schema)

Tipos de compatibilidade (**padrão do Confluent Schema Registry = BACKWARD**):

- **BACKWARD:** o consumidor com o **novo** schema lê dados escritos com o schema **anterior**. Típico: **adicionar campo opcional/com default**, **remover** campo.
- **FORWARD:** o consumidor com o schema **antigo** lê dados escritos com o **novo** schema. Típico: **adicionar** campo, **remover campo opcional**.
- **FULL:** **ambos** (adicionar/remover apenas campos opcionais/com default).
- **TRANSITIVE:** verifica compatibilidade contra **todas** as versões anteriores, não só a última. Variantes: `BACKWARD_TRANSITIVE`, `FORWARD_TRANSITIVE`, `FULL_TRANSITIVE`.
- **NONE:** sem verificação (quebra permitida) — exige migrar produtores e consumidores juntos ou criar novo tópico.

**Ordem de upgrade dos clientes conforme a compatibilidade:**
- `BACKWARD`: **atualizar consumidores primeiro**, depois produtores.
- `FORWARD`: **atualizar produtores primeiro**, depois consumidores.
- `FULL`: pode atualizar **independentemente**.

**Regras práticas (Avro, exemplo):** adicionar campo **com default** é backward e também forward; adicionar campo **obrigatório** sem default **quebra** backward; tornar obrigatório um campo que era opcional tende a quebrar. Para campos opcionais, usar **union com `null`** (`["null","string"]`). `Schema Registry` valida a compatibilidade na **registro** da nova versão e associa um **ID** a cada schema. Formatos suportados: **Avro** (nascido com evolução de schema em mente), **Protobuf**, **JSON Schema**. Nota: **Kafka Streams** só suporta `BACKWARD`/`FULL`/`BACKWARD_TRANSITIVE`.

### 4.3 Evolução de contratos de API

- **Semantic Versioning (SemVer):** `MAJOR.MINOR.PATCH`; mudança incompatível → MAJOR.
- **Estratégias de versionamento REST:**
  - **URI path** (`/v1/pedidos`) — a mais comum e explícita.
  - **Query parameter** (`?version=1`).
  - **Header customizado** (`X-API-Version: 1`).
  - **Media type (content negotiation)**: `Accept: application/vnd.exemplo.v1+json`.
- **Deprecação:** documentar, avisar, usar cabeçalhos como `Deprecation` e `Sunset`, período de coexistência de versões.
- **Postel's Law / Robustness Principle:** "seja **conservador** no que envia, **liberal** no que aceita". Combina com o **Tolerant Reader** (ignorar campos desconhecidos em vez de falhar).
- **Consumer-Driven Contracts (CDC):** são os **consumidores** que definem o contrato esperado; testes de contrato (ex.: **Pact**) verificam que o provedor continua atendendo. Ajuda a evoluir serviços de forma independente.
- **Evolução vs versionamento:** prefira mudanças **compatíveis** (adicionar campos, não remover/renomear); verse apenas quando a mudança quebra.

### 4.4 Expand–Contract / Parallel Change (Fowler, Danilo Sato)

Padrão para fazer mudança **incompatível** com segurança, em **três fases**:

1. **Expand (expandir):** introduza o **novo** ao lado do **antigo** (novo campo/método/endpoint), mantendo ambos.
2. **Migrate (migrar):** migre **incrementalmente** todos os consumidores/escritas para o novo (pode ser a fase mais longa; usar *feature flags*).
3. **Contract (contrair):** remova o **antigo** e padronize o novo.

Aplicações: refatoração de interfaces, **refatoração de banco de dados** (base do *evolutionary database design*), *deployments* (**blue-green**, **canary**), evolução de **APIs remotas**. Sem a fase de *contract*, o sistema fica **pior** que no início (dois caminhos mantidos) — exige **disciplina**.

### 4.5 Migração de esquemas de banco

- **Evolutionary Database Design:** toda mudança é uma **migração** versionada e automatizada; o esquema evolui junto com o código.
- Padrão **expand–contract** para colunas/tabelas: adicionar a nova coluna, migrar/backfill (preencher), manter compatibilidade durante a transição, só então remover a antiga.
- **Backfill** de dados em lotes; evitar *locks* longos; considerar *blue-green* de banco.
- **Migração de esquemas de eventos:** mais delicada (eventos antigos persistem no log). Estratégias: adicionar campos **opcionais**, **versionar** o evento, **upcasting** (converter eventos antigos para a forma nova na leitura/consumo), evitando reescrever o passado. Greg Young: **não** colocar lógica de negócio entre o evento e a representação de estado.
- **CDC** ajuda a manter *read models* atualizados durante migrações.

## Detalhes que merecem destaque

- **Saga é de 1987** (Garcia-Molina & Salem), **antes** dos microsserviços; não foi "inventada" para microsserviços.
- **2PC é bloqueante e CP** (mantém *locks*, coordenador é ponto único de falha); **Saga é AP/eventual** e não mantém locks entre passos.
- **Exactly-once delivery absoluto não existe**; existe **efeito** exactly-once via *at-least-once* + **idempotência**.
- **Idempotência ≠ executar uma vez:** é "repetir não muda o estado final".
- **Outbox resolve *dual write*** e garante *at-least-once*; **não** elimina duplicatas — por isso o consumidor deve ser idempotente.
- **Fila ≠ tópico:** fila (*point-to-point*) entrega a **um** consumidor; tópico (*publish-subscribe*) a **todos**.
- **Kafka retém** mensagens e permite **replay**; **RabbitMQ remove após ack**.
- **Ordem no Kafka é por partição**, não global.
- **Backward** = consumidor novo lê dado antigo; **Forward** = consumidor antigo lê dado novo. Padrão do Confluent = **BACKWARD** (não transitivo).
- **Ordem de upgrade:** *backward* → consumidores primeiro; *forward* → produtores primeiro; *full* → independente.
- **C do ACID ≠ C do CAP**.
- **Compensação não é rollback** — deixa rastro (refund fica no extrato).
- **Semantic lock** é a contramedida à falta de isolamento do Saga.
- **CDC vs Event Sourcing:** CDC lê o log do banco (estado); event sourcing grava eventos de domínio (intenção).
- **Correlation ID ≠ Idempotency Key:** o primeiro liga resposta a requisição; o segundo evita efeito duplicado.
- **Idempotent Receiver** (EIP) e **Idempotent Consumer** (microservices.io) são o mesmo conceito em vocabulários diferentes.

## Comparações que a banca costuma cobrar (certo/errado)

| Conceito A | Conceito B | Diferença-chave |
| --- | --- | --- |
| At-least-once | Exactly-once | At-least-once **pode duplicar**; exactly-once (efeito) exige **idempotência** — entrega exata absoluta é impossível |
| Fila (point-to-point) | Tópico (publish-subscribe) | Fila: **um** consumidor; tópico: **todos** os assinantes |
| Queue-based (RabbitMQ) | Log-based (Kafka) | RabbitMQ **remove após ack**; Kafka **retém** e permite **replay** por offset |
| Coreografia | Orquestração | Coreografia: **sem controlador**, eventos, difícil observar; orquestração: **controlador central**, estado explícito |
| 2PC/XA | Saga | 2PC **bloqueia** e usa coordenador (CP); Saga usa **transações locais + compensações** (eventual) |
| Compensação | Rollback | Rollback restaura o estado anterior; compensação é **nova transação** que desfaz semanticamente (deixa rastro) |
| ACID | BASE | ACID: atomicidade/isolamento fortes; BASE: disponibilidade + **consistência eventual** |
| Consistência (ACID) | Consistência (CAP) | ACID: **invariantes/integridade**; CAP: **linearizability** (ler a última escrita) |
| CAP | PACELC | CAP só fala de **partição**; PACELC acrescenta o trade-off **latência × consistência** fora da partição |
| Outbox | 2PC | Outbox evita transação distribuída gravando a mensagem **na mesma transação local** |
| Event Notification | Event-Carried State Transfer | Notification **não** carrega estado (consumidor consulta a fonte); state transfer **carrega** o estado (cópias locais) |
| Event Sourcing | CDC | Event sourcing grava **eventos de domínio**; CDC captura **mudanças de linhas** do banco |
| Backward compatible | Forward compatible | Backward: consumidor **novo** lê dado **antigo**; forward: consumidor **antigo** lê dado **novo** |
| Tolerant Reader | Consumer-Driven Contracts | Tolerant Reader: ignorar campos desconhecidos; CDC: **contrato definido pelo consumidor** e testado |
| Versionamento por URI | Por media type | URI: versão explícita no caminho; media type: negociação via `Accept` |
| Retry | Circuit Breaker | Retry repete a chamada; circuit breaker **interrompe** chamadas ao detectar falhas (evita cascata) |
| Idempotency Key | Correlation ID | Chave de idempotência evita **efeito duplicado**; correlation ID liga **resposta à requisição** |

## Pegadinhas e erros comuns

> Desconfie de termos absolutos ("sempre", "nunca", "garante exatamente uma vez") — são o alvo preferido do Cebraspe.

- Dizer que o **Kafka apaga a mensagem após o consumo** — ele **retém** por política de retenção e permite *replay*.
- Afirmar que existe **exactly-once delivery** absoluto — o que existe é **efeito** exactly-once com idempotência.
- Confundir **idempotência** com "executar uma única vez" — é repetir sem alterar o resultado.
- Achar que **at-least-once** garante **ordem global** — a ordem é **por partição/fila**.
- Tratar **Saga como rollback** — compensação é transação **nova** e semântica.
- Trocar **coreografia** e **orquestração** (quem tem controlador central?).
- Achar que **2PC/XA** é a solução padrão em microsserviços — é **bloqueante** e pouco suportado.
- Confundir **backward** com **forward** na compatibilidade de schema.
- Achar que **outbox** elimina duplicatas — não; exige consumidor **idempotente**.
- Trocar a **ordem de upgrade**: *backward* → consumidores antes; *forward* → produtores antes.
- Afirmar que **banco compartilhado** é a melhor integração em microsserviços — gera forte acoplamento (padrão é **banco por serviço**).
- Dizer que o **CAP** obriga a "escolher 2 de 3" sempre — o trade-off só se aplica **durante partições**.
- Confundir o **C do ACID** com o **C do CAP**.
- Achar que **CQRS** deve ser usado em **todo** o sistema — Fowler recomenda **cautela** e uso pontual.
- Achar que **event notification** entrega todos os dados — ele **não** carrega o estado.
- Confundir **event sourcing** com **CDC**.
- Esquecer que **Passos não compensáveis** (e-mail) devem vir **depois do pivot**.
- Achar que **retry** sempre resolve — sem **backoff/jitter** e **idempotência**, agrava o problema (retry storm).
- Confundir **durable subscriber** (tópico) com **competing consumers** (fila).
- Supor que **exatamente-uma-vez** dispensa de-duplicação no consumidor — rebalanceamentos ainda podem gerar duplicatas.

## Notas atômicas relacionadas

```dataview
LIST FROM "20 - Notas"
WHERE disciplina = this.disciplina
  AND contains(tema, this.tema)
SORT file.name ASC
```

## Fontes

- https://martinfowler.com/articles/201701-event-driven.html (Fowler — Event Notification, Event-Carried State Transfer, Event Sourcing, CQRS)
- https://martinfowler.com/eaaDev/EventSourcing.html (Fowler — Event Sourcing: rebuild, temporal query, replay)
- https://martinfowler.com/bliki/CQRS.html (Fowler — CQRS)
- https://martinfowler.com/bliki/ParallelChange.html (Danilo Sato/Fowler — Parallel Change / expand-contract)
- https://martinfowler.com/articles/evodb.html (Fowler — Evolutionary Database Design)
- https://martinfowler.com/articles/consumerDrivenContracts.html (Fowler — Consumer-Driven Contracts)
- https://martinfowler.com/articles/microservices.html (Fowler/Lewis — microsserviços, Tolerant Reader, contratos)
- https://microservices.io/patterns/data/saga.html (Chris Richardson — Saga)
- https://microservices.io/patterns/data/transactional-outbox.html (Chris Richardson — Transactional Outbox)
- https://learn.microsoft.com/en-us/azure/architecture/patterns/saga (Azure Architecture Center — Saga, coreografia × orquestração, compensações)
- https://docs.aws.amazon.com/prescriptive-guidance/latest/cloud-design-patterns/saga-choreography.html (AWS — Saga Choreography, outbox, idempotência)
- https://www.enterpriseintegrationpatterns.com/patterns/messaging/IdempotentReceiver.html (Hohpe/Woolf — Idempotent Receiver)
- https://www.enterpriseintegrationpatterns.com/patterns/messaging/GuaranteedMessaging.html (Hohpe/Woolf — Guaranteed Delivery)
- https://www.enterpriseintegrationpatterns.com/patterns/messaging/TransactionalClient.html (Hohpe/Woolf — Transactional Client)
- https://www.enterpriseintegrationpatterns.com/patterns/messaging/DeadLetterChannel.html (Hohpe/Woolf — Dead Letter Channel)
- https://en.wikipedia.org/wiki/Enterprise_Integration_Patterns (Hohpe/Woolf — catálogo de 65 padrões)
- https://docs.confluent.io/platform/current/schema-registry/fundamentals/schema-evolution.html (Confluent — backward/forward/full/transitive, ordem de upgrade)
- https://kafka.apache.org/38/javadoc/org/apache/kafka/clients/producer/KafkaProducer.html (Kafka — produtor idempotente e transacional, EOS)
- https://kafka.apache.org/documentation/ (Kafka — partições, offsets, consumer groups, retenção)
- https://www.rabbitmq.com/docs/compare/kafka (RabbitMQ — fila × log, roteamento, ack)
- https://aws.amazon.com/compare/the-difference-between-rabbitmq-and-kafka/ (AWS — comparação RabbitMQ × Kafka)
- https://debezium.io/blog/2019/02/19/reliable-microservices-data-exchange-with-the-outbox-pattern/ (Debezium — outbox com CDC / transaction log tailing)
- https://debezium.io/blog/2020/02/10/event-sourcing-vs-cdc/ (Debezium — event sourcing × CDC)
- https://docs.stripe.com/api/idempotent_requests (Stripe — Idempotency-Key)
- https://stripe.com/blog/idempotency (Stripe — APIs idempotentes e retries com backoff)
- https://en.wikipedia.org/wiki/CAP_theorem (CAP e PACELC)
- https://www.baeldung.com/cs/two-phase-commit-vs-saga-pattern (Baeldung — 2PC × Saga)
- https://www.baeldung.com/kafka-exactly-once (Baeldung — semânticas de entrega e EOS no Kafka)
- https://strimzi.io/blog/2023/05/03/kafka-transactions/ (Strimzi — transações Kafka e EOS)
- https://system-design.space/en/chapter/saga-pattern/ (Saga: compensação, outbox+CDC, chaves de idempotência)
- https://learn.microsoft.com/en-us/azure/architecture/patterns/ (Azure — catálogo de padrões de resiliência: Retry, Circuit Breaker, Bulkhead, DLQ)
- https://api7.ai/learning-center/api-101/api-versioning (estratégias de versionamento de API REST)
