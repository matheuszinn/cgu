---
tipo: resumo
disciplina: "Desenvolvimento Seguro, Qualidade e Gestão da Entrega"
tema: "Segurança de aplicações"
status: novo
data: "2026-10-16"
tags: [resumo, desenvolvimento-seguro, cgu-2026]
---

# Resumo: Segurança de aplicações

> [!info] MOC: [[Desenvolvimento Seguro, Qualidade e Gestão da Entrega]]
> Edital nº 1/2026 – CGU – AFFC · **Conhecimentos específicos** · Cargo 4 (TI / Desenvolvimento de Sistemas) · Item 1 — *Segurança de aplicações*.

## Escopo no edital (checklist)

- [x] 1.1 Ameaças e vulnerabilidades em aplicações e interfaces.
- [x] 1.2 Validação de entradas e controles de acesso.
- [x] 1.3 Proteção de segredos e dependências.
- [x] 1.4 Testes de segurança autorizados.
- [x] 1.5 Prevenção de vazamentos.
- [x] 1.6 Registros, preservação de evidências e tratamento de falhas de segurança, inclusive em integrações com IA.

## Resumo

O item cobre o núcleo de **segurança de aplicações** sob a ótica do OWASP e da prática de desenvolvimento seguro (*secure SDLC*): conhecer as **ameaças e vulnerabilidades** clássicas (Top 10), aplicar **validação de entrada** e **controles de acesso** corretos, **proteger segredos e dependências**, executar **testes de segurança autorizados** (SAST/DAST/IAST/pentest), **prevenir vazamentos** e, quando algo der errado, **registrar, preservar evidências e tratar** a falha — inclusive nos sistemas que integram **IA/LLM**.

A espinha dorsal é a **triângulo CIA** (Confidencialidade, Integridade, Disponibilidade) aplicado ao código e ao processo. Três ideias-força organizam tudo:

1. **Segurança não é funcionalidade opcional** — é requisito transversal, com *security by design* e *security by default*. O OWASP Top 10 é a referência mundial de riscos; a banca Cebraspe cobra a **ordem e o significado** de cada item e as **mitigações canônicas**.
2. **A defesa em profundidade (defense in depth)** — nunca confiar em uma única camada; validar entrada **no servidor** (nunca só no cliente), aplicar **menor privilégio** e **negação por padrão**, proteger segredos e monitorar.
3. **Segurança tem processo** — testar continuamente (shift-left), registrar eventos para **evidência forense** e responder a incidentes com rastreabilidade.

Em integrações com **IA/LLM**, somam-se riscos novos: **injeção de prompt** (direta e indireta), vazamento de informações sensíveis, *excessive agency* (autonomia/permissões excessivas de agentes) e *denial of wallet*. O guia de referência é o **OWASP Top 10 for LLM Applications**.

## 1. Ameaças e vulnerabilidades em aplicações e interfaces (1.1)

### 1.1 OWASP Top 10:2021

Lista dos dez riscos mais críticos de segurança em aplicações web, atualizada pela última vez em 2021 (o OWASP lançou uma revisão em 2025, mas a versão de 2021 ainda é a mais cobrada em prova):

| # | Item (2021) | Descrição essencial | Mitigação típica |
| --- | --- | --- | --- |
| A01 | Broken Access Control | Permissões não/ mal impostas; acesso indevido a dados/ações | Autorização no servidor, *deny by default*, testes de controle |
| A02 | Cryptographic Failures | Falha ao proteger dados em repouso/trânsito; senhas, cartões | TLS 1.2+, criptografia forte, gestão de chaves, não armazenar segredos |
| A03 | Injection | SQL/NoSQL/OS/LDAP/Command injection por entrada não tratada | Consultas parametrizadas, *allowlist*, princípio do menor privilégio |
| A04 | Insecure Design | Falhas de arquitetura/design; ausência de threat modeling | *Threat modeling*, padrões de projeto seguros, *design review* |
| A05 | Security Misconfiguration | Config padrão, páginas/recursos desnecessários, erros verbosos | *Hardening*, remoção de defaults, revisão de configuração |
| A06 | Vulnerable and Outdated Components | Dependências/libraries com CVEs, sem atualização | SBOM, SCA, atualização e *patching* contínuos |
| A07 | Identification and Authentication Failures | Autenticação fraca, força bruta, sessão/credencial mal gerida | MFA, política de senha, gestão segura de sessão |
| A08 | Software and Data Integrity Failures | Updates sem assinatura, desserialização insegura, CI/CD comprometido | Assinatura, verificação de integridade, cadeia de fornecimento |
| A09 | Security Logging and Monitoring Failures | Sem logs/alertas; detecção/ resposta lentas | Logging completo, monitoramento, alertas, resposta a incidentes |
| A10 | Server-Side Request Forgery (SSRF) | Servidor induzido a acessar recursos internos | *Allowlist* de destinos, segmentação de rede, validação de URL |

