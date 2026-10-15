---
tipo: flashcard
disciplina: "Arquitetura e Integração de Sistemas"
tema: "Confiabilidade das aplicações"
data: "2026-10-14"
tags:
  - flashcard/confiabilidade-das-aplicacoes
---

# Flashcards: Confiabilidade das aplicações

> Deck baseado no resumo [[Confiabilidade das aplicações - Arquitetura e Integração de Sistemas]].
> Formato: cards de linha única do plugin Spaced Repetition (pergunta e resposta no mesmo parágrafo).

## Contêineres

O que é um contêiner? :: Isolamento em nível de sistema operacional: processos empacotados com suas dependências, compartilhando o kernel do host.

Namespaces × cgroups? :: Namespaces isolam a visão do processo (PID, rede, sistema de arquivos, hostname, IPC, usuário); cgroups limitam e contabilizam recursos (CPU, memória, I/O).

Qual é a cadeia de artefatos do Docker? :: Dockerfile (receita), imagem (artefato imutável), contêiner (instância em execução) e registry (repositório de imagens).

## Contêiner × Máquina virtual

Contêiner × máquina virtual quanto a isolamento e kernel? :: Contêiner isola em nível de SO (namespaces/cgroups) e compartilha o kernel do host; VM isola em nível de hardware (hypervisor) e tem kernel próprio.

Contêiner × máquina virtual quanto a tamanho e segurança? :: Contêiner é leve e sobe em segundos/ms, porém menos isolado; VM é pesada (GB), sobe em minutos e é mais segura por isolamento de hardware.

## Kubernetes

O que um orquestrador de contêineres faz? :: Agendamento, replicação, auto-recuperação, balanceamento, service discovery e rolling updates (ex.: Kubernetes, Docker Swarm, Nomad).

O que é um Pod? :: A menor unidade implantável, com um ou mais contêineres que compartilham rede/armazenamento.

O que Deployment/ReplicaSet e Service fazem? :: Deployment/ReplicaSet mantêm o número desejado de réplicas (auto-recuperação); Service fornece IP/DNS estável e balanceamento.

## Probes e ciclo de vida de pods

O que faz a liveness probe? :: Verifica se o contêiner está vivo; se falhar, o contêiner é reiniciado (detecta deadlock/hang).

O que faz a readiness probe? :: Verifica se o pod pode receber tráfego; se falhar, o pod é removido do balanceamento, sem reiniciar.

O que faz a startup probe? :: Protege aplicações lentas para iniciar; enquanto não passa, liveness e readiness ficam suspensas.

PodDisruptionBudget e graceful shutdown? :: O PDB limita pods indisponíveis em manutenções voluntárias; terminationGracePeriodSeconds + SIGTERM fazem o graceful shutdown (parar novas requisições, terminar as em curso, fechar conexões).

Requests × limits no Kubernetes? :: Requests são a garantia mínima e limits o teto de recursos; limit de CPU apertado + liveness agressiva pode causar CrashLoopBackOff.

## Twelve-Factor App

Quais fatores do 12-factor importam à implantação? :: III Config no ambiente, VI processos stateless, IX disposability (startup rápido + shutdown gracioso) e XI logs como stream em stdout/stderr.

## Modelos de serviço em nuvem

Como variam os modelos de serviço em nuvem? :: Quanto mais alto no modelo (IaaS, CaaS, PaaS, FaaS, SaaS), mais o provedor gerencia e menos controle o cliente tem.

O que diz o modelo de responsabilidade compartilhada? :: O provedor garante a confiabilidade "da" nuvem; o cliente, a "na" nuvem (configuração, app, dados, IAM, escalonamento).

## Serverless (FaaS)

O que é serverless / FaaS? :: O provedor abstrai servidores e cobra por uso; funções acionadas por eventos escalam automaticamente por invocação, inclusive a zero.

O que é cold start e como mitigá-lo? :: Latência extra ao inicializar o runtime na primeira invocação (ou após ociosidade); mitiga-se com provisioned concurrency e imagens menores.

Quais limites o provedor impõe ao serverless? :: Tempo máximo de execução (timeout), memória, tamanho do pacote, concorrência e throttling.

Por que a idempotência é obrigatória em FaaS? :: Porque retries e entrega at-least-once são comuns, e a função deve poder rodar de novo sem efeitos duplicados.

