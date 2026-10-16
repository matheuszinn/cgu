---
tipo: resumo
disciplina: "Persistência, Integração e Proteção de Dados"
tema: "SQL e desempenho"
status: novo
data: "2026-10-16"
tags: [resumo, persistencia-dados, cgu-2026]
---

# Resumo: SQL e desempenho

> [!info] MOC: [[Persistência, Integração e Proteção de Dados]]
> Edital nº 1/2026 – CGU – AFFC · **Conhecimentos específicos** · Cargo 4 (TI / Desenvolvimento de Sistemas) · Item 2 — *SQL e desempenho*.

## Escopo no edital (checklist)

- [x] 2.1 Definição e manipulação de dados, controle de acesso e transações.
- [x] 2.2 Consultas com filtros, junções, agregações, subconsultas e expressões de tabela comuns.
- [x] 2.3 Índices, planos de execução, valores nulos e duplicações.
- [x] 2.4 Diagnóstico de consultas e efeitos sobre o desempenho da aplicação.

## Resumo

O item trata de **SQL** em dois níveis: a **linguagem** (as sublinguagens e as construções de consulta) e o **desempenho** (índices, planos e diagnóstico). Os quatro pilares:

1. **Sublinguagens SQL:** **DDL** (definição — `CREATE/ALTER/DROP/TRUNCATE`), **DML** (manipulação — `SELECT/INSERT/UPDATE/DELETE`), **DCL** (controle de acesso — `GRANT/REVOKE`) e **TCL** (controle de transação — `BEGIN/COMMIT/ROLLBACK/SAVEPOINT`).
2. **Consultas:** `WHERE`, **junções** (`INNER/LEFT/RIGHT/FULL/CROSS`), **agregações** (`GROUP BY` + `HAVING`), **subconsultas** (escalar/linha/tabela, correlacionadas), **CTEs** (`WITH ... AS`, inclusive recursivas) e operadores de conjunto (`UNION`/`INTERSECT`/`EXCEPT`).
3. **Índices e planos:** índices **B-tree** (e variações), `EXPLAIN`/planos de execução, semântica de **NULL** (lógica de três valores) e tratamento de **duplicações** (`DISTINCT`, `GROUP BY`, `UNION` × `UNION ALL`).
4. **Diagnóstico:** como identificar consultas lentas, *full scan*, falta de índice, problema N+1 e efeitos de ORM, conectando tudo ao desempenho da aplicação.

## 1. Definição, manipulação, controle de acesso e transações (2.1)

### 1.1 As sublinguagens SQL

| Sublinguagem | Comandos | Papel |
| --- | --- | --- |
| **DDL** (Data Definition) | `CREATE`, `ALTER`, `DROP`, `TRUNCATE`, `RENAME` | Estrutura (tabelas, índices, views, schemas) |
| **DML** (Data Manipulation) | `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `MERGE`/`UPSERT` | Dados (linhas) |
| **DCL** (Data Control) | `GRANT`, `REVOKE` | Permissões (acesso) |
| **TCL** (Transaction Control) | `BEGIN`/`START TRANSACTION`, `COMMIT`, `ROLLBACK`, `SAVEPOINT` | Transações |

- **`TRUNCATE`** × `DELETE`: `TRUNCATE` remove todas as linhas rapidamente (DDL, geralmente sem gatilho de linha e não-rollbackável da mesma forma em alguns SGBDs); `DELETE` é DML, pode ter `WHERE` e é transacional por linha.
- **`DROP`** remove o objeto (tabela/índice) inteiro; **`DELETE`** remove linhas mantendo a tabela.

### 1.2 Controle de acesso — `GRANT` / `REVOKE`

```sql
GRANT SELECT, INSERT ON pedido TO app_user;
GRANT SELECT ON pedido TO analista WITH GRANT OPTION;
REVOKE INSERT ON pedido FROM app_user;
```

- Concede/revoga **privilégios** a **usuários/roles**. Privilégios comuns: `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `TRUNCATE`, `REFERENCES`, `TRIGGER`, `EXECUTE`, `USAGE`, `CREATE`, `CONNECT`.
- **`WITH GRANT OPTION`** permite repassar o privilégio; **`REVOKE ... CASCADE`** propaga a revogação.
- Boas práticas: **menor privilégio**, usar **roles** (não conceder a usuários individuais), evitar `GRANT ALL`, separar conta de aplicação da de administração (princípio do Item 4).

