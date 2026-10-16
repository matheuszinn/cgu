---
tipo: análise
bloco: "Conhecimentos Específicos (Cargo 4 – TI)"
banca: Cebraspe
data: "2026-10-14"
tags: [analise, cebraspe, cgu-2026]
---

# Incidência CEBRASPE — Conhecimentos Específicos (Cargo 4 – TI)

> **Escopo:** Edital nº 1/2026 – CGU – AFFC, **Cargo 4 – Auditor Federal de Finanças e Controle – Especialidade: Tecnologia da Informação – Desenvolvimento de Sistemas**.
> Bloco analisado: **Conhecimentos Específicos (P3 – 90 itens, 180 pontos)** — Engenharia de Software e Programação; Arquitetura e Integração de Sistemas; Persistência, Integração e Proteção de Dados; Desenvolvimento Seguro, Qualidade e Gestão da Entrega.
> **Nota de método:** o concurso da CGU de **2021 foi da FGV**; o de **2026 é o primeiro da Cebraspe** para o AFFC. Por isso, esta análise usa a incidência histórica da **Cebraspe em provas de TI** (foco em controle/auditoria de TI: **TCU 2015/2025/2026**, TCEs, CGDF, Bacen, FUNPRESP-JUD, BANRISUL, STM, INPI, VALEC etc.), que é o melhor preditor disponível para a banca.
> Relacionado: [[Engenharia de Software e Programação]] · [[Arquitetura e Integração de Sistemas]] · [[Persistência, Integração e Proteção de Dados]] · [[Desenvolvimento Seguro, Qualidade e Gestão da Entrega]] · [[Edital CGU 2026 (texto integral)]]

---

## Metodologia

1. **Fontes quantitativas de incidência (Cebraspe):**
   - **Estratégia – Raio-X Estratégico "TCU – Auditor de TI"** (pós-edital 2025/2026): análise de milhares de questões da Cebraspe, 2021–2025 (Banco de Dados = 1.065 questões; Redes e Segurança = 1.547; Desenvolvimento de Software = 689; Engenharia de Software = 582; Sistemas Operacionais/Infra = 488; Gestão de TI = 367; IA = 272).
   - **QConcursos** — distribuição por disciplina das provas TCU 2026 (AUFC/Auditoria de TI, 200 itens), FUNPRESP-JUD 2026 (Analista TI – Desenvolvimento de Sistemas), BANRISUL 2022 (Analista – Desenvolvimento de Sistemas), BDMG 2025, Bacen 2024 (Analista TI).
   - **Estratégia (área Controle)** — cruzamento TCE-RJ, TCE-RO e TCM-BA (disciplina de TI/Análise de Dados).
   - **TecConcursos** — volume de questões por assunto de Engenharia de Software.
2. **Provas e cadernos oficiais da Cebraspe** (TCU 2026 TI, TCU 2015 TI, TCE/SC, CAU/BR, FUB, FUNPRESP-JUD, SEFAZ/SE 2025, INFRA S.A. 2026, CAGEPA 2024) para identificar **como** cada tema é cobrado.
3. **Prova CGU 2021 (FGV)** e a análise interna do vault ([[Analise Conteudo x Prova 2021]]) para calibrar o que a CGU valoriza em TI.
4. **Caveat de comparabilidade:** o cargo mais próximo da Cebraspe é o **TCU AUFC – Auditoria de TI**, mas ele é mais "auditoria/governança" que o **Cargo 4 da CGU**, que é explicitamente **desenvolvimento**. Por isso, na ponderação final, os temas de **software, banco de dados, arquitetura, segurança de aplicações, testes e DevOps** recebem peso maior do que governança pura.

> **Formato da P3 (Cargo 4):** 90 itens **Certo/Errado**, **+2 por acerto / −2 por erro**, mínimo de **54 pontos** em P3. Cada erro anula um acerto → a decisão de marcar é tão importante quanto o conteúdo.

---

## Ranking de incidência

> Ranking do **mais cobrado ao menos cobrado** para o perfil "Desenvolvimento de Sistemas" da Cebraspe, já mapeado para os itens do edital da CGU 2026. "Incidência" combina a frequência histórica da banca com o peso do item no edital.

