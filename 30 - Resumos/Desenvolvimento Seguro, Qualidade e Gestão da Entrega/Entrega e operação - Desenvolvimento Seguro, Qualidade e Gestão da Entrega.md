---
tipo: resumo
disciplina: "Desenvolvimento Seguro, Qualidade e Gestão da Entrega"
tema: "Entrega e operação"
status: novo
data: "2026-10-16"
tags: [resumo, desenvolvimento-seguro, cgu-2026]
---

# Resumo: Entrega e operação

> [!info] MOC: [[Desenvolvimento Seguro, Qualidade e Gestão da Entrega]]
> Edital nº 1/2026 – CGU – AFFC · **Conhecimentos específicos** · Cargo 4 (TI / Desenvolvimento de Sistemas) · Item 3 — *Entrega e operação*.

## Escopo no edital (checklist)

- [x] 3.1 Versionamento, integração e entrega contínuas.
- [x] 3.2 DevSecOps e segurança da cadeia de dependências.
- [x] 3.3 Automação de build, teste e implantação.
- [x] 3.4 Configuração e segregação de ambientes.
- [x] 3.5 Mudanças, reversão e observabilidade.
- [x] 3.6 Manutenção da continuidade durante entregas e incidentes.

## Resumo

O item trata da **entrega contínua de software** e da **operação** dos sistemas em produção: **versionamento** (Git), **integração/entrega contínuas** (CI/CD), **DevSecOps** e **segurança da cadeia de dependências**, **automação de build/teste/implantação**, **configuração e segregação de ambientes**, **estratégias de mudança e reversão** (blue-green, canary, rollback), **observabilidade** (logs, métricas, tracing) e **continuidade** (SRE, RTO/RPO) durante entregas e incidentes.

Três ideias-força:

1. **CI/CD é o coração:** *integração contínua* (CI) = integrar mudanças pequenas e frequentes com build/teste automático; *entrega contínua* (CD/delivery) = sempre pronto para liberar com botão; *implantação contínua* (deployment) = liberação automática em produção. A banca cobra a **diferença** entre delivery e deployment.
2. **DevSecOps = shift-left de segurança:** segurança embutida em todas as etapas (código, dependências, build, deploy, runtime), não como barreira final. SBOM, assinatura de artefatos e SCA protegem a **cadeia de fornecimento**.
3. **Operar é medir e continuar:** **observabilidade** (logs + métricas + tracing), **estratégias de liberação** com reversão segura e **gestão de continuidade** (RTO/RPO, *error budget* do SRE) mantêm o serviço de pé durante mudanças e incidentes.

## 1. Versionamento, integração e entrega contínuas (3.1)

### 1.1 Versionamento com Git

- **Git** é o VCS distribuído dominante; cada clone tem o repositório completo. Conceitos: *commit*, *branch*, *merge*, *rebase*, *tag*, *remote*, *staging area* (index).
- **Branching models:**
  - **Trunk-Based Development (TBD):** todos integram na `main`/trunk com **branches curtas** e commits pequenos; `main` está sempre implantável. Favorece CI/CD; exige forte automação de testes.
  - **Git Flow:** branches de longa duração (`develop`, `feature/*`, `release/*`, `hotfix/*`, `main`). Mais controle para releases versionadas, mas **integração tardia** e merge conflituoso.
  - **GitHub Flow / GitLab Flow:** baseada em PR/MR + `main` + branches curtas (variações do TBD com releases por ambiente).
- **Padrões de commit:** Conventional Commits (`feat:`, `fix:`, `chore:`), versionamento **SemVer** (MAJOR.MINOR.PATCH).

### 1.2 Integração contínua (CI)

- **CI:** prática de **integrar mudanças com frequência**, disparando **build e teste automáticos** a cada commit/PR. Objetivo: detectar conflitos/regressões **cedo**.
- Pipeline típico: *checkout* → *build* → *testes unitários/integração* → *análise estática/SAST/SCA* → *empacotamento* → *artefato*.
- **Fail fast:** build quebrado é prioridade máxima; ninguém integra sobre base quebrada.

### 1.3 Entrega e implantação contínuas (CD)

