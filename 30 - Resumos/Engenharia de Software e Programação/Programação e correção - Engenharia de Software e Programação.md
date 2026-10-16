---
tipo: resumo
disciplina: "Engenharia de Software e Programação"
tema: "Programação e correção"
status: novo
data: "2026-10-16"
tags: [resumo, engenharia-software, cgu-2026]
---

# Resumo: Programação e correção

> [!info] MOC: [[Engenharia de Software e Programação]]
> Edital nº 1/2026 – CGU – AFFC · **Conhecimentos específicos** · Cargo 4 (TI / Desenvolvimento de Sistemas) · Item 2 — *Programação e correção*.

## Escopo no edital (checklist)

- [x] 2.1 Linguagem Java: tipos de dados, estruturas de controle, métodos, classes e objetos.
- [x] 2.2 Encapsulamento, interfaces, herança e polimorfismo.
- [x] 2.3 Coleções e tipos genéricos.
- [x] 2.4 Igualdade de objetos, mutabilidade, tratamento de exceções e leitura e escrita de arquivos.
- [x] 2.5 Estruturas de dados, algoritmos e pseudocódigo.
- [x] 2.6 Leitura, depuração e testes de borda.
- [x] 2.7 Complexidade em decisões de desempenho.
- [x] 2.8 Modularidade e padrões de projeto aplicados à manutenção.

## Resumo

Este é o item mais denso da disciplina: o **núcleo da linguagem Java** e a **programação orientada a objetos**, somados a **estruturas de dados, algoritmos e complexidade**, fechando com **modularidade e padrões de projeto** para manutenção. O fio condutor é escrever **código correto, legível e com desempenho adequado**.

1. **Java** é **fortemente tipada**, **orientada a objetos** e roda numa **JVM** (compilada para *bytecode*, com *garbage collector*). Tipos dividem-se em **primitivos** e **de referência**, com **wrappers** e *autoboxing*.
2. **POO** se apoia em **encapsulamento** (modificadores de acesso), **herança** (única), **interfaces** (múltiplas) e **polimorfismo** (*overriding* em tempo de execução vs *overloading* em compilação).
3. **Coleções** (`List`, `Set`, `Map`, `Queue`) e **generics** dão segurança de tipo em tempo de compilação (com *type erasure* e *wildcards*).
4. **Correção** envolve o contrato **`equals`/`hashCode`**, **imutabilidade** (`String`, `record`), **exceções** (checadas/não checadas, *try-with-resources*) e I/O com **`java.nio.file`**.
5. **Estruturas de dados e algoritmos** (lista, pilha, fila, árvore, hash; busca/ordenação) determinam a **complexidade Big-O**, que guia **decisões de desempenho**.
6. **Leitura de código, depuração e testes de borda** completam a capacidade de **verificar e corrigir**; **modularidade** (coesão/acoplamento) e **padrões GoF** sustentam a **manutenção**.

## 1. Linguagem Java: fundamentos (2.1)

### 1.1 Tipos primitivos e valores padrão

| Tipo | Tamanho | Valores/faixa | Default |
| --- | --- | --- | --- |
| `byte` | 8 bits | −128 a 127 | `0` |
| `short` | 16 bits | −32.768 a 32.767 | `0` |
| `int` | 32 bits | ±2,1 bilhões | `0` |
| `long` | 64 bits | sufixo `L`/`l` | `0L` |
| `float` | 32 bits (IEEE 754) | sufixo `F`/`f` | `0.0f` |
| `double` | 64 bits (IEEE 754) | padrão p/ decimal | `0.0d` |
| `char` | 16 bits (Unicode) | `'\u0000'` a `'\uffff'` | `'\u0000'` |
| `boolean` | — | `true`/`false` | `false` |

- Primitivos **não são objetos**; variáveis de **referência** apontam para objetos e default é `null`.
- Java é **fortemente e estaticamente tipada**: o tipo é verificado em compilação e não há coerção implícita perigosa (ex.: `boolean` não vira `int`).
- Casting: **ampliação** (`int`→`long`) é implícito; **estreitamento** (`double`→`int`) exige cast explícito e pode perder precisão.

### 1.2 Wrappers e autoboxing

