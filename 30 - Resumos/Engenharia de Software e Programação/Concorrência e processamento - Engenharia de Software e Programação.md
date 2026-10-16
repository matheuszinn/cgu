---
tipo: resumo
disciplina: "Engenharia de Software e Programação"
tema: "Concorrência e processamento"
status: novo
data: "2026-10-16"
tags: [resumo, engenharia-software, cgu-2026]
---

# Resumo: Concorrência e processamento

> [!info] MOC: [[Engenharia de Software e Programação]]
> Edital nº 1/2026 – CGU – AFFC · **Conhecimentos específicos** · Cargo 4 (TI / Desenvolvimento de Sistemas) · Item 3 — *Concorrência e processamento*.

## Escopo no edital (checklist)

- [x] 3.1 Concorrência, paralelismo e assincronia.
- [x] 3.2 Condições de corrida e sincronização.
- [x] 3.3 Compartilhamento de estado, bloqueios e falhas.
- [x] 3.4 Correção e desempenho sob requisições concorrentes.

## Resumo

Este item trata de **programação concorrente em Java**: como múltiplas tarefas avançam simultaneamente, os perigos do **estado compartilhado** e as ferramentas para garantir **correção** sem sacrificar **desempenho**. É um dos tópicos que mais gera pegadinhas conceituais.

1. **Concorrência ≠ paralelismo:** concorrência é sobre **estruturar** tarefas que progridem intercaladamente; paralelismo é **executar de fato ao mesmo tempo** (multi-core). **Assincronia** desacopla a execução da espera (I/O).
2. **Condições de corrida** surgem quando threads alteram estado compartilhado sem coordenação; a solução passa por **sincronização** (`synchronized`, `Lock`) e **visibilidade** (`volatile`, *happens-before*).
3. **Compartilhar estado** de forma incorreta leva a **bloqueios** (*deadlock*, *livelock*, *starvation*) e **falhas** sutis de visibilidade/atomicidade.
4. Para **correção e desempenho sob requisições concorrentes**, usam-se **pools de threads** (`ExecutorService`), **programação assíncrona** (`CompletableFuture`), **coleções concorrentes** (`ConcurrentHashMap`) e **imutabilidade**.

## 1. Concorrência, paralelismo e assincronia (3.1)

### 1.1 Distinções conceituais (essenciais)

| Conceito | Definição |
| --- | --- |
| **Concorrência (concurrency)** | Múltiplas tarefas fazem progresso **intercalado**, potencialmente num único núcleo (fatiamento de tempo) |
| **Paralelismo (parallelism)** | Múltiplas tarefas executam **fisicamente ao mesmo tempo** (vários núcleos/CPUs) |
| **Assincronia (asynchrony)** | A operação **não bloqueia** quem a disparou; o resultado chega depois (callback/future) |
| **Multithreading** | Várias **threads** dentro de um mesmo **processo**, compartilhando heap |

- **Concorrência** é uma propriedade de **estrutura** do programa; **paralelismo** é uma propriedade do **hardware/execução**. Dá para ter concorrência sem paralelismo (threads em 1 núcleo) e paralelismo sem concorrência (SIMD, pipeline).
- **CPU-bound** (uso intenso de processador) beneficia-se de **paralelismo** real; **I/O-bound** (espera de rede/disco/banco) beneficia-se de **assincronia** e de mais threads que núcleos.

### 1.2 Processo × thread

- **Processo:** unidade com **memória própria** (espaço de endereçamento isolado); comunicação entre processos exige IPC.
- **Thread:** linha de execução **dentro** de um processo; threads **compartilham heap** (objetos) e têm **stack própria**. Troca de contexto entre threads é mais barata que entre processos.
- **Green threads vs nativas:** na JVM moderna, threads Java são mapeadas para **threads nativas do SO** (1:1); *virtual threads* (Java 21+, JEP 444) barateiam a criação massiva.

### 1.3 Criando threads em Java

```java
// 1) extends Thread
class MinhaThread extends Thread { public void run() { /* ... */ } }

// 2) implements Runnable (preferível — não consome a herança única)
Thread t = new Thread(() -> System.out.println("rodando"));
t.start();                       // inicia a thread; NUNCA chame run() diretamente

// 3) Callable — retorna valor e lança exceção
Callable<Integer> c = () -> 42;
```

