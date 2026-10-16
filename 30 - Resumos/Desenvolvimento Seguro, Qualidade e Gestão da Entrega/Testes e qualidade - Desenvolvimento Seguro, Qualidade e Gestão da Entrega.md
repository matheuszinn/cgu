---
tipo: resumo
disciplina: "Desenvolvimento Seguro, Qualidade e Gestão da Entrega"
tema: "Testes e qualidade"
status: novo
data: "2026-10-16"
tags: [resumo, desenvolvimento-seguro, cgu-2026]
---

# Resumo: Testes e qualidade

> [!info] MOC: [[Desenvolvimento Seguro, Qualidade e Gestão da Entrega]]
> Edital nº 1/2026 – CGU – AFFC · **Conhecimentos específicos** · Cargo 4 (TI / Desenvolvimento de Sistemas) · Item 2 — *Testes e qualidade*.

## Escopo no edital (checklist)

- [x] 2.1 Testes unitários, de integração, de contrato e de aceitação.
- [x] 2.2 Análise estática, cobertura e revisão de código.
- [x] 2.3 Automação e dados de teste.
- [x] 2.4 Limites das métricas de qualidade.
- [x] 2.5 Verificação de requisitos funcionais, segurança, desempenho e acessibilidade.

## Resumo

O item trata de **testes e qualidade** ao longo do ciclo de desenvolvimento: a **pirâmide de testes** (unitário, integração, contrato, e2e/aceitação), as técnicas de **análise estática, cobertura e revisão de código**, a **automação e os dados de teste**, os **limites das métricas de qualidade** e a **verificação de requisitos não-funcionais** (funcionais, segurança, desempenho, acessibilidade).

Três ideias-força:

1. **A pirâmide orienta o investimento:** muitos testes **unitários** (rápidos, baratos, isolados), menos de **integração**, poucos **e2e/aceitação** (lentos, caros, frágeis). O equilíbrio errado (muito e2e, pouco unitário) é o "cone invertido" (*ice cream cone*), antipadrão clássico.
2. **Cobertura de código é métrica necessária mas não suficiente:** alta cobertura **não garante** qualidade nem ausência de bugs — mede **código executado**, não **comportamento verificado**. A banca adora cobrar esse limite.
3. **Qualidade é verificável e multidimensional:** funcionalidade, segurança, desempenho e acessibilidade são requisitos com **técnicas de teste próprias**; métricas isoladas (cobertura, nº de testes) enganam quando usadas como meta única.

## 1. Testes unitários, de integração, de contrato e de aceitação (2.1)

### 1.1 A pirâmide de testes

- **Pirâmide de testes** (Mike Cohn): da base ao topo — **unitários** (muitos, rápidos), **integração** (médios), **e2e/aceitação** (poucos, lentos). Princípio: quanto mais **rápido e isolado**, mais abundante deve ser.
- **Antipadrão "ice cream cone"** (ou pirâmide invertida): poucos unitários e muitos e2e — lento, frágil, difícil de manter.

| Nível | O que testa | Escopo | Velocidade/custo | Exemplo |
| --- | --- | --- | --- | --- |
| Unitário | Unidade (método/classe) isolada | Baixo | Rápido/barato | JUnit, Mockito |
| Integração | Colaboração entre componentes/deps | Médio | Médio | Spring Boot Test + Testcontainers |
| Contrato | Acordo consumidor-provedor | Médio | Médio | Pact, Spring Cloud Contract |
| Aceitação/e2e | Fluxo completo de negócio (UI/API) | Alto | Lento/caro | Selenium, Cypress, Playwright |

### 1.2 Teste unitário

- Testa a **menor unidade** de código isoladamente, com **dependências mockadas/falsificadas**.
- **JUnit** (xUnit do Java; JUnit 5 = JUnit Platform/Jupiter/Vintage) com anotações `@Test`, `@BeforeEach`, `@AfterEach`, `@ParameterizedTest`, *assertions*.
- **Mockito:** criação de *mocks/stubs/spies* — `@Mock`, `@InjectMocks`, `when(...).thenReturn(...)`, `verify(...)`. **Mock** (verifica interação) ≠ **Stub** (só retorna valor fixo) ≠ **Fake** (implementação leve, ex.: banco em memória).
- **TDD (Test-Driven Development):** ciclo **Red → Green → Refactor** (escreve o teste que falha, faz passar, refatora). Teste é especificação executável.