- Classes empacotadoras: `Byte`, `Short`, `Integer`, `Long`, `Float`, `Double`, `Character`, `Boolean` — **imutáveis** e `final`.
- **Autoboxing/unboxing:** conversão automática primitivo↔wrapper.
- **Cache de `Integer`**: valores de `-128` a `127` são cacheados → `Integer a = 100; Integer b = 100; a == b` é `true` (mesmo objeto do cache); com `200`, `==` é `false`.
- Parsing: `Integer.parseInt("42")` (lança `NumberFormatException` — não checada); `Double.parseDouble(...)`.

### 1.3 Estruturas de controle

- `if/else`, `else if`; operador ternário `cond ? a : b`.
- `switch`: aceita `byte`, `short`, `char`, `int`, `String`, `enum` (e *switch expression* com `->` a partir do Java 14; `yield` para retornar valor).
- Laços: `for`, `while`, `do-while`, **enhanced for** (`for (T x : coleção)`) — funciona com arrays e `Iterable`.
- `break` (sai do laço/switch), `continue` (pula iteração), rótulos para laços aninhados.

### 1.4 Métodos, classes e objetos

- **Método:** assinatura = nome + lista de parâmetros (**não** inclui tipo de retorno). `void` não retorna nada.
- **Sobrecarga (overloading):** mesmo nome, **parâmetros diferentes** (número/tipo/ordem) — resolvida em **compilação**.
- **Classe/objeto:** classe é o molde; objeto é a instância. Criar com `new`.
- **Construtores:** mesmo nome da classe, sem retorno; **construtor padrão** só existe se nenhum for declarado. `this(...)`/`super(...)` devem ser a **primeira** instrução.
- **`static`:** membros pertencem à **classe** (não à instância); blocos `static` inicializam a classe; classes aninhadas `static`.
- **`final`:** em variável (constante), em método (impede override) e em classe (impede herança).
- **`var`** (Java 10+): inferência de tipo local — apenas para variáveis locais inicializadas.

```java
public final class Conta {
    private final String numero;          // imutável
    private double saldo;

    public Conta(String numero, double saldo) {   // construtor
        this.numero = numero;
        this.saldo = saldo;
    }

    public void depositar(double v) {            // método de instância
        if (v <= 0) throw new IllegalArgumentException("valor inválido");
        saldo += v;
    }

    public static Conta nova(String n) {         // factory estático
        return new Conta(n, 0);
    }
}
```

## 2. Encapsulamento, interfaces, herança e polimorfismo (2.2)

### 2.1 Encapsulamento e modificadores de acesso

- **Encapsulamento:** esconder o estado interno e expor apenas operações válidas — campos `private`, acesso via métodos.
- Modificadores (da menor à maior visibilidade):

| Modificador | Classe | Pacote | Subclasse | Qualquer lugar |
| --- | --- | --- | --- | --- |
| `private` | Sim | — | — | — |
| *(default/package-private)* | Sim | Sim | — | — |
| `protected` | Sim | Sim | Sim | — |
| `public` | Sim | Sim | Sim | Sim |

### 2.2 Herança

- **Herança única** em Java (uma classe só estende **uma** superclasse); `Object` é a raiz de todas as classes.
- `extends` herda membros não-`private`; construtores **não** são herdados.
- Sobrescrita respeita a visibilidade (não pode reduzir) e o tipo de retorno (covariante).

### 2.3 Interfaces × classes abstratas

| Aspecto | Interface | Classe abstrata |
| --- | --- | --- |
| Instanciar | Não | Não |
| Herança múltipla | Sim (várias interfaces) | Não (uma só) |
| Estado/campos | Apenas `public static final` (constantes) | Pode ter estado |
| Métodos | abstratos + `default`, `static`, `private` (Java 8/9) | abstratos + concretos |
| Construtores | Não | Sim |
| Semântica | **Contrato** ("o que faz") | **Reuso parcial** ("é-um", compartilha implementação) |

- Métodos de interface são implicitamente `public abstract`; campos, `public static final`.
- `default` (Java 8) permite implementação com compatibilidade retroativa; `static` e `private` complementam.

### 2.4 Polimorfismo

- **Polimorfismo por subtipo (overriding):** mesma assinatura, comportamento redefinido na subclasse — **dynamic binding** (a versão chamada é decidida em **tempo de execução**, pelo tipo real do objeto).
- **Sobrecarga (overloading):** mesmo nome, assinaturas diferentes — **compile-time**, decidido pelo tipo estático.
- **Upcasting** (subclasse→super) é implícito; **downcasting** exige cast e deve ser precedido por `instanceof` (ou *pattern matching for instanceof*, Java 16+).