## Boas práticas de implantação

Blue/green × canary × rolling update? :: Blue/green troca o tráfego entre dois ambientes (rollback instantâneo); canary libera para pequena porcentagem e observa; rolling update substitui instâncias gradualmente.

## Observabilidade × monitoramento

Monitoramento × observabilidade? :: Monitoramento vigia métricas conhecidas e alerta sobre o pré-definido; observabilidade permite fazer perguntas arbitrárias a partir das saídas e entender por que falhou.

Quais são os três pilares da observabilidade? :: Logs, métricas e traces (alguns autores estendem para MELT: Metrics, Events, Logs, Traces).

## Logs e métricas

O que logs, métricas e traces respondem? :: Logs respondem "o que aconteceu?" (eventos); métricas, "algo está errado?" (tendência/limites); traces, "onde/por que travou?".

O que é log estruturado e quais os níveis? :: JSON com campos nomeados (level, service, trace_id); níveis DEBUG, INFO, WARN, ERROR e FATAL. Não logar segredos nem PII.

Como funciona a centralização de logs? :: A aplicação escreve em stdout/stderr e um agente (Fluentd, Fluent Bit, Vector, Filebeat) envia a um backend (Elasticsearch/Kibana, Loki, Splunk, Datadog).

Quais são os tipos de métrica do Prometheus? :: Counter (só cresce), gauge (sobe/desce), histogram (distribuição, permite percentis) e summary (quantis pré-calculados).

Por que medir latência por percentis? :: A média esconde a cauda; poucas requisições lentas arruínam a experiência, então se monitora p95/p99. Cuidado com a armadilha da cardinalidade.

## 4 Sinais Dourados, RED e USE

Quais são os 4 Sinais Dourados? :: Latência, tráfego, erros e saturação.

Como se classificam os erros nos Sinais Dourados? :: Explícitos (HTTP 500), implícitos (HTTP 200 com conteúdo errado) ou por política (acima do tempo prometido).

O que é a saturação? :: Quão cheio está o sistema; muitos degradam antes de 100%, e o aumento de latência é indicador antecipado de saturação (p99 em janela curta).

RED × USE? :: RED (serviços/microservices) = Rate, Errors e Duration; USE (recursos, de Brendan Gregg) = Utilization, Saturation e Errors.

## Rastreamento e OpenTelemetry

O que é um span e um trace? :: Span é a unidade de trabalho com início/fim e span ID; trace é a árvore de spans ligada por um trace ID comum.

O que é context propagation e o W3C Trace Context? :: Trace ID e parent span ID viajam entre serviços; o padrão de fato é o W3C Trace Context, com os cabeçalhos traceparent e tracestate.

O que é o OpenTelemetry (OTel)? :: Projeto CNCF vendor-neutral que padroniza APIs/SDKs, o protocolo OTLP e o Collector, permitindo correlação entre traces, métricas e logs.

## Alertas

Alertas por sintoma e multi-burn-rate? :: Sintomas (o usuário sofre) geram menos ruído que causas (CPU alta); multi-window multi-burn-rate alerta quando o error budget queima rápido.

## Latência

O que é o penhasco de desempenho (performance cliff)? :: Acima de certo limiar, mais carga gera filas, a latência dispara, ocorrem timeouts e retries, criando uma espiral.

Como reduzir latência? :: Cache, assincronismo, pool de conexões, timeouts adequados, paralelizar chamadas seriais, CDN/edge e compressão.

## Disponibilidade e nines

O que é disponibilidade? :: A fração do tempo em que o serviço está utilizável, ou a proporção de requisições bem-sucedidas (para SLIs por requisição).

Nines: 99,9%, 99,99% e 99,999% por ano? :: Cerca de 8,8 h/ano, 52,6 min/ano e 5,3 min/ano, respectivamente.

Disponibilidade em série × em paralelo? :: Em série as disponibilidades se multiplicam (caem); redundância em paralelo aumenta a disponibilidade (1 − (1−p)^n).

## SLI, SLO, SLA e error budget

SLI, SLO e SLA? :: SLI é a medida; SLO é a meta sobre o SLI; SLA é o contrato com consequência (multa, crédito, ação jurídica).

Como distinguir SLO de SLA na prática? :: Se o objetivo não for atingido e não houver consequência explícita, é SLO, não SLA.