### 1.2 XSS, CSRF, SSRF, deserialização e logging

- **XSS (Cross-Site Scripting):** injetar script malicioso executado no navegador da vítima. Tipos: **refletido**, **armazenado** (persistido) e **baseado em DOM**. Mitigação: *output encoding* contextual, CSP (*Content Security Policy*), sanitização de HTML.
- **CSRF (Cross-Site Request Forgery):** o navegador da vítima autenticada é levado a enviar requisição não intencional. Mitigação: *token* anti-CSRF, cabeçalho `SameSite`, *double-submit cookie*.
- **SSRF:** a aplicação busca URL controlada pelo atacante e acessa rede interna/metadados (ex.: `169.254.169.254` na AWS). Mitigação: *allowlist* de hosts, bloquear esquemas, segmentação.
- **Deserialização insegura:** desserializar dados não confiáveis leva à execução de código (RCE). Mitigação: não desserializar entrada não confiável; validação de tipo; *allowlist* de classes.
- **Security Logging/Monitoring Failures:** ausência de logs de login, falhas e transações sensíveis; sem monitoramento, a invasão passa despercebida.

### 1.3 OWASP Top 10 for LLM Applications (2025)

Para aplicações que usam modelos de linguagem, o OWASP mantém lista própria (versão 2025):

| # | Risco LLM | Síntese |
| --- | --- | --- |
| LLM01 | Prompt Injection | Entrada manipula o modelo (direta ou indireta, via conteúdo externo) |
| LLM02 | Sensitive Information Disclosure | Vazamento de dados pessoais/segredos pelo modelo |
| LLM03 | Supply Chain | Dependências, modelos e dados de terceiros comprometidos |
| LLM04 | Data and Model Poisoning | Envenenamento de dados de treino/fine-tuning |
| LLM05 | Improper Output Handling | Saída do modelo usada sem validação (XSS, injeção, execução) |
| LLM06 | Excessive Agency | Permissões/autonomia excessivas dadas ao agente/ferramentas |
| LLM07 | System Prompt Leakage | Extração do *system prompt* e seus segredos/instruções |
| LLM08 | Vector and Embedding Weaknesses | RAG poisoning, inversão de embeddings, multitenancy |
| LLM09 | Misinformation | Alucinação/desinformação gerada com aparência de verdade |
| LLM10 | Unbounded Consumption | Consumo descontrolado de recursos/custo (Denial of Wallet) |

## 2. Validação de entradas e controles de acesso (1.2)

### 2.1 Validação de entrada

- **Nunca confie em entrada**, venha do usuário, de API, de arquivo ou de conteúdo externo. Valide **no servidor**; a validação no cliente é UX, não segurança.
- **Estratégia:** preferir ***allowlist*** (aceitar só o que é válido) a *blocklist* (negar o que é ruim), que é facilmente contornada.
- **Sanitização vs. validação:** validar (aceitar/rejeitar) é mais forte que sanitizar (limpar). **Codificação de saída** (*output encoding*) previne injeção no destino (HTML, SQL, JS, shell).
- **Injeção SQL:** usar **prepared statements / parâmetros** (ou ORM bem usado), nunca concatenar string. **Command injection:** não chamar shell com entrada; usar APIs que evitam interpretação.
- **Upload de arquivos:** validar tipo real (magic bytes), tamanho, nome, armazenar fora da raiz web, não executar.
- **Ataques de canal lateral de validação:** *format string*, *path traversal* (`../`), *XXE* (entidades externas XML). Mitigar com validação, *allowlist* e desabilitar recursos perigosos do parser.

### 2.2 Controle de acesso (autorização)