```java
interface Tributavel { double calcularImposto(); }       // contrato

class Produto implements Tributavel {
    private double valor;
    public double calcularImposto() { return valor * 0.10; }   // overriding
    public double calcularImposto(double aliquota) { return valor * aliquota; } // overloading
}

Tributavel t = new Produto();   // upcasting
t.calcularImposto();            // dynamic dispatch → Produto.calcularImposto()
```

- `@Override` documenta e previne erro de assinatura (compilador valida).

## 3. Coleções e tipos genéricos (2.3)

### 3.1 O Java Collections Framework

| Interface | Implementações | Característica |
| --- | --- | --- |
| `List` | `ArrayList`, `LinkedList` | Ordenada, **permite duplicados**, acesso por índice |
| `Set` | `HashSet`, `TreeSet`, `LinkedHashSet` | **Sem duplicados** |
| `Map` | `HashMap`, `TreeMap`, `LinkedHashMap` | Chave→valor |
| `Queue`/`Deque` | `ArrayDeque`, `LinkedList`, `PriorityQueue` | FIFO / dupla ponta / prioridade |

- **`ArrayList`:** array redimensionável — `get/set` O(1); inserção/remoção no meio O(n). Preferida para **leitura**.
- **`LinkedList`:** lista duplamente ligada (também `Deque`) — inserção/remoção nas pontas O(1); acesso por índice O(n).
- **`HashSet`:** baseado em `HashMap`, O(1) médio, **sem ordem garantida**; **`LinkedHashSet`** preserva ordem de inserção; **`TreeSet`** ordena (árvore rubro-negra, O(log n)).
- **`HashMap`:** O(1) médio, permite **uma** chave `null`; **`TreeMap`** ordena pelas chaves (O(log n)); **`Hashtable`** é legado e sincronizado (não permite `null`).
- **`PriorityQueue`:** heap binário — retira o **menor** elemento (ordem natural ou por `Comparator`) em O(log n).

### 3.2 Ordenação: Comparable × Comparator

- **`Comparable<T>`** (`compareTo`): define a **ordem natural** do tipo; a própria classe implementa.
- **`Comparator<T>`** (`compare`): define uma **ordem externa/alternativa**, sem alterar a classe; ideal para múltiplos critérios e `Comparator.comparing(...)`.

```java
class Pessoa implements Comparable<Pessoa> {
    private final String nome; private final int idade;
    public int compareTo(Pessoa o) { return this.nome.compareTo(o.nome); }  // natural: por nome
}

List<Pessoa> l = new ArrayList<>();
Collections.sort(l);                                  // usa compareTo
l.sort(Comparator.comparing(Pessoa::getIdade));       // ordem externa
l.sort(Comparator.comparing(Pessoa::getNome).thenComparing(Pessoa::getIdade)); // encadeado
```

### 3.3 Generics e wildcards

- **Generics** trazem **segurança de tipo em compilação**: `List<String>` só aceita `String`.
- **Type erasure:** o parâmetro de tipo é removido em tempo de execução (existe só em compilação); não dá para `new T()` nem `instanceof T`.
- **Wildcards:**
  - `?` (unbounded): leitura genérica (`List<?>`).
  - `? extends T` (upper-bounded): **produz** (leitura) — **PECS: Producer Extends**.
  - `? super T` (lower-bounded): **consome** (escrita) — **PECS: Consumer Super**.
- Métodos genéricos: `<T> T metodo(T x)`; bounds: `<T extends Number>`.
- Fábricas imutáveis (Java 9+): `List.of(...)`, `Set.of(...)`, `Map.of(...)` (não aceitam `null`); `Arrays.asList(...)` retorna lista de tamanho fixo; `Collections.unmodifiableList(...)` para visão somente-leitura.

## 4. Igualdade, mutabilidade, exceções e I/O (2.4)

### 4.1 equals/hashCode

