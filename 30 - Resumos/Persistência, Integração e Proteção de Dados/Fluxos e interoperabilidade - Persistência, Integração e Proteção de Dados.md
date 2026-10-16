---
tipo: resumo
disciplina: "Persistência, Integração e Proteção de Dados"
tema: "Fluxos e interoperabilidade"
status: novo
data: "2026-10-16"
tags: [resumo, persistencia-dados, cgu-2026]
---

# Resumo: Fluxos e interoperabilidade

> [!info] MOC: [[Persistência, Integração e Proteção de Dados]]
> Edital nº 1/2026 – CGU – AFFC · **Conhecimentos específicos** · Cargo 4 (TI / Desenvolvimento de Sistemas) · Item 3 — *Fluxos e interoperabilidade*.

## Escopo no edital (checklist)

- [x] 3.1 Ingestão, transformação e carga.
- [x] 3.2 ETL e ELT.
- [x] 3.3 Processamento em lote e fluxo, completo e incremental.
- [x] 3.4 APIs, contratos e formatos CSV, JSON, XML e Parquet.
- [x] 3.5 Qualidade, rastreabilidade, conciliação e repetição segura de processamento.
- [x] 3.6 Spring Batch: organização de trabalhos e etapas de processamento (jobs e steps).
- [x] 3.7 Leitura, processamento e escrita de registros.
- [x] 3.8 Controle transacional, registro do estado de execução e reinício após falhas.
- [x] 3.9 Prevenção de perdas e duplicações no reprocessamento.

## Resumo

Este item trata do **movimento de dados**: como trazê-los de uma fonte, transformá-los e entregá-los a um destino, com **qualidade** e **resiliência**. Dois eixos se cruzam:

1. **Conceitos de integração de dados:** a cadeia **ingestão → transformação → carga**, os padrões **ETL × ELT**, os modos **lote (batch) × fluxo (stream)** e **carga completa (full) × incremental**, os **formatos** de troca (CSV, JSON, XML, Parquet) e as garantias de **qualidade, rastreabilidade (linhagem), conciliação e repetição segura (idempotência)**.
2. **Spring Batch** como ferramenta concreta de processamento em lote: **Job/Step** (organização), **ItemReader/ItemProcessor/ItemWriter** (leitura/processamento/escrita), **chunk-oriented processing**, **controle transacional**, **JobRepository** (registro do estado) e **restart/skip/retry** para **reinício após falhas sem perda nem duplicação**.

O fio condutor final é a **entrega exatamente-uma-vez (ou pelo menos com efeito idempotente)**: reprocessar não pode nem perder nem duplicar registros.

## 1. Ingestão, transformação e carga (3.1)

- **Ingestão (extract):** capturar dados da fonte (banco, API, arquivo, fila, log). Pode ser *pull* (o processo busca) ou *push* (a fonte envia via evento/mensagem).
- **Transformação:** limpar, padronizar, deduplicar, enriquecer, validar, converter tipos/schema. Ex.: normalizar datas, remover duplicados, juntar com tabelas de referência, aplicar regras de negócio.
- **Carga (load):** gravar no destino (banco, data warehouse, data lake, índice, sistema externo). Modos: **full load** (carga completa) ou **incremental** (só o delta).
- **Staging area** (área de transição) é comum para aterrissar dados brutos antes de transformar/carregar.
- **Data lake** (dados brutos em formatos como Parquet, no object storage) × **data warehouse** (dados modelados para análise) são destinos frequentes.

## 2. ETL e ELT (3.2)

| | **ETL** (Extract → Transform → Load) | **ELT** (Extract → Load → Transform) |
| --- | --- | --- |
| Ordem | Transforma **antes** de carregar | Carrega **bruto** e transforma **depois** (dentro do destino) |
| Onde transforma | Ferramenta/motor externo (ex.: Talend, Informatica, Spring Batch) | No **próprio** warehouse/lake (SQL do destino) |
| Volume/custo | Transforma só o necessário; exige infra própria | Aproveita o poder de computação do destino (nuvem: BigQuery, Snowflake, Redshift) |
| Uso típico | Destinos tradicionais, schema rígido, limpeza complexa | Data lakes/cloud, grandes volumes, schema-on-read |