- `t.start()` cria nova thread e executa `run()` nela; chamar `t.run()` **diretamente** executa na thread atual (erro clássico).
- **`Runnable`** (void `run()`) vs **`Callable<V>`** (`V call() throws Exception`) — Callable retorna e propaga exceção.

### 1.4 ExecutorService (pool de threads)

Criar threads a cada requisição é caro; o pool **reutiliza** threads.

```java
ExecutorService pool = Executors.newFixedThreadPool(8);   // tamanho fixo
Future<Integer> f = pool.submit(() -> { return 42; });    // Callable
Integer r = f.get();          // bloqueia até terminar (ou timeout: get(1, SECONDS))
pool.shutdown();              // encerra graciosamente (não aceita novas tarefas)
```

- Fábricas: `newFixedThreadPool(n)`, `newCachedThreadPool` (cria sob demanda), `newSingleThreadExecutor`, `newScheduledThreadPool` (agendamento).
- `shutdown()` (deixa as tarefas em andamento terminarem) × `shutdownNow()` (tenta interromper).
- **`Future`**: `get()` (bloqueante), `get(tempo, unidade)` (com timeout), `isDone()`, `cancel(...)`.

### 1.5 Assincronia com CompletableFuture

`CompletableFuture<T>` permite **composição declarativa** de tarefas assíncronas.

```java
CompletableFuture<Integer> futuro = CompletableFuture.supplyAsync(() -> buscarId());
futuro.thenApply(id -> id * 2)              // transforma resultado
      .thenAccept(System.out::println)      // consome resultado
      .exceptionally(ex -> { log(ex); return 0; });  // trata erro

CompletableFuture.allOf(a, b, c).join();    // aguarda todos
```

| Método | Semântica |
| --- | --- |
| `supplyAsync(Supplier)` / `runAsync(Runnable)` | executa assíncrono (pool comum ou executor) |
| `thenApply` | transforma o resultado (retorna novo valor) |
| `thenAccept` / `thenRun` | consome / executa sem valor |
| `thenCompose` | encadeia (achata) outro `CompletableFuture` |
| `thenCombine` | combina dois resultados |
| `exceptionally` / `handle` | trata exceção / sempre executa |
| `allOf` / `anyOf` | aguarda todos / qualquer um |
| `join()` / `get()` | bloqueia pelo resultado (join lança unchecked) |

## 2. Condições de corrida e sincronização (3.2)

### 2.1 Race condition

- **Condição de corrida:** o resultado depende da **ordem/tempo** de execução das threads — ocorre com **estado mutável compartilhado** sem coordenação.
- Clássico `contador++` (leitura-modificação-escrita) **não é atômico**:

```java
class Contador {
    private int c = 0;
    public void incrementar() { c++; }   // c++ = ler, somar, gravar → não atômico!
}
```

Duas threads podem ler `c=0`, ambas somam `1` e gravam `1` → **atualização perdida**.

### 2.2 Sincronização: `synchronized`

- Garante **exclusão mútua** e **visibilidade** de memória (estabelece *happens-before*).
- Aplica-se a **métodos** (`synchronized void m()`) ou **blocos** (`synchronized(lock) { ... }`), usando o **monitor** do objeto.
- O lock é **reentrante** (a mesma thread pode readquirir o monitor que já possui).
- **Bloqueio no menor escopo possível** para reduzir contenção; sincronizar sobre objetos privados (não sobre `this` exposto).

```java
public synchronized void incrementar() { c++; }   // método sincronizado

public void incrementar2() {
    synchronized (this) { c++; }                  // bloco sincronizado
}
```

### 2.3 `volatile` (visibilidade, não atomicidade)

- **`volatile`** garante que toda leitura veja a **última escrita** em qualquer thread (sem cache) e estabelece *happens-before* — **visibilidade**, mas **não atomicidade**.
- `volatile int c; c++` **ainda é condição de corrida** (não é atômico). `volatile` serve para **flags**/estado simples (ex.: `volatile boolean parar`).

