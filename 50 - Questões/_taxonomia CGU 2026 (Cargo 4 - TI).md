---
tipo: referência
banca: Cebraspe
tags:
  - cgu-2026
  - taxonomia
  - TI
---

# Taxonomia — CGU 2026 · Cargo 4 (AFFC TI / Desenvolvimento de Sistemas)

> Fonte: **Edital nº 1/2026 – CGU – AFFC**, item **15.2.4 (CONHECIMENTOS ESPECÍFICOS – CARGO 4)**.
> Use **somente** esta taxonomia no cruzamento. Assunto que não pertença a ela → **descartar**.

## E1 — Engenharia de Software e Programação
- **E1.1 Problemas e requisitos** — necessidades de usuários; requisitos funcionais e não funcionais; restrições e critérios de aceitação; desenho centrado nas pessoas; relação problema público / processo de trabalho / solução digital.
- **E1.2 Programação e correção** — Java (tipos de dados, estruturas de controle, métodos, classes e objetos); encapsulamento, interfaces, herança e polimorfismo; coleções e tipos genéricos; igualdade de objetos, mutabilidade, tratamento de exceções e I/O de arquivos; estruturas de dados, algoritmos e pseudocódigo; leitura, depuração e testes de borda; complexidade em decisões de desempenho; modularidade e padrões de projeto.
- **E1.3 Concorrência e processamento** — concorrência, paralelismo e assincronia; condições de corrida e sincronização; estado compartilhado, bloqueios e falhas; correção e desempenho sob requisições concorrentes.
- **E1.4 Interfaces e experiência do usuário** — usabilidade, prototipagem e desenho responsivo; acessibilidade e barreiras digitais; componentes de interface e reaproveitamento; validação com usuários e prevenção de erros; JavaScript e Vue.js (componentes, reatividade, eventos, consumo de APIs).
- **E1.5 Manutenção e evolução** — débito técnico, documentação, modularidade e acoplamento; sustentação e modernização de legados; interoperabilidade e compatibilidade; impactos das mudanças e falhas na continuidade/qualidade dos serviços.

## E2 — Arquitetura e Integração de Sistemas
- **E2.1 Arquiteturas de aplicações** — monolitos, microsserviços e arquiteturas orientadas a eventos; distribuição de responsabilidades, acoplamento e dependências; desempenho, escalabilidade, segurança e custo; escolha de arquitetura; Java com Spring Framework e Spring Boot (componentes, IoC, injeção de dependências, configuração/autoconfiguração); serviços REST e separação apresentação/negócio/dados.
- **E2.2 APIs e identidade** — design, contratos e versionamento de APIs REST; autenticação e autorização; OAuth 2.0; OpenID Connect; uso/validação/proteção de tokens; controle de acesso e segregação de funções; Spring Security; proteção de endpoints e métodos; permissões excessivas e falhas de controle de acesso.
- **E2.3 Comunicação e consistência** — mensageria, eventos e persistência; falhas, repetição de requisições, idempotência e consistência; integração entre sistemas e coordenação de operações; evolução de contratos e migração de esquemas.
- **E2.4 Integração com dados e IA** — consumo/disponibilização de serviços de dados e modelos de linguagem; representações vetoriais, busca semântica e RAG; agentes e ferramentas; avaliação funcional de respostas e fontes; limites de autorização, supervisão e proteção contra instruções maliciosas (prompt injection).
- **E2.5 Confiabilidade das aplicações** — contêineres, serviços de nuvem e serverless; logs, métricas e rastreamento; latência, disponibilidade, capacidade e tolerância a falhas; diagnóstico de integrações e dependências; continuidade, recuperação e degradação de serviços.

## E3 — Persistência, Integração e Proteção de Dados
- **E3.1 Modelagem e persistência** — modelagem relacional, normalização e integridade; bancos documentais, chave-valor e vetoriais; cache e busca textual; escolha de armazenamento; transações, concorrência, consistência e evolução de esquemas; persistência em Java com JPA (mapeamento, ciclo de vida, contexto de persistência, consultas, transações); estratégias de carregamento; Spring Data JPA (repositórios, consultas, paginação); integração da persistência às regras de negócio.
- **E3.2 SQL e desempenho** — definição e manipulação de dados, controle de acesso e transações; filtros, junções, agregações, subconsultas e CTE; índices, planos de execução, nulos e duplicações; diagnóstico de consultas e efeitos no desempenho.
- **E3.3 Fluxos e interoperabilidade** — ingestão/transformação/carga; ETL e ELT; processamento em lote e fluxo, completo e incremental; APIs e formatos CSV, JSON, XML e Parquet; qualidade, rastreabilidade, conciliação e repetição segura; Spring Batch (jobs e steps, leitura/processamento/escrita, controle transacional, reinício após falhas, prevenção de perdas e duplicações).
- **E3.4 Privacidade e segurança de dados** — minimização, finalidade, acesso e segregação; criptografia em trânsito e repouso; pseudonimização e risco de reidentificação; retenção, descarte e proteção de cópias; compartilhamento e publicação com salvaguardas; proteção de dados desde a concepção (privacy by design).

## E4 — Desenvolvimento Seguro, Qualidade e Gestão da Entrega
- **E4.1 Segurança de aplicações** — ameaças e vulnerabilidades em aplicações e interfaces; validação de entradas e controles de acesso; proteção de segredos e dependências; testes de segurança autorizados; prevenção de vazamentos; registros, preservação de evidências e tratamento de falhas de segurança (inclusive integrações com IA).
- **E4.2 Testes e qualidade** — testes unitários, de integração, de contrato e de aceitação; análise estática, cobertura e revisão de código; automação e dados de teste; limites das métricas de qualidade; verificação de requisitos funcionais, segurança, desempenho e acessibilidade.
- **E4.3 Entrega e operação** — versionamento, integração e entrega contínuas; DevSecOps e segurança da cadeia de dependências; automação de build, teste e implantação; configuração e segregação de ambientes; mudanças, reversão e observabilidade; manutenção da continuidade durante entregas e incidentes.
- **E4.4 Gestão de produtos e governança** — descoberta de necessidades, entrega e ciclo de vida de produtos digitais; Scrum e Kanban; priorização, critérios de aceitação e indicadores de resultado; PDTIC, plano de transformação digital e plano de dados abertos; riscos, responsabilidades e evidências de efetividade de controles.
- **E4.5 Contratação e fiscalização de soluções** — necessidade, estudo técnico preliminar e termo de referência; comparação entre desenvolvimento próprio, contratação e compartilhamento; viabilidade, dimensionamento, custo total de propriedade e pesquisa de preços; qualidade, níveis de serviço e entregas verificáveis; fiscalização e pagamento; propriedade intelectual, portabilidade, acesso a código e dados, dependência tecnológica e plano de saída.