- **Contrato de `equals`:** reflexivo, simétrico, transitivo, consistente, e `x.equals(null)` → `false`.
- **Contrato com `hashCode`:** se `a.equals(b)` então `hashCode` iguais; `hashCode` iguais **não** implicam `equals` (colisões são permitidas).
- Default de `Object.equals` é **identidade** (`==`); por isso, para igualdade **por valor** é preciso sobrescrever `equals` **e** `hashCode` juntos (senão coleções hash — `HashSet`/`HashMap` — falham).
- `==` em referências compara endereço; em primitivos, valor.

```java
public final class Ponto {
    private final int x, y;
    @Override public boolean equals(Object o) {
        if (this == o) return true;
        if (!(o instanceof Ponto p)) return false;
        return x == p.x && y == p.y;
    }
    @Override public int hashCode() { return Objects.hash(x, y); }
}
```

### 4.2 Mutabilidade e imutabilidade

- **`String` é imutável:** toda operação retorna um **novo** objeto. Literais ficam no **string pool** (internados); `new String("x")` cria instância fora do pool.
- **`StringBuilder`** (não sincronizado) e **`StringBuffer`** (sincronizado) são mutáveis — usar em concatenações em laço.
- **Objeto imutável:** campos `final`/`private`, sem *setters*, e sem expor/aceitar referências mutáveis. Vantagens: **thread-safe por natureza**, seguro como chave de `Map`, previsível.
- **Records** (Java 16+, JEP 395): tipo imutável, conciso e transparente.

```java
public record Pessoa(String nome, int idade) {}   // acesso: pessoa.nome(), pessoa.idade()

// compact constructor (validação):
public record Pessoa {
    public Pessoa { if (idade < 0) throw new IllegalArgumentException(); }
}
```

- Records são **implicitamente `final`**, estendem `java.lang.Record`, geram `equals`/`hashCode`/`toString`, têm **acessores** com o nome do componente (`nome()`, não `getNome()`) e **construtor canônico**. Podem implementar interfaces; **não** podem estender classes nem ser estendidos.

### 4.3 Tratamento de exceções

Hierarquia: `Throwable` → **`Error`** (falhas sérias da JVM: `OutOfMemoryError`, `StackOverflowError` — normalmente **não** capturar) e **`Exception`** → **`RuntimeException`** (não checada) e **exceções checadas**.

| Categoria | Exemplos | Obriga tratar/declarar? |
| --- | --- | --- |
| **Checada (checked)** | `IOException`, `SQLException` | Sim (`catch` ou `throws`) |
| **Não checada (unchecked)** | `NullPointerException`, `IllegalArgumentException`, `IndexOutOfBoundsException`, `NumberFormatException` | Não (erro de programação) |
| **Error** | `OutOfMemoryError`, `StackOverflowError` | Não (não recuperável) |

- `try-catch-finally`: `finally` executa sempre (exceto `System.exit`); **multi-catch** `catch (IOException | SQLException e)` (tipos **não podem ser pai/filho** no mesmo `multi-catch`).
- **try-with-resources:** recursos que implementam **`AutoCloseable`** são fechados automaticamente em ordem **reversa**, com supressão de exceções de fechamento.

```java
try (BufferedReader br = Files.newBufferedReader(Path.of("dados.txt"))) {
    String linha;
    while ((linha = br.readLine()) != null) { System.out.println(linha); }
} catch (IOException e) {
    // tratar
}
```

- Exceções customizadas estendem `Exception` (checada) ou `RuntimeException` (não checada).

### 4.4 Leitura e escrita de arquivos (java.nio.file)

- `Path`/`Paths.get(...)`/`Path.of(...)` representam caminhos; `Files` fornece as operações.
- Leitura: `Files.readAllLines(path)` (lista de linhas), `Files.readString(path)` (Java 11+), `Files.newBufferedReader(...)`, `Files.lines(...)` (stream).
- Escrita: `Files.write(path, bytes)`, `Files.writeString(path, s)`, `Files.newBufferedWriter(...)` com `StandardOpenOption.APPEND`/`CREATE`/`TRUNCATE_EXISTING`.
- Utilitários: `Files.exists`, `Files.isDirectory`, `Files.copy`, `Files.move`, `Files.delete`, `Files.walk` (árvore).

```java
Path p = Path.of("saida.txt");
Files.writeString(p, "linha1\nlinha2", StandardCharsets.UTF_8);
List<String> linhas = Files.readAllLines(p);   // lê tudo
```