- **ETL** é o modelo clássico; **ELT** ganhou força com warehouses em nuvem (transformação via SQL/ELT tools como dbt).
- Em ambos, persistem as mesmas preocupações: **qualidade**, **linhagem** e **reprocessamento seguro** (item 3.5).

## 3. Processamento em lote e fluxo; completo e incremental (3.3)

### 3.1 Lote (batch) × Fluxo (stream)

| | **Batch (lote)** | **Stream (fluxo/contínuo)** |
| --- | --- | --- |
| Processa | Conjunto **finito** de registros de uma vez | Registros **contínuos**, um a um/em micro-lotes |
| Latência | Alta (minutos/horas/agendado) | Baixa (ms/s, em tempo real) |
| Exemplo | Fechamento contábil noturno, carga de cadastro | Telemetria, transações de cartão, eventos IoT |
| Ferramentas | Spring Batch, cron/schedulers, MapReduce | Kafka Streams, Flink, Spark Streaming, AWS Kinesis |
| Estado | Fim definido, restartável | Contínuo, com *checkpoint*/watermark |

- **Micro-batching** (ex.: Spark Streaming) fica no meio-termo: processa pequenos lotes em alta frequência.
- Escolha: **volume + janela de tempo** (batch) vs **latência** (stream). Muitas arquiteturas combinam: stream para a linha de frente, batch para consolidação.

### 3.2 Carga completa (full) × incremental

- **Full load:** recarrega **todos** os dados do zero (simples, porém caro; útil na primeira carga ou quando a fonte não expõe delta).
- **Incremental load:** carrega **só o que mudou** desde a última execução, usando **marca d'água (watermark)**:
  - por **timestamp** (`updated_at > último_processamento`),
  - por **versão/sequência** (ex.: `sequence > N`),
  - por **CDC** (*Change Data Capture* — log do banco, ex.: Debezium),
  - por **flag/marca de processamento**.
- Cuidados com incremental: **mudanças tardias** (registros que chegam fora de ordem), **deleções** (precisa de tombstone/CDC), **timezone** e **relógio da fonte**.

## 4. APIs, contratos e formatos CSV, JSON, XML e Parquet (3.4)

### 4.1 APIs e contratos

- **API** é a interface pela qual sistemas trocam dados; o **contrato** (schema, endpoints, formatos, versões) define a compatibilidade. Ver também o Item 2 de "Arquitetura e Integração de Sistemas" (APIs e identidade).
- Contratos: **OpenAPI** (REST), **AsyncAPI** (eventos), **JSON Schema**, **Avro/Protobuf** (schema evolutivo e binário), **XML Schema (XSD)**.
- **Evolução de contrato:** mudanças compatíveis (adicionar campo opcional) × incompatíveis (renomear/remover/tipar); *expand-and-contract*.

### 4.2 Formatos

| Formato | Natureza | Quando usar | Observações |
| --- | --- | --- | --- |
| **CSV** | Texto, linhas, delimitado (RFC 4180) | Troca simples, planilhas, import/export | Sem tipo/schema nativo; frágil a vírgula/quebra de linha/encoding |
| **JSON** | Texto, hierárquico, key-value | APIs, mensagens, config | Auto-descritivo, legível; sem schema obrigatório; tipos limitados (sem data nativa) |
| **XML** | Texto, marcado, com schema (XSD/XPath) | Integração legada, documentos, SOAP, padrões governamentais | Verboso; rico em metadados; XPath/XSLT para navegar/transformar |
| **Parquet** | **Binário colunar** | Analytics/data lake (Hadoop, Spark, BigQuery) | Ótima compressão + pushdown de colunas; **não** é legível/append-amigável como CSV/JSON |

