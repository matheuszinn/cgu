---
tipo: resumo
disciplina: "Engenharia de Software e Programação"
tema: "Manutenção e evolução"
status: novo
data: "2026-10-16"
tags: [resumo, engenharia-software, cgu-2026]
---

# Resumo: Manutenção e evolução

> [!info] MOC: [[Engenharia de Software e Programação]]
> Edital nº 1/2026 – CGU – AFFC · **Conhecimentos específicos** · Cargo 4 (TI / Desenvolvimento de Sistemas) · Item 5 — *Manutenção e evolução*.

## Escopo no edital (checklist)

- [x] 5.1 Débito técnico, documentação, modularidade e acoplamento.
- [x] 5.2 Sustentação e modernização de sistemas legados.
- [x] 5.3 Interoperabilidade e compatibilidade.
- [x] 5.4 Impactos das mudanças e das falhas sobre a continuidade e a qualidade dos serviços.

## Resumo

Este item fecha o ciclo de vida: sistemas **não morrem** depois de entregues — eles são **mantidos, evoluídos e, às vezes, modernizados**. O fio condutor é controlar o **custo da mudança** e proteger a **continuidade e qualidade** do serviço.

1. **Débito técnico** é a consequência de decisões de curto prazo; **documentação** e **modularidade** (alta coesão, baixo acoplamento) são as ferramentas que reduzem esse custo.
2. **Sistemas legados** exigem **sustentação** (manter rodando) e **modernização** (rehost, replatform, refactor, rearchitect, rebuild, replace — ou *strangler fig*).
3. **Interoperabilidade** (trocar e usar informação) e **compatibilidade** (retroativa/forward, versionamento) garantem que sistemas cooperem e evoluam sem quebrar.
4. **Mudanças e falhas** impactam a **continuidade** e a **qualidade** do serviço — exigem gestão de mudança, testes de regressão, monitoramento e estratégias de recuperação (RTO/RPO).

## 1. Débito técnico, documentação, modularidade e acoplamento (5.1)

### 1.1 Débito técnico (technical debt)

- Metáfora de **Ward Cunningham**: atalhos de curto prazo (código apressado, ausência de testes/refatoração) geram uma "dívida" que cobra **juros** — cada mudança futura fica mais cara e arriscada.
- **Quadrante do débito técnico (Martin Fowler):** combina **deliberado × inadvertido** com **imprudente × prudente**:

| | Imprudente | Prudente |
| --- | --- | --- |
| **Deliberado** | "Não temos tempo p/ design" | "Entregamos rápido; vamos pagar depois" |
| **Inadvertido** | Ignorância de boas práticas | "Agora sabemos como deveríamos ter feito" |

- **Juros do débito:** retrabalho, bugs crescentes, lentidão para evoluir, risco de rotatividade (perda de conhecimento).
- **Pagamento:** **refatoração** (reestruturar sem mudar comportamento), testes, melhoria de design, priorização técnica no backlog.
- Sinais (code smells) que indicam débito: **código duplicado**, **método/classes longas**, **obsessão por primitivos**, **inveja de funcionalidade** (*feature envy*), **mudança divergente**, **cirurgia com espingarda** (*shotgun surgery*).

### 1.2 Documentação

- Propósito: reduzir a dependência de "memória de pessoas" e acelerar a manutenção.
- Tipos e boas práticas:

| Tipo | Exemplo |
| --- | --- |
| **Código legível/auto-documentado** | Nomes claros, intenção explícita |
| **README / guia de execução** | Como rodar, configurar, testar |
| **Documentação de API** | OpenAPI/Swagger, JavaDoc (`/** ... */`) |
| **Arquitetura** | Diagrama C4, ADRs (*Architecture Decision Records*) |
| **Operação** | Runbooks, guias de incidente, monitoramento |
| **Domínio/negócio** | Glossário, regras de negócio, decisões |

- **ADR (Architecture Decision Record):** registra **decisões e o contexto** (por que se decidiu assim) — valioso para manutenção futura.
- **Documentação deve viver perto do código** e ser **atualizada junto** (documentação desatualizada é pior que ausente).

### 1.3 Modularidade