O que é error budget? :: O orçamento de erro, igual a 100% menos o SLO; governa o trade-off confiabilidade × inovação (sobrando, arrisca deploys; esgotado, congela mudanças).

## Capacidade e escalonamento

Escalonamento vertical × horizontal? :: Vertical aumenta CPU/memória da instância; horizontal adiciona/remove instâncias, preferível para resiliência e elasticidade.

HPA, VPA, KEDA e Cluster Autoscaler? :: HPA ajusta réplicas; VPA ajusta recursos dos pods; KEDA escala por eventos; Cluster Autoscaler ajusta os nós.

Qual o problema do autoscaling? :: É reativo, com atraso entre o pico e a nova capacidade; mitiga-se com métricas de antecipação, escalonamento agendado e provisioned capacity.

## Tolerância a falhas e padrões de resiliência

Timeout e retry? :: Timeout limita o tempo de espera por uma resposta; retry repete falhas transitórias com backoff exponencial + jitter.

O que é circuit breaker e quais seus estados? :: Interrompe chamadas a um serviço que está falhando; estados closed (passa), open (bloqueia, falha rápido) e half-open (testa algumas tentativas).

Bulkhead × fallback × load shedding? :: Bulkhead isola recursos por dependência; fallback dá resposta alternativa/cache; load shedding recusa ou reduz trabalho sob sobrecarga.

Qual o perigo do retry? :: Repetir operações não idempotentes causa duplicidade; retry sem limite + timeout longo amplifica carga e gera falha em cascata (retry storm).

Degradação graciosa × tolerância a falhas × load shedding? :: Degradação reduz funcionalidade para manter o núcleo; tolerância mascara a falha com redundância; load shedding recusa/reduz trabalho.

O que é falha em cascata e como prevenir? :: A falha de um componente sobrecarrega os demais (feedback positivo); previne-se com timeouts/retries limitados, circuit breakers, load shedding e isolamento.

## Testes de confiabilidade

O que é Chaos Engineering e seus princípios? :: Injetar falhas controladas; define estado estacionário, hipótese, eventos do mundo real, raio de explosão mínimo e critérios de abortar.

Qual a origem do Chaos Engineering? :: Netflix (Chaos Monkey e Chaos Kong); a métrica de steady state era Streams Per Second.

## Diagnóstico de integrações e dependências

O que a correlação de sinais permite no diagnóstico? :: Amarrar trace, log e métrica por trace_id: a métrica diz que há erro, o trace diz onde e o log diz o motivo.

Como diagnosticar dependências lentas e gray failures? :: Com tracing ponta a ponta e timeouts de chamada menores que o do cliente; gray failures são falhas intermitentes difíceis de reproduzir (rede/DNS).

Métricas de resposta a incidente? :: MTTD (detecção), MTTA (reconhecimento), MTTR (resolução) e MTBF (tempo médio entre falhas).

O que é a cultura blameless no postmortem? :: Buscar causa-raiz sistêmica e ações de melhoria sem punir pessoas, com timeline, impacto, causa e itens de ação.

## Continuidade e recuperação

Continuidade × DR × BIA? :: BC mantém a organização operando (amplo); DR restaura sistemas/dados (técnico, contido em BC); BIA fundamenta o RTO/RPO. Norma de referência: ISO 22301.

RTO, RPO e MTPD? :: RTO é o tempo máximo de parada; RPO é a perda máxima de dados (em tempo); MTPD é a disrupção máxima tolerável, e o RTO deve caber dentro dele.

Quais são as estratégias de DR por custo crescente? :: Backup & Restore, Pilot Light, Warm Standby e Multi-Site Active/Active (RTO/RPO decrescentes, custo crescente).

Multi-AZ × multi-região? :: Multi-AZ provê alta disponibilidade contra falha local de zona; multi-região provê DR contra desastres regionais.

## Degradação de serviços e backup

O que é degradação graciosa? :: Reduzir funcionalidades não essenciais para manter o núcleo; o espectro vai da perda total ao núcleo mínimo, cortando primeiro o menos crítico.

O que é a regra 3-2-1 de backup? :: 3 cópias, em 2 mídias diferentes, com 1 fora do site.

Um backup nunca testado é confiável? :: Não; o teste de restauração é a evidência que auditores querem. Backups devem ser imutáveis (contra ransomware) e criptografados.