### 2.4 Locks explícitos e contadores atômicos

- **`Lock`/`ReentrantLock`:** mais flexível que `synchronized` — `tryLock()` (não bloqueante), `lockInterruptibly()`, `tryLock(tempo, unidade)`, fairness opcional. **Sempre liberar em `finally`**.
- **`ReentrantReadWriteLock`:** múltiplas leituras concorrentes, uma escrita exclusiva.
- **Classes atômicas (`AtomicInteger`, `AtomicLong`, `AtomicBoolean`, `AtomicReference`)** usam **CAS (compare-and-swap)** — operações **atômicas sem bloqueio** (lock-free).

```java
private final AtomicInteger c = new AtomicInteger();
c.incrementAndGet();      // atômico, sem synchronized
c.compareAndSet(esperado, novo);   // CAS
```

### 2.5 Coordenação de threads

- **`Semaphore`:** controla o número de acessos simultâneos a um recurso (`acquire`/`release`).
- **`CountDownLatch`:** espera até um contador chegar a zero (one-shot).
- **`CyclicBarrier`:** várias threads se encontram num ponto comum (reutilizável).
- **`wait`/`notify`/`notifyAll`** (sobre monitor): mecanismo clássico de espera/notificação — sempre **dentro de `synchronized`**, com checagem em laço (`while`).
- **`BlockingQueue`** (`ArrayBlockingQueue`, `LinkedBlockingQueue`): filas thread-safe para **produtor-consumidor** (`put` bloqueia quando cheia, `take` quando vazia).

## 3. Compartilhamento de estado, bloqueios e falhas (3.3)

### 3.1 O modelo de memória Java (JMM)

- **Visibilidade:** sem sincronização, uma thread pode **não ver** as escritas de outra (registradores/caches) — daí a necessidade de `synchronized`/`volatile`.
- **Happens-before:** relação que garante que a escrita de uma ação seja visível à leitura posterior. Regras principais: ordem de programa (na mesma thread), liberação de monitor antes da aquisição, escrita `volatile` antes de leitura `volatile`, `start()` antes de qualquer ação da thread iniciada, término (`join`) após as ações da thread.
- **Atomicidade × visibilidade:** um incremento pode ser "visível" e ainda assim **não atômico** — os dois problemas são distintos.

### 3.2 Bloqueios e falhas de liveness

| Fenômeno | Descrição | Causa típica |
| --- | --- | --- |
| **Deadlock** | Duas ou mais threads bloqueiam-se **mutuamente**, aguardando recursos uma da outra, para sempre | Aquisição de locks em **ordem diferente** |
| **Livelock** | Threads **não bloqueiam**, mas também **não progridem** (ficam reagindo entre si) | Retentativas/backoff mal desenhados |
| **Starvation** | Uma thread **nunca** ganha o recurso (sempre preterida) | Prioridades injustas, fairness ausente |

**As 4 condições do deadlock** (Coffman): **1)** exclusão mútua; **2)** segurar e esperar (hold-and-wait); **3)** não-preempção; **4)** espera circular. **Basta quebrar uma** para evitá-lo — a prática mais comum é **adquirir locks sempre na mesma ordem** e usar `tryLock` com timeout.

```java
// deadlock clássico: duas threads travam A e B em ordem inversa
synchronized (a) { synchronized (b) { ... } }   // thread 1
synchronized (b) { synchronized (a) { ... } }   // thread 2 → deadlock
```

### 3.3 Estado compartilhado seguro

- **Imutabilidade** é a forma mais simples de thread-safety: objetos imutáveis (campos `final`, sem mutação) podem ser compartilhados livremente.
- **Confinamento (thread confinement):** o objeto é acessado por **uma única thread** (ex.: `ThreadLocal`, objetos locais de método).
- **Sincronização explícita** para o estado mutável compartilhado.
- **`ThreadLocal<T>`:** mantém um valor **por thread** (não compartilhado) — útil para contexto, mas cuidado com vazamentos em pools.

### 3.4 Coleções concorrentes e seguras