## 5. Estruturas de dados, algoritmos e pseudocódigo (2.5)

### 5.1 Estruturas de dados fundamentais

| Estrutura | Organização | Operações típicas |
| --- | --- | --- |
| **Array** | Posições contíguas, acesso indexado | leitura O(1), inserção/remoção O(n) |
| **Lista ligada** | Nós com ponteiros | inserção/remoção O(1) se conhecido o nó; busca O(n) |
| **Pilha (Stack)** | LIFO | push/pop/peek O(1) |
| **Fila (Queue)** | FIFO | enqueue/dequeue O(1) |
| **Árvore binária** | Nó com ≤ 2 filhos | percorrimento: pré-ordem, em-ordem, pós-ordem |
| **BST** | Esq. < nó < dir. | busca/inserção O(log n) médio, O(n) pior (degenerada) |
| **Árvore balanceada** (AVL, rubro-negra) | Altura balanceada | busca/inserção/remoção O(log n) garantido |
| **Heap** | Árvore binária com prioridade | `PriorityQueue`: extrair min/max O(log n) |
| **Tabela hash** | Função hash → bucket | busca/inserção/remoção O(1) médio |
| **Grafo** | Vértices + arestas | BFS/DFS, caminho mínimo (Dijkstra) |

### 5.2 Busca e ordenação

| Algoritmo | Melhor | Médio | Pior | Estável? | Observação |
| --- | --- | --- | --- | --- | --- |
| **Busca linear** | O(1) | O(n) | O(n) | — | lista desordenada |
| **Busca binária** | O(1) | O(log n) | O(log n) | — | exige lista **ordenada** |
| **Bubble/Insertion/Selection** | O(n) / O(n) / O(n²) | O(n²) | O(n²) | Sim (bubble/insertion) | quase ordenados: insertion é bom |
| **Merge sort** | O(n log n) | O(n log n) | O(n log n) | Sim | divide-e-conquista, memória extra |
| **Quicksort** | O(n log n) | O(n log n) | **O(n²)** | Não | pior caso com pivot ruim |
| **Heapsort** | O(n log n) | O(n log n) | O(n log n) | Não | in-place |

- **Recursão** vs **iteração**: recursão usa pilha de chamadas e pode estourar (`StackOverflowError`); toda recursão pode ser reescrita iterativamente.

### 5.3 Pseudocódigo

Representação independente de linguagem para expressar algoritmos (a banca cobra leitura/interpretação):

```text
função buscaBinaria(vetor V, alvo):
    esq ← 0
    dir ← tamanho(V) - 1
    enquanto esq ≤ dir:
        meio ← (esq + dir) div 2
        se V[meio] = alvo: retorne meio
        senão se V[meio] < alvo: esq ← meio + 1
        senão: dir ← meio - 1
    retorne -1   // não encontrado
```

## 6. Leitura, depuração e testes de borda (2.6)

### 6.1 Leitura e rastreamento de código

- **Rastrear (trace)** significa executar mentalmente, mantendo o **estado das variáveis** a cada passo (usar tabela de rastreamento).
- Atenção a: **precedência de operadores**, curto-circuito (`&&`, `||`), escopo de variáveis, passagem de **valor** (primitivos) vs **referência** (objetos), e efeitos colaterais.
- Java passa **todos** os argumentos **por valor** — para objetos, passa-se uma **cópia da referência** (mutações no objeto são visíveis; reatribuir a referência não).

### 6.2 Depuração

- Ferramentas: **debugger** (breakpoints, step over/into/out, watch, inspeção de pilha de chamadas), logs e testes.
- **Técnicas:** *divide and conquer* (isolar a falha), reproduzir o defeito com **entrada mínima**, inspecionar o **stack trace** (linha e causa raiz), verificar **invariantes**.
- Erros comuns de iniciante: **off-by-one** (erros de índice ±1), confundir `=` com `==`, `==` com `equals`, fechar recursos fora do `finally`/try-with-resources.

### 6.3 Testes de borda (boundary value analysis)

- **Partição de equivalência:** dividir o domínio de entrada em classes equivalentes e testar um representante de cada.
- **Análise de valor limite:** testar nos **limites** das partições — `mínimo`, `máximo`, `mínimo-1`, `máximo+1` (e valores "imediatamente dentro/fora").
- Exemplos: idade `[0, 130]` → testar `-1`, `0`, `1`, `129`, `130`, `131`; lista vazia; string nula; `Integer.MIN_VALUE`/`MAX_VALUE`; divisão por zero; coleção vazia no laço.