- **Colunar (Parquet)** armazena por **coluna** (não por linha): agregações sobre poucas colunas de muitas linhas são muito mais rápidas; permite **predicate/projection pushdown**. Contraste com **row-based** (CSV/JSON/linhas de banco OLTP).
- **JSON × XML:** ambos hierárquicos e legíveis; JSON é mais leve e domina APIs; XML tem namespaces/schema/transformações (muito usado no setor público — e-Social, NF-e, SPED).
- **CSV:** cuidado com aspas/escaping (`"a,b"`), separador decimal, BOM, CRLF — fonte constante de bugs de parse.

## 5. Qualidade, rastreabilidade, conciliação e repetição segura (3.5)

- **Qualidade de dados:** dimensões clássicas — **completude**, **acurácia/correção**, **consistência**, **unicidade**, **validade** (conformidade de formato/domínio), **atualidade**. Aplicar **validação** na ingestão (rejeitar/quarentena registros inválidos).
- **Rastreabilidade (linhagem/lineage):** saber **de onde** cada dado veio, **o que** foi feito com ele e **para onde** foi (data lineage). Essencial para auditoria e reprocessamento.
- **Conciliação (reconciliation):** conferir que **origem e destino batem** — contagem de registros, somas/checksums, amostragem. Detecta perda, duplicação e corrupção.
- **Repetição segura (idempotência):** reprocessar a mesma entrada N vezes produz o **mesmo efeito** que uma vez. Estratégias:
  - **upsert/merge** por chave natural (em vez de insert cego),
  - **chave de idempotência** (dedup por identificador),
  - **exclusão da janela antes de recarregar** (delete do lote + reload),
  - **marca/flag de processado**.
- **Semânticas de entrega:** **at-most-once** (pode perder), **at-least-once** (pode duplicar), **exactly-once** (nem perde nem duplica — na prática, *exactly-once effects* via idempotência/transação). A maioria das mensagerias dá at-least-once; cabe ao consumidor tornar o efeito idempotente.

## 6. Spring Batch: organização de jobs e steps (3.6)

### 6.1 Modelo de domínio

- **Job** = unidade de trabalho completa (o "trabalho"), composta por um ou mais **Steps** ordenados.
- **JobInstance** = uma execução **lógica** identificada por `(jobName + JobParameters)`. **JobExecution** = uma tentativa **física** de rodar aquela instância. **StepExecution** = tentativa de um step dentro de um job execution.
- **JobLauncher** inicia o job; **JobRepository** persiste metadados de execução (estado) em banco.
- **JobParameters** diferenciam instâncias (ex.: `data=2026-10-16`). Rodar de novo com os **mesmos parâmetros** reabre a mesma instância (restart) — não cria outra.
- **JobBuilderFactory/JobBuilder** (Java DSL) define o fluxo: `.start(step1).next(step2)...` com condicionais `.on("FAILED").to(...)`.

### 6.2 Steps e chunk-oriented processing

```java
@Bean
public Step step(JobRepository jobRepository, PlatformTransactionManager tx,
                 ItemReader<Pessoa> reader, ItemProcessor<Pessoa, Pessoa> processor,
                 ItemWriter<Pessoa> writer) {
    return new StepBuilder("stepImporta", jobRepository)
        .<Pessoa, Pessoa>chunk(100, tx)   // lote transacional de 100 itens
        .reader(reader)
        .processor(processor)
        .writer(writer)
        .faultTolerant()
        .skip(SkipException.class)
        .skipLimit(10)
        .retry(TransientException.class)
        .retryLimit(3)
        .build();
}
```

- **Chunk-oriented:** lê `N` itens (commit-interval), processa, grava e **comita** a transação a cada chunk. `N` (=100 acima) é o tamanho do chunk.
- Um **Step** tem **exatamente um** `ItemReader`, **um** `ItemProcessor` (opcional) e **um** `ItemWriter`.
- **Tasklet step** (alternativa) executa uma tarefa única (ex.: limpar tabela, mover arquivo) — para operações não item-a-item.