### 1.3 Teste de integração

- Verifica a **colaboração** entre componentes reais (ex.: repositório + banco, serviço + fila, integração com API).
- **Testcontainers:** sobe dependências reais (PostgreSQL, Kafka, Redis) em contêineres para teste de integração determinístico.
- **Teste de contrato:** garante que consumidor e provedor respeitam o **contrato** (schema/expectativas). **Consumer-Driven Contract** (ex.: **Pact**): o consumidor define expectativas; o provedor verifica em build. **Spring Cloud Contract** gera *stubs* e testes.

### 1.4 Teste de aceitação

- Valida se o sistema atende aos **critérios de aceitação** do negócio (do ponto de vista do usuário).
- **E2E (end-to-end):** percorre o fluxo completo real (UI + backend + integrações). Ferramentas: **Selenium**, **Cypress**, **Playwright**.
- **BDD (Behavior-Driven Development):** linguagem Gherkin (`Given/When/Then`) com **Cucumber** — conecta critérios de aceitação a testes automatizados.
- **Teste de aceitação (UAT)** pode ser manual (homologação do usuário) ou automatizado; o objetivo é o **aceite do produto**.

## 2. Análise estática, cobertura e revisão de código (2.2)

### 2.1 Análise estática

- **Análise estática** examina o **código sem executar**: detecta bugs potenciais, *code smells*, problemas de estilo, duplicação, complexidade e vulnerabilidades.
- Ferramentas: **SonarQube**, **ESLint**, **Checkstyle**, **PMD**, **SpotBugs**, **FindBugs** (Java); **SAST** é a análise estática voltada a segurança.
- **Linter** = análise de estilo/convenções; **analisador estático** = busca defeitos/vulnerabilidades. Ambos integram-se ao CI (*shift-left*, qualidade na origem).

### 2.2 Cobertura de código

- **Cobertura** mede a fração do código exercitada pelos testes. Tipos: **linhas**, **branches** (ramificações/desvios), **funções/métodos**, **condições**.
- Ferramentas: **JaCoCo** (Java), **Istanbul/nyc** (JS), **Coverage.py** (Python).
- **Mutation testing** (ex.: **PIT**): insere mutações no código e verifica se os testes "matam" os mutantes — mede a **efetividade** do teste, não apenas a execução.

### 2.3 Revisão de código

- **Code review** é inspeção humana por pares (qualidade, legibilidade, segurança, aderência a padrões).
- Abordagens: **pair programming**, revisão por PR/MR (*pull/merge request*), *over-the-shoulder*, *tool-assisted*.
- Complementa (não substitui) a automação: a máquina acha padrões, o humano acha problemas de design/semântica.

## 3. Automação e dados de teste (2.3)

### 3.1 Automação de testes

- **Por que automatizar:** rapidez, repetibilidade, segurança para refatorar (rede de segurança de regressão), feedback contínuo no CI.
- **O que automatizar:** testes **repetitivos e determinísticos** (unitários, integração, contrato, regressão). Testes **exploratórios** ficam manuais.
- **Teste de regressão:** garante que mudanças não quebraram comportamento existente.
- **Integração ao CI/CD:** a cada commit/PR, executar a suíte; falha bloqueia o merge (*fail fast*). Estratégia em **estágios**: rápido primeiro (unitário), lento depois (e2e).

### 3.2 Dados de teste

- **Dados de teste** devem ser **representativos, determinísticos e anonimizados**.
- **Fixtures** (conjuntos fixos), **fabricação de dados** (factory/builder), **fuzzing** (entradas aleatórias/mutadas para achar crashes).
- **Não usar dados reais de produção** com PII; aplicar **mascaramento/anonymização/sintetização** (LGPD).
- **Determinismo:** testes devem produzir o mesmo resultado sempre (sem dependência de relógio/rede/aleatoriedade não controlada) — isolar com *seeds*, relógio injetado, mocks.

