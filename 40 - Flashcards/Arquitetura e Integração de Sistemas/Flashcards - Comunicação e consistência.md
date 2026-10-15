---
tipo: flashcard
disciplina: "Arquitetura e Integração de Sistemas"
tema: "Comunicação e consistência"
data: "2026-10-14"
tags:
  - flashcard/comunicacao-e-consistencia
---

# Flashcards: Comunicação e consistência

> Deck baseado no resumo [[Comunicação e consistência - Arquitetura e Integração de Sistemas]].

## Estilos de integração

Quais quatro estilos clássicos de integração Hohpe e Woolf catalogaram? :: Transferência de arquivos, banco de dados compartilhado, invocação remota de procedimentos e mensageria.

Qual o principal defeito do estilo banco de dados compartilhado? :: Forte acoplamento de esquema entre os sistemas (anti-padrão em microsserviços).

Qual acoplamento caracteriza a chamada síncrona RPC/REST? :: Acoplamento temporal — chamador e chamado precisam estar no ar ao mesmo tempo, e o chamador bloqueia.

Quais são os prós da comunicação assíncrona por mensagens? :: Desacoplamento, absorção de picos (buffer do broker) e resiliência à indisponibilidade do consumidor.

Quais são os contras da comunicação assíncrona? :: Consistência eventual, maior complexidade de rastreamento, duplicatas e problemas de ordenação.

## Mensageria: conceitos e componentes

O que é um Message Channel? :: O canal por onde as mensagens trafegam entre produtores e consumidores.

Diferencie Point-to-Point Channel de Publish-Subscribe Channel. :: Fila (point-to-point) entrega cada mensagem a um consumidor; tópico (publish-subscribe) entrega a todos os assinantes (fan-out).

O que são Competing Consumers? :: Vários consumidores disputando mensagens da mesma fila, gerando balanceamento de carga e escalabilidade horizontal.

O que faz um durable subscriber? :: Assinante durável de um tópico que recebe mensagens mesmo estando offline.

Quais são os componentes de uma Message? :: Cabeçalho (metadados como roteamento e correlação) e corpo (payload).

Quais são os três tipos de mensagem citados? :: Command Message (instrui a fazer algo), Document Message (transfere dados) e Event Message (notifica que algo aconteceu).

O que é um Message Broker? :: Intermediário que roteia, entrega e pode persistir mensagens.

O que é um Message Bus? :: Backbone comum de integração por onde os sistemas trocam mensagens.

Que padrões fazem roteamento e seleção de mensagens por conteúdo? :: Message Router, Content-Based Router, Message Filter e Recipient List.

Para que servem Message Translator, Normalizer e Canonical Data Model? :: Traduzir formatos; o canonical data model reduz o número de tradutores de N vezes N menos 1 para 2N.

O que é um Dead Letter Channel (DLQ)? :: Canal para onde vão mensagens que não puderam ser processadas (poison messages) para análise posterior.

O que é Guaranteed Delivery? :: Persistência das mensagens no broker para não perdê-las em caso de queda.

Para que serve o Correlation Identifier? :: Associar a resposta à requisição em um Request-Reply assíncrono; não se confunde com chave de idempotência.

O que fazem Message Sequence / Resequencer e Message Expiration? :: O primeiro reordena mensagens; o segundo descarta mensagens por tempo (TTL).

O que é um Transactional Client? :: O produtor que participa de uma transação para enviar mensagens de forma confiável.

## Filas × logs (RabbitMQ × Kafka)

Qual a diferença central entre brokers queue-based e log-based? :: Queue-based (RabbitMQ) remove a mensagem após o ack; log-based (Kafka) retém a mensagem por tempo/tamanho em log append-only.

Como o RabbitMQ roteia mensagens? :: Por "broker inteligente" com exchanges (direct, topic, fanout, headers), bindings e routing keys.

Como o Kafka organiza e roteia mensagens? :: Tópicos divididos em partições, cada uma um log ordenado; consumo por tópico/partição, no estilo "pipe burro".

O que o offset do Kafka permite? :: Retomar a leitura e reler do início (replay), pois a mensagem não é apagada ao ser consumida.

Qual é a garantia de ordenação no Kafka? :: Ordem por partição, não global.

Até onde vai a escalabilidade no Kafka? :: Muito alta, via partições combinadas com consumer groups.

Quais recursos de ack e QoS o RabbitMQ oferece? :: nack/requeue, prefetch (QoS) e dead-letter exchange (DLX).