- **Autenticação ≠ autorização:** autenticar é verificar **quem é**; autorizar é decidir **o que pode** fazer. Confundir os dois é erro recorrente.
- **Menor privilégio (least privilege):** dar apenas as permissões necessárias. **Negação por padrão (deny by default):** bloquear salvo exceção explícita.
- **Níveis de autorização:** nível de **endpoint/método** (função), nível de **objeto** (IDOR/BOLA — *Broken Object Level Authorization*), nível de **campo/dado**.
- **IDOR (Insecure Direct Object Reference):** alterar o identificador (`/pedidos/123` → `/pedidos/124`) e acessar recurso alheio. Corrigir verificando **propriedade/escopo** em cada acesso.
- **Segregação de funções (SoD):** separar quem solicita, aprova e paga; evitar acúmulo de permissões conflitantes.
- **RBAC** (papéis), **ABAC** (atributos), **ReBAC** (relacionamentos) e **OAuth 2.0 scopes** são modelos de autorização; a escolha depende do domínio.

## 3. Proteção de segredos e dependências (1.3)

### 3.1 Gestão de segredos

- **Segredos** = senhas, chaves de API, tokens, chaves privadas, certificados, strings de conexão, chaves de criptografia.
- **Nunca** commitar segredos no repositório nem expô-los no cliente/browser. Usar **cofre de segredos (vault)** — HashiCorp Vault, AWS Secrets Manager, Azure Key Vault, GCP Secret Manager — com **rotação automática**, *audit* e *least privilege*.
- **Variáveis de ambiente** são melhores que hardcode, mas não são "segredo seguro" por si: vazam em logs/processos/APIs de orquestração. O ideal é injetar **referência ao cofre**, não o valor.
- **Detecção de vazamento:** *secret scanning* no CI/CD (GitGuardian, truffleHog, gitleaks, GitHub secret scanning). Rotacionar qualquer segredo exposto.
- **Criptografia de chaves:** separar **DEK** (chave de dados) de **KEK** (chave que cifra a DEK); armazenar KEK em HSM/KMS; nunca embutir chave no código.

### 3.2 Dependências e cadeia de suprimentos

- **SBOM (Software Bill of Materials):** inventário formal e estruturado de componentes, bibliotecas e dependências (diretas e **transitivas**). Formatos: **CycloneDX** e **SPDX**. Ferramentas: Syft, Trivy, Dependency-Track.
- **SCA (Software Composition Analysis):** análise de dependências contra bancos de CVEs (Snyk, OWASP Dependency-Check, GitHub Dependabot, OSS Index).
- **Dependências transitivas:** a vulnerabilidade pode vir de uma lib que você nem declarou; SBOM/SCA enxergam isso.
- **SLSA (Supply-chain Levels for Software Artifacts):** framework de níveis (L0–L3) de integridade da cadeia de build (procedência/assinatura de artefatos). Relacionado a *in-toto*, *sigstore/cosign*.
- **Ataques de supply chain:** typosquatting, *dependency confusion* (pacote malicioso de repositório público com mesmo nome), comprometimento de repositório upstream. Mitigar com *pinning*, *lockfile*, espelho interno de artefatos (Artifactory/Nexus) e verificação de assinatura.

## 4. Testes de segurança autorizados (1.4)

### 4.1 SAST, DAST, IAST, RASP, SCA

| Técnica | Analisa | Quando | Caixa | Observações |
| --- | --- | --- | --- | --- |
| **SAST** | Código-fonte/binário sem executar | Dev/CI (shift-left) | Branca | Muitos falsos positivos; depende da linguagem/framework |
| **DAST** | Aplicação em execução (de fora) | Staging/QA | Preta | Menos falsos positivos; não vê código; simula atacante |
| **IAST** | Execução com agente/sensor interno | Teste funcional | Cinza | Combina visão interna + runtime; menos falso positivo |
| **RASP** | Proteção em tempo real embutida | Produção | — | Bloqueia ataques em runtime (não é "teste", é controle) |
| **SCA** | Dependências/componentes | CI | — | Cobre código de terceiros (CVEs) |

- **SAST** = *white-box* (analisa o código em repouso); **DAST** = *black-box* (ataca a app rodando). São **complementares**, não substitutos.
- **Pentest (penetration test):** teste **manual/assistido e autorizado** que simula ataque real, com escopo e regras de engajamento definidos, entregando relatório de achados e correções. Diferente de *scan* automatizado: envolve raciocínio do testador.
- **Autorização:** todo teste ofensivo deve ser **formalmente autorizado** (contrato/escopo), respeitando limites e a legislação (ex.: art. 154-A do Código Penal — invasão de dispositivo informático). Testar sem autorização é crime.