| Prioridade | Assunto / Item do edital | Incidência | Evidências |
|---|---|---|---|
| **1** | **Engenharia de Software: metodologias ágeis (Scrum/Kanban), requisitos, ciclo de vida e arquitetura de software** — bloco 1 (itens 1 e 2.8) e bloco 4 (item 4.2) | **Muito alta** | Disciplina **mais cobrada** no TCU 2026 TI: **25/200 itens**. BANRISUL 2022: **27/120**; Bacen 2024: **24/120**. Raio-X Cebraspe: **Scrum 26,46%**, **Arquitetura de Software 20,62%**, **Metodologias ágeis 17,87%**, **Kanban/TDD/BDD/DDD 12,54%**, **SOA 9,11%**. |
| **2** | **Banco de Dados / SQL / persistência (modelagem relacional, normalização, JPA)** — bloco 3 (itens 1 e 2) | **Muito alta** | FUNPRESP-JUD 2026 (Dev. de Sistemas): **BD 21/120**; BDMG 2025: **12/120**. Raio-X BD (1.065 questões): **modelagem multidimensional 23,94%**, **DW/DataMart/DataLake/ETL 22,54%**, **SQL 19,15%**, **modelagem relacional e normalização 14,93%**, NoSQL 6,76%. |
| **3** | **Segurança de aplicações / Segurança da Informação (OWASP, SQLi, XSS, criptografia, LGPD)** — bloco 4 (item 1) e bloco 3 (item 4) | **Muito alta** | TCU 2026 TI: **Segurança 17/200**; BANRISUL 2022: **16/120**; FUNPRESP 2026: **14/120**; Bacen 2024: **7/120**. Raio-X Redes/Segurança: **malware/ataques (SQLi, XSS, DDoS) 9,50%**, **criptografia em trânsito/repouso 9,37%**, **ISO/IEC 27001 12,61%**, frameworks (MITRE/CIS/NIST) 5,43%. |
| **4** | **Arquitetura de aplicações: microsserviços, eventos, padrões (API Gateway, Service Mesh, CQRS, Saga)** — bloco 2 (itens 1 e 3) | **Alta** | Raio-X Eng. Software: **Arquitetura 20,62%**, **SOA 9,11%**, **padrões/monolito/micro/serverless/eventos 8,08%**. Cobrado em 2026: TCE-MG, TCE-RN, TELEBRAS, FUNPRESP, BANRISUL, CAU/BR (API Gateway, ESB). |
| **5** | **DevOps, CI/CD, DevSecOps, containers (Docker/Kubernetes)** — bloco 4 (item 3) | **Alta** | Raio-X Desenvolvimento: **DevOps/CI-CD/DevSecOps 18,58%**, **Docker e orquestração com Kubernetes 18,43%**, **pipelines Jenkins/GitHub Actions 4,64%**, **IaC/Terraform 3,63%**. |
| **6** | **Programação Java / POO / estruturas de dados / complexidade** — bloco 1 (item 2) | **Alta** | Raio-X: **Lógica de Programação 16,55%**, **linguagem Java 7,11%**. BANRISUL 2022: **Programação 10/120**; FUNPRESP 2026: 3; TCU 2026: 3. Questões de leitura de código Java (CAGEPA 2024, INPI 2024, SEFAZ-SE 2025). |
| **7** | **Testes e qualidade (unitário, integração, contrato, TDD/BDD, análise estática, cobertura)** — bloco 4 (item 2) | **Alta** | Raio-X: **testes automatizados 9,14%**, **qualidade de código/análise estática (SonarQube) 1,31%**; Eng. Software: **Kanban/TDD/BDD/DDD 12,54%**. Itens de TDD em FUNPRESP 2026, STJ 2018, VALEC 2026. |
| **8** | **APIs REST, contratos/versionamento, OAuth 2.0 / OpenID Connect / JWT, Spring Security** — bloco 2 (item 2) | **Alta** | Item explícito do edital. TCU 2026: item de **SSO SAML 2.0 × OAuth2**; STM 2025: **Spring service discovery/Eureka**; FUNPRESP 2026: **REST/JSON**; STJ 2018: **REST stateless**; SEFAZ/SE 2025: NoSQL/REST. |
| **9** | **Mensageria, eventos, idempotência e consistência** — bloco 2 (item 3) | **Média-alta** | Raio-X Desenvolvimento: **mensageria/eventos/padrões de integração 4,79%**; CAU/BR 2023: **mensageria síncrona × assíncrona, ESB**; simulados TCU 2026: **Saga, transações distribuídas/2PC**. |
| **10** | **Cloud, serverless e observabilidade (logs, métricas, tracing)** — bloco 2 (item 5) | **Média-alta** | Raio-X Redes/Segurança: **computação em nuvem e segurança em nuvem 15,32%**; Desenvolvimento: **Docker/K8s 18,43%**; monitoramento/observabilidade **1,87%**. TCU 2026: itens de **PaaS/nuvem**. |
| **11** | **Governança e gestão (ITIL/COBIT, PDTIC, indicadores, riscos, evidências)** — bloco 4 (item 4) | **Média** | TCU 2026 TI: **Governança de TI 17/200**. Raio-X Gestão de TI: **ITIL v4 57,77%**, **COBIT 42,23%**. Alta aderência ao perfil CGU (PDTIC, plano de dados abertos, controles). |
| **12** | **Integração com dados e IA (RAG, embeddings/busca vetorial, agentes, LLM, prompt injection)** — bloco 2 (item 4) | **Média (crescente)** | Item **novo** do edital. Raio-X IA (272 questões): **ML 47,43%**, **ética/explicabilidade 22,43%**, **redes neurais/deep learning 19,85%**, **PLN/agentes 6,99%**. TCU 2026 já cobrou IA; tendência de alta. |
| **13** | **Contratação e fiscalização de soluções de TI (ETP, TR, SLA, TCO, plano de saída)** — bloco 4 (item 5) | **Média** | Histórico TCU: **Fiscalização de Contratos de TI 17 questões**, **Contratações de TI 13**. CGU 2021 (FGV): **ETP (IN SGD/ME 1/2019)**. Discursiva do TCU 2026 tratou de **SaaS, SLA, lock-in e fiscalização**. |
| **14** | **Spring Batch / ETL / processamento em lote (jobs, steps, retry, checkpoint)** — bloco 3 (item 3) | **Média-baixa** | Item explícito do edital (Spring Batch). Raio-X BD: **DW/ETL 22,54%**; FUNPRESP 2026 e CAGEPA 2024 com itens de **ETL/ELT**. |