- **Módulo:** unidade com **fronteira clara** (interface pública) e **responsabilidade definida**; o interior (implementação) pode mudar sem afetar o exterior.
- Benefícios: **isolamento de mudanças**, **testabilidade**, **reuso**, **trabalho em paralelo** de equipes.
- Princípios de empacotamento: **REP** (Reuse/Release Equivalence), **CCP** (Common Closure), **CRP** (Common Reuse) — coesão de componentes.

### 1.4 Coesão e acoplamento

- **Coesão (interna):** quanto os elementos de um módulo pertencem à mesma responsabilidade. Quanto **mais alta, melhor**.
  - Tipos (do pior ao melhor): **coincidental** < **lógica** < **temporal** < **procedural** < **comunicacional** < **sequencial** < **funcional**.
- **Acoplamento (externo):** grau de dependência entre módulos. Quanto **mais baixo, melhor**.
  - Tipos (do pior ao melhor): **conteúdo** (acessa interno do outro) < **comum** (variável global) < **controle** (passa flag que decide fluxo) < **stamp** (estrutura inteira) < **dados** (só o necessário) < **mensagem** (sem dados).
- **Regra de ouro:** **alta coesão + baixo acoplamento** = manutenibilidade.

### 1.5 SOLID e refatoração (ligação com o item 2.8)

- **SOLID** (SRP, OCP, LSP, ISP, DIP) é o conjunto de princípios que orienta designs de **baixo acoplamento e alta coesão**.
- **Refatoração (refactoring):** mudança na **estrutura interna** do código **sem alterar o comportamento observável**, feita em **passos pequenos**, com **testes** garantindo a segurança (Martin Fowler).
- Catálogo de refatorações: *Extract Method*, *Rename*, *Move Method*, *Inline*, *Extract Class*, *Introduce Parameter Object*, etc.
- Refatorar **antes** de adicionar funcionalidade (preparar o terreno) reduz o débito e o risco.

## 2. Sustentação e modernização de sistemas legados (5.2)

### 2.1 Sistema legado

- **Legado:** sistema antigo, em produção, **crítico para o negócio**, mas difícil/caro de manter — tecnologia obsoleta, documentação escassa, conhecimento perdido, alto acoplamento, débito acumulado.
- **Nem todo sistema antigo é legado**; e **nem todo legado é ruim** — o problema é o **custo/risco de evolução**, não a idade em si.
- **Sustentação:** manter o sistema **rodando** (correções, pequenas evoluções, suporte), enquanto se decide a estratégia de futuro.

### 2.2 Estratégias de modernização

| Estratégia | O que é | Custo/Risco |
| --- | --- | --- |
| **Retain/Encapsulate** | Manter o legado e expor seus serviços via API/`wrapper` (fachada) | Baixo — ganha integração sem reescrever |
| **Rehost (lift-and-shift)** | Mover para nova infraestrutura **sem mudar o código** (ex.: nuvem) | Baixo — rápido, mas mantém limitações |
| **Replatform** | Migrar com **ajustes mínimos** (trocar banco, servidor de aplicação, containerizar) | Médio |
| **Refactor/Rearchitect** | Reestruturar/mudar a **arquitetura** mantendo o escopo funcional | Médio-alto |
| **Rebuild (rewrite)** | **Reescrever do zero** com requisitos (parcialmente) novos | Alto — risco de perder regras embutidas |
| **Replace (COTS/SaaS)** | **Substituir** por produto pronto (pacote/software) | Variável — perde customização |

- **Estratégia do estrangulador (strangler fig pattern, Martin Fowler):** **substituição incremental** — novas funcionalidades vão para o novo sistema, que "estrangula" gradualmente o legado, até este poder ser desligado. Reduz o risco do *big-bang rewrite*.
- **Anti-padrão Big Ball of Mud:** sistema sem arquitetura clara, de evolução caótica — fruto de anos de atalhos.
- Antes de modernizar: **mapear** dependências, **extrair conhecimento** (as regras de negócio vivem no código), **estabelecer testes de caracterização** (que capturam o comportamento atual) e **medir** o retorno.
- **Riscos do rewrite:** perda de funcionalidades não documentadas, interrupção longa, custo alto e baixo valor incremental — por isso o estrangulador costuma ser preferível.

### 2.3 Migração de dados e dual-run