## 4. Limites das métricas de qualidade (2.4)

- **Cobertura alta ≠ qualidade:** cobre código **executado**, não **comportamento correto**. Um teste sem *assertion* pode "cobrir" linha sem verificar nada.
- **Métrica de processo não é meta (lei de Goodhart):** quando a métrica vira alvo, perde valor — times "caçam cobertura" escrevendo testes triviais.
- **Nº de testes** ou **nº de bugs encontrados** não medem valor entregue.
- **Falsos positivos** da análise estática geram ruído e fadiga; **falsos negativos** dão falsa segurança.
- **Métricas compostas de qualidade:** *defect density*, *MTBF/MTTR*, taxa de escape de defeitos (defeitos que chegam a produção), *lead time* para correção, dívida técnica (SonarQube). Nenhuma isolada decide — usar **conjunto** e **tendência**.
- **Cobertura de branches** é mais rigorosa que a de linhas (exige testar cada desvio), mas ainda não garante correção.

## 5. Verificação de requisitos funcionais, segurança, desempenho e acessibilidade (2.5)

### 5.1 Requisitos funcionais

- Verificam **o que** o sistema faz: regras de negócio, casos de uso, critérios de aceitação.
- Técnicas: **caixa-preta** (sem ver o código) × **caixa-branca** (com o código); **partição de equivalência**, **análise de valor limite**, **tabela de decisão**, **transição de estados**, **casos de uso**.

### 5.2 Segurança (ver Item 1)

- **SAST/DAST/IAST/SCA**, **pentest**, **testes de controle de acesso** (IDOR, privilégio), **fuzzing** de entrada, verificação de **cabeçalhos/TLS**, **gestão de segredos** e **dependências vulneráveis**.

### 5.3 Desempenho

- **Teste de carga (load):** volume esperado de usuários/requisições.
- **Teste de estresse (stress):** levar o sistema ao limite/colapso e observar comportamento.
- **Teste de capacidade/escalabilidade:** comportamento ao adicionar recursos.
- **Teste de endurance/soak:** uso prolongado (vazamento de memória).
- **Teste de pico (spike):** variações abruptas de carga.
- Métricas: **latência** (p50/p95/p99), **throughput** (TPS/RPS), **uso de recursos**, **taxa de erro**, **tempo de resposta**. Ferramentas: JMeter, Gatling, k6, Locust.

### 5.4 Acessibilidade

- Garante que pessoas com deficiência possam usar o sistema. Referência: **WCAG** (Web Content Accessibility Guidelines) — princípios **POUR**: *Perceivable, Operable, Understandable, Robust*; níveis **A, AA, AAA**.
- Testes: **automáticos** (axe, Lighthouse, pa11y) e **manuais** (leitor de tela, navegação por teclado, contraste).
- No Brasil, obrigações legais: **LBI (Lei 13.146/2015 — Estatuto da Pessoa com Deficiência)** e, para serviços públicos digitais, diretrizes de acessibilidade do governo (eMAG — Modelo de Acessibilidade em Governo Eletrônico).

## Detalhes que merecem destaque

- **Pirâmide de testes** (Cohn): unitário (base) → integração → e2e/aceitação (topo). Quanto mais lento/frágil, menos testes.
- **Mock ≠ Stub ≠ Fake:** mock **verifica interação**; stub **só retorna**; fake é **implementação leve** (banco em memória).
- **Teste de contrato** protege a **fronteira entre serviços** (consumidor-provedor), diferente de teste de integração (que testa o fluxo interno).
- **Cobertura de branches > linhas** em rigor, mas **mutation testing** é o que mede **efetividade** real.
- **Análise estática** (SonarQube/SAST) roda **sem executar**; **análise dinâmica** exige a app rodando.
- **Dados de teste reais com PII = risco LGPD**; usar mascaramento/sintetização.
- **WCAG POUR + níveis A/AA/AAA** e **eMAG/LBI** são os marcos de acessibilidade.

