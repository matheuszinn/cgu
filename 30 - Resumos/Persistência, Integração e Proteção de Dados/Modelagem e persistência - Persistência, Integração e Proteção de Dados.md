---
tipo: resumo
disciplina: "Persistência, Integração e Proteção de Dados"
tema: "Modelagem e persistência"
status: novo
data: "2026-10-16"
tags: [resumo, persistencia-dados, cgu-2026]
---

# Resumo: Modelagem e persistência

> [!info] MOC: [[Persistência, Integração e Proteção de Dados]]
> Edital nº 1/2026 – CGU – AFFC · **Conhecimentos específicos** · Cargo 4 (TI / Desenvolvimento de Sistemas) · Item 1 — *Modelagem e persistência*.

## Escopo no edital (checklist)

- [x] 1.1 Modelagem relacional, normalização e integridade.
- [x] 1.2 Bancos documentais, chave-valor e vetoriais.
- [x] 1.3 Cache e busca textual.
- [x] 1.4 Escolha de armazenamento conforme uso.
- [x] 1.5 Transações, concorrência, consistência e evolução de esquemas.
- [x] 1.6 Persistência em Java com JPA: mapeamento de entidades e relacionamentos, ciclo de vida das entidades, contexto de persistência, consultas e transações.
- [x] 1.7 Estratégias de carregamento e seus efeitos sobre correção e desempenho.
- [x] 1.8 Spring Data JPA: repositórios, consultas e paginação.
- [x] 1.9 Integração da camada de persistência às regras de negócio.

## Resumo

Este item cobre o "chão" de qualquer sistema: **onde e como os dados são guardados, lidos e mantidos consistentes**. O fio condutor tem quatro blocos que se encadeiam:

1. **Modelagem relacional** formaliza o domínio em **entidades, atributos e relacionamentos** (MER), com **chaves** (primária, estrangeira, candidata, composta), **normalização** (1FN/2FN/3FN/BCNF) para eliminar redundância/anomalias e **integridade** (de entidade, referencial, de domínio) via restrições (`PRIMARY KEY`, `FOREIGN KEY`, `UNIQUE`, `CHECK`, `NOT NULL`).
2. **Modelos não relacionais (NoSQL)** resolvem problemas em que o relacional é ineficiente ou rígido: **documentais** (MongoDB, documentos JSON/BSON auto-descritivos), **chave-valor** (Redis, in-memory com estruturas ricas), **vetoriais** (embeddings + busca por similaridade). A escolha é governada pelo **CAP theorem** (só dá para ter 2 de 3 sob partição de rede) e pelo contraste **ACID × BASE**.
3. **Cache e busca textual** atacam dois gargalos: **cache** (armazenar resultado caro em memória — padrões *cache-aside*, *write-through*, TTL, invalidação) e **busca textual** (Elasticsearch/Lucene com **índice invertido**, tokenização, relevância BM25).
4. **Persistência em Java com JPA/Spring Data** mapeia o modelo orientado a objetos para o relacional: entidades e relacionamentos (`@Entity`, `@OneToMany`, `@ManyToOne`, …), **ciclo de vida** (*new/managed/detached/removed*), **contexto de persistência** (`EntityManager`), consultas (JPQL/Criteria), **transações**, **estratégias de carregamento** (*lazy/eager*, problema **N+1**) e **repositórios** do Spring Data JPA.

## 1. Modelagem relacional, normalização e integridade (1.1)

### 1.1 Conceitos fundamentais