## Garantias de entrega e EOS

O que garante a entrega at-most-once? :: Não reenvia; pode perder a mensagem (por exemplo, acks igual a zero, dispara e esquece).

O que caracteriza a entrega at-least-once? :: Reenvia em caso de falha; pode duplicar — é a garantia típica de brokers com ack.

Por que o exactly-once de transporte é impossível de garantir em absoluto? :: Por causa do problema dos dois generais sobre canal não confiável; obtém-se apenas o efeito exatamente-uma-vez.

Como se obtém o efeito exatamente-uma-vez na prática? :: Combinando entrega at-least-once com um consumidor idempotente.

Como funciona o produtor idempotente do Kafka? :: O broker atribui Producer ID e número de sequência por lote/partição; reenvios do mesmo lote são deduplicados, garantindo exatamente-uma-vez por partição e por sessão.

O que o produtor transacional do Kafka permite? :: Escrever atomicamente em várias partições/tópicos, com transactional.id e epoch para fencing de produtores zumbis.

Qual o ciclo de vida do produtor transacional do Kafka? :: initTransactions, beginTransaction, send e então commitTransaction ou abortTransaction.

Como funciona o padrão read-process-write no Kafka? :: sendOffsetsToTransaction grava os offsets do consumidor na mesma transação da escrita de saída; consumidores com isolation.level igual a read_committed só leem transações confirmadas.

O que significa o parâmetro exactly_once_v2 no Kafka Streams? :: A configuração processing.guarantee que ativa a semântica exactly-once, ao custo de mais latência e menor throughput.

A semântica EOS do Kafka cobre escrita em sistemas externos? :: Não; EOS cobre Kafka para Kafka, e escritas em sistemas externos exigem cooperação do destino ou idempotência.

## Padrões orientados a eventos (Fowler)

Quais são os quatro significados de event-driven separados por Fowler? :: Event Notification, Event-Carried State Transfer, Event Sourcing e CQRS.

Como funciona o Event Notification? :: Envia um evento avisando que algo mudou, sem carregar o estado; o consumidor precisa voltar à fonte para obter os dados.

Quais os pontos fortes e o problema do Event Notification? :: Baixo acoplamento e simplicidade; porém o fluxo lógico fica implícito e difícil de depurar.

O que faz o Event-Carried State Transfer? :: O evento carrega o estado, permitindo que consumidores mantenham cópias locais, com mais disponibilidade e menor latência.

Qual o custo do Event-Carried State Transfer? :: Duplicação de dados e consistência eventual.

O que é Event Sourcing? :: Todas as mudanças de estado são gravadas como sequência de eventos; o event log é a fonte da verdade e o estado é derivado.

O que o Event Sourcing possibilita? :: Rebuild completo, temporal query (estado no passado), replay, correção por eventos retroativos e snapshots para desempenho.

Quais cuidados o Event Sourcing exige? :: Evolução de schema dos eventos, supressão de efeitos colaterais externos no replay, ordenação e identificadores estáveis.

O que é CQRS? :: Usar modelos diferentes para escrita (command) e leitura (query), escalando cada lado independentemente, com read models/projeções de consistência eventual.

Qual o alerta de Fowler sobre CQRS? :: Não usar em todo o sistema; é complexo e só se justifica onde há ganho real.

Comando × evento? :: Comando expressa intenção e é endereçado a um destinatário; evento expressa fato ocorrido e é publicado (broadcast) a quem interessar.

## Persistência: banco por serviço, outbox e CDC

O que é o padrão Database per Service e qual problema ele cria? :: Cada serviço tem seu banco, eliminando acoplamento de esquema, mas cria o problema de consistência entre serviços (base da Saga).

O que é o dual write problem? :: Salvar no banco e publicar no broker são duas operações não atômicas; se uma falhar, o evento se perde ou se publica sem persistir.

Como o Transactional Outbox resolve o dual write? :: Grava a mensagem em uma tabela outbox na mesma transação local das entidades; um message relay separado lê e publica no broker.

Quais as duas implementações do relay da outbox? :: Polling Publisher (consulta a tabela) e Transaction Log Tailing (ler o transaction log do banco, isto é, CDC, como o Debezium).

O que é Inbox / Idempotent Consumer? :: O consumidor registra IDs de mensagens já processadas e ignora duplicatas.

O que é Change Data Capture (CDC)? :: Capturar mudanças de linhas no log transacional do banco e transmiti-las, útil para replicação, read models e relay da outbox.