- **`ConcurrentHashMap`:** map thread-safe com **não bloqueia a leitura** e usa **bloqueio fino/CAS** na escrita (melhor que `synchronizedMap`). **Não permite chave/valor `null`**.
- **`CopyOnWriteArrayList`/`CopyOnWriteArraySet`:** copiam o array a cada escrita — ótimo para **leitura predominante**, ruim para muitas escritas.
- **`ConcurrentLinkedQueue`/`ConcurrentLinkedDeque`:** filas lock-free.
- **`BlockingQueue`** e `BlockingDeque` para produtor-consumidor.
- **Legados sincronizados:** `Vector`, `Hashtable`, `Collections.synchronizedList/Map/Set` — sincronização global (mais contenção); preferir as coleções concorrentes modernas.
- **`StringBuffer`** (sincronizado) vs `StringBuilder` (não) — mesmo raciocínio.

## 4. Correção e desempenho sob requisições concorrentes (3.4)

### 4.1 Corretude em sistemas concorrentes

- **Thread-safety:** um tipo é *thread-safe* se se comporta corretamente sob acesso concorrente, sem coordenação adicional do chamador.
- Princípios: **minimizar estado mutável compartilhado**, **imutabilidade**, **escopos de lock curtos**, e **usar abstrações prontas** (`ConcurrentHashMap`, atômicos) em vez de reinventar.
- **Testes de concorrência** são não-determinísticos: usar cargas altas, detectores de race (ThreadSanitizer), e revisão de *happens-before*.
- **`double-checked locking`** (checar `null` fora e dentro do lock) só é seguro se a referência for **`volatile`** — ou preferir `enum`/holder para singletons.

### 4.2 Desempenho: dimensionamento e contenção

- **Contenção de lock** degrada desempenho quando muitas threads disputam o mesmo monitor → reduzir a **granularidade** (locks menores, `ConcurrentHashMap`) ou evitar o lock (atômicos, imutáveis).
- **Dimensionar o pool:** para **CPU-bound**, ~`núcleos` threads; para **I/O-bound**, mais threads que núcleos (depende da latência). Pool grande demais causa overhead de troca de contexto; pequeno demais subutiliza recursos.
- **Overhead de criação de thread** justifica o pool; **virtual threads (Java 21)** reduzem drasticamente esse custo para tarefas I/O-bound massivas.
- **Amdahl's law:** o ganho do paralelismo é limitado pela **fração serial** do programa — nem tudo paraleliza.
- **Trade-off correção × desempenho:** `synchronized` é simples e correto, mas tem contenção; CAS/lock-free é mais rápido, porém mais difícil de acertar.

### 4.3 Padrões para requisições concorrentes

- **Thread-per-request** (modelo servidor tradicional) × **async/non-blocking** (event loop, reativo) — assíncrono escala melhor para I/O-bound.
- **Produtor-consumidor** com `BlockingQueue` para desacoplar produção e consumo.
- **Fork/Join (`ForkJoinPool`)**: divide-e-conquista recursivo (`RecursiveTask`) para workloads paralelizáveis.
- **Paralelismo de dados:** `Stream.parallelStream()` para operações independentes (cuidado com o pool comum).

```java
// Fork/Join: somar um array em paralelo
class Soma extends RecursiveTask<Long> {
    private final long[] a; private final int lo, hi;
    protected Long compute() {
        if (hi - lo <= LIMIAR) { long s = 0; for (int i = lo; i < hi; i++) s += a[i]; return s; }
        int meio = (lo + hi) / 2;
        Soma esq = new Soma(a, lo, meio); Soma dir = new Soma(a, meio, hi);
        esq.fork();
        return dir.compute() + esq.join();
    }
}
```

### 4.4 Falhas comuns em requisições concorrentes

- **Perda de atualização** (incremento não atômico) → usar `AtomicInteger`/`synchronized`.
- **Leitura de estado inconsistente** (ver o objeto "pela metade") → imutabilidade/sincronização.
- **Deadlock entre pools** ou entre serviços (ordem de lock) → ordem consistente + timeout.
- **Vazamento de threads** (pool nunca `shutdown`) e **starvation** de tarefas em fila.
- **Bloquear a thread de UI/event-loop** com chamadas síncronas pesadas.
- **Compartilhar objetos de infra não-thread-safe** (ex.: `SimpleDateFormat`) entre threads → usar `DateTimeFormatter` (imutável) ou `ThreadLocal`.