## 7. Leitura, processamento e escrita de registros (3.7)

### 7.1 ItemReader

- `ItemReader<T>` fornece **um item por vez**: `T read()` retorna o item ou `null` no fim.
- Implementações comuns: **`FlatFileItemReader`** (CSV/posicional), **`JdbcCursorItemReader`/`JdbcPagingItemReader`** (banco), **`JpaPagingItemReader`**, **`KafkaItemReader`**, **`StaxEventItemReader`** (XML), `JsonItemReader`.
- **`ItemStream`** (interface adicional) permite **abrir/fechar/atualizar** recursos e, crucialmente, **persistir estado** (`update(ExecutionContext)`) para **restart**.

### 7.2 ItemProcessor

- `ItemProcessor<I, O>` transforma/item a item: validação, enriquecimento, filtragem.
- **Retornar `null`** indica que o item **não deve ser gravado** (filtro).
- Deve ser **idempotente** e **sem efeitos colaterais persistentes** que quebrem o retry (cuidado com chamadas externas dentro do processor).

### 7.3 ItemWriter

- `ItemWriter<T>` grava **um chunk** de itens: `write(List<? extends T> items)`.
- Implementações: **`JdbcBatchItemWriter`**, **`JpaItemWriter`**, **`FlatFileItemWriter`**, **`StaxEventItemWriter`** (XML), `KafkaItemWriter`.
- Pode ser chamado com **chunk vazio** (quando o processor filtrou tudo) — precisa tratar graciosamente.

## 8. Controle transacional, estado e reinício (3.8)

### 8.1 Transações e commit-interval

- O **chunk** é a **unidade transacional**: lê N itens, processa, grava e **comita** a cada chunk. `commit-interval` define N.
- Erro no meio do chunk → **rollback** do chunk inteiro (não grava parcial), e o framework pode fazer **skip/retry** do item culpado, dependendo da configuração *fault-tolerant*.
- **Skip** (pular itens inválidos até `skipLimit`), **retry** (tentar itens transitórios até `retryLimit`, com *backoff*), **no-rollback** (exceções que não derrubam a transação).

### 8.2 JobRepository e estado de execução

- **`JobRepository`** persiste em banco as tabelas de metadados (meta-data schema): `BATCH_JOB_INSTANCE`, `BATCH_JOB_EXECUTION`, `BATCH_JOB_EXECUTION_PARAMS`, `BATCH_STEP_EXECUTION`, `BATCH_JOB_EXECUTION_CONTEXT`, `BATCH_STEP_EXECUTION_CONTEXT`, além das sequências (`BATCH_JOB_SEQ`, etc.).
- **`ExecutionContext`** é o mapa (key-value) que guarda o **estado** de cada step/execution. O `ItemReader`/`ItemWriter` gravam ali **até onde chegaram** (ex.: última linha lida).
- **Spring Batch 5:** o `JobRepository` **in-memory/map-based foi removido** — é obrigatório um **`DataSource`** (banco) para o repositório. `@EnableBatchProcessing` registra os beans de infraestrutura.

### 8.3 Restart

- Ao **reiniciar** uma `JobInstance` que falhou, o Spring Batch **recarrega o `ExecutionContext`** da última execução; o reader consulta o estado salvo e **retoma de onde parou** (não do zero).
- `Job` pode ser **`restartable`** ou não (`.preventRestart()`); reiniciar uma instância **já concluída** lança `JobInstanceAlreadyCompleteException` (e, se não restartable, `JobRestartException`).
- Por isso o `ItemReader`/`ItemWriter` precisam implementar **`ItemStream`** corretamente (salvar/restaurar estado).

## 9. Prevenção de perdas e duplicações no reprocessamento (3.9)