### 1.3 Transações — `BEGIN` / `COMMIT` / `ROLLBACK` / `SAVEPOINT`

```sql
BEGIN;
  UPDATE conta SET saldo = saldo - 100 WHERE id = 1;
  UPDATE conta SET saldo = saldo + 100 WHERE id = 2;
  SAVEPOINT depois_transferencia;
  -- algo deu errado:
  ROLLBACK TO SAVEPOINT depois_transferencia;  -- desfaz só até o ponto
COMMIT;  -- ou ROLLBACK para desfazer tudo
```

- **`COMMIT`** torna as mudanças permanentes; **`ROLLBACK`** as desfaz; **`SAVEPOINT`** cria ponto de retorno parcial.
- **ACID:** Atomicidade, Consistência, Isolamento, Durabilidade (ver Item 1). **`SET TRANSACTION ISOLATION LEVEL ...`** ajusta o isolamento (`READ COMMITTED`, `REPEATABLE READ`, `SERIALIZABLE`).
- **`SELECT ... FOR UPDATE` / `FOR SHARE`** — *row lock* para concorrência pessimista.
- Diferenças entre SGBDs: PostgreSQL usa `BEGIN`; MySQL/InnoDB usa `START TRANSACTION`; SQL Server usa `BEGIN TRANSACTION`.

## 2. Consultas: filtros, junções, agregações, subconsultas, CTEs (2.2)

### 2.1 Filtros — `WHERE`

- `WHERE` filtra **antes** da agregação; `HAVING` filtra **depois** (sobre grupos). Ordem lógica de avaliação: `FROM` → `WHERE` → `GROUP BY` → `HAVING` → `SELECT` → `ORDER BY` → `LIMIT/OFFSET`.
- Operadores: `=`, `<>`/`!=`, `<`, `>`, `<=`, `>=`, `BETWEEN`, `IN`, `LIKE`/`ILIKE` (padrão `%`/`_`), `IS NULL`, `EXISTS`, `ANY`/`ALL`.
- **`LIKE '%texto%'`** impede uso de índice B-tree comum (busca de prefixo `'texto%'` ainda pode usar).

### 2.2 Junções

```sql
SELECT c.nome, p.valor
FROM cliente c
INNER JOIN pedido p ON p.cliente_id = c.id;          -- só linhas com correspondência
```

| Junção | Retorna |
| --- | --- |
| **INNER JOIN** | Apenas linhas com correspondência nos dois lados |
| **LEFT (OUTER) JOIN** | Todas da esquerda + correspondentes da direita (NULL se não houver) |
| **RIGHT (OUTER) JOIN** | Todas da direita + correspondentes da esquerda |
| **FULL (OUTER) JOIN** | Todas de ambos os lados (NULL onde não houver) |
| **CROSS JOIN** | Produto cartesiano (todas as combinações) |
| **SELF JOIN** | Junção da tabela consigo mesma (ex.: gerente × subordinado) |

- **`LEFT JOIN` + `WHERE t.col IS NULL`** é o padrão clássico para achar "os que **não** têm correspondência" (anti-join).
- O `ON` define a condição da junção; `WHERE` filtra o resultado. Com `OUTER JOIN`, colocar a condição no `ON` × no `WHERE` muda o resultado (filtro no `WHERE` pode transformar LEFT em INNER na prática).

### 2.3 Agregações — `GROUP BY` / `HAVING`

```sql
SELECT cliente_id, COUNT(*) AS total, SUM(valor) AS soma
FROM pedido
WHERE status = 'PAGO'          -- antes do agrupamento
GROUP BY cliente_id
HAVING SUM(valor) > 1000;      -- depois do agrupamento
```

- Funções de agregação: `COUNT`, `SUM`, `AVG`, `MIN`, `MAX`. `COUNT(*)` conta linhas; `COUNT(coluna)` conta **não-nulos**.
- Regra: toda coluna no `SELECT` que **não** está numa agregação deve aparecer no **`GROUP BY`**.
- **`HAVING`** filtra grupos (não pode referenciar coluna "crua" que não esteja no `GROUP BY`); **`WHERE`** filtra linhas antes.