- **Migração de dados** (ETL, validação, reconciliação) é parte crítica da modernização.
- **Dual-run/paralelo:** rodar legado e novo lado a lado, comparando resultados, até a estabilização.
- **Degradação graciosa e fallback:** capacidade de reverter para o legado se o novo falhar.

## 3. Interoperabilidade e compatibilidade (5.3)

### 3.1 Interoperabilidade

- **Definição (ISO/IEC 2382-01 / IEEE):** capacidade de sistemas distintos **trocarem informações e usarem as informações trocadas**.
- Dois níveis (frequentemente cobrados):

| Nível | Significado |
| --- | --- |
| **Sintática** | Capacidade de **trocar** dados (formatos, protocolos, estruturas compatíveis — ex.: JSON, XML, HTTP) |
| **Semântica** | Capacidade de **interpretar/usar** o significado dos dados trocados (vocabulários, ontologias, códigos comuns) |

- **Interoperabilidade técnica** (protocolos, formatos), **organizacional** (processos alinhados) e **semântica** (significado comum) — o e-PING (padrões de interoperabilidade do governo federal brasileiro) e o barramento gov.br são exemplos no setor público.
- Instrumentos: **APIs** (REST/SOAP), **padrões abertos** (JSON, XML, CSV), **mensageria** (filas, eventos), **códigos/identificadores comuns** (ex.: CPF/CNPJ, classificações), **dados abertos**.

### 3.2 Compatibilidade

- **Compatibilidade retroativa (backward):** a nova versão **continua funcionando** para quem usa a antiga (consumidores antigos não quebram).
- **Compatibilidade direta (forward):** a versão atual tolera dados/requisições de versões **futuras** (mais rara/difícil).
- **Versionamento semântico (SemVer):** `MAJOR.MINOR.PATCH` — `MAJOR` quebra compatibilidade; `MINOR` adiciona de forma compatível; `PATCH` corrige sem mudar API.
- **Estratégias de compatibilidade:** versionar na URI/header/media type (ver resumo de APIs), **`Deprecation`/`Sunset` headers** para descontinuar com aviso, janelas de suporte.
- **Depreciação (deprecation):** marcar algo como descontinuado mantendo-o **funcionando** por um período, comunicando a substituição — evita quebras abruptas.
- **Compatibility testing:** testar a nova versão contra clientes/dados da versão anterior.

### 3.3 Interoperabilidade × compatibilidade

- **Interoperabilidade** é sobre **cooperação entre sistemas diferentes**; **compatibilidade** é sobre **uma mesma família evoluir sem quebrar**. Ambas se apoiam em **contratos estáveis** e **padrões abertos**.

## 4. Impactos das mudanças e falhas na continuidade e qualidade (5.4)

### 4.1 Gestão de mudanças

- **Change management (ITIL):** mudanças planejadas, **avaliadas quanto a risco/impacto**, **aprovadas** e **testadas** antes de ir a produção — com **rollback** definido.
- **Gestão de configuração e versionamento (Git):** controlar versões de código e configuração para rastrear e reverter.
- **Pipeline CI/CD:** automação de **build, testes e deploy** reduz erros manuais; **deploy** pequeno e frequente reduz o risco de cada mudança.
- **Testes de regressão:** garantir que uma mudança **não quebrou** o que já funcionava (essencial na manutenção).
- **Feature flags:** liberar mudanças **gradualmente** (canary, blue/green) e desligar rapidamente se algo falhar.

### 4.2 Impacto de falhas

- **Falha** (defeito em produção) afeta a **qualidade percebida** e a **continuidade** do serviço.
- Classificação: **incidente** (interrupção/degradração) × **problema** (causa-raiz subjacente) — ITIL.
- **RCA (Root Cause Analysis):** investigar a **causa raiz** (5 porquês, diagrama de Ishikawa) para evitar recorrência.
- **Postmortem/lições aprendidas:** documento **sem culpa** sobre o que houve e o que melhorar.

### 4.3 Continuidade e confiabilidade do serviço