**Leitura do ranking:** os três primeiros lugares (Engenharia de Software, Banco de Dados/SQL e Segurança) concentram, sozinhos, a maior parte das provas de TI da Cebraspe e devem receber ~50% do tempo. Arquitetura, DevOps e Java vêm logo atrás. Os itens de "cauda" (IA, contratações, Spring Batch) são importantes para **cobertura integral do edital** e para a **discursiva**, mas têm menor frequência histórica.

---

## Análise por item do edital

### Engenharia de Software e Programação

**Subtemas do edital → incidência Cebraspe:**

| Subtema do edital | Cobrança | Como a Cebraspe cobra |
|---|---|---|
| 1.1–1.5 Requisitos (funcionais/não funcionais), critérios de aceitação, desenho centrado nas pessoas | Alta | Itens conceituais; distinção requisito funcional × não funcional; TCE/SC cobrou "não funcionais **não** devem abordar restrições…" (item errado). |
| 2.1–2.4 Java (tipos, controle, métodos, classes, encapsulamento, herança, polimorfismo, coleções, genéricos, exceções, arquivos) | Alta | Leitura de código Java (CAGEPA 2024, INPI 2024); herança múltipla de interfaces; Records; `do-while` com `;`. |
| 2.5–2.7 Estruturas de dados, algoritmos, complexidade | Média-alta | Complexidade O(1)/O(n) (INPI 2024: "lista circular ordenada, acesso ao maior elemento O(1)"); estruturas de dados. |
| 2.8 Modularidade e padrões de projeto (GoF/GRASP) | Média | Padrões (Singleton × Prototype em simulados TCU); SOLID; baixo acoplamento/alta coesão. |
| 3 Concorrência, paralelismo, assincronia, condições de corrida, bloqueios | Média | Menor incidência isolada, mas cai em itens de Java/threads e mensageria. |
| 4 Interfaces/UX: usabilidade, acessibilidade, JavaScript e Vue.js | Média | Acessibilidade (FUNPRESP 2026: diretrizes internacionais); Vue.js é item **novo** do edital. |
| 5 Manutenção, débito técnico, legado, interoperabilidade | Média | Refatoração, reengenharia, interoperabilidade (FUNPRESP 2026). |