### 2.4 Subconsultas

- **Escalar** (retorna 1 valor): `WHERE salario > (SELECT AVG(salario) FROM emp)`.
- **De linha/coluna**: `WHERE (a, b) = (SELECT ...)`.
- **De tabela** (no `FROM` ou com `IN`): `WHERE id IN (SELECT cliente_id FROM ...)`.
- **Correlacionada:** referencia a tabela externa e é reavaliada por linha — frequentemente mais cara; `EXISTS`/`NOT EXISTS` costumam ser mais eficientes que `IN`/`NOT IN` (sobretudo com NULL).
- **`IN` × `EXISTS`:** semântica parecida para conjuntos sem NULL; `NOT IN` com NULL no subresultado **não retorna nada** (surpresa clássica); `EXISTS` para quando você só quer saber se "existe".
- **`ANY`/`ALL`:** `> ANY(...)` = maior que algum; `> ALL(...)` = maior que todos.

### 2.5 CTEs (`WITH`) e recursão

```sql
WITH total_cliente AS (
  SELECT cliente_id, SUM(valor) AS soma
  FROM pedido GROUP BY cliente_id
)
SELECT c.nome, t.soma
FROM cliente c JOIN total_cliente t ON t.cliente_id = c.id
WHERE t.soma > 500;
```

- **CTE (Common Table Expression)** = subconsulta nomeada e reutilizável na mesma instrução (`WITH ... AS (...)`); melhora legibilidade e permite **CTE recursiva** (`WITH RECURSIVE`) para hierarquias/grafos (ex.: árvore de órgãos, explosão de BOM).
- **`UNION`** (elimina duplicatas, aplica DISTINCT) × **`UNION ALL`** (mantém todas, mais rápido). **`INTERSECT`** (interseção) e **`EXCEPT`/`MINUS`** (diferença).
- **CTE materializada × inlined:** em PostgreSQL, `MATERIALIZED`/`NOT MATERIALIZED` controlam a otimização (mudança de comportamento/perf possível).

## 3. Índices, planos, nulos e duplicações (2.3)

### 3.1 Índices

- **B-tree** (padrão) otimiza igualdade e **intervalos/ordenação** (`=`, `>`, `<`, `BETWEEN`, `ORDER BY`, prefixo `LIKE 'x%'`). É balanceado (altura ~log n).
- **Hash** otimiza apenas **igualdade** (PostgreSQL).
- **GIN/GiST** (PostgreSQL) para arrays, JSONB e texto (*full-text*); **BRIN** para grandes faixas sequenciais.
- **Único** (`UNIQUE`) — garante não duplicação; **composto** (várias colunas); **covering** (inclui colunas extras — *index-only scan*); **parcial** (filtro `WHERE`); **clustered** (ordena fisicamente a tabela — SQL Server/MySQL InnoDB) × **nonclustered**.
- **Trade-off:** índice acelera leitura, mas **custa** escrita (INSERT/UPDATE/DELETE atualizam o índice) e ocupa espaço. **Índice demais piora escrita.**
- Regra do **prefixo à esquerda**: índice `(a, b, c)` serve `a`, `a+b`, `a+b+c`, mas **não** serve consultas só por `b` ou `c`.

### 3.2 Planos de execução — `EXPLAIN`

```sql
EXPLAIN SELECT * FROM pedido WHERE cliente_id = 42;
EXPLAIN (ANALYZE, BUFFERS) SELECT * FROM pedido WHERE valor > 100;
```

- **`EXPLAIN`** mostra o **plano de execução** (sem executar); **`EXPLAIN ANALYZE`** executa e mostra tempos/linhas reais.
- Nós comuns: **Seq Scan** (varredura sequencial — caro em tabelas grandes), **Index Scan**, **Index Only Scan**, **Bitmap Index Scan**, **Nested Loop**, **Hash Join**, **Merge Join**.
- A decisão usa **estatísticas** (histogramas, `ANALYZE`/`VACUUM`), **seletividade** (quantas linhas o filtro retém) e **custo** estimado. Estatística desatualizada → plano ruim.
- Leituras-chave: *seq scan* em tabela grande com filtro seletivo = **falta índice**; `cost`/`rows`/`actual time` para comparar; **buffer/`filter`** indicam trabalho desperdiçado.