- **Disponibilidade:** fração de tempo em que o serviço está operante — `(tempo_total − indisponibilidade) / tempo_total` (ex.: 99,9% = "três noves" ≈ 8,76 h/ano de downtime).
- **RTO (Recovery Time Objective):** tempo máximo aceitável para **recuperar** após falha.
- **RPO (Recovery Point Objective):** quantidade máxima de **dados** que se aceita perder (medido em tempo de backup/replicação).
- **MTBF / MTTR:** tempo médio entre falhas / tempo médio de reparo — compõem a disponibilidade.
- **DR (Disaster Recovery) e BCP (Business Continuity):** planos e infraestrutura (réplicas, backup, sites alternados) para manter/restaurar o serviço.
- **Observabilidade:** **métricas, logs e traces** permitem **detectar, diagnosticar e reagir** a falhas; **alertas** (SLO/SLI) disparam antes do usuário perceber.
- **Degradação graciosa e circuit breaker:** isolar falhas para que uma parte não derrube o todo (resiliência).

### 4.4 Qualidade sob mudança contínua

- **Qualidade** é função de **prevenção** (revisão, testes, design) **+ detecção** (monitoramento, testes) **+ reação** (rollback, RCA).
- Ciclo: **mudança pequena e frequente → testes automatizados → deploy seguro → observação → correção rápida** — é o que sustenta a **evolução contínua com qualidade**.
- A **manutenibilidade** (facilidade de corrigir/evoluir) é o atributo de qualidade que amarra todo o item: débito baixo, documentação boa e modularidade são o que permitem evoluir sem degradar.

## Detalhes que merecem destaque

- **Débito técnico (Ward Cunningham)** cobra **juros**: cada mudança fica mais cara; paga-se com **refatoração** e testes.
- **Quadrante de Fowler:** deliberado × inadvertido, imprudente × prudente.
- **Refatoração = mudar estrutura interna SEM mudar comportamento**, em passos pequenos e com testes.
- **Coesão alta + acoplamento baixo** = manutenibilidade; tipos de coesão (coincidental → funcional) e acoplamento (conteúdo → mensagem).
- **Code smells** (duplicação, método longo, feature envy, shotgun surgery) sinalizam débito.
- **Legado** é definido por **custo/risco de evolução**, não por idade.
- **Strangler fig** substitui o legado **incrementalmente**, evitando o risco do *big-bang rewrite*.
- **Modernização:** retain/encapsulate → rehost → replatform → refactor/rearchitect → rebuild → replace (custo/risco crescente).
- **Interoperabilidade sintática (trocar) × semântica (usar o significado)** — a banca adora essa distinção.
- **SemVer `MAJOR.MINOR.PATCH`**: MAJOR quebra compatibilidade; MINOR adiciona compatível; PATCH corrige.
- **Backward (funciona com antigos) × forward (tolera futuros) compatibility**.
- **RTO (tempo p/ recuperar) × RPO (dados que pode perder)** — conceitos de continuidade.
- **Incidente × problema (ITIL)**: incidente é a interrupção; problema é a causa-raiz.
- **Observabilidade** (métricas/logs/traces) + **CI/CD** + **rollback** sustentam evolução com qualidade.

## Comparações que a banca costuma cobrar (certo/errado)

| Conceito A | Conceito B | Diferença-chave |
| --- | --- | --- |
| Coesão | Acoplamento | Coesão é interna (foco); acoplamento é externo (dependência) — alta coesão + baixo acoplamento |
| Refatoração | Otimização | Refatoração muda estrutura (comportamento igual); otimização muda desempenho (pode mudar estrutura) |
| Refatoração | Rewrite | Refatorar é incremental; reescrever é do zero (maior risco) |
| Débito deliberado | Débito inadvertido | Deliberado = decisão consciente; inadvertido = desconhecimento |
| Rehost | Replatform | Rehost muda só infra (lift-and-shift); replatform faz ajustes mínimos |
| Rebuild | Refactor | Rebuild reescreve do zero; refactor reestrutura mantendo escopo |
| Strangler fig | Big-bang rewrite | Estrangulador substitui incrementalmente; big-bang troca tudo de uma vez |
| Interoperabilidade | Compatibilidade | Interoperabilidade = cooperação entre sistemas; compatibilidade = evolução sem quebrar |
| Interoperabilidade sintática | Semântica | Sintática troca dados; semântica interpreta/usufrui o significado |
| Backward compatibility | Forward compatibility | Backward aceita versões antigas; forward tolera futuras |
| RTO | RPO | RTO = tempo p/ recuperar; RPO = dado que pode perder |
| Incidente | Problema | Incidente = interrupção; problema = causa-raiz |
| MTBF | MTTR | MTBF = tempo entre falhas; MTTR = tempo de reparo |
| Documentação de código | Documentação de API | Código é auto-documentado; API é contrato formal (OpenAPI/JavaDoc) |
| Teste de regressão | Teste unitário | Regressão garante que nada quebrou; unitário testa unidade isolada |
| Depreciação | Remoção | Depreciação mantém funcionando com aviso; remoção quebra |