**Conclusão do item 1:** o núcleo é **Engenharia de Software clássica (requisitos, ciclo de vida, metodologias ágeis) + Java/POO**. As metodologias ágeis (Scrum/Kanban) são o assunto **mais recorrente** de toda a disciplina na Cebraspe — prioridade máxima.

### Arquitetura e Integração de Sistemas

**Subtemas → incidência:**

| Subtema do edital | Cobrança | Evidência / como cai |
|---|---|---|
| 1.1–1.4 Monolitos, microsserviços, eventos, acoplamento, escalabilidade, escolha de arquitetura | Alta | Microsserviços em TCE-MG, TCE-RN, TELEBRAS, BANRISUL, VALEC (2026); "microsserviço pode ter várias linguagens/servidores?" (item errado); orquestração × coreografia. |
| 1.5–1.7 Spring Framework/Boot: IoC, injeção de dependência, autoconfiguração, REST em camadas | Alta | Spring é cobrado como conceito (STM 2025: Eureka/service discovery; FGV 2025: Spring Boot Starter/Redis, servidor embutido). Spring Boot = framework "âncora" do edital. |
| 2.1–2.4 REST (design, contratos, versionamento), autenticação/autorização, OAuth 2.0, OIDC, tokens | Alta | REST stateless (STJ 2018); SSO SAML × OAuth2 (TCU 2026); validação de requisições em RESTful. |
| 2.5–2.8 Spring Security, controle de acesso, segregação de funções, endpoints/métodos, permissões excessivas | Alta | Casamento direto com o perfil de auditoria: **falhas de controle de acesso** e **permissões excessivas** são tema "casa" da CGU. |
| 3.1–3.4 Mensageria, eventos, idempotência, consistência, evolução de contratos | Média-alta | Mensageria síncrona × assíncrona (CAU/BR 2023); Saga/2PC (simulados TCU 2026); idempotência e retries. |
| 4.1–4.5 Integração com dados e IA (LLM, embeddings, RAG, agentes, prompt injection) | Média (crescente) | Item **novo**; tema de fronteira — a Cebraspe vem inserindo IA nas provas de 2026 (TCU, TCE-MG). |
| 5.1–5.5 Contêineres, nuvem, serverless, logs/métricas/tracing, latência, tolerância a falhas | Média-alta | Docker/K8s (18,43%); nuvem (15,32%); PaaS (TCU 2026); observabilidade. |

**Conclusão do item 2:** bloco muito rico em **arquitetura distribuída + APIs/identidade**. É o "coração técnico" do cargo. Priorize **microsserviços + REST + OAuth2/OIDC/JWT + Spring (Boot/Security)** e, em seguida, **mensageria, nuvem/containers e observabilidade**. O item de **IA/RAG** é diferencial de atualidade.

### Persistência, Integração e Proteção de Dados

**Subtemas → incidência:**

| Subtema do edital | Cobrança | Evidência / como cai |
|---|---|---|
| 1.1–1.5 Modelagem relacional, normalização, integridade, NoSQL (documento/chave-valor/vetorial), cache, transações/ACID | Muito alta | BD é uma das disciplinas mais cobradas (21/120 no FUNPRESP 2026). Normalização (3FN), ACID, DER (FUNPRESP: "entidades fortes"; 3FN). |
| 1.6–1.9 Persistência em Java com JPA, ciclo de vida, contexto, consultas/transações, Spring Data JPA, carregamento (lazy/eager) | Alta | JPA/Hibernate é item explícito e recorrente (CGU 2021: `SessionFactory` thread-safety; SEFAZ-SE 2025: .NET/EF Core análogo). |
| 2.1–2.4 SQL (DDL/DML, controle de acesso, transações), joins, agregações, subconsultas, CTEs, índices, planos de execução | Muito alta | SQL = **19,15%** do Raio-X de BD; PostgreSQL/SQL Server; `CREATE SEQUENCE` (CGU 2021); índices secundários (TCE/SC). |
| 3.1–3.5 Ingestão/ETL/ELT, lote × fluxo, formatos (CSV/JSON/XML/Parquet), qualidade/reprocessamento | Alta | DW/DataLake/DataMesh + ETL = **22,54%**; formatos planos (JSON 4,79%, XML 2,61%, CSV/Parquet 1,55%). |
| 3.6–3.9 Spring Batch (jobs/steps, leitura/processamento/escrita, transacional, restart, idempotência) | Média-baixa | Item explícito do edital; baixa frequência histórica, mas cobrável por leitura de código/conceito. |
| 4.1–4.6 Privacidade e segurança de dados: minimização, criptografia, pseudonimização, retenção/descarte, privacy by design | Alta | Criptografia em trânsito/repouso **9,37%**; LGPD é "figurinha carimbada" (Cebraspe e FCC); privacy by design. |