CDC × Event Sourcing? :: CDC registra o que mudou no banco (estado); event sourcing grava eventos de domínio (intenção/semântica de negócio).

O que são projeções / read models / materialized views? :: Views otimizadas para leitura, derivadas de eventos, que aceitam consistência eventual.

## Falhas distribuídas

Quais são os principais tipos de falha em sistemas distribuídos? :: Falha de rede (timeouts, perdas, partições/split-brain), crashes de processo/nó, falha parcial, duplicatas e desordem de mensagens.

O que é falha parcial? :: Parte do sistema funciona e parte não, de modo que o chamador não sabe se a operação ocorreu.

O que diz o problema dos dois generais? :: É impossível, por troca de mensagens sobre canal não confiável, garantir acordo e entrega exatamente-uma-vez absoluta.

## Retry

Por que o retry é necessário e qual seu efeito colateral? :: Falhas transitórias são comuns, mas o retry cria duplicatas se a primeira tentativa já foi aplicada.

Quais erros devem e quais não devem ser repetidos? :: Repetir apenas transitórios (timeout, 5xx, conexão); não repetir permanentes (4xx de validação ou autorização).

O que são exponential backoff e jitter e por que usá-los? :: Espera crescente e aleatória entre tentativas para evitar retry storm / thundering herd.

Qual regra toda operação retentável deve seguir? :: Ser idempotente; caso contrário, repetir duplica efeitos (por exemplo, cobrança em dobro).

## Idempotência

O que significa uma operação idempotente? :: Produz o mesmo resultado se executada uma ou várias vezes; repetir não altera o estado final.

Quais métodos HTTP são idempotentes por definição? :: GET, HEAD, PUT e DELETE.

Por que POST e PATCH não são, em geral, idempotentes? :: POST pode criar recurso a cada envio e PATCH pode não ser idempotente; GET/HEAD, além de idempotentes, são seguros.

O que é e como funciona a chave de idempotência? :: O cliente envia um identificador único (ex.: cabeçalho Idempotency-Key, como no Stripe); o servidor armazena o resultado por chave e devolve o mesmo resultado em repetição.

Quais são as formas de garantir idempotência no consumidor? :: Deduplicação explícita (guardar IDs processados ou tabela inbox) ou semântica idempotente (SET de status, upsert, restrição de unicidade).

O que é o Idempotent Receiver (EIP)? :: Projetar o receptor para receber a mesma mensagem com segurança, por de-duping explícito ou por semântica idempotente.

Qual a fórmula central de idempotência na prática? :: At-least-once mais idempotência resulta em efeito exatamente-uma-vez.

## Modelos de consistência

O que significa ACID? :: Atomicidade, Consistência, Isolamento e Durabilidade, típico de transações locais.

O que significa BASE? :: Basically Available, Soft state, Eventual consistency, típico de sistemas distribuídos/NoSQL.

O que é consistência forte? :: Toda leitura enxerga a escrita mais recente, exigindo coordenação e aumentando a latência.

O que é consistência eventual e quais modelos intermediários existem? :: As réplicas convergem com o tempo se cessarem as escritas; intermediários incluem read-your-writes, monotonic reads e causal consistency.

Em que difere o C do ACID do C do CAP? :: No ACID, consistência é integridade de restrições/invariantes; no CAP, é linearizability (cada leitura vê a última escrita).

O que afirma o teorema CAP? :: Sob partição de rede (P), o sistema escolhe entre consistência (C) e disponibilidade (A); como partições são inevitáveis, sistemas reais são CP ou AP.

O que o CAP não significa? :: Não significa escolher 2 de 3 sempre; o trade-off só se aplica durante partições.

O que acrescenta o PACELC ao CAP? :: Se há partição (P), escolhe-se A × C; senão (E), escolhe-se latência (L) × consistência (C).

## Padrões de resiliência

Como funciona o Circuit Breaker? :: Abre após detectar falhas para evitar cascata, com estados fechado, aberto e meio-aberto.

Para que serve o Bulkhead? :: Isolar recursos por compartimento para evitar falha total do sistema.

O que é Queue-Based Load Leveling? :: Uma fila absorve picos de carga, nivelando o processamento pelo consumidor.

Para que serve uma Dead Letter Queue? :: Para onde vão mensagens não processáveis, separadas para análise e tratamento.