## Pegadinhas e erros comuns

> Cuidado com termos absolutos ("sempre", "nunca", "exclusivamente") e com a troca de requisitos.

- Dizer que **"sistema antigo = sistema legado"** — legado é definido por **custo/risco de evolução**, não idade.
- Achar que **refatoração muda o comportamento** — por definição, **não muda** o comportamento observável.
- Confundir **coesão com acoplamento** (coesão é interna; acoplamento é externo).
- Afirmar que **"quanto mais acoplamento, melhor"** — quer-se **baixo** acoplamento.
- Achar que **interoperabilidade é só "trocar dados"** — exige também **usar o significado** (semântica).
- Trocar **RTO e RPO** (tempo de recuperação × dado perdido).
- Confundir **incidente com problema** (ITIL): incidente é a interrupção; problema é a causa-raiz.
- Achar que **rewrite é sempre a melhor opção** para legados — é a de **maior risco** (perde regras embutidas); o estrangulador costuma ser preferível.
- Supor que **documentação substitui código limpo** (ou vice-versa) — são complementares; documentação desatualizada atrapalha.
- Dizer que **MAJOR no SemVer não quebra compatibilidade** — **MAJOR indica quebra**.
- Achar que **compatibilidade retroativa e direta são a mesma coisa** — retroativa aceita antigos; direta tolera futuros.
- Esquecer o **rollback** ao falar de gestão de mudança — toda mudança deve ter plano de reversão.
- Achar que **CI/CD elimina a necessidade de teste de regressão** — o teste de regressão é parte do pipeline.
- Confundir **disponibilidade** (fração de tempo operante) com **confiabilidade** (executar sem falhas) ou **resiliência** (recuperar-se).

## Notas atômicas relacionadas

```dataview
LIST FROM "20 - Notas"
WHERE disciplina = this.disciplina
  AND contains(tema, this.tema)
SORT file.name ASC
```

## Fontes

- https://martinfowler.com/bliki/TechnicalDebt.html — Martin Fowler, technical debt (débito técnico).
- https://martinfowler.com/bliki/TechnicalDebtQuadrant.html — Martin Fowler, quadrante do débito técnico.
- https://martinfowler.com/bliki/DesignStaminaHypothesis.html — Martin Fowler, Design Stamina Hypothesis (valor do bom design).
- https://martinfowler.com/bliki/StranglerFigApplication.html — Martin Fowler, Strangler Fig (modernização incremental).
- https://refactoring.com/ — Martin Fowler, Refactoring (catálogo e conceito).
- https://refactoring.guru/refactoring — Refactoring Guru, catálogo de refatorações e code smells.
- https://refactoring.guru/design-patterns — Refactoring Guru, padrões de projeto GoF.
- https://refactoring.guru/solid — Refactoring Guru, princípios SOLID.
- https://martinfowler.com/articles/cohesive-concepts.html — Martin Fowler, coesão e modularidade.
- https://semver.org/ — Semantic Versioning 2.0.0 (MAJOR.MINOR.PATCH).
- https://www.iso.org/standard/51073.html — ISO/IEC 25010 (manutenibilidade, compatibilidade e interoperabilidade).
- https://www.gov.br/governodigital/pt-br/estrategias-e-politicas-digitais/interoperabilidade — e-PING, padrões de interoperabilidade de governo.
- https://www.atlassian.com/incident-management/postmortem — Postmortem/lições aprendidas e análise de causa raiz.
- https://sre.google/sre-book/table-of-contents/ — Google SRE Book (confiabilidade, SLO/SLI, disponibilidade).
- https://www.itgovernance.co.uk/blog/what-are-rto-rpo-mtbf-mttr — RTO, RPO, MTBF, MTTR (continuidade de serviços).
- https://datatracker.ietf.org/doc/html/rfc8594 — RFC 8594, Sunset header (descontinuação compatível de APIs).