## 5. Prevenção de vazamentos (1.5)

- **Vazamento de dados** = exposição não autorizada de informação sensível (PII, segredos, dados de negócio, logs).
- **Causas comuns:** logging excessivo de dados sensíveis, mensagens de erro verbosas com *stack trace*, dados em URL/logs, controle de acesso quebrado (A01), criptografia ausente (A02), *backup* público, bucket S3/cloud mal configurado (A05).
- **Classificação de dados:** público, interno, confidencial, restrito — determina controles de acesso, criptografia e retenção.
- **Data masking / tokenização / anonimização:** mascarar PII em logs e telas; tokenizar cartões; anonimizar em ambientes de teste (LGPD).
- **DLP (Data Loss Prevention):** monitorar/bloquear exfiltração em canais (e-mail, web, endpoints). **Privacidade:** LGPD exige minimização, finalidade e proteção de dados pessoais.
- **Princípio do menor dado:** coletar só o necessário, reter só o necessário, expor só o necessário.

## 6. Registros, evidências e tratamento de falhas (1.6)

### 6.1 Logging seguro e monitoramento

- **O que registrar:** autenticação (sucesso/falha), mudanças de privilégio, transações sensíveis, validações falhas, exceções, acessos a dados sensíveis.
- **O que NÃO registrar:** senhas, tokens completos, número de cartão, PII desnecessária (evitar vazamento via log).
- **Log estruturado** (JSON), com *timestamp*, correlação (*trace/span ID*), origem e severidade. Centralizar (SIEM), correlacionar e **alertar** (A09).
- **Monitoramento e detecção:** alertas de comportamento anômalo, brute force, repetidas falhas; tempo de detecção e resposta (MTTD/MTTR).

### 6.2 Preservação de evidências e forense

- **Evidência forense** deve ser íntegra e auditável: preservar **cadeia de custódia**, *hash* (SHA-256) dos artefatos, *timestamps* confiáveis, cópia forense (imagem) sem alterar o original.
- **Logs como evidência:** armazenar em local protegido contra adulteração (WORM), com retenção definida por política/legislação. Relógio sincronizado (NTP) é essencial.
- **Preservar, não apagar:** durante um incidente, manter logs, dumps de memória, imagens de disco, tráfego de rede antes de corrigir.

### 6.3 Tratamento de falhas e resposta a incidentes

- **Ciclo:** preparação → detecção/análise → contenção/erradicação → recuperação → lições aprendidas (alinhado ao NIST SP 800-61).
- **Fail secure (fail closed):** em caso de erro de segurança, negar acesso (não "falhar aberto").
- **Comunicação responsável:** *responsible disclosure*; não expor detalhes técnicos em mensagem de erro ao usuário.
- **Em IA/LLM:** tratar *prompt injection* e vazamento como incidente; registrar *prompts*, saídas e chamadas de ferramenta para **auditoria/forense**; *human-in-the-loop* para ações sensíveis; autorização **fora do modelo**.

## Detalhes que merecem destaque

- **Ordem do OWASP Top 10 2021:** A01 = Broken Access Control (subiu para o topo em 2021, substituindo Injection/A03); A10 = SSRF (novo).
- **XSS é categoria de *injection*** no OWASP 2017/2021 — mas a mitigação-chave é **output encoding**, não apenas validação de entrada.
- **CSRF** explora a **sessão autenticada** do navegador; **SSRF** explora a **confiança do servidor** em si próprio.
- **SAST (branca, estático)** × **DAST (preta, dinâmico)** × **IAST (cinza, agente)** — a banca cobra a **perspectiva** (código × runtime) e a **fase** (shift-left × staging).
- **Prepared statements** eliminam a **SQL injection**; **allowlist** elimina a maioria das injeções de comando/SSRF.
- **SBOM** é a "lista de ingredientes" do software; **SCA** é o "detector de veneno" que cruza o SBOM com CVEs.
- **Prompt injection indireta** vem de **conteúdo externo** (site, documento, e-mail) processado pelo LLM — mais difícil de prever que a direta.
- **Autorização de agente IA** deve ser **mediada pela aplicação** (menor privilégio por ferramenta), não delegada à "boa vontade" do modelo.

## Comparações que a banca costuma cobrar (certo/errado)