**Conclusão do item 3:** núcleo = **SQL + modelagem/normalização + JPA**. Depois: **ETL/formatos**, **privacidade/criptografia/LGPD** e, por último, **Spring Batch**. O tema "vetorial" (bancos vetoriais) conecta-se ao item de IA.

### Desenvolvimento Seguro, Qualidade e Gestão da Entrega

**Subtemas → incidência:**

| Subtema do edital | Cobrança | Evidência / como cai |
|---|---|---|
| 1.1–1.6 Segurança de aplicações: ameaças/vulnerabilidades, validação de entrada, controle de acesso, segredos, testes de segurança, vazamentos, evidências | Muito alta | SQLi/XSS **9,50%**; OWASP; "prevenção de vazamentos" e "preservação de evidências" = perfil auditoria; DevSecOps (Porto Velho 2026). |
| 2.1–2.5 Testes (unitário/integração/contrato/aceitação), análise estática, cobertura, automação, limites das métricas | Alta | Testes automatizados **9,14%**; TDD; SonarQube; "microsserviços: testes de código e de carga" (VALEC 2026). |
| 3.1–3.6 CI/CD, DevSecOps, cadeia de dependências, build/teste/deploy, ambientes, reversão, observabilidade, continuidade | Alta | DevOps/CI-CD/DevSecOps **18,58%**; Docker/K8s **18,43%**; GitHub Actions; IaC. |
| 4.1–4.5 Gestão de produtos, Scrum/Kanban, priorização, indicadores, PDTIC/plano de transformação digital/dados abertos, riscos e evidências | Média | Scrum **26,46%**; ITIL/COBIT (Governança 17/200 no TCU 2026); PDTIC e plano de dados abertos são "marca" da CGU. |
| 5.1–5.6 Contratação e fiscalização de soluções de TI (ETP, TR, TCO, SLA, pagamento, propriedade intelectual, plano de saída) | Média | TCU: Fiscalização de Contratos de TI 17; CGU 2021: ETP; discursiva TCU 2026: SaaS, SLA, lock-in. |

**Conclusão do item 4:** bloco de **maior aderência ao perfil CGU** (segurança + evidências + governança + contratações). Núcleo = **segurança de aplicações/OWASP + testes + DevOps/CI-CD**; depois **gestão (Scrum/Kanban/PDTIC)** e **contratações/fiscalização**.

---

## Padrões de cobrança da banca