- **Entidade:** objeto do mundo real com existência independente (ex.: `Pessoa`, `NotaFiscal`, `Produto`). No banco, vira **tabela**; cada instância vira **linha** (tupla).
- **Atributo:** propriedade da entidade (coluna). Ex.: `nome`, `cpf`, `data_nascimento`.
- **Relacionamento:** associação entre entidades, com **cardinalidade**: **1:1** (um gerente–um departamento), **1:N** (um cliente–muitos pedidos), **N:M** (alunos–disciplinas). N:M vira **tabela associativa** (de ligação).
- **MER (Modelo Entidade-Relacionamento):** representação conceitual (diagrama de Chen ou crow's foot) independente de SGBD. Antecede o **modelo lógico** (tabelas/colunas) e o **físico** (índices, partições, storage).

### 1.2 Chaves

| Chave | Definição |
| --- | --- |
| **Superchave** | Conjunto de atributos que identifica unicamente uma linha. |
| **Chave candidata** | Superchave **mínima** (sem atributos supérfluos). |
| **Chave primária (PK)** | Chave candidata escolhida; não nula e única. |
| **Chave estrangeira (FK)** | Atributo que referencia a PK de outra tabela (relacionamento). |
| **Chave composta** | Chave formada por mais de um atributo. |

- **Chave natural** (ex.: CPF) × **chave substituta/surrogate** (ex.: `id BIGSERIAL`/`UUID`). Em prática de microsserviços, IDs opacos (UUID) reduzem acoplamento.

### 1.3 Normalização (1FN, 2FN, 3FN, BCNF)

Objetivo: **eliminar redundância** e as **anomalias** de inserção/atualização/exclusão.

- **1FN:** valores **atômicos** (sem listas/tabelas aninhadas em um campo) e sem grupos repetidos. Ex.: não guardar `telefones: "11-9999,21-8888"` numa coluna.
- **2FN:** além da 1FN, **não pode haver dependência parcial** da PK — só se aplica a **chaves compostas**: todo atributo não-chave deve depender da PK **inteira**, não de parte dela.
- **3FN:** além da 2FN, **não pode haver dependência transitiva** — atributo não-chave não pode depender de outro atributo não-chave. Ex.: tabela `Pedido(id, idCliente, nomeCliente)` → `nomeCliente` depende de `idCliente`, não de `idPedido`.
- **BCNF (Forma Normal de Boyce-Codd):** refinamento da 3FN; todo determinante é uma chave candidata.
- **Desnormalização:** inversão **deliberada** para ganho de leitura (ex.: colunas redundantes/agregadas), comum em *data warehouse* (modelo estrela/neve) — aceita redundância controlada em troca de consulta mais rápida.

### 1.4 Integridade

- **De entidade:** PK não pode ser nula nem duplicada.
- **Referencial:** FK deve apontar para uma PK existente, ou ser `NULL`. Garantida por `FOREIGN KEY ... REFERENCES`; ações `ON DELETE/ON UPDATE` (`CASCADE`, `SET NULL`, `RESTRICT`, `NO ACTION`, `SET DEFAULT`).
- **De domínio:** valores válidos por tipo/regra → `CHECK`, `NOT NULL`, `UNIQUE`, `DEFAULT`, enumerações.
- **De negócio (regras semânticas):** ex.: "data_fim ≥ data_inicio", "saldo ≥ 0" — podem exigir *triggers* ou validação na aplicação.

## 2. Bancos documentais, chave-valor e vetoriais (1.2)

### 2.1 Documental — MongoDB

- Armazena **documentos** (JSON/BSON) auto-descritivos em **coleções**; **schema flexível** (não exige DDL nem estrutura homogênea).
- Unidade atômica é o **documento** (transações multi-documento existem, mas o padrão histórico é single-document). **RDBMS → MongoDB:** tabela→coleção, linha→documento, coluna→campo, índice→índice, join→**documentos embutidos** (embedding) ou **referências**.
- `_id` é a chave primária (com índice único). Suporta **índices secundários**, réplicas (*replica set*), *sharding*.
- Bom para: dados **hierárquicos/irregulares**, catálogos, conteúdo, evolução rápida de esquema, cargas de leitura pesada.

### 2.2 Chave-valor — Redis

- **Dicionário (hash map) em memória**: chave → valor, com **O(1)** para leitura de ponto. Valor pode ser mais que string: **lists, sets, sorted sets, hashes, streams, bitmaps, hyperloglog, geo**.
- **Single-threaded** no núcleo de comandos → operações são **atômicas por construção** (sem corrida entre comandos). **Extremamente rápido** (ordem de centenas de milhares a milhões de ops/s).
- Usos: **cache**, sessões, filas/pub-sub, contadores, rate limiting, leaderboards. Persistência: **RDB** (snapshots) e/ou **AOF** (append-only file); TTL por chave (`EXPIRE`).

### 2.3 Vetoriais

- Guardam **embeddings** (vetores de números que representam semântica de textos/imagens) e respondem **busca por similaridade** (distância de cosseno, produto interno, L2), com índices **ANN** (HNSW, IVF).
- São a base de **RAG** (recuperação + geração) com LLMs: transforma a pergunta em vetor e recupera os trechos mais próximos.
- Exemplos: **pgvector** (extensão do PostgreSQL), **Qdrant**, **Pinecone**, **Weaviate**, **Milvus**.

### 2.4 Quando usar cada um e o CAP theorem

- **Relacional (SQL):** transações ACID, consultas complexas (joins), esquema estável, integridade forte → sistemas transacionais (OLTP), financeiro, cadastro.
- **Documental:** esquema flexível/heterogêneo, leitura de documentos inteiros, evolução ágil.
- **Chave-valor:** latência baixíssima, acessos por chave exata, cache/sessão.
- **Vetorial:** similaridade semântica, recomendação, busca por significado (não por texto literal).
- **Colunar (analítico, ex.: Parquet/BigQuery/ClickHouse):** agregações sobre poucas colunas de muitas linhas (OLAP).

**CAP theorem** (conjecturado por Eric Brewer em 2000, provado por Gilbert & Lynch em 2002): num sistema **distribuído** e **replicado**, sob **partição de rede (P)** só é possível garantir **um** dos dois — **Consistência (C)** ou **Disponibilidade (A)**. Como partições acontecem, na prática o sistema é **CP** (sacrifica disponibilidade) ou **AP** (sacrifica consistência imediata).

- **C** do CAP = consistência de **replicação** (uma única cópia lógica vista por todos), **diferente** do C de ACID (respeito a regras/constraints).
- **BASE** (Basically Available, Soft state, Eventually consistent) é o contraponto "relaxado" ao ACID nos NoSQL.
- Referências comuns: MongoDB **CP** (no replica set, com `writeConcern: "majority"`), Cassandra **AP** (eventual), Redis **CP** quando single-node/sentinel. O edital quer a **capacidade de justificar a escolha**, não decorar rótulos.

## 3. Cache e busca textual (1.3)

### 3.1 Cache

Armazenar o resultado de uma operação cara para servir rapidamente em acessos futuros.

- **Padrões:** *cache-aside* (aplicação lê cache → se ausente, lê o banco e popula o cache), *read-through*, *write-through* (escreve no cache e no banco), *write-behind/write-back* (escreve no cache e depois propaga).
- **TTL** (tempo de vida) e **invalidação** (remover chaves quando o dado muda) são os grandes desafios — cache **obsoleto** é pior que ausente.
- **Penetração/avalanche/stampede:** chave inexistente, expiração em massa, rajada de requisições simultâneas (mitigar com valores sentinela, TTL com jitter, bloqueio).
- Ferramentas: **Redis/Memcached** (servidor), **cache local** (em memória da JVM — Caffeine), **cache de 2º nível do Hibernate**.

### 3.2 Busca textual — Elasticsearch

- **Elasticsearch** é um motor de busca/análise distribuído construído sobre **Apache Lucene**. Conceitos: **índice**, **documento** (JSON), **mapping** (tipos), **shards/replicas**, **nó/cluster**.
- O coração é o **índice invertido**: um dicionário que mapeia **termo → lista de documentos**. Requer **análise** do texto: *tokenização*, *lowercase*, remoção de *stopwords*, *stemming* ("correndo"→"corr").
- **Relevância:** score **BM25** (TF-IDF moderno) ordena resultados; suporta *full-text query* (`match`), *bool* (must/should/filter), agregações, *autocomplete* (*edge n-gram*), *fuzzy*, *highlight*.
- É **diferente de um banco relacional**: busca por relevância em texto livre, não por chaves/joins. RDBMS cuida da "verdade"; o Elasticsearch costuma ser um **índice derivado/assíncrono** da fonte.

## 4. Escolha de armazenamento conforme uso (1.4)

Critérios práticos para decidir:

| Critério | Aponta para |
| --- | --- |
| Transações ACID / joins complexos | Relacional (PostgreSQL, MySQL, SQL Server, Oracle) |
| Escala horizontal massiva de escrita | NoSQL distribuído (Cassandra, DynamoDB, MongoDB sharded) |
| Latência de microsegundos / cache | Chave-valor em memória (Redis, Memcached) |
| Texto livre + relevância | Elasticsearch (busca) |
| Semântica / RAG / recomendação | Vetorial (pgvector, Qdrant, Pinecone) |
| Analytics/agregações em volume | Colunar (Parquet, ClickHouse, BigQuery, Redshift) |
| Arquivos/binários grandes | Object storage (S3), não o banco |

**Heurísticas que a banca gosta de cobrar:** "preciso de NoSQL" muitas vezes é "preciso de **índice**" (um *full scan* corrigido por B-tree/índice parcial); "esquema flexível" pode ser **JSONB + GIN** no PostgreSQL; a escolha segue **o padrão de acesso** (leitura por chave vs. varredura vs. agregação) e os **requisitos de consistência/disponibilidade** (CAP).

## 5. Transações, concorrência, consistência e evolução de esquemas (1.5)

### 5.1 ACID

- **Atomicidade:** tudo ou nada (ou todas as operações aplicam, ou nenhuma). *Rollback* desfaz.
- **Consistência:** a transação leva o banco de um estado válido a outro válido (respeita constraints/invariantes).
- **Isolamento:** transações concorrentes não interferem entre si "como se" rodassem em série.
- **Durabilidade:** efeitos de uma transação *committed* sobrevivem a falhas (log WAL, disco).

### 5.2 Níveis de isolamento e fenômenos

| Nível | Dirty read | Non-repeatable read | Phantom read |
| --- | --- | --- | --- |
| READ UNCOMMITTED | Possível | Possível | Possível |
| READ COMMITTED | Não | Possível | Possível |
| REPEATABLE READ | Não | Não | Possível* |
| SERIALIZABLE | Não | Não | Não |

- **Dirty read:** ler dado não *committed* de outra transação.
- **Non-repeatable read:** reler a mesma linha e obter valor diferente (outra transação alterou/*commitou*).
- **Phantom read:** reexecutar uma consulta e obter **conjunto de linhas** diferente (outra transação inseriu/removeu).
- **PostgreSQL:** default é **READ COMMITTED**; implementa via **MVCC**. `READ UNCOMMITTED` comporta-se como READ COMMITTED; **REPEATABLE READ no PG já não permite phantom** (mais forte que o padrão SQL). Ver Item 2.
- **Concorrência otimista** (versiona, compara no *commit* — `@Version`) × **pessimista** (locks `SELECT ... FOR UPDATE`). **Deadlock:** dois processos esperam locks um do outro; SGBD detecta e aborta um (*deadlock victim*). Mitigar com ordem consistente de acesso e transações curtas.
- **MVCC** (Multi-Version Concurrency Control): cada transação vê um *snapshot* consistente; leitores não bloqueiam escritores e vice-versa (base do PostgreSQL e de parte dos SGBDs modernos).

### 5.3 Evolução de esquemas

- **Migrações versionadas:** cada mudança de schema é um arquivo ordenado e versionado (**Flyway**, **Liquibase**), aplicado de forma idempotente e registrado numa tabela de histórico (`flyway_schema_history`).
- Estratégias: *expand-and-contract* (adicionar coluna nova → popular → remover a antiga) para evitar quebra; migrações **não-destrutivas** em produção; *blue-green* de banco quando necessário.

## 6. Persistência em Java com JPA (1.6)

### 6.1 Mapeamento de entidades e relacionamentos

```java
@Entity
public class Pedido {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @ManyToOne(fetch = FetchType.LAZY)            // N:1
    private Cliente cliente;

    @OneToMany(mappedBy = "pedido", cascade = CascadeType.ALL, orphanRemoval = true)
    private List<Item> itens;
}

@Entity
public class Item {
    @Id @GeneratedValue private Long id;

    @ManyToOne private Pedido pedido;             // lado dono do N:1
}
```

- **`@Entity`** marca a classe persistível; **`@Id`** a PK; **`@GeneratedValue`** define a estratégia de geração: `AUTO`, `IDENTITY` (auto-incremento do banco), `SEQUENCE` (sequence, recomendado no PostgreSQL/Oracle) e `TABLE` (tabela emuladora).
- **Relacionamentos:**
  - **`@ManyToOne`** (N:1) — o mais comum; dono da FK.
  - **`@OneToMany`** (1:N) — usa **`mappedBy`** para apontar o lado dono, evitando tabela de junção espúria.
  - **`@OneToOne`** (1:1) — FK num dos lados.
  - **`@ManyToMany`** (N:M) — gera tabela de junção; `@JoinTable` para customizar.
- **Dono do relacionamento (*owning side*):** o lado que possui a FK; `mappedBy` indica o lado **inverso** (só leitura da relação). Errar `mappedBy` gera tabelas/colunas duplicadas.
- **`cascade`** propaga operações (`PERSIST`, `MERGE`, `REMOVE`, `REFRESH`, `DETACH`, `ALL`); **`orphanRemoval = true`** remove o filho quando ele sai da coleção (distinto de `CascadeType.REMOVE`).

### 6.2 Ciclo de vida das entidades

| Estado | Significado | Como chega |
| --- | --- | --- |
| **New (transient)** | Instância criada com `new`, sem identidade, fora do contexto. | `new Pedido()` |
| **Managed (persistent)** | Associada ao **contexto de persistência**; mudanças são sincronizadas no *flush*. | `em.persist()`, `em.find()`, `em.merge()`, consultas |
| **Detached** | Tem identidade, mas **não** está mais no contexto. | `em.detach()`, `em.clear()`, fechamento do `EntityManager` |
| **Removed** | Marcada para exclusão; DELETE no *commit*. | `em.remove()` |

- Operações do `EntityManager`: `persist` (new→managed), `find` (busca por PK), `merge` (detached→copia para managed), `remove` (managed→removed), `refresh` (recarrega do banco), `detach`/`clear` (managed→detached).
- `persist` sobre entidade **detached** lança exceção; `remove` sobre detached também (JPA). `merge` **retorna** a instância managed (não muda a original passada).
- **Flush:** sincronização do contexto com o banco (envia INSERT/UPDATE/DELETE pendentes), podendo ocorrer antes do *commit* (auto-flush antes de queries).

### 6.3 Contexto de persistência e transações

- **Persistence context** = conjunto de instâncias managed; garante que para uma dada **identidade** (tipo + PK) há **no máximo uma instância** (cache de 1º nível do Hibernate).
- **Escopos:** *transaction-scoped* (um contexto por transação; padrão no Spring) e *extended* (contexto sobrevive a várias transações).
- `PersistenceUnit`/`EntityManagerFactory` (pesado, um por app) → `EntityManager` (leve, um por transação).
- **Transações:** *resource-local* (controla com `EntityTransaction`/`PlatformTransactionManager`) ou **JTA** (gerenciada pelo container). No Spring, **`@Transactional`** delimita a transação.
- **JPQL** (consultas sobre entidades, não tabelas) e **Criteria API** (type-safe programática); `TypedQuery`. JPQL não tem `FROM tabela`, e sim `FROM Entidade` (com alias), suportando joins por navegação.

## 7. Estratégias de carregamento (1.7)

### 7.1 Lazy × Eager

- **`FetchType.EAGER`:** carrega a associação **junto** com a entidade (sempre). Rápido no ponto de uso, mas pode carregar um grafo inteiro de objetos sem necessidade (desperdício).
- **`FetchType.LAZY`:** carrega a associação **sob demanda** (proxy/coleção), no primeiro acesso.
- **Defaults:** `@ManyToOne` e `@OneToOne` são **EAGER**; `@OneToMany` e `@ManyToMany` são **LAZY** (padrões JPA). **Boas práticas:** usar LAZY em coleções e associações, e carregar explicitamente o necessário.

### 7.2 N+1 problem

Ocorre quando uma consulta traz **N** entidades e, para cada uma, dispara **+1** consulta para carregar a associação lazy → **N+1 queries** em vez de 1.

- **Correções:**
  - **`JOIN FETCH`** (JPQL): `SELECT p FROM Pedido p JOIN FETCH p.itens` — traz tudo numa consulta.
  - **`@EntityGraph`** — define grafo de carregamento por anotação/API, reutilizável em consultas derivadas.
  - **Batch fetching** (`hibernate.default_batch_fetch_size`) — carrega associações em lotes com `IN`.
  - **DTOs/projeções** — trazer só as colunas necessárias (`SELECT NEW ...`), evitando carregar entidades inteiras.
- **Cuidado:** `JOIN FETCH` em coleção + paginação pode dar resultados/contagens errados (duplicação de linhas). Efeitos de **correção** (dado certo) e **desempenho** (menos round-trips) são o ponto do edital.

## 8. Spring Data JPA (1.8)

### 8.1 Repositórios

```java
public interface PedidoRepository extends JpaRepository<Pedido, Long> { }
```

- Hierarquia: **`Repository`** (marcador) → **`CrudRepository`** (`save`, `findById`, `findAll`, `delete`, `count`) → **`PagingAndSortingRepository`** (`findAll(Sort)`, `findAll(Pageable)`) → **`JpaRepository`** (extensões JPA: `saveAndFlush`, `flush`, `deleteAllInBatch`, …).
- **`ListCrudRepository`/`ListPagingAndSortingRepository`** (Spring Data 3) retornam `List` em vez de `Iterable`.
- Implementação padrão: **`SimpleJpaRepository`**; configurada por **`@EnableJpaRepositories`** (base packages, estratégia de lookup).

### 8.2 Consultas derivadas (query methods)

- O nome do método vira a consulta: `findByNomeAndAtivoOrderByDataCriacaoDesc(String, boolean)`.
- Palavras-chave: `findBy/readBy/queryBy`, `And/Or`, `Between`, `LessThan/GreaterThan`, `Like`, `Containing`, `In`, `IgnoreCase`, `OrderBy...Asc/Desc`, `Top/Limit`, `Distinct`, `First`, `Exists`, `CountBy`, `DeleteBy/RemoveBy`.
- **Estratégia de lookup** (`queryLookupStrategy`): `CREATE` (deriva do nome), `USE_DECLARED_QUERY` (só `@Query`), `CREATE_IF_NOT_FOUND` (padrão).

### 8.3 `@Query`, modificação e paginação

```java
@Query("SELECT p FROM Pedido p WHERE p.cliente.id = :clienteId AND p.status = :status")
Page<Pedido> porCliente(@Param("clienteId") Long clienteId, @Param("status") Status s, Pageable pageable);

@Modifying
@Query("UPDATE Pedido p SET p.status = :status WHERE p.id IN :ids")
int marcarEncerrados(@Param("ids") List<Long> ids, @Param("status") Status s);

@Query(value = "SELECT * FROM pedido WHERE valor > :v", nativeQuery = true)
List<Pedido> caros(@Param("v") BigDecimal v);
```

- **`@Query`** aceita **JPQL** ou **SQL nativo** (`nativeQuery = true`). **`@Modifying`** + `@Transactional` para `UPDATE`/`DELETE`; `@Modifying(clearAutomatically = true, flushAutomatically = true)` para coerência do contexto.
- **Paginação:** `Pageable`/`Page` (faz **count query** extra → sabe o total), `Slice` (só sabe se há próxima página, mais leve), `Sort`; `PageRequest.of(page, size, sort)`. Retorno `Page`/`Slice`/`List` (neste último, ignora a contagem).
- Projeções (interface, DTO), `@EntityGraph`, *specifications* (critérios dinâmicos), *query by example*.

## 9. Integração da camada de persistência às regras de negócio (1.9)

- **Separação de camadas:** serviços de domínio orquestram **regras de negócio**; **repositórios** encapsulam acesso a dados. O domínio **não** deve vazar SQL/JPQL; o repositório não deve conter regra de negócio.
- **Fronteira transacional:** `@Transactional` fica no **serviço** (não no repositório), para que toda a regra seja **atômica** — ou a operação inteira comita, ou nada.
- **Agregados** (DDD): persistir/validar o agregado como unidade de consistência (cuidar `cascade` + `orphanRemoval`).
- **DTOs vs entidades:** exponha **DTOs** na borda; não serialize entidades JPA diretamente (evita `LazyInitializationException`, N+1 acidental e exposição de dados — ver Item 4).
- **Idempotência e concorrência:** `@Version` (lock otimista) para evitar perda de atualização; evitar efeitos colaterais em *getters*; não fazer chamadas remotas dentro de transação longa.
- **Anti-padrões:** lógica de negócio no *controller*, transação no *repository*, contexto de persistência aberto demais (OSIV — *Open Session In View*), consultas de negócio espalhadas no serviço.

## Detalhes que merecem destaque

- **Chave candidata é a superchave mínima**; PK é a candidata escolhida; FK materializa o relacionamento.
- **2FN só faz sentido com PK composta** (dependência parcial). **3FN** elimina dependência **transitiva**.
- **Integridade referencial = FK aponta para PK existente ou NULL**; ações `ON DELETE CASCADE/SET NULL/RESTRICT`.
- **Documental (MongoDB)** é atômico por **documento**; embute (embedding) em vez de `JOIN`.
- **Redis é single-threaded** no núcleo → operações atômicas por construção; velocidade na casa de ~100k–1M ops/s.
- **CAP:** sob **partição (P)**, escolhe-se **C** ou **A**; o "C" do CAP (replicação) ≠ "C" do ACID (constraints).
- **Elasticsearch** = busca por **relevância** (índice invertido + BM25), não um banco transacional.
- **Isolamento:** PG default = **READ COMMITTED**; MVCC faz leitores não bloquearem escritores.
- **Ciclo de vida JPA:** `new` → (persist) → `managed` → (detach/clear/close) → `detached` → (merge) → `managed` → (remove) → `removed` → (commit) → deletado.
- **`mappedBy`** marca o lado **inverso** (não dono); o lado dono tem a FK.
- **N+1:** resolver com **`JOIN FETCH`**, **`@EntityGraph`**, **batch fetching** ou **projeções/DTO**.
- **Spring Data:** `Page` dispara **count query** extra; `Slice` é mais leve (não conta).
- **Transação no serviço**, não no repositório; agregado como unidade de persistência.

## Comparações que a banca costuma cobrar (certo/errado)

| Conceito A | Conceito B | Diferença-chave |
| --- | --- | --- |
| Chave candidata | Chave primária | Candidata = mínima que identifica; primária = a candidata escolhida |
| 2FN | 3FN | 2FN remove dependência **parcial** (PK composta); 3FN remove **transitiva** |
| MER | Modelo lógico/relacional | MER é conceitual (entidades/relacionamentos); lógico vira tabelas/chaves |
| Integridade de entidade | Integridade referencial | Entidade = PK única/não-nula; referencial = FK válida |
| MongoDB (documental) | Redis (chave-valor) | Documento JSON auto-descritivo × mapa chave→valor em memória |
| Relacional (SQL) | Documental (NoSQL) | Esquema fixo + joins + ACID × esquema flexível + documento atômico |
| Vetorial | Busca textual (Elasticsearch) | Similaridade **semântica** (vetores) × relevância por **termo** (invertido) |
| ACID | BASE | Forte consistência × *Basically Available, Soft state, Eventually consistent* |
| C (CAP) | C (ACID) | CAP: consistência de réplica; ACID: respeito a regras/invariantes |
| Consistência (CP) | Disponibilidade (AP) | Sob partição, sacrifica A ou sacrifica C imediato |
| Concorrência otimista | Concorrência pessimista | Otimista versiona e checa no commit; pessimista bloqueia (`FOR UPDATE`) |
| Dirty read | Phantom read | Dirty = lê não-commitado; phantom = conjunto de linhas muda |
| `persist` | `merge` | persist = new→managed; merge = detached→copia managed (retorna cópia) |
| `CascadeType.REMOVE` | `orphanRemoval` | Cascade remove o referenciado; orphan remove quem saiu da coleção |
| LAZY | EAGER | LAZY carrega sob demanda; EAGER carrega junto (risco de grafo desnecessário) |
| `JOIN FETCH` | `@EntityGraph` | Ambos evitam N+1; EntityGraph é declarativo/reutilizável |
| `CrudRepository` | `JpaRepository` | Crud = CRUD genérico; JPA = extensões + paginação + flush/batch |
| `Page` | `Slice` | Page conhece total (count extra); Slice só se há próxima página |
| JPQL | SQL nativo (`nativeQuery`) | JPQL sobre **entidades**; nativo sobre **tabelas/colunas** |

## Pegadinhas e erros comuns

> Cuidado com termos absolutos ("sempre", "nunca", "exclusivamente") e com a troca de requisitos.

- Dizer que **NoSQL é sempre mais rápido** que SQL — depende do padrão de acesso; NoSQL é troca de garantias, não "upgrade" universal.
- Afirmar que **CAP permite ter C, A e P ao mesmo tempo** — sob partição, só 2; e confundir o **C do CAP com o C do ACID**.
- Achar que **normalizar sempre** é obrigatório — desnormalização é **deliberada** e legítima em analytics.
- Confundir **2FN com 3FN** (parcial × transitiva), ou aplicar 2FN a uma PK simples.
- Dizer que **documental não tem transações** — MongoDB tem transações multi-documento (apesar do padrão single-document).
- Achar que **Redis guarda só strings** — tem lists, sets, sorted sets, hashes, streams, etc.
- Supor que **Elasticsearch substitui o banco relacional** como fonte de verdade — ele costuma ser índice derivado/assíncrono.
- Confundir **cache com banco** — cache pode ficar obsoleto; invalidação/TTL são obrigatórios.
- Dizer que **`@ManyToOne` é LAZY por padrão** — é **EAGER** (assim como `@OneToOne`); LAZY é padrão de `@OneToMany`/`@ManyToMany`.
- Esquecer que **`merge` retorna a cópia managed** e não altera a instância passada (que segue detached).
- Chamar **`persist`/`remove` em entidade detached** — lança `IllegalArgumentException` (JPA).
- Achar que **`JOIN FETCH` + Pageable** sempre funciona em coleções — pode duplicar linhas/errar a contagem.
- Dizer que **`Page` não dispara consulta extra** — ela **conta** o total (count query); `Slice` não.
- Esquecer que **`@Modifying` precisa de `@Transactional`** (e `flushAutomatically`/`clearAutomatically` para coerência).
- Colocar **regra de negócio no repositório** ou **transação no repositório** — a fronteira é o serviço.
- Achar que **`mappedBy` fica no lado dono** — fica no lado **inverso** (não dono da FK).
- Confundir **`orphanRemoval` (saiu da coleção) com `CascadeType.REMOVE` (remove o referenciado)**.

## Notas atômicas relacionadas

```dataview
LIST FROM "20 - Notas"
WHERE disciplina = this.disciplina
  AND contains(tema, this.tema)
SORT file.name ASC
```

## Fontes

- https://jakarta.ee/specifications/persistence/ — Jakarta Persistence (especificação JPA), entidades, ciclo de vida, JPQL, transações.
- https://jakarta.ee/specifications/persistence/3.2/apidocs/jakarta.persistence/jakarta/persistence/entitymanager — Javadoc do `EntityManager` (estados new/managed/detached/removed, persist/merge/remove).
- https://hibernate.org/orm/documentation/ — Documentação do Hibernate ORM (provedor JPA de referência).
- https://docs.hibernate.org/devguide/en-US/html/ch03.html — Hibernate Dev Guide, cap. 3: persistence contexts e estados das entidades.
- https://docs.spring.io/spring-data/jpa/reference/ — Spring Data JPA Reference (repositórios, query methods, `@Query`, paginação).
- https://docs.spring.io/spring-data/commons/reference/repositories/query-methods-details.html — Query derivation (estratégias CREATE/USE_DECLARED_QUERY/CREATE_IF_NOT_FOUND).
- https://www.mongodb.com/docs/ — Documentação oficial do MongoDB (documentos, coleções, réplicas, sharding).
- https://www.mongodb.com/resources/basics/databases/cap-theorem — MongoDB: explicação do CAP theorem e trade-offs C/A/P.
- https://redis.io/docs/latest/ — Documentação do Redis (estruturas de dados, persistência RDB/AOF, TTL).
- https://www.elastic.co/guide/en/elasticsearch/reference/current/index.html — Elasticsearch Reference (índice invertido, análise, relevância BM25).
- https://www.postgresql.org/docs/current/transaction-iso.html — PostgreSQL: níveis de isolamento e fenômenos (dirty/non-repeatable/phantom).
- https://www.postgresql.org/docs/current/mvcc.html — PostgreSQL: MVCC (controle de concorrência multiversão).
- https://en.wikipedia.org/wiki/CAP_theorem — CAP theorem (Brewer 2000; prova de Gilbert & Lynch 2002).
- https://en.wikipedia.org/wiki/Database_normalization — Normalização (1FN/2FN/3FN/BCNF) e dependências funcionais.