### 3.3 Valores nulos (NULL)

- **NULL = "desconhecido/ausente"**, não zero nem string vazia. `NULL = NULL` é **UNKNOWN**, não TRUE → usar **`IS NULL`** / **`IS NOT NULL`**.
- **Lógica de três valores** (3VL): TRUE / FALSE / **UNKNOWN**. Em `WHERE`, só TRUE passa; UNKNOWN é descartado.
- `NULL` em expressões: `NULL + 1 = NULL`; `CONCAT`/`||` (PostgreSQL) ignora NULL; em funções de agregação, `COUNT(*)` conta NULL, `COUNT(col)` não.
- Funções de tratamento: **`COALESCE(a, b, ...)`** (primeiro não-nulo), **`NULLIF(a, b)`** (NULL se iguais — útil contra divisão por zero), `ISNULL`/`NVL` (dialetos).
- **`NOT IN` com NULL** (surpresa): `x NOT IN (1, 2, NULL)` nunca é TRUE. `UNIQUE` permite múltiplos NULL (NULL ≠ NULL) — em PostgreSQL, `UNIQUE` aceita vários NULL; em SQL Server (única coluna) apenas um.

### 3.4 Duplicações

- **`DISTINCT`** elimina duplicatas do resultado (custo de ordenação/hash); **`GROUP BY`** também deduplica, mas é para agregação.
- **`UNION`** deduplica; **`UNION ALL`** mantém. **`DISTINCT` em demasia** costuma mascarar um join/condição errados.
- Duplicação de linhas por **join de 1:N** (uma linha da esquerda × várias da direita) infla somas — corrigir com `DISTINCT`, subconsulta agregada ou `GROUP BY` antes do join.

## 4. Diagnóstico de consultas e efeitos no desempenho (2.4)

### 4.1 Roteiro de diagnóstico

1. **Identificar a consulta lenta** (logs de *slow query*, telemetria/APM, métricas do pool).
2. **Obter o plano** (`EXPLAIN ANALYZE`) e procurar `Seq Scan` em tabela grande com filtro seletivo, `Nested Loop` com muitas execuções, estimativas (`rows`) muito distantes do real.
3. **Verificar índices** (falta, ou existente mas não usado por função na coluna `WHERE func(col)` ou `LIKE '%x%'`).
4. **Atualizar estatísticas** (`ANALYZE`) se o plano está ruim com dados recentes.
5. **Reescrever** (corrigir semântica, usar CTE/subconsulta, mover predicado, evitar DISTINCT/ORDER BY desnecessários, paginar com *keyset* em vez de `OFFSET`).

### 4.2 Problemas clássicos e remédios

| Sintoma | Causa provável | Remédio |
| --- | --- | --- |
| `Seq Scan` em tabela grande com filtro seletivo | Falta índice | Criar índice (B-tree) adequado |
| Índice existe mas não usado | Função na coluna (`LOWER(col)`), `LIKE '%x%'`, conversão de tipo | Índice funcional/expressão, prefixo, trigram (GIN) |
| Estimativa `rows` muito errada | Estatísticas desatualizadas | `ANALYZE`/`VACUUM` |
| N+1 (muitas queries pequenas) | ORM com lazy loading em loop | `JOIN FETCH`, batch, DTO (Item 1.7) |
| Resultado duplicado/soma errada | Join 1:N sem agregação | `GROUP BY`/`DISTINCT` antes do join |
| `OFFSET` grande lento | Paginação por deslocamento | *Keyset/cursor* (`WHERE id > :last`) |
| `SELECT *` puxa tudo | Colunas/`filter` no plano | Projeção só das colunas necessárias |
| Lock/contention, `FOR UPDATE` amplo | Isolamento alto + transações longas | Transações curtas, escopo de lock mínimo |

### 4.3 Efeitos sobre a aplicação