1. **Certo/Errado com pontuação negativa (net scoring).** Na P3, cada erro vale **−2** e anula um acerto. A banca explora a **decisão binária segura**: quem "chuta" perde muito. Regra prática: só marque quando houver convicção; itens com **"sempre", "nunca", "exclusivamente", "apenas", "todos"** são candidatos a **errado**.
2. **Pegadinhas por inversão conceitual e por excesso.** O erro típico não é desconhecimento, é **exagero ou troca de papéis** (ex.: "serviços compartilham o mesmo banco para reduzir acoplamento"; "nó secundário processa as mesmas requisições"; "EF Core elimina a necessidade de mapeamento"). Valide cada afirmação contra o comportamento real da tecnologia.
3. **Cobrança conceitual e "de reconhecimento", com pitadas de código.** Predomina a teoria (definições, arquitetura, frameworks), mas há **leitura de código** (Java, Python, SQL) e itens de "situação hipotética + assertiva".
4. **Nomes de tecnologia como âncoras.** Spring/Spring Boot, Spring Security, JPA/Hibernate, JUnit, Docker, Kubernetes, Jenkins/GitHub Actions, SonarQube, OWASP, OAuth2/OIDC/JWT, MongoDB/Elasticsearch, Parquet, Spring Batch. Saber **o que cada um faz e não faz** rende itens.
5. **Fronteiras borradas entre blocos.** Segurança aparece dentro de arquitetura e de dados; dados aparecem dentro de desenvolvimento. O edital da CGU misturou os temas de propósito — estude de forma **integrada**, não estanque.
6. **Atualidade e IA.** A Cebraspe vem incluindo **DevSecOps, zero trust, IA generativa/LLM, RAG, MLOps** e **computação em nuvem**. O item "Integração com dados e IA" do edital sinaliza cobrança desse tema.
7. **Perfil "auditoria de TI".** Em provas da área de controle, temas como **controle de acesso, permissões excessivas, prevenção de vazamentos, preservação de evidências, SLA, lock-in e plano de saída** aparecem com frequência — e são exatamente o elo entre TI e a atuação da CGU.
8. **Discursiva pesada em específicos.** A P4 tem uma **situação-problema de 70 pontos** sobre conhecimentos específicos do cargo (60 linhas) + 30 pontos de complementares. Historicamente, o TCU cobrou **contratação de SaaS, SLA, fiscalização e segurança** — temas que atravessam o bloco 4.

---

## Recomendações de estudo (prioridades)

**Ordem prática (do maior retorno ao menor):**

1. **Engenharia de Software ágil + requisitos + arquitetura de software** (Scrum, Kanban, ciclo de vida, requisitos funcionais/não funcionais, padrões GoF/GRASP, SOLID). É a disciplina mais cobrada — comece por aqui.
2. **Banco de Dados/SQL + JPA** (modelagem relacional, normalização/3FN, ACID, joins/agregações/CTEs, índices, JPA/Hibernate, Spring Data JPA, lazy/eager).
3. **Segurança de aplicações + Segurança da Informação** (OWASP Top 10, SQLi, XSS, validação de entrada, controle de acesso, criptografia simétrica/assimétrica, PKI, ISO 27001, LGPD, DevSecOps).
4. **Arquitetura distribuída** (monolito × microsserviços, eventos, API Gateway, Service Mesh, CQRS, Saga, idempotência, mensageria).
5. **APIs REST + identidade** (design/versionamento, REST stateless, OAuth 2.0, OIDC, JWT, SAML, Spring Security, RBAC/segregação de funções).
6. **Java/POO + estruturas de dados** (classes, herança, polimorfismo, coleções, genéricos, exceções, concorrência, complexidade, leitura de código).
7. **DevOps/CI-CD/containers** (Docker, Kubernetes, Jenkins/GitHub Actions, IaC/Terraform, build/teste/deploy, DevSecOps e cadeia de dependências).
8. **Testes e qualidade** (unitário, integração, contrato, aceitação, TDD/BDD, análise estática, cobertura, SonarQube, limites das métricas).
9. **Cloud, serverless e observabilidade** (IaaS/PaaS/SaaS, serverless/cold start, logs/métricas/tracing, latência, tolerância a falhas, continuidade).
10. **Governança e gestão da entrega** (ITIL 4, COBIT, PDTIC, plano de transformação digital/dados abertos, indicadores, riscos, evidências).
11. **Integração com dados e IA** (RAG, embeddings/busca semântica, agentes, avaliação de respostas, prompt injection) — diferencial de atualidade.
12. **Contratação/fiscalização de TI e Spring Batch/ETL** — feche as lacunas do edital (menor frequência, mas cobráveis e úteis para a discursiva).

**Estratégia de execução:**