## Detalhes que merecem destaque

- **`start()` vs `run()`:** `start()` cria thread nova; `run()` executa na thread **atual** (sem concorrência).
- **`Runnable` (void) × `Callable<V>` (retorna + lança)**: `submit` aceita ambos; só `Callable`/`submit` devolvem `Future`.
- **`synchronized` = exclusão mútua + visibilidade; `volatile` = só visibilidade** (não torna `c++` atômico).
- **`AtomicInteger` usa CAS (lock-free)** — alternativa ao `synchronized` para operações simples.
- **Deadlock tem 4 condições** (exclusão mútua, hold-and-wait, não-preempção, espera circular) — quebrar uma evita; a prática é **ordem consistente de locks**.
- **`ConcurrentHashMap` não permite `null`** (chave ou valor) e **não trava a leitura** — superior a `Hashtable`/`synchronizedMap`.
- **`CopyOnWriteArrayList`** é para **leitura predominante** (copia a cada escrita).
- **Happens-before** é o conceito que rege **visibilidade** no JMM.
- **Imutabilidade = thread-safety "de graça"**; objetos imutáveis podem ser compartilhados livremente.
- **`shutdown()` vs `shutdownNow()`** e a importância de **encerrar o pool** (senão a JVM não termina).
- **`CompletableFuture`** compõe tarefas assíncronas sem bloquear (`thenApply`/`thenCompose`/`allOf`/`exceptionally`).
- **Amdahl's law:** ganho limitado pela fração serial; nem tudo paraleliza.
- **Virtual threads (Java 21)** barateiam threads para I/O-bound massivo.
- **`StringBuilder` é não-thread-safe**; `StringBuffer` é sincronizado (mais lento).

## Comparações que a banca costuma cobrar (certo/errado)

| Conceito A | Conceito B | Diferença-chave |
| --- | --- | --- |
| Concorrência | Paralelismo | Concorrência = estrutura/intercalação; paralelismo = execução simultânea real |
| Assincronia | Paralelismo | Assíncrono desacopla execução da espera; paralelo usa vários núcleos |
| Processo | Thread | Processo tem memória isolada; threads compartilham heap e têm stack própria |
| `start()` | `run()` | `start()` cria nova thread; `run()` roda na thread atual |
| `Runnable` | `Callable` | Runnable retorna void e não lança; Callable retorna valor e lança |
| `synchronized` | `volatile` | synchronized = exclusão + visibilidade; volatile = só visibilidade |
| Atomicidade | Visibilidade | Atômico = indivisível; visível = enxergar a última escrita (problemas distintos) |
| `ReentrantLock` | `synchronized` | ReentrantLock tem `tryLock`/timeout/fairness; synchronized é sintaxe simples |
| `AtomicInteger` | `synchronized` (incremento) | Atômico usa CAS (lock-free); synchronized usa monitor (bloqueante) |
| `ConcurrentHashMap` | `Hashtable`/`synchronizedMap` | CHM bloqueio fino, leitura sem lock; Hashtable trava o map inteiro |
| `CopyOnWriteArrayList` | `synchronizedList` | COW copia na escrita (leitura rápida); syncList trava tudo |
| `StringBuffer` | `StringBuilder` | StringBuffer sincronizado (thread-safe); StringBuilder não (mais rápido) |
| Deadlock | Livelock | Deadlock bloqueia para sempre; livelock não bloqueia mas não progride |
| Deadlock | Starvation | Deadlock = espera mútua; starvation = uma thread nunca é atendida |
| `shutdown()` | `shutdownNow()` | shutdown termina tarefas em curso; shutdownNow tenta interromper |
| `Future.get()` | `CompletableFuture.join()` | get lança exceção checada; join lança unchecked; ambos bloqueiam |
| `thenApply` | `thenCompose` | thenApply transforma valor; thenCompose achata outro CompletableFuture |
| `CountDownLatch` | `CyclicBarrier` | Latch é one-shot (contagem decrescente); barrier é reutilizável |
| Virtual thread | Thread de plataforma | Virtual é leve/barata (I/O-bound); plataforma mapeia 1:1 ao SO |