- **Consulta lenta** → transação aberta por mais tempo → **lock** retido → fila de conexões do **pool** esgota → indisponibilidade em cascata.
- **N+1 do ORM** multiplica round-trips de rede e latência (pior ainda com latência de rede alta).
- **`SELECT *`** e paginação errada aumentam I/O, memória e tráfego.
- **Índices mal dimensionados** degradam escrita (cada INSERT atualiza N índices).
- Diagnóstico conecta **banco** (plano/estatística/índice) e **aplicação** (ORM, transação, pool, cache) — é isso que o edital pede em "efeitos sobre o desempenho da aplicação".

## Detalhes que merecem destaque

- **DDL** (estrutura) × **DML** (dados) × **DCL** (acesso) × **TCL** (transação): decorar os comandos de cada grupo.
- **`WHERE` filtra antes, `HAVING` depois** da agregação.
- **`LEFT JOIN ... WHERE t.col IS NULL`** = linhas sem correspondência (anti-join).
- **`IN` × `EXISTS`**: `NOT IN` com NULL retorna vazio; `EXISTS` costuma ser mais eficiente e seguro.
- **`UNION` deduplica, `UNION ALL` não**; `COUNT(*)` inclui NULL, `COUNT(col)` não.
- **`NULL = NULL` é UNKNOWN** → sempre `IS NULL`; lógica de três valores.
- **Índice B-tree** serve igualdade/intervalo/ordenação; **não** serve `LIKE '%x%'` nem coluna dentro de função.
- **Índice composto (a,b,c)**: só funciona pelo **prefixo à esquerda**.
- **`EXPLAIN ANALYZE`** mostra o plano **real**; `Seq Scan` seletivo = falta de índice.
- **`TRUNCATE` ≠ `DELETE`** (estrutura/rápido × linha a linha).
- **`WITH RECURSIVE`** resolve hierarquias (CTE recursiva).
- **Paginar por `OFFSET`** é caro em páginas altas → *keyset* (`WHERE id > último`).

## Comparações que a banca costuma cobrar (certo/errado)

| Conceito A | Conceito B | Diferença-chave |
| --- | --- | --- |
| DDL | DML | DDL define estrutura; DML manipula dados |
| DCL | TCL | DCL controla **acesso** (GRANT/REVOKE); TCL controla **transação** (COMMIT/ROLLBACK) |
| `TRUNCATE` | `DELETE` | TRUNCATE apaga tudo rápido (DDL); DELETE é linha a linha com WHERE (DML) |
| `WHERE` | `HAVING` | WHERE filtra linhas antes; HAVING filtra grupos depois |
| INNER JOIN | LEFT JOIN | INNER = só com correspondência; LEFT = todas da esquerda (NULL à direita) |
| `ON` | `WHERE` (em OUTER JOIN) | ON condiciona a junção; WHERE filtra o resultado (pode "matar" o OUTER) |
| `GROUP BY` | `DISTINCT` | GROUP BY agrega; DISTINCT só deduplica |
| `COUNT(*)` | `COUNT(coluna)` | COUNT(*) conta linhas; COUNT(col) ignora NULL |
| Subconsulta escalar | Subconsulta correlacionada | Escalar devolve 1 valor; correlacionada referencia a query externa por linha |
| `IN` | `EXISTS` | IN compara conjunto; EXISTS só testa existência (seguro com NULL) |
| `NOT IN` (com NULL) | `NOT EXISTS` | NOT IN pode retornar vazio com NULL; NOT EXISTS é previsível |
| CTE | Subconsulta no FROM | CTE é nomeada/reutilizável/recursiva; subconsulta é inline |
| `UNION` | `UNION ALL` | UNION elimina duplicatas; UNION ALL mantém (mais rápido) |
| Índice B-tree | Índice hash | B-tree = igualdade+intervalo+ordenação; hash = só igualdade |
| Índice único | Índice não-único | Único impõe constraint de unicidade; não-único só acelera |
| `EXPLAIN` | `EXPLAIN ANALYZE` | EXPLAIN mostra plano estimado; ANALYZE executa e mostra real |
| Seq Scan | Index Scan | Seq = varredura total; Index = acesso via índice |
| `NULL` | Zero / string vazia | NULL = ausente/desconhecido; não é 0 nem '' |
| `IS NULL` | `= NULL` | `IS NULL` testa nulo; `= NULL` é sempre UNKNOWN |
| Paginação `OFFSET` | Paginação *keyset* | OFFSET degrada em páginas altas; keyset usa `WHERE id > último` |