- **Ciclo de 4 blocos** alinhado ao edital (Eng. Software/Programação → Arquitetura/Integração → Persistência/Dados → Desenvolvimento Seguro/Entrega), reservando ~50% do tempo aos 3 primeiros colocados do ranking.
- **Treino pesado em Certo/Errado** com **estatística de erros por motivo** (conceito, norma, detalhe de ferramenta). Aprender a **decidir não marcar** vale tanto quanto acertar.
- **Tabelas de siglas e frameworks** (OWASP, OAuth2/OIDC, ISO 27001/27005, ITIL/COBIT, MITRE/CIS/NIST) para fixação rápida.
- **Resolva provas-alvo:** TCU 2015 e 2026 (AUFC TI), FUNPRESP-JUD 2026 (Dev. de Sistemas), BANRISUL 2022, BDMG 2025, Bacen 2024, TCEs 2025/2026 e a **CGU 2021 (FGV)** como referência de "o que a CGU gosta".
- **Treine a discursiva** com casos de **arquitetura, segurança e contratação de TI** (situação-problema de 60 linhas), pois ela vale 70 pontos e a nota final é metade objetiva / metade discursiva (normalizadas).
- **Cuidado com o mínimo de 54 pontos na P3:** a nota de corte elimina, e o erro anula acerto — o domínio dos itens de maior incidência é o caminho mais seguro.

---

## Fontes