O que é Compensating Transaction? :: Desfazer efeitos já confirmados por meio de nova operação de efeito oposto; é a base da Saga.

## Coordenação de operações: 2PC e Saga

Descreva as duas fases do 2PC. :: Fase 1 (prepare/vote) o coordenador pede o prepare e os recursos ficam bloqueados; fase 2 (commit/rollback) confirma se todos votam sim, ou aborta em todos se algum vota não.

Quais são os problemas do 2PC/XA? :: É bloqueante (mantém locks), o coordenador é ponto único de falha, não escala e muitos bancos NoSQL/cloud não suportam XA.

O que é o padrão Saga? :: Decompor uma transação longa em uma sequência de transações locais commitadas imediatamente; em falha, executa-se a cadeia de transações compensatórias.

Como se comporta a compensação em uma Saga? :: Não é rollback; como a transação já foi commitada e é visível, compensar é uma nova transação de efeito oposto (charge vira refund), em ordem inversa.

Onde devem ficar ações não compensáveis, como enviar e-mail? :: Depois do pivot, o ponto de não retorno da Saga.

Quais são as categorias de passos de uma Saga? :: Compensável (pode ser desfeito), pivot (ponto de não retorno) e retentável (após o pivot, garante-se concluir).

Que característica do ACID a Saga não garante e quais anomalias surgem? :: Não há isolamento; estados intermediários são visíveis, gerando dirty reads e lost updates.

Quais contramedidas de isolamento a Saga pode usar? :: Semantic lock (ex.: pedido em PENDING), commutative updates, pessimistic view, reread value e version files.

Quais requisitos uma Saga impõe aos seus passos? :: Passos e compensações idempotentes, compensação em ordem inversa e estado da Saga durável; se a compensação falhar, retry com backoff e escalar para intervenção humana.

O que é o TCC (Try-Confirm-Cancel)? :: Meio-termo entre 2PC e Saga em que Try reserva recursos, Confirm efetiva e Cancel libera, explicitando a reserva.

O que é API Composition? :: Para leituras, um agregador consulta vários serviços e compõe a resposta; não é transação.

Saga × consenso? :: Saga resolve fluxo longo com compensação semântica (abdica de isolamento); consenso (Raft/Paxos/etcd) resolve ordem global sobre um estado único; são coisas diferentes e podem coexistir.

Do que depende a confiabilidade end-to-end de uma Saga? :: De transactional outbox com CDC (o evento não se perde) e de idempotência (duplicata não faz mal).

## Coreografia × orquestração

O que caracteriza a coreografia? :: Não há controlador central; cada serviço publica e consome eventos e reage.

Quais são os prós e contras da coreografia? :: Baixo acoplamento e sem ponto único de falha, boa para fluxos simples (2 a 4 passos); porém lógica espalhada, difícil de depurar, risco de ciclos e resiliência global difícil.

O que caracteriza a orquestração? :: Um orquestrador central (máquina de estados) comanda os participantes e dispara compensações.

Quais são os prós e contras da orquestração? :: Lógica em um só lugar, estado explícito e observável, compensação determinística; porém vira ponto de falha e hub de acoplamento, risco de monólito distribuído.

Qual a regra prática entre coreografia e orquestração? :: Coreografia para fluxos simples e autonomia de times; orquestração para fluxos complexos com branching e compensações condicionais; sistemas reais costumam ser híbridos.

Quais engines/ferramentas implementam orquestração de sagas? :: Temporal, Camunda/Zeebe, AWS Step Functions, Azure Durable Functions, Axon e Eventuate.

Como um cliente síncrono acompanha um fluxo assíncrono? :: Respondendo só ao fim da Saga, via polling (GET do recurso) ou webhook/websocket.

Quais padrões de coordenação vêm dos EIP? :: Process Manager, Routing Slip, Scatter-Gather, Aggregator e Splitter.

## Evolução de contratos e APIs

O que é um contrato em integração de sistemas? :: A interface observável: assinatura de API (REST/gRPC), campos de payload, schema de mensagens ou esquema de tabela.

O que é uma mudança backward-compatible? :: Consumidores novos conseguem ler dados antigos; a incompatível exige versionamento ou migração coordenada.

O que é Semantic Versioning? :: Versionamento MAJOR.MINOR.PATCH, em que mudança incompatível incrementa o MAJOR.

Quais são as estratégias de versionamento REST citadas? :: URI path (/v1/pedidos), query parameter (?version=1), header customizado (X-API-Version) e media type via content negotiation no Accept.