## Pegadinhas e erros comuns

> Cuidado com termos absolutos ("sempre", "nunca", "exclusivamente") e com a troca de requisitos.

- Dizer que **`DELETE` e `TRUNCATE` são equivalentes** — TRUNCATE é DDL, remove tudo, costuma ser mais rápido e não aciona gatilhos por linha.
- Confundir **`WHERE` com `HAVING`** (antes × depois da agregação).
- Achar que **`LEFT JOIN` com condição no `WHERE`** preserva todas as linhas da esquerda — o filtro no `WHERE` pode eliminar as linhas sem correspondência.
- Supor que **`NOT IN` funciona bem com NULL** — `x NOT IN (1,2,NULL)` nunca é TRUE.
- Usar **`= NULL`** em vez de **`IS NULL`**.
- Achar que **`COUNT(*)` ignora NULL** — ele conta todas as linhas; quem ignora é `COUNT(coluna)`.
- Dizer que **`UNION` e `UNION ALL` são iguais em custo** — `UNION` deduplica (mais caro).
- Achar que **qualquer índice acelera qualquer consulta** — `LIKE '%x%'` e funções na coluna ignoram B-tree.
- Supor que **índice (a,b,c) serve consulta só por `b`** — exige prefixo à esquerda.
- Achar que **mais índice é sempre melhor** — índice custa escrita e espaço.
- Confundir **`EXPLAIN` (estimado) com `EXPLAIN ANALYZE` (real)**.
- Dizer que **`GROUP BY` e `DISTINCT` são a mesma coisa** — GROUP BY é para agregação; DISTINCT só remove duplicatas.
- Achar que **subconsulta correlacionada é sempre ruim** — em alguns casos (top-N por grupo) pode ser a melhor opção.
- Supor que **estatísticas desatualizadas não afetam o plano** — afetam (planos ruins por `rows` erradas).
- Confundir **DDL/DML/DCL/TCL** — ponto de decoreba com alta incidência.

## Notas atômicas relacionadas

```dataview
LIST FROM "20 - Notas"
WHERE disciplina = this.disciplina
  AND contains(tema, this.tema)
SORT file.name ASC
```

## Fontes

- https://www.postgresql.org/docs/current/sql.html — PostgreSQL: comandos SQL (DDL/DML/DCL/TCL de referência).
- https://www.postgresql.org/docs/current/ddl.html — PostgreSQL: Data Definition (CREATE/ALTER/DROP, constraints, chaves).
- https://www.postgresql.org/docs/current/dml.html — PostgreSQL: Data Manipulation (INSERT/UPDATE/DELETE).
- https://www.postgresql.org/docs/current/queries-table-expressions.html — PostgreSQL: cláusula FROM, JOINs (INNER/LEFT/RIGHT/FULL/CROSS).
- https://www.postgresql.org/docs/current/queries-with.html — PostgreSQL: WITH/CTE e consultas recursivas.
- https://www.postgresql.org/docs/current/sql-grant.html — PostgreSQL: GRANT (privilégios e controle de acesso).
- https://www.postgresql.org/docs/current/indexes.html — PostgreSQL: índices (B-tree, hash, GIN/GiST, único, multicoluna).
- https://www.postgresql.org/docs/current/using-explain.html — PostgreSQL: EXPLAIN e planos de execução.
- https://www.postgresql.org/docs/current/transaction-iso.html — PostgreSQL: níveis de isolamento e fenômenos de concorrência.
- https://dev.mysql.com/doc/refman/8.4/en/ — MySQL 8.4 Reference Manual (dialeto, InnoDB, índices clustered).
- https://learn.microsoft.com/en-us/sql/ — SQL Server (T-SQL): documentação oficial Microsoft.
- https://use-the-index-luke.com/ — "Use The Index, Luke!" — tutorial clássico sobre indexação e planos de execução.
- https://www.sqlite.org/lang.html — SQLite: linguagem SQL (referência didática e enxuta dos comandos).
- https://en.wikipedia.org/wiki/SQL — Visão geral da linguagem SQL e suas sublinguagens (DDL/DML/DCL/TCL).