- Estratégia Concursos — **Raio-X Estratégico "TCU – Auditor de TI"** (incidência por disciplina/assunto, Cebraspe 2021–2025): <https://mkt.estrategia.com/concursos/wp-content/uploads/sites/2/2025/12/ID-380-TCU-%E2%80%93-Auditor-de-TI-%E2%80%93-Raio-X-Estrategico.pdf>
- Estratégia Concursos — **"TI: Temas Quentes do Cebraspe/Cespe para a Área de Controle"** (TCE-RJ, TCE-RO, TCM-BA; cruzamento percentual): <https://concursos.estrategia.com/portal/ti-controle-cebraspe-cespe/>
- Estratégia Concursos — **"TI: Temas quentes do Cebraspe/Cespe para a área Fiscal"** (SEFAZ-AL, ISS-Aracaju, SEFAZ-SE): <https://concursos.estrategia.com/portal/ti-quentes-cebraspe-fiscal/>
- Estratégia Concursos — **"Concurso TCU: os temas de TI mais modernos da prova!"** (nuvem, dados, IA, contratações, continuidade): <https://www.estrategiaconcursos.com.br/blog/concurso-tcu-temas-ti>
- QConcursos — **Prova Cebraspe TCU 2026 – AUFC – Auditoria de TI** (distribuição por disciplina: Engenharia de Software 25, Segurança 17, Governança de TI 17, Sistemas Operacionais 14 etc.): <https://www.qconcursos.com/questoes-de-concursos/provas/cespe-cebraspe-2026-tcu-auditor-federal-de-controle-externo-area-de-controle-externo-orientacao-auditoria-de-tecnologia-da-informacao>
- QConcursos — **Prova Cebraspe FUNPRESP-JUD 2026 – Analista TI – Desenvolvimento de Sistemas** (BD 21, Segurança 14, Arquitetura 7 etc.): <https://www.qconcursos.com/questoes-de-concursos/provas/cespe-cebraspe-2026-funpresp-jud-analista-de-tecnologia-da-informacao-especialidade-desenvolvimento-de-sistemas>
- QConcursos — **Prova Cebraspe BANRISUL 2022 – Analista – Desenvolvimento de Sistemas** (Eng. Software 27, Segurança 16, Programação 10, Arquitetura 8): <https://www.qconcursos.com/questoes-de-concursos/provas/cespe-cebraspe-2022-banrisul-desenvolvimento-de-sistemas>
- QConcursos — **Prova Cebraspe BDMG 2025 – Analista – Sistemas, Arquitetura e Solução de Dados** (Eng. Software 29, BD 12, Programação 8): <https://www.qconcursos.com/questoes-de-concursos/provas/cespe-cebraspe-2025-bdmg-analista-de-desenvolvimento-sistemas-arquitetura-e-solucao-de-dados>
- Folha Dirigida/QConcursos — **"Concurso Bacen auditor: veja percentual do conteúdo mais cobrado"** (TI: Eng. Software 24/120, Infraestrutura 17): <https://folha.qconcursos.com/n/concurso-bacen-auditor-disciplina-mais-cobrada>
- Folha Dirigida/QConcursos — **"Concurso CGU: veja as disciplinas mais cobradas para auditor"** (CGU 2021: TI com 8 questões de cada subárea): <https://folha.qconcursos.com/n/concurso-cgu-auditor-disciplina-mais-cobrada>
- TecConcursos — **TI – Engenharia de Software (volume de questões por assunto)**: <https://www.tecconcursos.com.br/materias/ti-engenharia-de-software>
- Cebraspe — **Prova TCU 2015 – Auditor – Auditoria de TI** (caderno oficial): <https://cdn.cebraspe.org.br/concursos/tcu_15_aufc/arquivos/TCU_AUDITOR_ABT_ED._6.PDF>
- Cebraspe — **TCE/SC – Auditor (conhecimentos específicos, itens de BD e Eng. Software)**: <https://cdn.cebraspe.org.br/concursos/tce_sc_21_auditor/arquivos/660_TCESC_003_01.PDF>
- Cebraspe — **CAU/BR 2023 (MVC, N-camadas, API Gateway, ESB, DevOps, mensageria, Git)**: <https://cdn.cebraspe.org.br/concursos/cau_br_23/arquivos/921_CAU_BR_003_01.PDF>
- Cebraspe — **FUNPRESP-JUD 2026 (NoSQL, JPA/EF Core, SQL, ETL, LGPD)**: <https://cdn.cebraspe.org.br/concursos/funpresp_26_jud/arquivos/53B8C3BA148907A01557B09C617EDF8930D28884B2D50D99C0F77DC9DC17C754.pdf>
- Cebraspe — **FUB 2020 (BD relacional, normalização, triggers, views, data mining, OLAP)**: <https://cdn.cebraspe.org.br/concursos/fub_19/arquivos/545_FUB_001_01.PDF>
- Cebraspe — **CAGEPA 2024 (código Java/Ruby/Python, SQLite, análise estática, MVC)**: <https://cdn.cebraspe.org.br/concursos/CAGEPA_24/arquivos/992_CAGEPA_003_01.PDF>
- Cebraspe — **SEFAZ/SE 2025 – Auditor (design patterns/SOLID, NoSQL, ACID, Hadoop/Spark, IaaS/PaaS/SaaS, DevSecOps)**: <https://cdn.cebraspe.org.br/concursos/sefaz_se_25_auditor/arquivos/F2DF078E18C57C4C205666B52B19C8FA823D2A4ACC43B1A0E31C0C05D6C7F3D0.pdf>
- Cebraspe — **INFRA S.A. 2026 (microsserviços, arquitetura/design/testes, TCP/port scan)**: <https://cdn.cebraspe.org.br/concursos/infrasa_26_analista/arquivos/FFBDFDD029A3100A430BBE3AFF3F3570154DBA24ADD3514177FB5F4B15616D63.pdf>
- QConcursos — **TCU 2026 – item de SSO SAML 2.0 × OAuth2** (gestão de identidade e acesso): <https://www.qconcursos.com/questoes-de-concursos/questoes/45beff06-15>
- Gran Questões — **Spring / Arquitetura de Microsserviços (questões Cebraspe 2025–2026)**: <https://questoes.grancursosonline.com.br/questoes-de-concursos/tecnologia-da-informacao-spring-428775> e <https://questoes.grancursosonline.com.br/questoes-de-concursos/tecnologia-da-informacao-arquitetura-de-microsservicos-428766>
- Estratégia Concursos — **Simulado Final TCU (AUFC – Auditoria TI), 15/02/2026** (Saga/2PC, Records Java, serverless/cold start, design patterns): <https://dhg1h5j42swfq.cloudfront.net/2026/02/13155807/sem_comentario_tcu_auditor_15-02.pdf>
- Gran Cursos — **"Resolvendo a prova discursiva do TCU 2026"** (SaaS, SLA, lock-in, fiscalização de contratos de TI): <https://blog.grancursosonline.com.br/resolvendo-a-prova-discursiva-do-concurso-tribunal-de-contas-da-uniao-2026-parte-2>
- Cebraspe — **Página oficial do concurso CGU 26 AFFC**: <https://www.cebraspe.org.br/concursos/cgu_26_affc>
- Edital **nº 1 – CGU – AFFC (08/10/2026)** — texto integral no vault: [[Edital CGU 2026 (texto integral)]].
- Análise interna do vault — **[[Analise Conteudo x Prova 2021]]** (CGU 2021 / FGV).