- **Continuous Delivery:** o artefato está **sempre pronto** para ir a produção; a liberação exige **aprovação humana** (botão).
- **Continuous Deployment:** a liberação em produção é **automática** após passar no pipeline (sem aprovação manual).
- **Pipeline (CI/CD):** automação em **estágios** que movem o artefato de build → teste → homologação → produção, com *gates* de qualidade/segurança.

## 2. DevSecOps e segurança da cadeia de dependências (3.2)

### 2.1 DevSecOps e shift-left

- **DevSecOps** integra **segurança** ao ciclo DevOps, como responsabilidade de todos e de cada etapa — **shift-left** (antecipar segurança para o início do ciclo).
- Práticas: **SAST** no commit, **SCA/SBOM** nas dependências, **segredos em cofre**, **assinatura de artefatos**, **DAST/IAST** no staging, **RASP** em produção, **IaC segura** (Terraform/Ansible com verificação).
- **Pipeline segura:** cada estágio tem *gates* que **bloqueiam** o avanço se houver falha crítica (vulnerabilidade, segredo exposto, teste quebrado).

### 2.2 Segurança da cadeia de dependências

- **SBOM (CycloneDX/SPDX)** documenta componentes; **SCA** cruza com CVEs; **SLSA** garante níveis de integridade da cadeia de build.
- **Assinatura de artefatos:** *sigstore/cosign* (assinatura de imagens), *in-toto* (proveniência). Verificar integridade antes de implantar.
- **Registro interno de artefatos** (Nexus/Artifactory, registry privado) e **pinning de versão + lockfile** reduzem typosquatting e *dependency confusion*.
- **Renovação automatizada de dependências** (Dependabot/Renovate) com testes de regressão antes do merge.

## 3. Automação de build, teste e implantação (3.3)

- **Build automatizado:** empacotar o artefato de forma **reproduzível** (mesmo código → mesmo artefato). Ferramentas: Maven/Gradle (Java), npm/pnpm (JS), Docker (imagens).
- **Teste automatizado no pipeline:** unitário → integração → contrato → e2e, em **estágios** (rápidos primeiro).
- **Implantação automatizada (deploy):** IaC + *declarativo* (Kubernetes manifests, Helm, Terraform, Ansible) e **GitOps** (Argo CD/Flux — o estado desejado fica no Git e um agente reconcilia).
- **Imutabilidade:** artefato **imutável** (imagem de contêiner) promovido pelos ambientes — nunca "patchar em produção".
- **Pipeline as Code:** pipeline versionada no repositório (GitHub Actions, GitLab CI, Jenkinsfile).

## 4. Configuração e segregação de ambientes (3.4)

- **Ambientes:** desenvolvimento → teste/homologação (staging) → produção. Cada um com **configuração, dados e acesso** próprios.
- **Segregação:** produção **isolada** de homologação (redes, credenciais, bancos); dados de produção **não** usados em teste sem anonimização.
- **Configuração como código (Config as Code):** config **versionada** e **imutável**; **12-Factor App** recomenda config em **variáveis de ambiente** (não no código).
- **Paridade dev/prod:** ambientes o mais **semelhantes** possível (mesma infra, mesmas dependências) para reduzir o "funciona na minha máquina".
- **Ambientes efêmeros (preview):** criados por PR para testar mudanças e destruídos depois.

## 5. Mudanças, reversão e observabilidade (3.5)

### 5.1 Estratégias de liberação (deployment)

| Estratégia | Como funciona | Rollback | Custo |
| --- | --- | --- | --- |
| **Recreate** | Para tudo, troca, sobe | Simples, mas com downtime | Baixo custo, alto downtime |
| **Rolling** | Substitui instâncias em lotes | Retornar versão gradualmente | Médio; sem duplicar infra |
| **Blue-Green** | Dois ambientes; troca o roteador (blue↔green) | Instantâneo (volta o roteador) | Dobra a infraestrutura |
| **Canary** | Libera para % pequena de usuários e expande | Rápido, impacto mínimo | Precisa roteamento + métricas |