```java
// Exemplo clássico de borda: tamanho e índices
for (int i = 0; i < lista.size(); i++) { ... }     // ok
for (int i = 1; i <= lista.size(); i++) { ... }    // off-by-one (estoura no fim)
```

## 7. Complexidade em decisões de desempenho (2.7)

### 7.1 Notação Big-O

- Mede o **crescimento do tempo/espaço em função do tamanho da entrada (n)**, no **pior caso** (ou médio), **ignorando constantes** e termos de menor ordem.
- Ordem (da melhor à pior): **O(1)** < **O(log n)** < **O(n)** < **O(n log n)** < **O(n²)** < **O(2ⁿ)**.
- Exemplos: acesso por índice O(1); busca binária O(log n); percorrer array O(n); ordenação eficiente O(n log n); laço aninhado O(n²); enumerar subconjuntos O(2ⁿ).

### 7.2 Escolhas guiadas por complexidade

| Decisão | Trade-off |
| --- | --- |
| `ArrayList` × `LinkedList` | ArrayList: leitura O(1); LinkedList: inserção/remoção nas pontas O(1), leitura O(n) |
| `HashMap` × `TreeMap` | HashMap O(1) médio, sem ordem; TreeMap O(log n), ordenado |
| `HashSet` × `TreeSet` | HashSet O(1); TreeSet ordenado O(log n) |
| Busca em lista não ordenada × ordenada | Não ordenada O(n); ordenar + busca binária compensa em buscas repetidas |
| Concatenação `String` em laço × `StringBuilder` | `+` em laço cria muitos objetos (O(n²) de alocação); `StringBuilder` é O(n) |

- **Constante importa pouco para n grande**, mas muito para n pequeno/caminho quente — por isso **medição (profiling)** deve preceder otimizações prematuras ("*premature optimization is the root of all evil*").
- Regra de ouro: **complexidade assintótica primeiro**, depois **constantes e localidade de cache**.

## 8. Modularidade e padrões de projeto (2.8)

### 8.1 Modularidade, coesão e acoplamento

- **Coesão alta:** um módulo faz **uma** coisa bem (responsabilidade única). **Acoplamento baixo:** módulos dependem pouco entre si.
- Bom design = **alta coesão + baixo acoplamento** — facilita leitura, teste e manutenção.
- **SOLID**:
  - **S**ingle Responsibility (uma razão para mudar);
  - **O**pen/Closed (aberto à extensão, fechado à modificação);
  - **L**iskov Substitution (subclasses substituem a superclasse sem quebrar);
  - **I**nterface Segregation (interfaces específicas, não "gordas");
  - **D**ependency Inversion (depender de abstrações, não de concretos).

### 8.2 Padrões de projeto (GoF)

Classificação clássica (Gamma et al., "Design Patterns"):

| Categoria | Padrões | Propósito |
| --- | --- | --- |
| **Criacionais** | Singleton, Factory Method, Abstract Factory, Builder, Prototype | Como criar objetos |
| **Estruturais** | Adapter, Decorator, Facade, Proxy, Composite, Bridge | Como compor objetos/classes |
| **Comportamentais** | Strategy, Observer, Template Method, Command, Iterator, State | Como objetos colaboram |

- **Strategy:** encapsula algoritmos intercambiáveis (mudar comportamento sem `if`s gigantes).
- **Observer:** notifica dependentes quando o estado muda (padrão pub/sub).
- **Decorator:** adiciona responsabilidades dinamicamente (ex.: `BufferedReader` sobre `Reader`).
- **Factory Method:** delega a criação à subclasse (define uma interface para criar, deixando a subclasse decidir a classe).
- **Adapter:** converte uma interface em outra esperada pelo cliente.
- **Facade:** fornece interface simplificada para um subsistema complexo.
- **Template Method:** define o esqueleto do algoritmo, com passos sobrescrevíveis.
- **Singleton:** uma única instância (cuidado: estado global e testes).

> Relação com a manutenção: padrões reduzem acoplamento e facilitam **mudanças futuras** (conexão com o item 5.1).