Como se faz a deprecação de uma versão de API? :: Documentar, avisar, usar cabeçalhos Deprecation e Sunset e manter período de coexistência de versões.

O que diz a Postel's Law (Robustness Principle)? :: Seja conservador no que envia e liberal no que aceita; combina com o Tolerant Reader, que ignora campos desconhecidos em vez de falhar.

O que são Consumer-Driven Contracts? :: Os consumidores definem o contrato esperado e testes de contrato (ex.: Pact) verificam que o provedor continua atendendo.

Evolução versus versionamento: o que preferir? :: Preferir mudanças compatíveis (adicionar campos, não remover/renomear) e versionar apenas quando a mudança quebra.

## Compatibilidade de schema

O que é compatibilidade BACKWARD? :: O consumidor com o novo schema lê dados escritos com o schema anterior; típico ao adicionar campo opcional/com default ou remover campo.

O que é compatibilidade FORWARD? :: O consumidor com o schema antigo lê dados escritos com o novo schema; típico ao adicionar campo ou remover campo opcional.

O que é compatibilidade FULL? :: Ambos os sentidos funcionam, permitindo apenas adicionar/remover campos opcionais ou com default.

O que é compatibilidade TRANSITIVE? :: Verifica compatibilidade contra todas as versões anteriores, não só a última (BACKWARD_TRANSITIVE, FORWARD_TRANSITIVE, FULL_TRANSITIVE).

O que significa o nível NONE de compatibilidade? :: Sem verificação, quebra permitida — exige migrar produtores e consumidores juntos ou criar novo tópico.

Qual é o padrão de compatibilidade do Confluent Schema Registry? :: BACKWARD, não transitivo.

Qual a ordem de upgrade dos clientes conforme a compatibilidade? :: BACKWARD atualiza consumidores primeiro; FORWARD atualiza produtores primeiro; FULL permite atualização independente.

Adicionar um campo obrigatório sem default quebra qual compatibilidade? :: Quebra a backward; adicionar campo com default é compatível nos dois sentidos.

Como representar campos opcionais em Avro? :: Com union com null, como ["null","string"].

Quais formatos o Schema Registry suporta e como valida? :: Avro, Protobuf e JSON Schema; valida a compatibilidade no registro da nova versão e associa um ID a cada schema.

## Migração de esquemas

O que é Evolutionary Database Design? :: Toda mudança de esquema vira uma migração versionada e automatizada, evoluindo junto com o código.

Como o padrão expand-contract se aplica a colunas de banco? :: Adicionar a nova coluna, migrar/backfill os dados, manter compatibilidade na transição e só então remover a antiga.

O que é o padrão Expand-Contract (Parallel Change) e suas três fases? :: Mudar de forma incompatível com segurança em Expand (introduzir o novo ao lado do antigo), Migrate (migrar incrementalmente) e Contract (remover o antigo).

O que acontece se a fase de Contract não for executada? :: O sistema fica pior que no início, mantendo dois caminhos; por isso o padrão exige disciplina.

Por que a migração de esquemas de eventos é mais delicada? :: Porque eventos antigos persistem no log; usam-se campos opcionais, versionamento do evento e upcasting, evitando reescrever o passado.

O que é upcasting na migração de eventos? :: Converter eventos antigos para a forma nova no momento da leitura/consumo, sem reescrever o log.

Qual recomendação de Greg Young sobre event sourcing? :: Não colocar lógica de negócio entre o evento e a representação de estado.

## Confusões que a banca cobra

Correlation ID × Idempotency Key? :: O correlation ID liga resposta à requisição; a chave de idempotência evita efeito duplicado.

Retry × Circuit Breaker? :: Retry repete a chamada; circuit breaker interrompe chamadas ao detectar falhas, evitando cascata.

Tolerant Reader × Consumer-Driven Contracts? :: Tolerant Reader ignora campos desconhecidos; CDC faz o contrato ser definido pelo consumidor e testado.

Outbox × 2PC? :: Outbox evita transação distribuída gravando a mensagem na mesma transação local; 2PC usa coordenação distribuída e bloqueante.

Durable subscriber × Competing Consumers? :: Durable subscriber é do modelo tópico (recebe offline); competing consumers são do modelo fila (disputam a mesma mensagem).

Por que exatamente-uma-vez não dispensa de-duplicação no consumidor? :: Porque rebalanceamentos e reentregas ainda podem gerar duplicatas.