- **Blue-Green:** mantém **duas versões completas**; o *switch* de tráfego é instantâneo e a **reversão é trivial** (mudar o roteador de volta). **Custo:** infraestrutura em dobro.
- **Canary:** libera a nova versão para um **subconjunto** (ex.: 5%) e observa métricas; se ruim, **corta e reverte**. Necessita **análise comparativa** (canário × controle).
- **Feature flags (feature toggles):** separam **liberação (deploy)** de **ativação (release)** — permite ativar/desativar funcionalidade sem novo deploy; reversão = desligar a flag.
- **Rollback vs. roll forward:** reverter para versão anterior (rollback) × lançar correção adiante (roll forward). A escolha depende de compatibilidade de dados/schema.

### 5.2 Observabilidade

- **Observabilidade** = capacidade de inferir o estado interno a partir das saídas externas. Três pilares (três pilares + correlação):
  - **Logs:** eventos textuais estruturados (o que aconteceu).
  - **Métricas:** séries numéricas agregadas (latência, throughput, erros, saturação — "four golden signals": **latência, tráfego, erros, saturação**).
  - **Tracing (rastreamento distribuído):** percorre uma requisição entre serviços (trace → spans); ferramentas **OpenTelemetry**, Jaeger, Zipkin.
- **Monitoramento ≠ observabilidade:** monitorar é alertar sobre métricas **conhecidas**; observabilidade explora o **desconhecido** (perguntas novas sobre o sistema).
- **Alerting:** evitar fadiga de alerta; alertar sobre sintomas (impacto ao usuário), não causas; **on-call** e resposta.

## 6. Continuidade durante entregas e incidentes (3.6)

### 6.1 SRE e error budget

- **SRE (Site Reliability Engineering — Google):** aplica **engenharia de software** à operação. Práticas: **SLO/SLI**, **error budget**, automação de toil, blameless postmortem.
- **SLI** (indicador: latência, disponibilidade) → **SLO** (objetivo interno, ex.: 99,9% disponível) → **SLA** (acordo externo/contratual com o cliente).
- **Error budget:** o "orçamento de erro" = 1 − SLO. Se estourou, **congelar mudanças** e priorizar confiabilidade; se sobrou, pode arriscar mais features.

### 6.2 Continuidade de negócios e recuperação de desastres

- **RTO (Recovery Time Objective):** tempo máximo aceitável para **recuperar** o serviço.
- **RPO (Recovery Point Objective):** quantidade máxima de **dados** que se aceita **perder** (definida pela janela de backup/replicação).
- **BIA (Business Impact Analysis)** identifica processos críticos e define RTO/RPO; **DRP (Disaster Recovery Plan)** descreve a recuperação.
- **Backup** (3-2-1: 3 cópias, 2 mídias, 1 fora), **replicação** (síncrona/assíncrona), **failover** (ativo-ativo/ativo-passivo), **restauração testada** periodicamente.

### 6.3 Continuidade durante entregas e incidentes

- **Entregas sem interrupção:** blue-green/canary, **migrações compatíveis** (expand-contract), **deploys reversíveis**.
- **Gestão de incidentes:** detecção → contenção → mitigação → comunicação → **postmortem blameless** → ação corretiva. Papéis de **comando de incidente** (ICS).
- **Comunicação de status:** página de status, atualizações a stakeholders.
- **Confiabilidade durante incidente:** degradação graciosa, *circuit breaker*, *rate limiting*, *bulkhead*, *timeouts* e *retries*.

## Detalhes que merecem destaque

- **Continuous Delivery ≠ Continuous Deployment:** na delivery a liberação é **manual/aprovada**; na deployment é **automática**.
- **Trunk-Based Development** é a prática de versionamento que **habilita** CI/CD (integração pequena e frequente); **Git Flow** favorece releases versionadas, mas com integração tardia.
- **Blue-Green** = dois ambientes + troca de roteador (rollback trivial, custo dobrado); **Canary** = liberação gradual para % de usuários com análise de métricas.
- **Feature flag** separa **deploy** de **release** — permite reverter **sem novo deploy**.
- **Observabilidade = logs + métricas + tracing**; os **four golden signals** (latência, tráfego, erros, saturação) vêm do Google SRE.
- **SLI → SLO → SLA** (indicador → objetivo interno → acordo externo); **error budget = 1 − SLO**.
- **RTO** é **tempo** até recuperar; **RPO** é **dados** que se aceita perder — não confundir.
- **12-Factor App** e **config as code** colocam configuração fora do código (variáveis de ambiente), essencial para **segregação de ambientes**.