## Comparações que a banca costuma cobrar (certo/errado)

| Conceito A | Conceito B | Diferença-chave |
| --- | --- | --- |
| Teste unitário | Teste de integração | Unidade isolada (mock) × colaboração real |
| Teste de integração | Teste de contrato | Fluxo interno × fronteira consumidor-provedor |
| Teste de aceitação | Teste e2e | Valida critério de negócio (perspectiva usuário) × percorre fluxo técnico completo |
| Mock | Stub | Verifica interação × só retorna valor |
| Análise estática | Análise dinâmica | Sem executar × executa a aplicação |
| Cobertura de linha | Cobertura de branch | Linha executada × desvio/ramo testado |
| Teste de carga | Teste de estresse | Volume esperado × levar ao limite/colapso |
| Teste funcional | Teste não-funcional | "O que faz" × "como se comporta" (perf/seg/acessibilidade) |
| Validação | Verificação | Atende à necessidade (certo produto) × está conforme especificação (produto certo) |
| Teste de regressão | Teste de aceitação | Não quebrou o que existia × atende ao aceite do usuário |

## Pegadinhas e erros comuns

> Cuidado com termos absolutos ("sempre", "nunca", "exclusivamente") e com a troca de requisitos.

- Achar que **100% de cobertura garante software sem bugs** — cobre execução, não correção.
- Confundir **validação** (atende à necessidade do usuário) com **verificação** (está conforme a especificação).
- Trocar **teste de integração** (colaboração de componentes) por **teste de contrato** (fronteira consumidor-provedor).
- Achar que **teste e2e é igual a teste de aceitação** — e2e é técnica de percurso; aceitação é validação de negócio.
- Achar que **mock e stub são sinônimos** — mock verifica interação; stub só devolve.
- Achar que **análise estática executa o código** — é feita **sem executar**.
- Achar que **teste de carga = teste de estresse** — carga usa volume esperado; estresse leva ao limite.
- Usar **dados reais de produção** em teste sem anonimizar (viola LGPD).
- Achar que **cobertura alta dispensa revisão de código** — são complementares.
- Achar que **teste manual é desnecessário** se houver automação — testes **exploratórios** seguem manuais.
- Achar que **métrica (cobertura/nº de testes) é meta** — vira jogo (lei de Goodhart) e não mede valor.

## Notas atômicas relacionadas

```dataview
LIST FROM "20 - Notas"
WHERE disciplina = this.disciplina
  AND contains(tema, this.tema)
SORT file.name ASC
```

## Fontes

- https://junit.org/junit5/ (JUnit 5 — framework de teste unitário Java)
- https://site.mockito.org/ (Mockito — mocks/stubs para testes Java)
- https://martinfowler.com/bliki/TestPyramid.html (Martin Fowler — pirâmide de testes)
- https://docs.pact.io/ (Pact — consumer-driven contract testing)
- https://spring.io/projects/spring-cloud-contract (Spring Cloud Contract — teste de contrato)
- https://testcontainers.com/ (Testcontainers — dependências reais em contêiner)
- https://www.sonarsource.com/products/sonarqube/ (SonarQube — análise estática e qualidade)
- https://www.eclemma.org/jacoco/ (JaCoCo — cobertura de código Java)
- https://pitest.org/ (PIT — mutation testing)
- https://www.selenium.dev/ (Selenium — automação e2e de UI)
- https://playwright.dev/ (Playwright — automação e2e)
- https://cucumber.io/ (Cucumber — BDD/Gherkin)
- https://www.w3.org/WAI/standards-guidelines/wcag/ (W3C — WCAG, acessibilidade web)
- https://www.gov.br/governodigital/pt-br/acessibilidade-e-usuario/eMAG (eMAG — Modelo de Acessibilidade em Governo Eletrônico)
- https://k6.io/ (k6 — teste de desempenho/carga)