## Detalhes que merecem destaque

- **`==` vs `equals`:** `==` compara referência (objetos) ou valor (primitivos); `equals` sobrescrito compara **valor**. Em `String`, use sempre `equals`.
- **Contrato equals/hashCode:** sobrescrever um **obriga** sobrescrever o outro (senão `HashSet`/`HashMap` quebram).
- **`String` imutável × `StringBuilder` mutável:** concatenação em laço deve usar `StringBuilder` (evita O(n²) de alocação).
- **Records:** imutáveis, `final`, geram acessores `nome()` (não `getNome()`), `equals`/`hashCode`/`toString`; **não** herdam de classe e **não** são herdáveis.
- **Checada × não checada:** checadas (`IOException`, `SQLException`) exigem tratar/declarar; não checadas (`RuntimeException`) indicam erro de programação; `Error` não se captura.
- **try-with-resources** exige `AutoCloseable` e fecha em **ordem reversa**.
- **`ArrayList` leitura O(1) × `LinkedList` inserção nas pontas O(1)**; `HashMap` O(1) × `TreeMap` O(log n) ordenado.
- **`Comparable` (ordem natural, `compareTo`) × `Comparator` (ordem externa, `compare`)**.
- **PECS:** `? extends` produz (leitura); `? super` consome (escrita).
- **Type erasure:** generics não existem em tempo de execução; não dá `new T()`/`instanceof T`.
- **Overloading = compilação; overriding = execução (dynamic dispatch).**
- **Autoboxing + cache de `Integer` (−128 a 127):** `==` pode enganar.
- **Big-O ignora constantes**; decisões de desempenho: complexidade primeiro, depois medição.
- **Java passa argumentos por valor** (para objetos, cópia da referência).
- **Coesão alta + acoplamento baixo + SOLID** = manutenibilidade; **GoF** organiza soluções recorrentes.

## Comparações que a banca costuma cobrar (certo/errado)

| Conceito A | Conceito B | Diferença-chave |
| --- | --- | --- |
| Tipo primitivo | Tipo de referência | Primitivo guarda valor (default 0/false); referência guarda endereço (default `null`) |
| `==` | `equals` | `==` é identidade/referência; `equals` (sobrescrito) é igualdade por valor |
| Overloading | Overriding | Overloading = mesma classe, assinaturas diferentes (compilação); overriding = subclasse, mesma assinatura (execução) |
| Interface | Classe abstrata | Interface = contrato (múltipla, sem estado); abstrata = reuso parcial (única, com estado) |
| `Comparable` | `Comparator` | Comparable = ordem natural (`compareTo`); Comparator = ordem externa (`compare`) |
| `ArrayList` | `LinkedList` | ArrayList leitura O(1), inserção no meio O(n); LinkedList inserção nas pontas O(1), leitura O(n) |
| `HashMap` | `TreeMap` | HashMap O(1) sem ordem; TreeMap O(log n) ordenado |
| `HashSet` | `TreeSet` | HashSet O(1) sem ordem; TreeSet O(log n) ordenado |
| `? extends T` | `? super T` | `extends` = leitura (produtor); `super` = escrita (consumidor) |
| Exceção checada | Exceção não checada | Checada exige tratar/declarar; não checada é `RuntimeException` (não obriga) |
| `Error` | `Exception` | Error = falha JVM não recuperável; Exception = recuperável pela aplicação |
| `String` | `StringBuilder` | String imutável (novo objeto); StringBuilder mutável (não sincronizado) |
| `StringBuilder` | `StringBuffer` | StringBuilder não sincronizado (rápido); StringBuffer sincronizado (thread-safe) |
| Classe `final` | Método `final` | Classe final = não herda; método final = não sobrescreve |
| Recursão | Iteração | Recursão usa pilha de chamadas (pode estourar); iteração usa laço |
| Busca linear | Busca binária | Linear O(n) em desordenada; binária O(log n) exige ordenada |
| Merge sort | Quicksort | Merge O(n log n) sempre (estável); quicksort O(n²) no pior (não estável) |
| Coesão | Acoplamento | Coesão = foco interno; acoplamento = dependência externa (quer alta coesão, baixo acoplamento) |
| Strategy | Template Method | Strategy delega todo o algoritmo (composição); Template fixa esqueleto com passos variáveis (herança) |