## Comparações que a banca costuma cobrar (certo/errado)

| Conceito A | Conceito B | Diferença-chave |
| --- | --- | --- |
| Integração contínua (CI) | Entrega contínua (Delivery) | Build/teste automático a cada commit × sempre pronto (botão) |
| Entrega contínua (Delivery) | Implantação contínua (Deployment) | Liberação manual/aprovada × automática |
| Trunk-Based | Git Flow | Integração frequente na main × branches longas (develop/release) |
| Blue-Green | Canary | Troca total via roteador × liberação gradual por % |
| Rollback | Roll forward | Voltar à versão anterior × lançar correção adiante |
| Monitoramento | Observabilidade | Alertas sobre o conhecido × explorar o desconhecido |
| Métrica | Trace | Número agregado × percurso de uma requisição |
| SLI | SLO | Indicador medido × objetivo interno |
| SLO | SLA | Objetivo interno × acordo externo/contratual |
| RTO | RPO | Tempo para recuperar × dados que se perde |
| Backup | Replicação | Cópia restauradora × cópia contínua p/ failover |

## Pegadinhas e erros comuns

> Cuidado com termos absolutos ("sempre", "nunca", "exclusivamente") e com a troca de requisitos.

- Confundir **continuous delivery com continuous deployment** — a diferença é a **automação da liberação**.
- Achar que **Git Flow é o único modelo** ou que **trunk-based dispensa testes** — TBD **exige** forte automação.
- Achar que **blue-green e canary são a mesma coisa** — blue-green troca **todo** o tráfego; canary é **gradual**.
- Confundir **rollback** (voltar) com **roll forward** (seguir adiante).
- Achar que **monitoramento = observabilidade** — observabilidade permite investigar o **desconhecido**.
- Trocar **RTO por RPO** — um é **tempo**, outro é **volume de dados perdidos**.
- Achar que **SBOM corrige vulnerabilidade** — SBOM **inventaria**; SCA detecta; o *patch* corrige.
- Achar que **feature flag substitui teste** — flag controla **liberação**, não garante qualidade.
- Achar que **deploy imutável** permite "patchar em produção" — a imutabilidade **proíbe** alteração do artefato em produção.
- Achar que **SLA é meta interna** — SLA é **contratual/externo**; meta interna é **SLO**.
- Achar que **observabilidade dispensa logs** — os três pilares (logs, métricas, tracing) são **complementares**.

## Notas atômicas relacionadas

```dataview
LIST FROM "20 - Notas"
WHERE disciplina = this.disciplina
  AND contains(tema, this.tema)
SORT file.name ASC
```

## Fontes

- https://www.atlassian.com/continuous-delivery/continuous-integration/trunk-based-development (Atlassian — Trunk-Based Development)
- https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow (Atlassian — Git Flow workflow)
- https://www.atlassian.com/continuous-delivery/continuous-integration (Atlassian — Continuous Integration)
- https://www.atlassian.com/continuous-delivery/principles/continuous-integration-vs-delivery-vs-deployment (Atlassian — CI vs Delivery vs Deployment)
- https://martinfowler.com/bliki/ContinuousDelivery.html (Martin Fowler — Continuous Delivery)
- https://martinfowler.com/bliki/BlueGreenDeployment.html (Martin Fowler — Blue-Green Deployment)
- https://martinfowler.com/bliki/CanaryRelease.html (Martin Fowler — Canary Release)
- https://sre.google/workbook/canarying-releases/ (Google SRE — Canary Releases)
- https://sre.google/sre-book/monitoring-distributed-systems/ (Google SRE — Monitoring Distributed Systems; four golden signals)
- https://sre.google/sre-book/service-level-objectives/ (Google SRE — SLI/SLO/SLA e error budget)
- https://slsa.dev/ (SLSA — Supply-chain Levels for Software Artifacts)
- https://www.nist.gov/itl/executive-order-14028-improving-nations-cybersecurity/software-supply-chain-security-guidance-20 (NIST — SBOM)
- https://opentelemetry.io/ (OpenTelemetry — padrão de observabilidade)
- https://12factor.net/config (The Twelve-Factor App — configuração)
- https://github.com/sigstore/cosign (sigstore/cosign — assinatura de artefatos)
