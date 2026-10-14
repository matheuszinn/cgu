---
tipo: resumo
disciplina: "Arquitetura e Integração de Sistemas"
tema: "Confiabilidade das aplicações"
status: estudando
data: "2026-10-14"
tags:
  - resumo
  - arquitetura
  - cgu-2026
---

# Resumo: Confiabilidade das aplicações

> [!info] MOC: [[Arquitetura e Integração de Sistemas]]
> Edital nº 1/2026 – CGU – AFFC · **Conhecimentos específicos** · Cargo 4 (TI / Desenvolvimento de Sistemas) · Item 5 — *Confiabilidade das aplicações*.

## Escopo no edital (checklist)

- [x] 5.1 Contêineres, serviços de nuvem e processamento serverless como ambientes de implantação.
- [x] 5.2 Logs, métricas e rastreamento.
- [x] 5.3 Latência, disponibilidade, capacidade e tolerância a falhas.
- [x] 5.4 Diagnóstico de integrações e dependências.
- [x] 5.5 Continuidade, recuperação e degradação de serviços.

## Resumo

**Confiabilidade** é a capacidade de uma aplicação cumprir sua função corretamente, de forma consistente, mesmo sob falhas e condições adversas. Ela não depende de um único fator, mas de um encadeamento:

1. **Onde a aplicação roda (5.1).** O ambiente de implantação define o que o time controla: contêineres empacotam a aplicação e suas dependências (isolamento de processo via *namespaces/cgroups*), serviços de nuvem terceirizam infraestrutura (IaaS/PaaS/SaaS/CaaS/FaaS) e o *serverless* (FaaS) delega ao provedor o escalonamento, o *patching* e boa parte da resiliência — em troca de menor controle, *cold starts* e limites como tempo de execução e *timeout*.
2. **Como enxergar o que acontece (5.2).** Sem observabilidade não há confiabilidade: os três pilares **logs, métricas e rastreamento (traces)** respondem, respectivamente, *o que aconteceu*, *que algo está errado (tendência)* e *onde/por que travou* no caminho distribuído. Logs são eventos (preferir estruturado/JSON), métricas são séries temporais numéricas (baixo custo, alta agregação), rastreamento reconstrói a jornada de uma requisição por vários serviços por meio de **trace ID/span ID** propagados (W3C Trace Context, OpenTelemetry).
3. **O que medir e garantir (5.3).** Confiabilidade se quantifica com **SLI/SLO/SLA** e **error budget**; o desempenho se avalia por **latência** (média engana — usar **percentis p50/p95/p99**), **disponibilidade** ("nines"), **capacidade** (planejamento e escalonamento) e **tolerância a falhas** (redundância, isolamento, padrões de resiliência).
4. **Como diagnosticar (5.4).** Integrações e dependências são o principal vetor de falhas: é preciso correlação de traces/logs, *health checks*, *timeouts*, *circuit breaker*, e ferramentas para investigar latência de terceiros, *retries* e falhas em cascata.
5. **O que fazer quando falha (5.5).** Quando o incidente ocorre, entram a **continuidade** (BCP/BIA, RTO/RPO), a **recuperação** (estratégias de DR) e a **degradação graciosa** (entregar o essencial em vez de tudo ou nada), com respostas do tipo *fallback*, *load shedding* e *feature flags*.

**Ideia-chave para a prova:** confiabilidade é um **trade-off** entre custo, velocidade de inovação e disponibilidade. Não se busca 100% — busca-se o nível adequado ao negócio, medido e gerenciado (é para isso que serve o *error budget*). E sistemas distribuídos **falham por definição**: o objetivo é **tolerar** e **conter** falhas, não fingir que elas não ocorrem.

---

## 1. Contêineres, serviços de nuvem e processamento serverless (5.1)

### 1.1 Contêineres

**Contêiner** é um mecanismo de **isolamento em nível de sistema operacional**: processos são empacotados com suas bibliotecas/dependências e executam isolados, **compartilhando o kernel do host**. Os blocos de construção no Linux são:

- ***namespaces*** → isolam a **visão** do processo (PID, rede, montagem de sistema de arquivos, hostname/UTS, IPC, usuário). Cada contêiner "acha" que tem seu próprio espaço.
- ***cgroups*** (control groups) → limitam e contabilizam **recursos** (CPU, memória, I/O de bloco/rede). É o que permite definir *requests* e *limits*.
- **Camadas de imagem (UnionFS/overlay)** → imagens são **imutáveis** e compostas por camadas empilhadas; instanciar um contêiner é barato e rápido.

**Docker** popularizou o modelo: `Dockerfile` (receita) → **imagem** (artefato imutável) → **contêiner** (instância em execução) → **registry** (repositório de imagens). O **artefato é imutável**: a mesma imagem vai de desenvolvimento a produção; muda-se apenas a **configuração externa**.

**Contêiner × máquina virtual (VM):**

| Aspecto | Contêiner | VM (virtual machine) |
| --- | --- | --- |
| Isolamento | Nível de SO (*namespaces/cgroups*) | Nível de hardware (*hypervisor*) |
| Kernel | Compartilha o kernel do host | Kernel próprio (SO convidado) |
| Tamanho/inicialização | Imagem leve; sobe em segundos/ms | Imagem pesada (GB); sobe em minutos |
| Densidade | Alta (muitos por host) | Menor |
| Segurança/isolamento | Mais fraco (mesmo kernel) | Mais forte (isolamento por hardware) |

**Orquestração (Kubernetes).** Em produção, contêineres raramente rodam soltos. O **orquestrador** (ex.: Kubernetes, Docker Swarm, Nomad) cuida de *agendamento*, *replicação*, *auto-recuperação*, *balanceamento*, *service discovery* e *rolling updates*.

Conceitos Kubernetes relevantes à confiabilidade:

- **Pod** = menor unidade implantável (um ou mais contêineres que compartilham rede/armazenamento).
- **Deployment/ReplicaSet** = mantém o número desejado de réplicas (auto-recuperação: se um pod morre, outro é criado).
- **Service** = IP/DNS estável e balanceamento entre pods.
- **Probes (sondas de saúde):**
  - ***liveness*** → "está vivo?"; se falhar, o **contêiner é reiniciado** (detecta *deadlock*/*hang*).
  - ***readiness*** → "pode receber tráfego?"; se falhar, o pod é **removido do balanceamento** (não é reiniciado). Útil no *startup* e em lentidão momentânea.
  - ***startup*** → protege aplicações **lentas para iniciar**; enquanto não passar, *liveness* e *readiness* ficam suspensas (evita matar app que ainda está subindo).
- ***terminationGracePeriodSeconds*** + tratamento de **SIGTERM** → *graceful shutdown* (parar de aceitar novas requisições, terminar as em curso, fechar conexões).
- ***PodDisruptionBudget* (PDB)** → limita quantos pods podem ficar indisponíveis em manutenções **voluntárias**.
- ***Requests* e *limits*** → garantia mínima e teto de recursos. *Limit* de CPU mal calibrado + *liveness* agressiva podem gerar **CrashLoopBackOff** em cascata (ver pegadinhas).

### 1.2 Fatores do *Twelve-Factor App* ligados à implantação

A metodologia **12-factor** (12factor.net, criada na Heroku ~2011) orienta aplicações *cloud-native*. Fatores mais cobrados aqui:

- **III. Config** → configuração no **ambiente** (*env vars*), não no código. Um mesmo artefato + configurações diferentes = implantações diferentes.
- **VI. Processes** → processos **sem estado** (*stateless*); não guardar sessão em memória local nem dados persistentes em disco local.
- **IX. Disposability** → processos **descartáveis**: *startup* rápido e *shutdown* gracioso (SIGTERM). Habilita escalonamento elástico e *deploys* rápidos; robustez contra "morte súbita" (*crash-only design*).
- **XI. Logs** → tratar logs como **fluxo de eventos**; escrever em **stdout/stderr**, sem gerenciar rotação/armazenamento na aplicação. O ambiente coleta e roteia.

Observação de prova: o 12-factor original fala só em *logs* (2011), mas o princípio se estende hoje a **todos os sinais de telemetria** (métricas e traces): **emita, não gerencie** dentro da aplicação.

### 1.3 Serviços de nuvem (modelos de serviço)

Quanto "mais para cima" no modelo, **mais o provedor gerencia** e **menos controle** o cliente tem — e vice-versa.

| Modelo | O provedor gerencia | O cliente gerencia | Exemplos |
| --- | --- | --- | --- |
| **On-premise** | Nada | Tudo (SO, virtualização, app, dados) | Data center próprio |
| **IaaS** (Infraestrutura) | Virtualização, rede, armazenamento, servidores | SO, *runtime*, app, dados | EC2, Azure VMs, GCE |
| **CaaS** (Contêineres) | Infra + orquestração de contêineres | Imagem/app, config | EKS, AKS, GKE, ECS |
| **PaaS** (Plataforma) | Infra + SO + *runtime* + *middleware* | App e dados | Elastic Beanstalk, App Engine, Heroku |
| **FaaS** (*serverless*) | Tudo, inclusive escalonamento por invocação | Apenas a função/código | AWS Lambda, Azure Functions, Cloud Functions |
| **SaaS** (Software) | Tudo | Apenas uso/dados do usuário | Gmail, Office 365, Salesforce |

- **Nuvem pública / privada / híbrida / multicloud** → modelo de **implantação** (distinto do modelo de *serviço*). Nuvem híbrida combina ambiente próprio com nuvem; *multicloud* usa dois ou mais provedores (reduz *vendor lock-in*, mas aumenta complexidade).
- **Modelo de responsabilidade compartilhada**: a confiabilidade **não** é 100% do provedor. Nuvem cuida de "segurança/confiabilidade **da** nuvem"; o cliente cuida de "**na** nuvem" (configuração, app, dados, IAM, escalonamento). Erro comum de prova: achar que ao migrar para nuvem toda a responsabilidade se transfere ao provedor.

### 1.4 Processamento serverless

**Serverless** = modelo em que o provedor **abstrai servidores** e cobra por **uso** (execução/tempo), não por servidor provisionado. Duas frentes:

- **FaaS** (*Function as a Service*) → funções acionadas por **eventos** (HTTP, fila, agendamento, arquivo). Escala automaticamente **por invocação**, inclusive a zero.
- **BaaS** (*Backend as a Service*) → serviços gerenciados de apoio (auth, banco, filas, armazenamento).

**Características e trade-offs:**

- **Escala automática e "scale to zero"** → não paga quando ocioso; ótimo para carga intermitente.
- ***Cold start*** → primeira invocação (ou após ociosidade) precisa inicializar o *runtime*/contêiner → **latência extra**. Mitigações: ***provisioned concurrency*** (instâncias pré-aquecidas), imagens menores, *runtime* mais rápido, código de inicialização enxuto.
- **Limites impostos pelo provedor**: **tempo máximo de execução** (*timeout*, ex.: 15 min no AWS Lambda), memória, tamanho do pacote, concorrência.
- **Concorrência e *throttling*** → há um teto de invocações simultâneas; ao estourá-lo, invocações são *throttled* (erro/reenfileiramento). `provisioned concurrency` reserva capacidade; `reserved concurrency` limita.
- **Estado** → funções devem ser **stateless**; estado vai para serviços externos (S3, DynamoDB, Redis).
- **Idempotência é obrigatória** → como *retries* são comuns (falha de função, entrega *at-least-once* de eventos), a função deve poder ser executada mais de uma vez **sem efeitos duplicados** (ex.: cobrar duas vezes).
- **Observabilidade distribuída** → *cold start*, execuções assíncronas e *fan-out* dificultam o diagnóstico; exige *tracing* e métricas de concorrência/erros.

**Erros clássicos em serverless:** respostas de erro podem vir como **HTTP 200** se não forem mapeadas corretamente (*e.g.* integração API Gateway + Lambda); falhas padrão do Lambda **não** viram código HTTP automaticamente.

### 1.5 Boas práticas de implantação (relevantes à confiabilidade)

- **Deploy imutável** e imagem versionada (tag por *digest*/*commit*), nunca "editar em produção".
- **Rolling update** (substituição gradual), ***blue/green*** (dois ambientes, troca de tráfego, *rollback* instantâneo) e ***canary*** (liberar para pequena % de usuários e observar antes de generalizar).
- **Rollback automatizado** disparado por SLI (erro/latência pioram → reverte).
- **Escalonamento horizontal** e **elástico** para absorver picos.

---

## 2. Logs, métricas e rastreamento (5.2)

### 2.1 Observabilidade × monitoramento

- **Monitoramento** = observar **métricas conhecidas** e alertar sobre condições **pré-definidas** ("o que eu já sei que pode quebrar").
- **Observabilidade** = capacidade de **fazer perguntas arbitrárias** sobre o sistema a partir de suas saídas externas e entender **por que** algo falhou (não só **que** falhou). Exige correlação entre sinais.

Os **três pilares (ou sinais)** da observabilidade são **logs, métricas e traces**. Alguns autores estendem para **MELT** (Metrics, Events, Logs, Traces).

| Pilar | O que é | Natureza | Responde | Custo/uso |
| --- | --- | --- | --- | --- |
| **Logs** | Registros de eventos com *timestamp* | Texto/estruturado (JSON) | "O que aconteceu?" | Alto volume; ótimo para contexto e detalhe |
| **Métricas** | Valores numéricos em séries temporais | Numérico, agregável | "Algo está errado? (tendência/limites)" | Baixo custo, alta agregação; bom para alertas |
| **Traces** | Jornada de uma requisição por serviços | Árvore de *spans* | "Onde/por que travou?" | Correlaciona a causa ao longo do caminho |

**Regra de ouro:** **métricas** avisam que algo está errado; **traces** mostram **por onde** o problema passou; **logs** fornecem o **contexto** para a causa-raiz. Combinados reduzem **MTTD** (tempo para detectar) e **MTTR** (tempo para resolver).

### 2.2 Logs

- **Log estruturado** (JSON com campos nomeados, ex.: `level`, `service`, `trace_id`, `user_id`, `duration_ms`) é muito superior ao texto livre → permite busca, filtro e correlação.
- **Níveis**: `DEBUG`, `INFO`, `WARN`, `ERROR`, `FATAL`. Boa prática: não logar senha/segredo/dado pessoal (*PII*); não transformar log em *stream* de debug em produção.
- **Gravidade × severidade:** mensagens devem ter **carimbo de tempo confiável**, **contexto** (ID de correlação) e **formato consistente**.
- ***Centralização/agregação***: a aplicação escreve em **stdout/stderr** e um agente (*Fluentd*, *Fluent Bit*, *Vector*, *Filebeat*) envia para um *backend* (Elasticsearch/OpenSearch + Kibana, Loki, Splunk, Datadog...). Isso é o fator XI do 12-factor.
- **Log distribuído**: para rastrear uma requisição que passa por vários serviços, injeta-se um **correlation ID / trace ID** em todas as linhas.

### 2.3 Métricas

- **Série temporal** = conjunto de pontos `(timestamp, valor)` identificados por **labels/tags** (ex.: `http_requests_total{method="GET", status="500"}`).
- **Tipos (Prometheus):** *counter* (só cresce), *gauge* (sobe/desce), *histogram* (distribuição, permite percentis) e *summary* (quantis pré-calculados).
- **Percentis (p50/p95/p99):** em latência, a **média engana** — poucas requisições muito lentas não movem a média, mas arruínam a experiência. Por isso se monitora **p95/p99** (e p99.9 em sistemas críticos). Cuidado com a **"armadilha da cardinalidade"**: muitas combinações de *labels* explodem o custo de armazenamento.
- **Os 4 Sinais Dourados (Google SRE):**
  1. **Latência** — tempo de atendimento; **separar** latência de requisições **bem-sucedidas** das **falhas** (um erro rápido de 500 pode "melhorar" a média falsamente; um erro **lento** é pior ainda).
  2. **Tráfego** — demanda sobre o sistema (ex.: requisições/segundo, sessões, transações).
  3. **Erros** — taxa de requisições que falham, **explícitas** (HTTP 500), **implícitas** (HTTP 200 com conteúdo errado) ou **por política** (acima do tempo prometido).
  4. **Saturação** — quão "cheio" está o sistema. Muitos sistemas degradam **antes** de 100%; definir meta de utilização. **Aumento de latência é indicador antecipado de saturação** (medir p99 em janela curta).
- **Métodos complementares:**
  - **RED** (para serviços/*microservices*): **R**ate (taxa), **E**rrors (erros), **D**uration (duração/latência).
  - **USE** (para **recursos**, de Brendan Gregg): **U**tilization, **S**aturation, **E**rrors. Aplicado a CPU, memória, disco, rede.
  - *Golden Signals* ≈ combinação de RED (latência/tráfego/erros) + saturação (do USE).

### 2.4 Rastreamento (tracing) distribuído

- **Span** = unidade de trabalho com início/fim, nome, atributos, status e *span ID*. **Trace** = árvore/conjunto de *spans* ligados por um **trace ID** comum.
- **Context propagation**: o **trace ID** e o **parent span ID** viajam entre serviços (em cabeçalhos HTTP, mensagens, etc.). O padrão de fato é o **W3C Trace Context**, com o cabeçalho **`traceparent`** no formato `<versão>-<trace-id>-<parent-id>-<trace-flags>` e o **`tracestate`** para dados específicos de fornecedor.
- **Span kinds**: *server*, *client*, *producer*, *consumer*, *internal*.
- **Amostragem (*sampling*)**: rastrear 100% do tráfego é caro; usam-se amostragens (*head sampling* na origem vs *tail sampling* no coletor, preservando traces "interessantes" — erros/lentos).
- **OpenTelemetry (OTel)** — projeto CNCF **vendor-neutral**: padroniza APIs/SDKs para instrumentar traces, métricas e logs, o **protocolo OTLP** e o **Collector** (recebe, processa e exporta). Permite **instrumentação automática** (agentes) e **correlação entre sinais**.
- **Service mesh** (Istio, Linkerd) pode gerar traces/métricas de rede sem alterar o código.

### 2.5 Alertas (ligação com SLO)

- Alertas **baseados em sintomas** (o usuário está sofrendo) > alertas baseados em **causas** (CPU alta) — menos ruído.
- **Multi-window, multi-burn-rate**: para defender um SLO, alertar quando o *error budget* queima **rápido** em várias janelas (ex.: 5 min + 1 h para incidentes graves), evitando alarmes inúteis. Alertar em cada erro isolado gera fadiga de alertas.

---

## 3. Latência, disponibilidade, capacidade e tolerância a falhas (5.3)

### 3.1 Latência

- **Latência** = tempo para atender uma requisição (inclui fila, processamento, I/O, rede, dependências).
- **Latência × throughput (vazão):** ≥ relacionadas; acima de certo limiar há um **"penhasco de desempenho"** (*performance cliff*): mais carga → filas → latência dispara → *timeouts* → *retries* → espiral.
- **Medir com percentis** (p50, p95, p99). Diferenciar latência **de sucesso** e **de erro**.
- Fontes comuns: **contenção de recursos** (CPU throttling, *lock* de banco), *cold start*, **saltos de rede** entre serviços, dependências lentas, **N+1 de chamadas** (fan-out), *garbage collection*.
- **Técnicas de redução:** *cache*, assincronismo, *pool* de conexões, *timeouts* adequados, evitar chamadas em cascata seriais (paralelizar), *CDN*, *edge*, compressão.

### 3.2 Disponibilidade

- **Disponibilidade** = fração do tempo em que o serviço está utilizável (ou proporção de requisições bem-sucedidas, para SLIs por requisição).
  - Fórmula simples: `(tempo total − indisponibilidade) / tempo total × 100%`.
- **"Nines" (noves)** — decorar a tabela:

| Nines | Disponibilidade | Indisponibilidade/ano | Indisponibilidade/mês | Indisponibilidade/dia |
| --- | --- | --- | --- | --- |
| 2 | 99% | ~3,65 dias | ~7,2 h | ~14,4 min |
| 3 | 99,9% | ~8,77 h | ~43,8 min | ~1,44 min |
| 4 | 99,99% | ~52,6 min | ~4,38 min | ~8,64 s |
| 5 | 99,999% | ~5,26 min | ~26 s | ~864 ms |
| 6 | 99,9999% | ~31,5 s | ~2,6 s | ~86 ms |

- Quanto mais "noves", **mais caro** e complexo. Ir de *failover* simples (ativos/passivos) para **ativo-ativo** é o que costuma habilitar 5 noves.
- **Disponibilidade de dependências (cálculo):** em **série** (A depende de B), as disponibilidades **se multiplicam** → a disponibilidade **cai** (`0,999 × 0,999 ≈ 0,998`). Componentes em **paralelo/redundantes** aumentam a disponibilidade (`1 − (1−p)^n`). **Corolário:** quanto mais dependências em série, menor a disponibilidade global → reduza dependências e adicione redundância.
- **Falha ≠ indisponibilidade:** um sistema pode estar "no ar" e **degradado**. Por isso existe SLO de latência, além de SLO de disponibilidade.

### 3.3 SLI, SLO e SLA e *error budget*

- **SLI (*Service Level Indicator*)** = **métrica** quantitativa de um aspecto do serviço (proporção de requisições bem-sucedidas, latência p99, *freshness* de dados). Deve ser **específica e mensurável**; escala 0–100% para permitir *error budget*.
- **SLO (*Service Level Objective*)** = **meta/alvo** para o SLI (ex.: disponibilidade ≥ 99,9%; 99% das requisições < 900 ms em 4 semanas). Recomenda-se **ter poucos SLOs**. Não é realista/útil perseguir 100%.
- **SLA (*Service Level Agreement*)** = **contrato** (com consequências — multa, crédito, ação jurídica) com cliente/usuário. O SLA **externo** costuma ser **mais frouxo** que o SLO interno (ex.: SLA 99,9%, SLO interno 99,95%).
  - Teste prático: "o que acontece se o objetivo não for atingido?". **Sem consequência explícita → é SLO, não SLA.**
- **Error budget (orçamento de erro)** = `100% − SLO`. Ex.: SLO de 99,9% → 0,1% de erros permitidos. Gerencia o **trade-off confiabilidade × inovação**: se há orçamento sobrando, pode arriscar mais *deploys*; se esgotado, **congela mudanças e prioriza estabilidade**.
  - Exemplo de prova: SLO de 99,9% e 3 milhões de requisições em 4 semanas → orçamento de **3.000 erros**. Uma falha que causa 1.500 erros consome **50%** do orçamento.

### 3.4 Capacidade e escalonamento

- **Planejamento de capacidade** = prever demanda e provisionar recursos para atendê-la dentro do SLO, considerando picos e folga (*headroom*).
- **Escalonamento:**
  - **Vertical (*scale up/down*)**: aumentar CPU/memória da instância.
  - **Horizontal (*scale out/in*)**: adicionar/remover **instâncias** — preferível para resiliência e elasticidade.
- **Kubernetes:**
  - **HPA** (*Horizontal Pod Autoscaler*) → ajusta o **número de réplicas** com base em CPU/memória (padrão) ou **métricas customizadas/externas** (fila, latência, RPS). Controla por *requests*, não pela capacidade real; tem **atraso** (pipeline métrica→decisão→pod pronto ⇒ de ~30 s a >3 min).
  - **VPA** (*Vertical PodAutoscaler*) → ajusta recursos (CPU/memória) dos pods; **cuidado** ao usar VPA e HPA **no mesmo sinal** (decisões conflitantes).
  - **KEDA** → escalonamento por **eventos** (profundidade de fila etc.).
  - **Cluster Autoscaler** → ajusta o número de **nós**.
- **Limites de recurso** mal calibrados prejudicam: *requests* superdimensionados "cegam" o HPA; CPU *limit* apertado provoca *throttling* e *restarts*.
- **Autoscaling é reativo** → há latência entre o pico e a nova capacidade; mitigar com métricas de antecipação, escalonamento agendado e *provisioned capacity*.

### 3.5 Tolerância a falhas e padrões de resiliência

**Tolerância a falhas** = continuar funcionando (talvez degradado) quando componentes falham. Estratégias estruturais:

- **Redundância** (réplicas, múltiplas zonas/regiões), **balanceamento de carga**, **failover**, **replicação** de dados (síncrona × assíncrona).
- **Isolamento**: *bulkhead*, *cell-based architecture* (células/domínios de falha independentes para limitar o **raio de explosão**/*blast radius*).

**Padrões de resiliência (cobrança alta em prova):**

| Padrão | Objetivo |
| --- | --- |
| **Timeout** | Limitar o tempo de espera por uma resposta; evita "pendurar" recursos indefinidamente |
| **Retry (com backoff exponencial + jitter)** | Repetir falhas **transitórias**; o *jitter* evita efeito manada (retries sincronizados) |
| **Circuit Breaker** | Interromper chamadas a um serviço que está falhando; estados **fechado → aberto → meio-aberto**; dá tempo à dependência de se recuperar |
| **Bulkhead** | Isolar recursos (pools/fios) por dependência; falha de um não derruba os outros |
| **Fallback** | Resposta alternativa/valor padrão/*cache* quando a primária falha |
| **Load Shedding** | **Recusar/reduzir** trabalho sob sobrecarga para preservar o essencial |
| **Backpressure** | Sinalizar ao produtor para desacelerar (controle de fluxo) |
| **Rate limiting / throttling** | Limitar taxa de requisições (proteção e *fairness*) |

Detalhes finos cobrados:

- **Retry perigoso:** repetir operações **não idempotentes** causa duplicidade (cobrança dupla). *Retry* sem limite + *timeout* longo = **amplificação de carga** e **falha em cascata** (efeito *retry storm*).
- **Circuit breaker** tem **três estados**: *closed* (passa), *open* (bloqueia, falha rápido), *half-open* (permite algumas tentativas de teste). *Fallback* pode ser combinado ao breaker.
- **Idempotência** é pré-requisito para *retries* seguros.
- ***Graceful degradation*** (degradação graciosa): reduzir funcionalidade não essencial para manter o núcleo. Diferente de ***load shedding*** (recusar/reduzir trabalho) e de ***fault tolerance*** (mascarar a falha com redundância).

### 3.6 Falhas em cascata e feedback positivo

- **Falha em cascata** ocorre quando a falha de um componente **sobrecarrega** os demais, propagando o problema (***positive feedback***).
- Cadeia clássica: sobrecarga → filas crescem → latência sobe → ***timeouts*** → **retries** (amplificam carga) → mais sobrecarga → *threads/conexões* esgotam → serviço cai → dependentes caem.
- **Prevenção:** *timeouts* e *retries* com limites, *circuit breakers*, *load shedding*, reservar capacidade de emergência, evitar filas ilimitadas, desligar *retries* em cascata, isolar.

### 3.7 Testes de confiabilidade

- **Testes de carga/stress** (verificar comportamento no limite e o "penhasco").
- ***Chaos Engineering***: injetar falhas **controladas** para descobrir fraquezas. Princípios: (1) definir **estado estacionário** (steady state) mensurável; (2) formular **hipótese**; (3) variar eventos do mundo real (latência, perda de nó, dependência fora do ar); (4) **minimizar o raio de explosão**; (5) ter **critérios de abortar**. Prática de **Game Days**. Origem: **Netflix (Chaos Monkey, Chaos Kong)**; métrica de *steady state* deles: *Streams Per Second*.

---

## 4. Diagnóstico de integrações e dependências (5.4)

### 4.1 Por que dependências são o ponto crítico

Em sistemas distribuídos, a maioria dos incidentes envolve **integrações** (APIs de terceiros, bancos, filas, *caches*, serviços internos). O diagnóstico precisa responder: **a falha é minha ou da dependência? onde está o gargalo? qual o impacto?**

### 4.2 Instrumentos de diagnóstico

- **Distributed tracing ponta a ponta** → mostra o *span* lento/errado e a dependência culpada; essencial com *fan-out* (uma requisição → muitos serviços).
- **Correlação de sinais** → amarrar **trace + log + métrica** por `trace_id` (a OpenTelemetry busca exatamente isso). Fecha o ciclo "métrica diz que há erro → trace diz onde → log diz o motivo".
- **Health checks / probes** → liveness, readiness, startup (K8s); endpoints de saúde para o balanceador tirar instância ruim de rotação.
- **SLOs de dependências** → definir e monitorar o nível esperado de cada dependência crítica; usar *fallback* quando ela degrada.
- **Service mesh** → telemetria de rede (latência, retries, taxas de erro), *circuit breaking* e *mTLS* sem tocar no código.
- **Testes sintéticos (canários/*blackbox*)** → verificar a experiência real do usuário mesmo sem tráfego.
- **Dashboards e alertas** por dependência, com *error budget*.

### 4.3 Padrões de integração resiliente

- **Timeouts** por chamada (**menores** que o timeout do cliente, para que o erro apareça em quem chamou).
- **Retries** só para falhas **transitórias** e operações **idempotentes**; *backoff* exponencial + *jitter*; limite de tentativas.
- **Circuit breaker** por dependência (isola a falha daquela dependência específica).
- **Bulkhead** (pools separados por dependência) e **fallback** (dados em *cache*, resposta parcial, fila para reprocessar).
- **Backpressure** e **filas** (com DLQ — *dead letter queue*) para desacoplar e absorver picos.
- **Idempotência** e chaves de idempotência para reprocessamento seguro.
- **Contratos/versionamento** de API e *schema* (compatibilidade), evitando quebra de integração.

### 4.4 Causas comuns de falha de integração

- **Falhas parciais/**de rede: pacotes perdidos, DNS, latência variável (***gray failures*** — falhas intermitentes e difíceis de reproduzir).
- **Dependência lenta (não morta)** → pior que dependência fora: consome recursos e propaga lentidão.
- **Configuração/credencial** expirada, *quota*/*rate limit* excedido.
- **Retries** mal configurados (amplificação), *timeouts* desalinhados.
- **Mudança de contrato** (breaking change) na dependência externa.

### 4.5 Diagnóstico de incidentes e postmortem

- **Métricas de resposta a incidente:** **MTTD** (detecção), **MTTA** (reconhecimento), **MTTR** (resolução), **MTBF** (tempo médio entre falhas).
- **Cultura *blameless* (sem culpa):** o postmortem busca **causa-raiz sistêmica** e ações de melhoria, não punir pessoas. Inclui *timeline*, impacto, causa, o que funcionou/falhou e **itens de ação**.
- Ferramentas: **runbooks/playbooks**, plantão (*on-call*), gerência de incidente, comunicação com *stakeholders*.

---

## 5. Continuidade, recuperação e degradação de serviços (5.5)

### 5.1 Conceitos de continuidade

- **Business Continuity (BC)** / **BCP** = capacidade **ampla** de manter a organização funcionando durante e após a disrupção (pessoas, processos, fornecedores, instalações, TI, comunicação).
- **Disaster Recovery (DR)** = parte **técnica**: restaurar **sistemas e dados**. DR está **contido** na continuidade (não são sinônimos).
- **BIA (*Business Impact Analysis*)** = análise que identifica **atividades críticas** e quantifica o impacto da interrupção; **fundamenta o RTO/RPO**. Também define a **Minimum Business Continuity Objective** (nível reduzido aceitável durante a recuperação).
- Norma de referência: **ISO 22301** (Sistema de Gestão de Continuidade de Negócios). "Plano sem exercício é só suposição" → **testes/exercícios** são exigência.

### 5.2 RTO, RPO e MTPD

- **RTO (*Recovery Time Objective*)** = **tempo máximo aceitável** de interrupção até o serviço voltar (mede **downtime**). "Quanto tempo podemos ficar fora?".
- **RPO (*Recovery Point Objective*)** = **quantidade máxima aceitável de perda de dados**, medida em tempo desde o último ponto íntegro (mede **perda de dados**). "Quanto de dado podemos perder?".
- **MTPD (*Maximum Tolerable Period of Disruption*)** = tempo máximo que a disrupção pode durar antes de dano inaceitável ao negócio. O **RTO deve caber dentro do MTPD**.
- **Regra econômica:** RTO/RPO **menores** ⇒ **maior custo** e complexidade. São decisões de **negócio**, não só técnicas.
- **RTO × MTTR:** conceitualmente próximos (ambos medem tempo relacionado a indisponibilidade), mas **RTO é meta/alvo** e **MTTR é medição** histórica.

### 5.3 Estratégias de recuperação de desastre (DR)

Da **mais barata/lenta** para a **mais cara/rápida** (RTO/RPO **decrescentes**):

1. **Backup & Restore** (backup e restauração) → mais barata, **maior** RTO/RPO. Dados em *backup*; infraestrutura recriada do zero. Bom para cargas não críticas.
2. **Pilot Light** (luz piloto) → núcleo mínimo ligado (ex.: dados replicados), demais recursos criados sob demanda no desastre. RTO/RPO **intermediários**.
3. **Warm Standby** (standby aquecido) → réplica **funcional em escala reduzida**, pronta para ser ampliada. RTO/RPO **baixos**.
4. **Multi-Site Active/Active** (ativo-ativo multirregião) → **menor** RTO/RPO (quase zero), **maior custo**. Requer replicação contínua e roteamento entre sites.

Outros elementos: **replicação** (síncrona × assíncrona), **snapshots**, **failover/failback** automáticos, **multi-AZ** (alta disponibilidade) × **multi-região** (DR), **backups imutáveis** e **testados** (restauração é a evidência que auditores querem, não o log de backup).

### 5.4 Degradação de serviços (graceful degradation)

- **Degradação graciosa** = **reduzir funcionalidades não essenciais** para manter o **núcleo** funcionando (ex.: esconder recomendações, servir conteúdo "cacheado", aceitar pedido para processar depois).
- **Espectro de degradação:** de "perda total" → funcionalidade parcial → resposta *cacheada*/*stale* → *read-only* → núcleo mínimo.
- **Classificação por criticidade** (ex.: P1 essencial, P2, P3) → sob pressão, **cortar primeiro o menos crítico** (*priority-based degradation*).
- **Ferramentas:** *circuit breakers*, *feature flags* (desligar funcionalidades sem *deploy*), *fallbacks*, *cache-first reads*, *load shedding*, *rate limiting*, filas e *backpressure*.
- **Escalonamento gracioso:** recusar (429) com mensagem clara é melhor que travar e derrubar todos.
- **Continuidade no desenho:** idempotência, filas com *dead letter queue*, *read replicas*, modo somente leitura, *bulkheads*, células.

### 5.5 Backup como pilar da recuperação

- **3-2-1**: **3** cópias, em **2** mídias diferentes, **1** fora do site.
- **Backups imutáveis/invioláveis** (proteção contra *ransomware* e exclusão).
- **Teste de restauração periódico** (um backup nunca testado não é confiável).
- Política de retenção e **criptografia**.

---

## Detalhes que merecem destaque

- **12-factor:** fator **III (Config no ambiente)**, **VI (processos stateless)**, **IX (disposability — startup rápido + graceful shutdown)**, **XI (logs como stream em stdout)**. O 12-factor original **não** mencionava métricas nem tracing (é de 2011).
- **Contêiner compartilha o kernel**; **VM tem kernel próprio**. Isolamento de contêiner = **namespaces + cgroups**.
- **Probes K8s:** *liveness* **reinicia** o contêiner; *readiness* apenas **tira do balanceamento** (não reinicia); *startup* protege app **lento para iniciar**.
- **Cold start** é o principal custo de latência do **serverless**; mitigado por ***provisioned concurrency***.
- **FaaS cobra por uso e escala por invocação**; exige aplicação **stateless** e **idempotente**; sofre **timeout** e **throttling** do provedor.
- **Três pilares da observabilidade:** logs, métricas, **traces** (+ eventos = MELT). Logs = eventos; métricas = números no tempo; traces = jornada distribuída.
- **trace ID/span ID** e **W3C Trace Context (`traceparent`)** são o que permite **propagação de contexto** entre serviços.
- **OpenTelemetry** = padrão **vendor-neutral** (CNCF) para instrumentar e exportar telemetria (OTLP + Collector).
- **4 Sinais Dourados:** latência, tráfego, erros, saturação. **RED** = taxa/erros/duração (serviços); **USE** = utilização/saturação/erros (recursos).
- **Latência se mede por percentis** (p95/p99), nunca só pela média. **Erros em latência devem ser analisados à parte.**
- **SLI** = indicador (medida); **SLO** = meta; **SLA** = contrato com consequência. Sem consequência explícita → **é SLO, não SLA**.
- **Error budget = 100% − SLO**; governa o ritmo de *deploys* (se esgotado, congela mudança).
- **Nines:** 99,9% ≈ **8,8 h/ano**; 99,99% ≈ **53 min/ano**; 99,999% ≈ **5,3 min/ano**.
- **Disponibilidade em série se multiplica** (cai); **redundância em paralelo** aumenta.
- **RTO** = tempo de parada aceitável; **RPO** = perda de dados aceitável; ambos **dentro do MTPD**; **menores ⇒ mais caros**.
- **Estratégias de DR (ordem de custo crescente):** Backup & Restore → Pilot Light → Warm Standby → Multi-Site Active/Active.
- **Padrões de resiliência:** timeout, retry (backoff+jitter), circuit breaker (closed/open/half-open), bulkhead, fallback, load shedding, backpressure, rate limiting.
- **Idempotência** é pré-requisito de *retry* seguro; **retry sem controle amplifica carga** e causa **falha em cascata**.
- **Chaos engineering:** estado estacionário + hipótese + raio de explosão mínimo + critérios de abortar (Netflix/Chaos Monkey).
- **Degradação graciosa** reduz funcionalidade; **tolerância a falhas** mascara com redundância; **load shedding** recusa/reduz trabalho.
- **BIA** fundamenta **RTO/RPO**; **ISO 22301** é a norma de continuidade; **DR ⊆ Continuidade**.
- **Nuvem:** responsabilidade compartilhada — o provedor garante **da** nuvem; o cliente, **na** nuvem.

## Comparações que a banca costuma cobrar (certo/errado)

| Conceito A | Conceito B | Diferença-chave |
| --- | --- | --- |
| Contêiner | Máquina virtual | Contêiner compartilha o **kernel** do host e isola por *namespaces/cgroups*; VM tem **kernel próprio** e isolamento por *hypervisor* |
| Contêiner (IaaS/CaaS) | Serverless (FaaS) | Contêiner exige gerir *runtime*/escala; FaaS **abstrai servidor**, escala por invocação e cobra por uso |
| Logs | Métricas | Logs = **eventos** (o que aconteceu); métricas = **números no tempo** (tendência/alerta) |
| Métricas | Traces | Métricas dizem **que** há problema; traces mostram **onde** no caminho distribuído |
| Monitoramento | Observabilidade | Monitoramento = métricas/alertas **conhecidos**; observabilidade = **explorar perguntas arbitrárias** a partir dos sinais |
| SLI | SLO | SLI = **medida**; SLO = **meta** sobre o SLI |
| SLO | SLA | SLO = objetivo **interno** sem consequência externa; SLA = **contrato** com penalidade |
| RTO | RPO | RTO = **tempo** máximo de parada; RPO = **perda de dados** máxima (em tempo) |
| RTO | MTPD | RTO é a meta de recuperação e deve **caber dentro** do MTPD (limite tolerável de disrupção) |
| MTTR | MTTD | MTTR = tempo para **resolver**; MTTD = tempo para **detectar** |
| Readiness probe | Liveness probe | Readiness **tira do balanceamento** (não reinicia); liveness **reinicia** o contêiner |
| Escalonamento horizontal | Escalonamento vertical | Horizontal = mais **instâncias**; vertical = mais **recursos** por instância |
| HPA | VPA | HPA ajusta **réplicas**; VPA ajusta **recursos** dos pods (evitar conflito no mesmo sinal) |
| Circuit breaker | Retry | Circuit breaker **para** de chamar (falha rápido); retry **repete** a chamada |
| Bulkhead | Fallback | Bulkhead **isola** recursos; fallback dá **resposta alternativa** |
| Degradação graciosa | Load shedding | Degradação **reduz funcionalidade**; load shedding **recusa/reduz trabalho** sob sobrecarga |
| Alta disponibilidade (multi-AZ) | Recuperação de desastre (DR) | HA cobre falhas **locais** (zona); DR cobre desastre **regional/amplo** |
| Continuidade de negócio (BC) | Disaster recovery (DR) | BC = manter a **organização** operando (amplo); DR = restaurar **sistemas/dados** (técnico) |
| Backup & Restore | Multi-Site Active/Active | Backup & Restore = **maior** RTO/RPO e menor custo; Active/Active = **menor** RTO/RPO e maior custo |

## Pegadinhas e erros comuns

> A banca adora **termos absolutos** ("sempre", "nunca", "exclusivamente") e **trocas sutis** de definição.

- Dizer que contêiner é "uma máquina virtual leve" — **não é VM**: compartilha o **kernel** do host.
- Achar que **readiness** reinicia o pod — quem reinicia é a **liveness**; readiness só **remove do tráfego**.
- Trocar **liveness** por **startup**: a *startup* existe justamente para **app lenta para iniciar**, suspendendo as demais.
- Afirmar que, no serverless, **não há limites** de tempo/concorrência — há **timeout**, **throttling** e limites de pacote.
- Ignorar o **cold start** como fonte de latência em FaaS.
- Achar que, com serverless, o provedor assume **toda** a confiabilidade — vale a **responsabilidade compartilhada**.
- Afirmar que o **12-factor** já previa métricas e tracing — ele menciona apenas **logs** (2011).
- Confundir **observabilidade** (explorar/entender) com **monitoramento** (vigiar o conhecido) — ou tratá-los como sinônimos.
- Trocar **logs** por **métricas** ao falar de "séries temporais numéricas".
- Esquecer que **trace** depende de **propagação de contexto** (trace ID/span ID) — sem isso, não há rastreamento distribuído.
- Medir **latência** só pela **média**: a média esconde a cauda (p95/p99).
- Somar **latência de sucesso e de erro** sem separar — erro **rápido** mascara a média; erro **lento** é pior.
- Trocar **SLI** (indicador/medida) por **SLO** (meta) — e **SLO** por **SLA** (contrato com consequência).
- Dizer que se busca **100%** de disponibilidade — não é realista nem desejável; usa-se **error budget**.
- Errar os **nines**: 99,9% é **~8,8 h/ano** (~43 min/mês), **não** minutos/ano.
- Achar que **redundância em série** aumenta a disponibilidade — componentes **em série** a **reduzem** (multiplicação).
- Trocar **RTO** (tempo) com **RPO** (perda de dados). **RTO** = quanto tempo fora; **RPO** = quanto dado perdido.
- Achar que **RTO/RPO menores são mais baratos** — é o **contrário**: menor RTO/RPO ⇒ **maior** custo.
- Confundir **HA (multi-AZ)** com **DR (multi-região)** — HA não substitui DR.
- Tratar **retry** como sempre benéfico: retry **sem limite/backoff** **amplifica** carga e causa **falha em cascata**; exige **idempotência**.
- Achar que **circuit breaker** e **retry** são a mesma coisa (um **para**, o outro **repete**).
- Confundir **degradação graciosa** (reduzir funcionalidades) com **tolerância a falhas** (mascarar com redundância) e com **load shedding** (recusar trabalho).
- Dizer que **DR** e **continuidade de negócio** são sinônimos — **DR ⊆ BC**.
- Esquecer que um **backup apenas criado, nunca testado**, **não** garante recuperação.
- Confundir **modelo de serviço** (IaaS/PaaS/SaaS/FaaS) com **modelo de implantação** (pública/privada/híbrida/multicloud).
- Achar que **HPA** escala os **nós** — quem escala nós é o **Cluster Autoscaler**; HPA escala **pods**.
- Ignorar o **atraso do autoscaling** (a capacidade nova não aparece instantaneamente após o pico).

## Notas atômicas relacionadas

```dataview
LIST FROM "20 - Notas"
WHERE disciplina = this.disciplina
  AND contains(tema, this.tema)
SORT file.name ASC
```

## Fontes

- https://12factor.net/ (The Twelve-Factor App — metodologia cloud-native)
- https://12factor.net/config (III. Config — config no ambiente)
- https://12factor.net/disposability (IX. Disposability — startup rápido e shutdown gracioso)
- https://12factor.net/logs (XI. Logs — logs como fluxo de eventos)
- https://kubernetes.io/docs/concepts/workloads/pods/probes/ (Kubernetes — Liveness, Readiness e Startup probes)
- https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/ (Kubernetes — configurar probes)
- https://kubernetes.io/docs/concepts/workloads/autoscaling/horizontal-pod-autoscale/ (Kubernetes — Horizontal Pod Autoscaler)
- https://cloud.google.com/blog/products/containers-kubernetes/kubernetes-best-practices-setting-up-health-checks-with-readiness-and-liveness-probes (Google — health checks)
- https://opentelemetry.io/docs/concepts/observability-primer/ (OpenTelemetry — observability primer)
- https://opentelemetry.io/docs/what-is-opentelemetry/ (OpenTelemetry — o que é)
- https://opentelemetry.io/docs/concepts/signals/traces/ (OpenTelemetry — traces/spans)
- https://opentelemetry.io/docs/concepts/context-propagation/ (OpenTelemetry — context propagation)
- https://www.w3.org/TR/trace-context/ (W3C Trace Context — traceparent/tracestate)
- https://sre.google/sre-book/service-level-objectives/ (Google SRE — Service Level Objectives)
- https://sre.google/workbook/implementing-slos/ (Google SRE Workbook — Implementing SLOs)
- https://sre.google/workbook/alerting-on-slos/ (Google SRE Workbook — Alerting on SLOs / burn rate)
- https://sre.google/sre-book/monitoring-distributed-systems/ (Google SRE — Four Golden Signals)
- https://sre.google/sre-book/addressing-cascading-failures/ (Google SRE — Addressing Cascading Failures)
- https://sre.google/sre-book/handling-overload/ (Google SRE — Handling Overload / load shedding)
- https://cloud.google.com/blog/products/devops-sre/sre-fundamentals-slis-slas-and-slos (Google Cloud — SLIs, SLAs e SLOs)
- https://docs.aws.amazon.com/wellarchitected/latest/reliability-pillar/disaster-recovery-dr-objectives.html (AWS Well-Architected — DR: RTO e RPO)
- https://docs.aws.amazon.com/wellarchitected/latest/reliability-pillar/plan-for-disaster-recovery-dr.html (AWS Well-Architected — planejar DR)
- https://aws.amazon.com/blogs/architecture/disaster-recovery-dr-architecture-on-aws-part-i-strategies-for-recovery-in-the-cloud/ (AWS — estratégias de DR)
- https://docs.aws.amazon.com/wellarchitected/latest/serverless-applications-lens/aws-lambda.html (AWS — Serverless Applications Lens / Lambda)
- https://aws.amazon.com/blogs/compute/understanding-and-remediating-cold-starts-an-aws-lambda-perspective/ (AWS — cold starts no Lambda)
- https://www.datadoghq.com/blog/well-architected-serverless-applications-best-practices/ (Datadog — boas práticas serverless / idempotência)
- https://cloud.google.com/learn/paas-vs-iaas-vs-saas (Google Cloud — IaaS, PaaS, SaaS e CaaS)
- https://www.ibm.com/think/topics/iaas-paas-saas (IBM — modelos de serviço de nuvem)
- https://www.ibm.com/think/insights/observability-pillars (IBM — três pilares da observabilidade)
- https://cribl.io/blog/the-3-pillars-of-observability/ (Cribl — pilares e MELT)
- https://www.jrebel.com/blog/microservices-resilience-patterns (JRebel — padrões de resiliência)
- https://www.codecentric.de/en/knowledge-hub/blog/resilience-design-patterns-retry-fallback-timeout-circuit-breaker (codecentric — retry, fallback, timeout, circuit breaker)
- https://java-design-patterns.com/patterns/fallback/ (Fallback Pattern — degradação graciosa)
- https://www.brendangregg.com/usemethod.html (Brendan Gregg — USE Method)
- https://en.wikipedia.org/wiki/High_availability (High availability — tabela dos "nines")
- https://uptime.is/ (calculadora de disponibilidade / nines)
- https://grcopilot.app/blog/iso-22301-business-continuity (ISO 22301 — BIA, RTO/RPO, continuidade)
- https://en.wikipedia.org/wiki/IT_disaster_recovery (IT disaster recovery — visão geral)
- https://arxiv.org/html/2609.16148v1 (Containers vs. Virtual Machines — estudo comparativo)
- https://northflank.com/blog/containers-vs-virtual-machines (Containers vs VMs — isolamento e trade-offs)
- https://www.explainthis.io/en/swe/chaos-engineering-why-industry-uses-it (Chaos engineering — princípios, Netflix)