- **Perda:** registros que nunca chegam ao destino (falha sem checkpoint, buffer não comitado). **Duplicação:** registros gravados mais de uma vez (reprocessar janela já carregada, retry sem idempotência).
- **Medidas-chave:**
  1. **Idempotência por chave natural:** `UPSERT`/`MERGE` em vez de `INSERT` cego; atualizar por PK/chave de negócio.
  2. **Processamento em janelas** com **delete+reload**: apagar o lote daquela partição antes de recarregar (ex.: `DELETE WHERE particao = :p` e depois `INSERT`).
  3. **Checkpoint/marca d'água persistida:** salvar a posição (timestamp/sequência) após cada chunk commitado — retomar daí.
  4. **Dedup de entrada:** chave de idempotência/hash dos registros (ex.: `event_id` único + `UNIQUE` constraint).
  5. **Conciliação de contagens:** comparar origem × destino (total, somas) ao final; alertar divergência.
  6. **Transação do chunk**: gravar dados e avançar checkpoint **na mesma transação** — garante consistência entre o dado e a marca de progresso.
- **Cuidado com o at-least-once:** se a fonte/mensageria pode redeliverar, o consumidor **precisa** ser idempotente (ou deduplicar) para entregar *exactly-once effects*.

## Detalhes que merecem destaque

- **ETL** transforma **antes** de carregar; **ELT** carrega bruto e transforma **no destino** (warehouse na nuvem).
- **Batch** = conjunto finito/agendado; **stream** = contínuo/baixa latência; **micro-batch** é o meio-termo.
- **Incremental** precisa de **marca d'água** (timestamp/sequência/CDC); **full** recarrega tudo.
- **CSV/JSON/XML** são texto (row/hierárquico); **Parquet** é **binário colunar** (analytics).
- **At-most-once / at-least-once / exactly-once (effects):** mensagerias dão at-least-once; a idempotência do consumidor fecha o exactly-once.
- **Spring Batch:** `Job` → `Steps` → `ItemReader/Processor/Writer`; **chunk = unidade transacional**.
- **`ItemProcessor` retorna `null`** para **filtrar** (não gravar) o item.
- **`JobInstance` = job + JobParameters**; reexecutar com os mesmos parâmetros = **restart**, não nova instância.
- **`JobRepository`** (banco) guarda o estado; **`ExecutionContext`** guarda a posição para retomada.
- **Spring Batch 5 removeu o repositório in-memory** — exige `DataSource`.
- **Restart** recarrega o `ExecutionContext` e retoma **de onde parou** (via `ItemStream`).
- **Prevenir perda/duplicação** = upsert + delete&reload + checkpoint na mesma transação + dedup + conciliação.

## Comparações que a banca costuma cobrar (certo/errado)