| Conceito A | Conceito B | Diferença-chave |
| --- | --- | --- |
| Autenticação | Autorização | "Quem é" (credenciais) × "o que pode" (permissões) |
| Validação (allowlist) | Sanitização | Aceitar/rejeitar regras × limpar caracteres |
| XSS | CSRF | Executa script no cliente × faz requisição forjada autenticada |
| SSRF | CSRF | Servidor acessa recurso interno × navegador envia requisição |
| SAST | DAST | Código sem executar (white-box) × app rodando (black-box) |
| SCA | SAST | Dependências de terceiros (CVEs) × seu próprio código |
| SBOM | SCA | Inventário (documento) × análise/varredura (processo) |
| Encriptação (confidencialidade) | Hash (integridade) | Reversível com chave × irreversível (senha/verificação) |
| Encriptação simétrica | Encriptação assimétrica | Mesma chave × par público/privado |
| Logging | Monitoramento | Registrar eventos × analisar/alertar sobre eles |
| Prompt injection | Jailbreak | Explora instrução de conteúdo não confiável × subtipo que "quebra" regras de segurança |

## Pegadinhas e erros comuns

> Cuidado com termos absolutos ("sempre", "nunca", "exclusivamente") e com a troca de requisitos.

- Achar que **validação no cliente** é suficiente — é apenas UX; a segurança exige validação **no servidor**.
- Confundir **autenticação com autorização** e vice-versa (clássico em prova).
- Achar que **hash é criptografia reversível** — hash (ex.: SHA-256, bcrypt/Argon2 para senha) é **unidirecional**.
- Achar que **blocklist é mais segura que allowlist** — allowlist é mais forte por negar o desconhecido.
- Pensar que **SAST substitui DAST** (ou o contrário) — são **complementares**.
- Achar que **variáveis de ambiente tornam o segredo seguro** — reduzem o hardcode, mas ainda vazam em logs/dumps de processo.
- Achar que **SBOM elimina vulnerabilidade** — SBOM apenas **inventaria**; a correção vem de SCA + patch.
- Confundir **RASP** (controle de produção) com **teste** (SAST/DAST/IAST).
- Achar que **pentest é só rodar um scanner** — pentest envolve raciocínio manual e **autorização formal**.
- Ignorar que **prompt injection não tem "patch" definitivo** — exige **defesa em profundidade** (validação, privilégio mínimo, HITL, filtragem de saída).
- Achar que **negação por padrão** é "menos funcional" — é princípio de segurança, não limitação de funcionalidade.

## Notas atômicas relacionadas

```dataview
LIST FROM "20 - Notas"
WHERE disciplina = this.disciplina
  AND contains(tema, this.tema)
SORT file.name ASC
```

## Fontes

- https://owasp.org/Top10/ (OWASP Top 10:2021 — lista oficial dos dez riscos)
- https://top10.owasp.org/2021/A01_2021-Broken_Access_Control/ (OWASP A01 — Broken Access Control)
- https://top10.owasp.org/2021/A03_2021-Injection/ (OWASP A03 — Injection; SQL/NoSQL/OS/LDAP/Command)
- https://top10.owasp.org/2021/A10_2021-Server-Side_Request_Forgery_%28SSRF%29/ (OWASP A10 — SSRF)
- https://cheatsheetseries.owasp.org/IndexTopTen.html (OWASP Cheat Sheet Series — índice do Top 10)
- https://cheatsheetseries.owasp.org/cheatsheets/Input_Validation_Cheat_Sheet.html (OWASP — validação de entrada)
- https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html (OWASP — prevenção de XSS)
- https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html (OWASP — prevenção de CSRF)
- https://cheatsheetseries.owasp.org/cheatsheets/Secrets_Management_Cheat_Sheet.html (OWASP — gestão de segredos)
- https://genai.owasp.org/llm-top-10/ (OWASP Top 10 for LLM Applications 2025)
- https://genai.owasp.org/llmrisk/llm01-prompt-injection/ (OWASP LLM01 — Prompt Injection)
- https://cheatsheetseries.owasp.org/cheatsheets/LLM_Prompt_Injection_Prevention_Cheat_Sheet.html (OWASP — prevenção de injeção de prompt)
- https://snyk.io/articles/sast-dast-iast-rasp/ (Snyk — SAST vs DAST vs IAST vs RASP)
- https://www.nist.gov/itl/executive-order-14028-improving-nations-cybersecurity/software-supply-chain-security-guidance-20 (NIST — SBOM e supply chain)
- https://slsa.dev/ (SLSA — Supply-chain Levels for Software Artifacts)