## Pegadinhas e erros comuns

> Cuidado com termos absolutos ("sempre", "nunca", "exclusivamente") e com a troca de requisitos.

- Dizer que **`volatile` torna `i++` atômico** — garante só **visibilidade**; o incremento continua sendo corrida.
- Achar que **concorrência é o mesmo que paralelismo** — são conceitos distintos (estrutura × execução).
- Chamar **`run()` em vez de `start()`** — não há nova thread.
- Afirmar que **`synchronized` apenas bloqueia** — ele também garante **visibilidade** de memória (happens-before).
- Achar que **`ConcurrentHashMap` permite `null`** — **não permite** (nem chave, nem valor).
- Supor que **`Vector`/`Hashtable` são equivalentes às coleções concorrentes modernas** — são legados com lock global.
- Esquecer de **liberar `Lock` em `finally`** (diferente do `synchronized`, que libera automaticamente).
- Achar que **deadlock só ocorre com `synchronized`** — qualquer lock adquirido em ordem inconsistente pode causar.
- Ignorar a **visibilidade** e achar que basta "atualizar a variável" sem `volatile`/lock.
- Supor que **mais threads = sempre mais rápido** — há overhead de contexto, contenção e o limite de **Amdahl**.
- Achar que **`CompletableFuture.get()` nunca bloqueia** — ele bloqueia até a conclusão (use callbacks para não bloquear).
- Esquecer de **`shutdown()` do `ExecutorService`** — a JVM não encerra com pool ativo.
- Confundir **`CountDownLatch` (one-shot)** com **`CyclicBarrier` (reutilizável)**.
- Compartilhar objetos **não-thread-safe** (ex.: `SimpleDateFormat`, `ArrayList` comum) entre threads sem sincronização.
- Dizer que **imutabilidade exige sincronização** — ao contrário, objetos imutáveis são seguros sem lock.

## Notas atômicas relacionadas

```dataview
LIST FROM "20 - Notas"
WHERE disciplina = this.disciplina
  AND contains(tema, this.tema)
SORT file.name ASC
```

## Fontes

- https://docs.oracle.com/javase/tutorial/essential/concurrency/ — The Java Tutorials: Concurrency (threads, sincronização, liveness, executors).
- https://docs.oracle.com/javase/tutorial/essential/concurrency/executors.html — Executors, thread pools e `ExecutorService`.
- https://docs.oracle.com/javase/tutorial/essential/concurrency/atomic.html — Atomic access (`AtomicInteger`, CAS, visibilidade).
- https://docs.oracle.com/javase/tutorial/essential/concurrency/locksync.html — Synchronized methods, locks e `ReentrantLock`.
- https://docs.oracle.com/javase/tutorial/essential/concurrency/deadlock.html — Deadlock e liveness.
- https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/package-summary.html — Javadoc `java.util.concurrent` (executors, locks, atomics, collections).
- https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/CompletableFuture.html — Javadoc `CompletableFuture` (composição assíncrona).
- https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ExecutorService.html — Javadoc `ExecutorService` (`submit`, `shutdown`).
- https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ConcurrentHashMap.html — Javadoc `ConcurrentHashMap`.
- https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/atomic/package-summary.html — Javadoc das classes atômicas (`AtomicInteger`, CAS).
- https://docs.oracle.com/javase/specs/jls/se17/html/jls-17.html — Java Language Specification §17: Threads and Locks (happens-before, JMM).
- https://openjdk.org/jeps/444 — JEP 444: Virtual Threads (Java 21).
- https://docs.oracle.com/javase/tutorial/essential/concurrency/forkjoin.html — Fork/Join (`RecursiveTask`, `ForkJoinPool`).
- https://en.wikipedia.org/wiki/Deadlock — Condições de deadlock (Coffman) e prevenção.
- https://en.wikipedia.org/wiki/Amdahl%27s_law — Lei de Amdahl e limites do paralelismo.