| Conceito A | Conceito B | Diferença-chave |
| --- | --- | --- |
| ETL | ELT | ETL transforma antes de carregar; ELT carrega bruto e transforma no destino |
| Batch | Stream | Batch = finito/agendado; stream = contínuo/baixa latência |
| Full load | Incremental load | Full recarrega tudo; incremental só o delta (marca d'água) |
| CSV | Parquet | CSV = texto por linha; Parquet = binário **colunar** (compressão + pushdown) |
| JSON | XML | JSON leve/APIs; XML com schema (XSD)/namespaces/transformações |
| Ingestão (extract) | Carga (load) | Extract captura da fonte; load grava no destino |
| Data lake | Data warehouse | Lake = dados brutos (schema-on-read); warehouse = modelado p/ análise |
| Job | Step | Job é o trabalho; Step é uma etapa sequencial dentro dele |
| JobInstance | JobExecution | Instância = identidade lógica (job+parâmetros); execution = tentativa física |
| ItemReader | ItemWriter | Reader lê um item por vez; Writer grava um chunk |
| ItemProcessor | ItemReader | Processor transforma/filtra; Reader fornece o item bruto |
| Chunk-oriented | Tasklet step | Chunk processa itens em lotes transacionais; tasklet executa tarefa única |
| Skip | Retry | Skip pula o item inválido; retry tenta de novo o transitório |
| `ExecutionContext` | JobRepository | Context guarda o **estado/posição**; repository persiste os **metadados** |
| at-least-once | exactly-once | at-least pode duplicar; exactly-once (effects) nem perde nem duplica |
| Idempotência | Conciliação | Idempotência = reprocessar tem mesmo efeito; conciliação = conferir origem×destino |
| Commit-interval | Chunk size | Sinônimos práticos: quantos itens por transação |

## Pegadinhas e erros comuns

> Cuidado com termos absolutos ("sempre", "nunca", "exclusivamente") e com a troca de requisitos.

- Trocar **ETL por ELT** (a diferença é **onde/quando** transforma, não o "o quê").
- Dizer que **stream substitui batch** sempre — depende de latência × volume/custo; muitas vezes convivem.
- Achar que **CSV tem schema/tipo nativo** — é texto sem tipo; e esquecer escaping/encoding.
- Confundir **JSON com Parquet** em natureza (texto legível × binário colunar).
- Supor que **at-least-once garante sem duplicação** — pode duplicar; a idempotência é responsabilidade do consumidor.
- Dizer que **`ItemProcessor` que retorna `null` grava o item** — `null` **filtra** (não grava).
- Achar que **reprocessar com os mesmos parâmetros cria nova instância** — reabre a mesma `JobInstance` (restart).
- Supor que **restart recomeça do zero** — retoma do `ExecutionContext` (se o reader implementar `ItemStream`).
- Esquecer que **Spring Batch 5 exige `DataSource`** para o `JobRepository` (in-memory foi removido).
- Dizer que **o chunk não é transacional** — ele **é** a unidade de transação (commit a cada chunk).
- Confundir **skip (invalido, segue) com retry (transitório, tenta de novo)**.
- Achar que **full load é sempre melhor** que incremental — é mais simples, porém caro e pode ser inviável em grande volume.
- Supor que **upsert não ajuda contra duplicação** — é uma das ferramentas centrais de idempotência.
- Achar que **exactly-once em mensageria é trivial** — na prática é *exactly-once effects* (idempotência/transação), não "a mensagem nunca reentrega".
- Confundir **data lake com data warehouse** (bruto/schema-on-read × modelado).

## Notas atômicas relacionadas

```dataview
LIST FROM "20 - Notas"
WHERE disciplina = this.disciplina
  AND contains(tema, this.tema)
SORT file.name ASC
```

## Fontes

- https://docs.spring.io/spring-batch/reference/ — Spring Batch Reference (documentação oficial atual).
- https://docs.spring.io/spring-batch/reference/domain.html — Spring Batch: domain language (Job/Step/JobInstance/JobExecution/StepExecution).
- https://docs.spring.io/spring-batch/reference/job.html — Spring Batch: configuração e execução de Job.
- https://docs.spring.io/spring-batch/reference/step/chunk-oriented-processing.html — Spring Batch: chunk-oriented processing (commit-interval, transações).
- https://docs.spring.io/spring-batch/reference/readersAndWriters.html — Spring Batch: ItemReader/ItemProcessor/ItemWriter (e ItemStream/estado).
- https://docs.spring.io/spring-batch/reference/step/chunk-oriented-processing/controlling-step-flow.html — Spring Batch: restart, skip e retry.
- https://parquet.apache.org/docs/ — Apache Parquet (formato colunar) — documentação oficial.
- https://datatracker.ietf.org/doc/html/rfc4180 — RFC 4180: Common Format and MIME Type for CSV Files.
- https://www.json.org/json-en.html — JSON (introdução ao formato).
- https://www.w3.org/XML/ — W3C XML (padrão e links para XSD/XPath/XSLT).
- https://kafka.apache.org/ — Apache Kafka (mensageria/streaming, semânticas de entrega e CDC com Debezium).
- https://en.wikipedia.org/wiki/Extract,_transform,_load — ETL/ELT (definição e contraste).
- https://en.wikipedia.org/wiki/Stream_processing — Stream processing (processamento em fluxo) e contraste com batch.
- https://debezium.io/ — Debezium (Change Data Capture para cargas incrementais).