## Pegadinhas e erros comuns

> Cuidado com termos absolutos ("sempre", "nunca", "exclusivamente") e com a troca de requisitos.

- Achar que **`==` compara conteúdo de `String`** — compara referência; `"a" == "a"` pode dar `true` só por **internação** no string pool.
- Sobrescrever **`equals` sem `hashCode`** — objetos "iguais" em `HashSet`/`HashMap` deixam de funcionar.
- Confundir **`compareTo` (Comparable)** com **`compare` (Comparator)**.
- Dizer que **Java tem herança múltipla de classes** — só de **interfaces** (classe tem herança única).
- Afirmar que **generics existem em runtime** — há **type erasure**.
- Achar que **`? super T` serve para leitura** — serve para **escrita** (PECS).
- Supor que **`LinkedList` é sempre mais rápida que `ArrayList`** — para acesso por índice, `ArrayList` ganha (O(1)).
- Tratar **`Error`** (`OutOfMemoryError`) como exceção recuperável.
- Esquecer de **fechar recurso** ou fechar fora do `finally`/try-with-resources.
- Confundir **`float`/`double`** (sufixo `f`/`F`) e achar que **`boolean` tem tamanho 1 bit** em qualquer representação (tamanho não é definido pela linguagem; depende da JVM).
- Dizer que **`record` tem getters `getX()`** — os acessores são `x()`.
- Achar que **construtor é herdado** ou que **método `final` pode ser sobrescrito**.
- Confundir **overloading (compilação)** com **overriding (execução)**.
- Afirmar que **quicksort é sempre O(n log n)** — no **pior caso é O(n²)**.
- Achar que **busca binária funciona em lista desordenada** — exige **ordenação**.
- Ignorar **off-by-one** em laços e **valores limite** (`Integer.MAX_VALUE`, lista vazia, nulo) nos testes.
- Otimizar prematuramente sem **medir** — a complexidade assintótica deve vir antes das constantes.

## Notas atômicas relacionadas

```dataview
LIST FROM "20 - Notas"
WHERE disciplina = this.disciplina
  AND contains(tema, this.tema)
SORT file.name ASC
```

## Fontes

- https://docs.oracle.com/javase/tutorial/java/nutsandbolts/ — The Java Tutorials: tipos de dados, variáveis e operadores.
- https://docs.oracle.com/javase/tutorial/java/javaOO/ — The Java Tutorials: classes, objetos, herança, interfaces e polimorfismo.
- https://docs.oracle.com/javase/tutorial/collections/ — The Java Tutorials: Collections Framework (interfaces, implementações, algoritmos).
- https://docs.oracle.com/javase/tutorial/java/generics/ — The Java Tutorials: generics, type erasure e wildcards.
- https://docs.oracle.com/javase/8/docs/api/java/util/Collections.html — Javadoc de `java.util.Collections` (algoritmos e fábricas).
- https://docs.oracle.com/javase/8/docs/api/java/lang/Comparable.html — Javadoc de `Comparable` (ordem natural).
- https://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html — Javadoc de `Comparator` (ordem externa).
- https://docs.oracle.com/javase/tutorial/essential/exceptions/ — The Java Tutorials: exceções (checked/unchecked, try-with-resources).
- https://docs.oracle.com/javase/tutorial/essential/io/ — The Java Tutorials: I/O e leitura/escrita de arquivos.
- https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html — Javadoc de `java.nio.file.Files` (read/write, Path).
- https://openjdk.org/jeps/395 — JEP 395: Records (classes imutáveis e transparentes de dados).
- https://docs.oracle.com/javase/specs/jls/se17/html/jls-4.html — Java Language Specification: tipos, valores e variáveis.
- https://docs.oracle.com/javase/tutorial/java/javaOO/equals.html — The Java Tutorials: contrato de `equals`/`hashCode`.
- https://www.baeldung.com/java-big-o-notation — Big-O notation e complexidade de algoritmos em Java (referência de estudo).
- https://refactoring.guru/design-patterns — Padrões de projeto GoF (categorias criacional/estrutural/comportamental).
- https://refactoring.guru/solid — Princípios SOLID (SRP, OCP, LSP, ISP, DIP).
- https://en.wikipedia.org/wiki/Time_complexity — Complexidade de tempo (notação Big-O) e tabelas de algoritmos.
