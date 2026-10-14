---
tipo: resumo
disciplina: "Arquitetura e Integração de Sistemas"
tema: "APIs e identidade"
status: estudando
data: "2026-10-14"
tags: [resumo, arquitetura, cgu-2026]
---

# Resumo: APIs e identidade

> [!info] MOC: [[Arquitetura e Integração de Sistemas]]
> Edital nº 1/2026 – CGU – AFFC · **Conhecimentos específicos** · Cargo 4 (TI / Desenvolvimento de Sistemas) · Item 2 — *APIs e identidade*.

## Escopo no edital (checklist)

- [x] 2.1 Design, contratos e versionamento de APIs REST.
- [x] 2.2 Autenticação e autorização.
- [x] 2.3 OAuth 2.0 para autorização e OpenID Connect para autenticação federada.
- [x] 2.4 Uso, validação e proteção de tokens.
- [x] 2.5 Controle de acesso e segregação de funções nas aplicações.
- [x] 2.6 Spring Security: configuração e avaliação de mecanismos de autenticação e autorização.
- [x] 2.7 Proteção de endpoints e métodos.
- [x] 2.8 Identificação e correção de permissões excessivas e falhas de controle de acesso.

## Resumo

O item reúne dois mundos que se cruzam o tempo todo em uma API: **como expor o recurso** (design/contrato/versionamento) e **quem pode acessá-lo** (identidade, autenticação, autorização e tokens). O fio condutor é este:

1. **API REST bem projetada** = recursos identificados por URI, manipulados por métodos HTTP com semântica correta, representações (JSON) negociadas, **contrato explícito** (OpenAPI) e **versionamento** que evita quebrar clientes.
2. **Identidade** começa por separar **autenticação** (quem você é) de **autorização** (o que você pode fazer) — erro conceitual que a banca cobra com frequência.
3. **OAuth 2.0** é um **framework de autorização delegada** (o cliente obtém acesso limitado a um recurso em nome do usuário), **não** um protocolo de autenticação. **OpenID Connect (OIDC)** é a **camada de identidade** sobre o OAuth 2.0 que resolve autenticação federada, entregando o **ID Token** (JWT com claims de autenticação).
4. **Tokens** são a moeda de troca: **access token** (acessa a API), **refresh token** (renova o access, sem ir ao resource server) e **ID token** (prova de autenticação no OIDC). Precisam ser **validados** (assinatura, algoritmos permitidos, `iss`, `aud`, `exp`/`nbf`) e **protegidos** (TLS, vida curta, sem URL/logs, sender-constrained).
5. **Controle de acesso** aplica-se em vários níveis (endpoint, método, objeto, dado, campo) sob os princípios de **menor privilégio** e **negação por padrão**, com **segregação de funções (SoD)** para impedir conflito de interesses.
6. **Spring Security** é o framework de referência em Java: filter chain, `AuthenticationManager`, `AuthorizationManager`, `authorizeHttpRequests`, `@PreAuthorize`, OAuth2 resource server/OIDC login, CSRF, CORS e gestão de sessão.
7. **Falhas de controle de acesso** dominam o OWASP API Security Top 10 (BOLA/API1, BFLA/API5, BOPLA/API3, Broken Authentication/API2) e devem ser **identificadas por auditoria/testes** e **corrigidas** com checagens de objeto, negação por padrão e revisão periódica de permissões.

## 1. Design, contratos e versionamento de APIs REST (2.1)

### 1.1 REST: origem e restrições arquiteturais

REST (*Representational State Transfer*) é um **estilo arquitetural** descrito por **Roy Fielding** em sua tese de doutorado (2000), não uma norma nem um protocolo. As restrições (constraints) que definem um sistema REST:

- **Cliente–servidor:** separação de responsabilidades entre UI e dados/lógica.
- **Sem estado (stateless):** cada requisição contém toda a informação necessária; o servidor não guarda estado de sessão entre chamadas (o "estado" do acrônimo é o **estado do recurso**, não o da sessão).
- **Cacheável:** respostas devem declarar-se cacheáveis ou não (`Cache-Control`, `ETag`).
- **Interface uniforme:** recursos identificados por URI; manipulação por **representações**; mensagens autodescritivas; **HATEOAS**.
- **Sistema em camadas:** proxies, gateways e balanceadores são transparentes ao cliente.
- **Código sob demanda** (opcional): o servidor pode enviar código executável ao cliente.

**Recursos** são a abstração central; uma **representação** (ex.: JSON) captura o estado atual ou desejado do recurso e é transferida via HTTP. **HATEOAS** (*Hypermedia as the Engine of Application State*) fornece links que guiam as transições de estado — é o nível 3 do **Modelo de Maturidade de Richardson** (nível 0 = POX/RPC, 1 = recursos, 2 = verbos HTTP + status, 3 = hypermedia). Na prática, a maioria das APIs "REST" do mercado são **nível 2**.

### 1.2 Recursos, URIs e substantivos

- A URI identifica um **substantivo** (recurso), não uma ação: prefira `/pedidos/123` a `/getPedido?id=123`.
- Use **plural** para coleções (`/usuarios`), **hierarquia** para sub-recursos (`/usuarios/42/pedidos`), **kebab-case** em minúsculas; evita-se `snake_case`/`camelCase` em paths.
- Evite colocar **verbos** na URI; a ação vem do **método HTTP**. Exceções pragmáticas: ações não-CRUD ("`POST /pedidos/123/cancelar`").
- **Stateless**: nada de guardar contexto de sessão no servidor para a API; o token/credencial acompanha cada requisição.

### 1.3 Métodos HTTP: segurança e idempotência

Da RFC 7231 (semântica HTTP; hoje substituída pela RFC 9110):

| Método | Significado | Seguro (safe) | Idempotente |
| --- | --- | --- | --- |
| GET | Obter representação | Sim | Sim |
| HEAD | Igual ao GET, sem corpo | Sim | Sim |
| OPTIONS | Opções/comunicação | Sim | Sim |
| POST | Criar / processar | Não | **Não** |
| PUT | Substituir recurso inteiro | Não | **Sim** |
| PATCH | Modificar parcialmente | Não | **Não necessariamente** |
| DELETE | Remover recurso | Não | **Sim** |

- **Seguro (safe)** = não altera o estado do recurso (somente leitura).
- **Idempotente** = repetir a operação N vezes produz o mesmo efeito que 1 vez.
- **POST não é idempotente** → risco de duplicidade em retentativas. Mitigação: **Idempotency-Key** (chave única por operação, com resposta cacheada).
- **PUT** (substituição total) ≠ **PATCH** (parcial) ≠ **POST** (criação/processamento).
- Para idempotência e consistência de integrações, ver também o Item 3.2 do edital (mensageria/retentativas).

### 1.4 Códigos de status (uso semântico correto)

- **2xx:** 200 OK, 201 Created (+ `Location`), 202 Accepted (processamento assíncrono), 204 No Content.
- **3xx:** 301/302, 304 Not Modified (cache/condicional), 307/308 (preservam método e corpo).
- **4xx:** 400 Bad Request; **401 Unauthorized** (falta/não autenticou → incluir `WWW-Authenticate`); **403 Forbidden** (autenticou, mas **não tem permissão**); 404 Not Found; 405 Method Not Allowed; 406 Not Acceptable; 409 Conflict; 412 Precondition Failed; 415 Unsupported Media Type; 422 Unprocessable Entity (validação semântica); 429 Too Many Requests.
- **5xx:** 500 Internal Server Error; 501 Not Implemented; 503 Service Unavailable.

**Erros padronizados:** use **RFC 9457** (*Problem Details for HTTP APIs*, que sucede a RFC 7807) com `Content-Type: application/problem+json` e campos `type`, `title`, `status`, `detail`, `instance`. Não vaze *stack traces* nem detalhes internos.

### 1.5 Representações e negociação de conteúdo

- Formato predominante: **JSON** (`application/json`). Alternativas: XML, Protobuf, Avro.
- **Content negotiation** via `Accept` (cliente) e `Content-Type` (corpo). Se nenhum formato for aceitável → **406 Not Acceptable**; mídia enviada não suportada → **415 Unsupported Media Type**.
- Não copie cegamente o `Accept` para o `Content-Type` da resposta (risco de *MIME sniffing*/injeção).

### 1.6 Contratos de API (design-first)

O **contrato** descreve endpoints, parâmetros, schemas, respostas e erros — é a interface estável entre consumidores e provedores.

- **OpenAPI Specification (OAS) 3.x** — padrão de facto para APIs REST; antes chamada **Swagger** (Swagger 2.0 → OpenAPI 3.0/3.1). Ferramentas: Swagger UI, Swagger Editor, Redoc, geradores de código.
- **JSON Schema** — validação de estruturas JSON; usado dentro do OpenAPI.
- **AsyncAPI** — equivalente para APIs assíncronas/eventos (mensageria).
- **Design-first** (contrato antes do código) vs **code-first** (código gera o contrato): o design-first favorece alinhamento entre times e governança; o code-first favorece velocidade.
- **Contract testing / consumer-driven contracts** (ex.: **Pact**): o consumidor define expectativas e o provedor as verifica em build.
- **Governança de contrato**: versionamento do arquivo, revisão, *linting*, compatibilidade retroativa.

### 1.7 Versionamento

Formas de versionar (com trade-offs):

| Estratégia | Exemplo | Prós | Contras |
| --- | --- | --- | --- |
| **URI** | `/v1/usuarios` | Simples, visível, fácil de rotear | Mistura versão com recurso; "polui" a URI |
| **Query param** | `/usuarios?version=1` | Fácil | Menos idiomático |
| **Header customizado** | `X-API-Version: 1` | URI limpa | Invisível, difícil de testar no navegador |
| **Media type (content negotiation)** | `Accept: application/vnd.acme.v1+json` | "Puro" REST | Complexo; pouco suportado por ferramentas |

- **Mudança compatível (não quebra cliente):** adicionar campo opcional, novo endpoint, novo valor em enum tratável. **Mudança incompatível (breaking):** remover/renomear campo, mudar tipo, tornar campo obrigatório, alterar semântica/status code.
- Só versione em **mudanças incompatíveis**. Ferramentas de política: **Versionamento Semântico (SemVer)**, header **`Deprecation`** e **`Sunset`** (RFC 8594, RFC 9745), janelas de suporte e descontinuação anunciada.
- Evite explosão de versões: prefira **compatibilidade retroativa** e *expand-and-contract*.

### 1.8 Boas práticas de design

- **Paginação** (`?page=&size=` ou **cursor**), **filtros** (`?status=ativo`), **ordenação** (`?sort=-criado_em`), **sparse fieldsets**, limites (`limit`) e limites de tamanho de payload (413).
- **Rate limiting** → **429** + `Retry-After`.
- **Idempotência** e **timestamps** padronizados (ISO 8601/UTC).
- **Segurança desde o design**: validar entrada, restringir métodos (allowlist, **405**), CORS restritivo, headers de segurança, não expor endpoints de gestão na internet.

## 2. Autenticação e autorização (2.2)

### 2.1 Distinção conceitual (essencial)

- **Autenticação (AuthN):** verificar **quem é** o sujeito (usuário, sistema, cliente). Responde "você é quem diz ser?".
- **Autorização (AuthZ):** decidir **o que** o sujeito autenticado **pode fazer**. Responde "você tem permissão para isto?".
- **Autenticação vem antes da autorização**, mas são mecanismos independentes. Falhar na AuthN → **401**; falhar na AuthZ → **403**.
- **Identidade** = conjunto de atributos de uma entidade; **credencial** = evidência apresentada para provar a identidade.

### 2.2 Fatores de autenticação e MFA

- **Fatores:** algo que você **sabe** (senha, PIN), **tem** (token, celular, chave), **é** (biometria) — e, em modelos modernos, o **local/contexto** ("em algum lugar que você está").
- **MFA** = dois ou mais fatores **de categorias diferentes**. Senha + PIN **não** é MFA (mesma categoria "sabe").
- **2FA/autenticação forte**; **passkeys/WebAuthn/FIDO2** (resistente a phishing).
- Senhas: nunca em texto claro; usar **hash + salt** com algoritmos lentos (**bcrypt, scrypt, Argon2, PBKDF2**); políticas contra **credential stuffing** (rate limiting, lockout, CAPTCHA, verificação de senhas vazadas).

### 2.3 Sessões x tokens

- **Sessão no servidor:** cookie com *session id* opaco; servidor mantém estado; invalidação fácil; requer proteção **CSRF**.
- **Token stateless (JWT):** servidor não guarda estado; escalável; **dificulta revogação** (precisa de denylist/curta duração).
- Cookies de sessão devem usar `HttpOnly`, `Secure`, `SameSite` e `__Host-`/`__Secure-`.
- APIs puramente de máquina normalmente usam **Bearer token** no header `Authorization` (sem cookies), o que dispensa CSRF.

### 2.4 Autenticação federada e SSO

- **Federada:** a autenticação é delegada a um **IdP (Identity Provider)** externo/confiável; o serviço (**RP/SP**) confia na asserção. Protocolos: **OIDC**, **SAML 2.0**, WS-Federation.
- **SSO (Single Sign-On):** autenticar uma vez e acessar vários serviços; **SLO (Single Logout)** encerra todas.
- **Provisionamento:** **SCIM** (RFC 7643/7644) padroniza usuários/grupos; **JIT provisioning** cria o usuário no primeiro login.
- **Federação de identidade** reduz senhas duplicadas e centraliza políticas, mas cria **dependência do IdP** (ponto único de falha).

### 2.5 Modelos de autorização

- **DAC (Discretionary AC):** o **dono** do recurso concede acesso (discricionário).
- **MAC (Mandatory AC):** rótulos de segurança e níveis de classificação; decisão central; comum em ambientes militares/governamentais.
- **RBAC (Role-Based AC):** permissões atribuídas a **papéis**; usuários recebem papéis. Simples de administrar, mas sofre de **explosão de papéis** e **role explosion**.
- **ABAC (Attribute-Based AC):** decisão por **atributos** (sujeito, recurso, ação, ambiente) via políticas → mais granular/flexível, mais complexo.
- **ReBAC (Relationship-Based AC):** decisões por **relações** (ex.: "usuário é dono do recurso", Google Zanzibar, OpenFGA).
- **Policy engines** externos: **OPA/Rego**, XACML.

### 2.6 Autenticação de clientes (machine-to-machine)

- **API keys:** identificam a **aplicação** (não o usuário); simples, porém fáceis de vazar e sem granularidade; **não** substituem autenticação de usuário; não colocar na URL.
- **mTLS:** certificado de cliente; forte, comum em B2B e *sender-constrained*.
- **OAuth 2.0 client credentials:** o cliente autentica-se no AS e recebe access token (sem usuário).
- **HMAC/signature-based (ex.: AWS SigV4)** e **private_key_jwt** (asserção JWT assinada).

## 3. OAuth 2.0 e OpenID Connect (2.3)

### 3.1 OAuth 2.0 — o que é

**RFC 6749** (e RFC 6750 para bearer tokens). É um **framework de autorização** que permite a uma aplicação de terceiros obter **acesso limitado** a um serviço HTTP, **em nome do dono do recurso** ou **em nome próprio**, sem compartilhar a senha. Introduz uma **camada de autorização** que separa o papel do **cliente** do papel do **dono do recurso**.

> **Ponto decisivo:** OAuth 2.0 é **autorização**, não autenticação. Usar "Login com OAuth" sem OIDC é um antipadrão — daí a necessidade do OpenID Connect.

### 3.2 Os quatro papéis (RFC 6749)

1. **Resource Owner** (dono do recurso) — normalmente o usuário final.
2. **Client** (cliente) — aplicação que pede acesso em nome do dono.
3. **Authorization Server** (AS) — emite os tokens após autenticar/autorizar.
4. **Resource Server** (RS) — hospeda o recurso protegido e aceita o access token.

### 3.3 Tokens e endpoints

- **Access token:** credencial para acessar recursos; opaco ao cliente; representa escopo, duração e atributos.
- **Refresh token:** usado **somente com o AS** para obter novo access token; **nunca** vai ao resource server.
- Endpoints: **authorization** (interação com o usuário), **token** (troca de grant por token), **redirection** (retorno ao cliente), **introspection** (RFC 7662, valida o token), **revocation** (RFC 7009), **JWKS** (chaves públicas).
- Tipos de cliente: **confidential** (consegue guardar segredo, ex.: app servidor) e **public** (não consegue, ex.: SPA/mobile).
- Autenticação de cliente: `client_secret_basic`, `client_secret_post`, `private_key_jwt`, **mTLS** (RFC 8705).

### 3.4 Grant types (fluxos)

- **Authorization Code** — o principal e recomendado. O cliente redireciona o usuário ao AS, recebe um **código** e o troca no token endpoint (com autenticação do cliente). Os tokens não passam pelo user-agent.
- **Authorization Code + PKCE (RFC 7636)** — obrigatório para **public clients** e recomendado para todos. O cliente gera `code_verifier` (aleatório, alta entropia), envia `code_challenge` (S256 = SHA-256 do verifier) e apresenta o verifier na troca; impede interceptação do código.
- **Client Credentials** — cliente age em nome próprio, sem usuário (M2M). `sub` normalmente é o identificador do cliente.
- **Implicit** — **obsoleto/desencorajado**: token entregue na resposta de autorização (exposto em URL/fragment/histórico). Não usar.
- **Resource Owner Password Credentials (ROPC)** — **proibido pela RFC 9700**: expõe credenciais ao cliente, incompatível com MFA.
- **Refresh Token** — renova o access token sem novo consentimento.
- **Device Authorization Grant (RFC 8628)** — dispositivos com entrada limitada (TV, CLI).
- **Token Exchange (RFC 8693)** — troca de tokens entre serviços/domínios.
- **JWT Bearer (RFC 7523)** — asserção JWT como grant (server-to-server).

### 3.5 Escopos, consentimento e parâmetros de segurança

- **Scope:** string delimitada por espaços que limita o acesso (`read`, `write`, `openid profile email`). O AS só deve emitir escopos autorizados.
- **`state`:** valor opaco anti-**CSRF**, vinculado à sessão do usuário.
- **`nonce`:** no OIDC, vincula a requisição ao ID Token e mitiga **replay**.
- **`redirect_uri`:** deve casar **exatamente** com o pré-registrado (comparação literal).
- **`response_type`:** `code` (recomendado), `token` (implicit, não usar), combinações híbridas do OIDC.
- **`resource`** (RFC 8707) e **`aud`** ajudam a restringir o público do token.

### 3.6 Segurança do OAuth (RFC 9700 — BCP)

Práticas atuais (o que a banca tende a cobrar como "certo"):

- **Exact match** de `redirect_uri`; **proibição de open redirectors**.
- **PKCE obrigatório**; AS deve impedir **PKCE downgrade**; `S256` (não `plain`).
- **`state`/`nonce`** para CSRF/replay; proteção contra **mix-up attack** via `iss` (RFC 9207) ou URIs distintas.
- **Implicit e ROPC proibidos/desencorajados**.
- **Access tokens com vida curta** e **audience-restricted**; **refresh tokens** para public clients devem ser **sender-constrained** ou usar **rotação**.
- **Sender-constrained tokens:** **mTLS (RFC 8705)** ou **DPoP (RFC 9449)**.
- **TLS ponta a ponta**; **Authorization Server Metadata (RFC 8414)** e *discovery* para evitar endpoints errados.
- CORS **não** no authorization endpoint; CORS pode nos endpoints acessados diretamente pela SPA (token, jwks).

### 3.7 OpenID Connect (OIDC) — autenticação federada

O **OpenID Connect Core 1.0** é uma **camada de identidade simples sobre o OAuth 2.0**. Permite o **cliente** (agora **RP, Relying Party**) verificar a **identidade do usuário** com base na autenticação feita pelo **OpenID Provider (OP)** — o AS que implementa OIDC.

- É acionado incluindo o escopo **`openid`** na requisição de autorização.
- O resultado da autenticação vem num **ID Token** (JWT) com claims sobre o evento de autenticação.
- Fluxos: **Authorization Code Flow** (`code`, recomendado), **Implicit** (`id_token`, obsoleto) e **Hybrid** (`code id_token`, etc.).
- **UserInfo Endpoint:** recurso protegido que, com o access token, devolve **claims** do usuário.
- **Discovery:** `.well-known/openid-configuration` publica endpoints e **`jwks_uri`**.
- Escopos padrão: `openid` (obrigatório), `profile`, `email`, `address`, `phone`, `offline_access` (refresh token).

### 3.8 ID Token: claims essenciais

- **Obrigatórias:** `iss` (emissor), `sub` (identificador local do usuário), `aud` (deve conter o `client_id` da RP), `exp` (expiração), `iat` (emissão).
- **Opcionais/contextuais:** `auth_time`, `nonce`, `acr` (classe de contexto de autenticação), `amr` (métodos usados), `azp` (parte autorizada).
- O ID Token **deve ser assinado** (JWS); pode ser assinado **e depois cifrado** (JWE → *nested JWT*).
- **Validação obrigatória** do ID Token: assinatura, `iss`, `aud` (= client_id), `exp`, e `nonce` quando aplicável.
- **`sub` pode ser público ou pairwise** (PPID — identificador pseudônimo por RP, evita correlação entre serviços).

### 3.9 OAuth 2.0 x OIDC (não confundir)

- **OAuth 2.0** → **autorização** delegada; emite **access token**.
- **OIDC** → **autenticação** federada sobre OAuth; emite **ID token** (+ access token).
- Nunca use o **access token** como prova de autenticação do usuário, nem o **ID token** para acessar APIs. São tokens com **finalidades distintas** (confusão → *cross-JWT confusion*).

## 4. Uso, validação e proteção de tokens (2.4)

### 4.1 Opaco x JWT

- **Token opaco:** string sem significado para o cliente; o RS valida por **introspecção (RFC 7662)** no AS. Vantagens: revogação imediata, sem vazar dados. Desvantagem: depende do AS a cada validação.
- **JWT (RFC 7519):** token **autocontido** e assinado; o RS valida localmente pela chave pública (**sem** ida ao AS). Ótimo para escalabilidade; cuidado com revogação e com exposição de dados.

### 4.2 Estrutura do JWT

Formato: `base64url(header).base64url(payload).base64url(signature)`.

- **JOSE Header:** `alg` (algoritmo de assinatura), `typ` (ex.: `JWT`, `at+jwt`), `kid` (id da chave), e opcionalmente `jku`/`jwk`/`x5c`/`x5u` (chave/certificado — **não confiar neles como fonte de verdade**), `cty` (para *nested JWT*).
- **Claims (payload):** registradas (`iss`, `sub`, `aud`, `exp`, `nbf`, `iat`, `jti`), públicas (URI com namespace) e privadas (acordadas in-band).
- **Assinatura:** JWS. **JWS fornece integridade/autenticidade, mas NÃO confidencialidade** — o payload é apenas base64url, legível por qualquer um. Para sigilo, usar **JWE** (ou *nested JWT*: assina e depois cifra).
- Algoritmos: **simétricos (HS256/384/512)** — mesma chave assina e verifica; **assimétricos (RS256, PS256, ES256, EdDSA)** — chave privada assina, pública verifica (recomendado para multi-serviço). Não usar `none`.

### 4.3 Validação de token — checklist

Segundo **RFC 9068** (perfil JWT para access tokens OAuth 2.0), o resource server **deve**:

1. Verificar que o header `typ` é **`at+jwt`** (ou `application/at+jwt`) e rejeitar os demais (evita aceitar um ID token como access token).
2. Validar a **assinatura** com as chaves publicadas pelo AS (`jwks_uri`), **rejeitando `alg: none`**.
3. Conferir `iss` **exatamente** com o emissor esperado.
4. Conferir que `aud` contém o identificador do próprio RS; senão **rejeitar**.
5. Conferir `exp` (com pequena tolerância de *clock skew*) e, se presente, `nbf`.
6. Escolher a chave pelo **`kid`** dentro do JWKS **do emissor validado** (não misturar chaves de emissores).
7. Usar **allowlist de algoritmos** e **nunca** deixar o header `alg` escolher o algoritmo.
8. Respeitar **escopos/roles** para a decisão de autorização.

### 4.4 Ataques e antipadrões com tokens

- **`alg: none`:** aceitar token sem assinatura → forja completa. Nunca aceitar.
- **Confusão de algoritmo/tipo de chave (*key/alg confusion*):** o atacante troca `RS256` por `HS256` e usa a **chave pública** como segredo HMAC. Mitigar com allowlist e tipagem forte.
- **Confiar em material de chave do header (`jku`, `jwk`, `x5u`, `x5c`):** o header é **entrada não autenticada**; obter chave só de fonte confiável (`jwks_uri` do `iss`).
- **Confusão de emissor/audiência:** token de um serviço aceito em outro; validar `iss`/`aud` e não unir JWKS de vários emissores.
- **Cross-JWT confusion:** ID token usado como access token (ou reset token como access). Usar **tipagem explícita (`typ`)** e regras **mutuamente exclusivas** (chaves/claims isolados).
- **Replay:** token roubado reutilizado. Mitigar com curta duração, `jti`/denylist, `nonce` e tokens *sender-constrained*.
- **Vazamento:** token em URL, logs, histórico do navegador, referrer, `localStorage` exposto a XSS.
- **Segredo HMAC fraco/reutilizado:** usar segredo com entropia ≥ tamanho do output (`HS256` → 256 bits) e **não** reutilizar segredo entre audiências/emissores; nunca usar senha como segredo.

### 4.5 Proteção de tokens

- **TLS em todo o trânsito** (BCP 195); validar a cadeia de certificados do servidor.
- **Vida curta** para access tokens (≤ 1 hora, idealmente minutos); **refresh tokens** de vida maior com **rotação** e *reuse detection*.
- **Sender-constrained:** **mTLS** (RFC 8705) e **DPoP** (RFC 9449) amarram o token à posse de uma chave.
- **Audience restriction e escopo mínimo**; nada de token "faz-tudo".
- **Armazenamento:** servidor → cofre de segredos; navegador → preferir **cookie `HttpOnly` + `Secure` + `SameSite`**; evitar `localStorage` (vulnerável a XSS). **Não** armazenar bearer token em cookie enviado em claro (RFC 6750).
- **Não colocar token na URL** (query params); usar header `Authorization: Bearer <token>`.
- **Não logar tokens**; mascarar em logs e telemetria.
- **Revogação:** introspecção (opaco), **denylist por `jti`/`iss`** (JWT) ou **Token Status List**; encerrar sessão invalida tokens.
- **Rotação de chaves** e **JWKS** com `kid`; *cryptographic agility*.
- **JWE** quando for necessário sigilo de claims; **não** colocar dado sensível no JWT se ele puder ficar opaco.

### 4.6 Access x refresh x ID token

| Token | Emitido por | Para quem | Finalidade |
| --- | --- | --- | --- |
| **Access token** | AS | Resource Server | Acessar a API (autorização) |
| **Refresh token** | AS | Cliente (só com o AS) | Renovar access token |
| **ID token** | OP (OIDC) | Cliente (RP) | Provar autenticação do usuário |

## 5. Controle de acesso e segregação de funções nas aplicações (2.5)

### 5.1 Princípios fundamentais

- **Menor privilégio (*least privilege*):** conceder o **mínimo** necessário, pelo **menor tempo** necessário.
- **Negação por padrão (*deny by default*):** tudo proibido, salvo o explicitamente permitido (allowlist).
- **Need-to-know:** acessar só o que é indispensável à função.
- **Fail-safe defaults / fail closed:** na dúvida, negar.
- **Defesa em profundidade:** validar no gateway, na aplicação e no dado.
- **Privilégio mínimo também para serviços/infra** (service accounts, containers).

### 5.2 Segregação de funções (SoD)

- **Segregação de funções (*Segregation/Separation of Duties*):** nenhuma pessoa deve concentrar funções incompatíveis; ex.: quem **autoriza** um pagamento ≠ quem **executa**; quem **cadastra** fornecedor ≠ quem **aprova**.
- **Conflito de interesses (CoI)** e **princípio dos dois pares de olhos**.
- **SoD estática** (papéis mutuamente exclusivos — um usuário não pode ter os dois) vs **dinâmica** (pode ter os papéis, mas não exercer ao mesmo tempo).
- Instrumentos: matriz **RBAC** com papéis conflitantes, workflows com aprovação, *break-glass* controlado e auditado.
- Relaciona-se a **governança/controles internos** (COSO, Three Lines Model) e à **governança de identidades (IGA)**.

### 5.3 Onde o controle de acesso atua

- **Nível de endpoint/função:** quais rotas/ações o sujeito pode chamar (evita **BFLA**).
- **Nível de objeto:** o sujeito só acessa os objetos aos quais tem direito (evita **BOLA/IDOR**).
- **Nível de propriedade/campo:** quais campos pode ler/escrever (evita **BOPLA**/exposição excessiva e *mass assignment*).
- **Nível de dado/linha:** filtros por tenant/órgão/unidade.
- **Nível de operação:** leitura x escrita x exclusão (métodos HTTP).

### 5.4 RBAC x ABAC na prática

- **Papéis** agrupam **permissões**; evite checar "nome de usuário" ou ids fixos no código.
- **Autoridade vs papel:** `Papel` (role) é um conceito de negócio; **autoridade** (`GrantedAuthority`) é o que o framework verifica. Em Spring, `hasRole("ADMIN")` verifica a autoridade **`ROLE_ADMIN`** (prefixo `ROLE_`).
- **Papéis administrativos** merecem tratamento especial: nunca confiar no path (`/admin`) como única barreira.
- **Centralização:** uma camada clara de decisão de autorização reutilizada por todas as funções (evita checagens esquecidas).

### 5.5 Controle de acesso em APIs de microserviços

- Autenticar centralmente no **IdP** e **autorizar localmente** em cada serviço (decisão próxima, baixa latência).
- **Zero Trust:** não confiar implicitamente na rede; toda chamada serviço-a-serviço autenticada/autorizada (mTLS, tokens com audience específica).
- **Propagação de identidade** (*identity propagation*) e **delegação**: distinguir "em nome de" (usuário) de "em nome próprio" (serviço).
- Evitar que um serviço com escopo amplo vire "confused deputy".

## 6. Spring Security (2.6)

### 6.1 Arquitetura central

- **Filter chain:** um conjunto de filtros encadeados (`SecurityFilterChain`), gerenciado pelo `FilterChainProxy` via `DelegatingFilterProxy`. O **`AuthorizationFilter`** é, por padrão, o **último** filtro.
- **`SecurityContextHolder`:** guarda o `SecurityContext` (por padrão em `ThreadLocal`) com o objeto **`Authentication`**.
- **`Authentication`:** contém `principal` (o usuário), `credentials` (senha/token — geralmente apagados) e `authorities` (`GrantedAuthority`), além de `isAuthenticated()`.
- **Fluxo de autenticação:** `AuthenticationManager` → `ProviderManager` → um ou mais `AuthenticationProvider` (ex.: `DaoAuthenticationProvider`) → `UserDetailsService` + `PasswordEncoder`.
- **`GrantedAuthority`:** representa uma permissão (ex.: `ROLE_ADMIN`, `SCOPE_read`, `permission:write`).

### 6.2 Configuração (Servlet/Java Config)

- Declarar um **`@Bean SecurityFilterChain`** e definir regras com **`authorizeHttpRequests`** (substitui o antigo `authorizeRequests`); o `authorizeRequests`/`FilterSecurityInterceptor` é legado.
- Exemplo típico:

```java
http
    .authorizeHttpRequests(auth -> auth
        .requestMatchers("/public/**").permitAll()
        .requestMatchers("/admin/**").hasRole("ADMIN")
        .anyRequest().authenticated())
    .oauth2ResourceServer(o -> o.jwt(Customizer.withDefaults()));
```

- **Regras avaliadas em ordem; vale a primeira que casa** → do mais específico para o mais genérico e **`denyAll()`** no fim como *catch-all*.
- **`permitAll`** (libera) ≠ `denyAll` (nega sempre); `authenticated` exige autenticação; `hasAuthority`/`hasAnyAuthority`; `hasRole`/`hasAnyRole` (prefixo `ROLE_`); `hasAllAuthorities`.
- Preferir `permitAll` a **ignorar** rotas (garante headers de segurança e gestão de sessão).

### 6.3 Autenticação: componentes

- **`UserDetailsService`** carrega o usuário (in-memory, JDBC, LDAP, custom).
- **`PasswordEncoder`**: usar `DelegatingPasswordEncoder` com **BCrypt** (padrão comum) ou **Argon2**; nunca `NoOpPasswordEncoder`.
- **Autenticação HTTP:** form login, HTTP Basic, Digest (legado), X.509, **OAuth2/OIDC login**, SAML 2.0.
- **`PasswordEncoder`** + `UserDetailsService` + `DaoAuthenticationProvider`.
- **MFA** (`mfa(...)`), *passkeys*, *one-time token*, *remember-me*, *pre-auth*.

### 6.4 Autorização em métodos

- Habilitar com **`@EnableMethodSecurity`** (substitui o `@EnableGlobalMethodSecurity`).
- **`@PreAuthorize`** (antes de invocar), **`@PostAuthorize`** (após, examina `returnObject` — útil contra **IDOR**), **`@PreFilter`** e **`@PostFilter`** (filtram coleções por `filterObject`).
- **JSR-250**: `@RolesAllowed`, `@PermitAll`, `@DenyAll` (requer `jsr250Enabled = true`); **`@Secured`** (legado, `securedEnabled = true`).
- **Meta-anotações** (`@IsAdmin`) e **templates** de expressão reduzem duplicação.
- **`RoleHierarchy`** para hierarquia de papéis (ex.: `ROLE_ADMIN > permission:read`).
- **Ponto de atenção:** o *Spring Boot Starter Security* **não ativa** method security por padrão; **métodos não anotados ficam desprotegidos** se você depender só de anotações → por isso o *catch-all* no `HttpSecurity`.

### 6.5 OAuth2 / OIDC no Spring Security

- **Resource Server** (`spring-security-oauth2-resource-server` + `spring-security-oauth2-jose`): configura-se com **`oauth2ResourceServer().jwt()`** e a propriedade **`issuer-uri`** — que descobre o AS (`.well-known`) e o `jwks_uri`.
- **`JwtDecoder`** (`NimbusJwtDecoder`): valida assinatura e claims (por padrão confia em **RS256**); `JwtValidators` validam `iss`/`exp`/`nbf`; é possível fixar `jwk-set-uri`, chave pública/segredo, ou trocar o decoder.
- **`JwtAuthenticationConverter`** + **`JwtGrantedAuthoritiesConverter`**: convertem o JWT em autoridades; por padrão o claim **`scope`** vira autoridades com prefixo **`SCOPE_`**.
- **`hasScope("message:read")`** (`OAuth2AuthorizationManagers`) é o atalho para proteger por escopo.
- **OAuth2 Client / OIDC Login**: `oauth2Login()` para login federado; `OidcUser` expõe as claims.
- Suporte a **opaque token introspection**, **DPoP-bound access tokens**, multitenancy e *protected resource metadata*.

### 6.6 Proteções transversais

- **CSRF:** habilitado por padrão; essencial para apps com **sessão em cookie**; **desabilitar** em APIs stateless com Bearer token (`csrf.disable()` / `SessionCreationPolicy.STATELESS`).
- **CORS:** configurar origens explicitamente; não usar `*` com credenciais.
- **Headers de segurança:** HSTS, `X-Content-Type-Options: nosniff`, `X-Frame-Options`/CSP, `Cache-Control: no-store` para respostas sensíveis.
- **`HttpFirewall`** contra paths malformados; **session fixation**, concorrência de sessão, logout.
- **Avaliação de configuração** (ponto do edital: "avaliação de mecanismos"): verificar se há **rotas sem regra**, **`permitAll` amplo**, **method security desativada**, **CSRF desabilitado indevidamente**, **algorithm `none` aceito**, **validação de `iss`/`aud` ausente** e **`hasRole`/`hasAuthority` trocados**.

## 7. Proteção de endpoints e métodos (2.7)

### 7.1 Dois níveis complementares

- **Request-level (HTTP):** regras por URI/método no `HttpSecurity` → **granularidade grossa**, configuração centralizada.
- **Method-level:** anotações no serviço → **granularidade fina**, lógica próxima ao domínio (usa `Authentication` e parâmetros/retorno).
- Use ambos: **catch-all** no nível de request + regras finas por método.

### 7.2 Como casar requisições

- **Ant** (padrão): `/resource/**`, variáveis de path `{name}`; **Regex** (`RegexRequestMatcher`) para critérios estritos; **método HTTP** (`requestMatchers(HttpMethod.GET)`); **dispatcher type**; **matchers customizados**.
- Spring Security casa por **path** (não por query string).
- Cuidado com padronização de barra e **verb tampering** (usar o mesmo método indevidamente para burlar regras).

### 7.3 Autorização por método

- `@PreAuthorize("hasAuthority('permission:read')")`, `@PostAuthorize("returnObject.owner == authentication.name")`, `@PreFilter`, `@PostFilter`.
- **`@PostAuthorize` não é recomendado para escritas** (a alteração pode ocorrer antes da checagem) — ler primeiro, checar, depois escrever.
- Expressões podem acessar `principal`, `authentication`, `returnObject`, `filterObject` e variáveis de path.
- Prefira **conceder autoridades** em vez de SpEL complexo.

### 7.4 Proteções adicionais de endpoint

- **Restringir métodos HTTP** (allowlist) → `405` para métodos inesperados.
- **Validação de entrada** (tipo, tamanho, formato), **limite de payload** (`413`).
- **Validação de `Content-Type`** → `415`; negociação de resposta → `406`.
- **Rate limiting/anti-automação** → `429` (+ `Retry-After`); proteger fluxos sensíveis (login, recuperação de senha) contra força bruta.
- **Mass assignment:** usar DTOs/*allowlist* de campos, nunca *binding* direto de todo o corpo para a entidade.
- **Exposição excessiva de dados:** a resposta deve conter só o necessário (serialização consciente).
- **Endpoints de gestão** fora da internet, com autenticação forte e rede segregada.
- **CORS, CSRF, headers, HSTS**, e não vazar credenciais em URL/logs.

## 8. Identificação e correção de permissões excessivas e falhas de controle de acesso (2.8)

### 8.1 OWASP API Security Top 10 (2023) — mapa do item

| ID | Risco | Relação com o item |
| --- | --- | --- |
| **API1** | **BOLA** (*Broken Object Level Authorization*) | Checar dono/acesso ao **objeto** em toda função que usa ID do cliente |
| **API2** | **Broken Authentication** | Fluxos de autenticação fracos, tokens não validados |
| **API3** | **BOPLA** (*Broken Object Property Level Authorization*) | Exposição excessiva de dados + *mass assignment* |
| **API5** | **BFLA** (*Broken Function Level Authorization*) | Usuário comum acessa função administrativa |
| **API6** | Acesso irrestrito a fluxos de negócio sensíveis | Automação abusiva de fluxos |
| **API8** | Security Misconfiguration | Configurações inseguras de authz |
| **API9** | Improper Inventory Management | Versões antigas/endpoints esquecidos sem controle |

### 8.2 BOLA (API1) — falha nº 1 em APIs

- Ocorre quando o endpoint recebe um **ID de objeto** e **não valida** se o solicitante pode acessá-lo. `GET /pedidos/123` retorna o pedido de outro usuário.
- **Não basta** comparar o `sub` do token com o ID do objeto — é a solução para apenas um subconjunto de casos.
- **IDOR** (*Insecure Direct Object Reference*) é a manifestação clássica no lado web/app.
- Prevenção: **checagem de autorização em nível de objeto** em **toda** função que acessa dado por ID do cliente; IDs **não previsíveis** (GUID/UUID); testes automatizados de autorização.

### 8.3 BFLA (API5)

- Usuário autenticado (ou anônimo) consegue chamar **função** que não deveria (ex.: `POST /api/invites/new`, `GET /api/admin/v1/users/all`).
- Ocorre por hierarquias/roles complexos, separação pouco clara entre funções admin e comuns e confiança no path.
- Prevenção: **negar por padrão**, exibir *grants* explícitos por função, **herança de controllers administrativos** com checagem, revisão dos endpoints contra o modelo de negócio.

### 8.4 BOPLA (API3), exposição excessiva e mass assignment

- **Exposição excessiva:** resposta devolve mais campos que o cliente precisa (ex.: dados sensíveis/internos).
- **Mass assignment:** o cliente injeta campos que não deveria alterar (ex.: `"role":"admin"`, `"saldo"`), porque a aplicação faz *bind* do corpo direto para o modelo.
- Prevenção: **DTOs** com campos permitidos, serialização explícita, checagem de propriedade, validação de entrada.

### 8.5 Como identificar (diagnóstico/auditoria)

- **Mapear** todos os endpoints, versões, hosts e quem acessa (inventário — API9).
- **Testes manuais e automatizados** de autorização: trocar IDs, trocar métodos HTTP, acessar endpoints admin como usuário comum, tentar **verb tampering**.
- **Revisão de código/config** de autenticação e autorização; procurar rotas sem regra, `permitAll` amplo e method security desligada.
- **Testar tokens**: `alg:none`, token expirado, `aud` errado, token de outro emissor, ID token usado como access token.
- **Revisão de papéis e acessos** (revisão de permissões, *access review*).
- Ferramentas: scanners DAST (ZAP), testes de contrato, linters de OpenAPI, **testes de regressão de autorização**.

### 8.6 Como corrigir (remédio)

- **Negar por padrão** e conceder explicitamente; centralizar a lógica de autorização.
- **Checagem em nível de objeto** em toda função que acessa dado; não confiar só no front-end.
- **Menor privilégio**: revisar papéis, remover permissões não usadas, aplicar **segregação de funções**.
- **DTOs/allowlist** contra mass assignment e exposição excessiva.
- **Validação robusta de tokens** (assinatura, algoritmos, `iss`, `aud`, `exp`, `typ`).
- **Rotação/expiração** de credenciais e tokens; remover contas/segredos órfãos.
- **Registrar e monitorar** decisões de acesso (logs de segurança e alertas); testes de autorização no **pipeline** (CI) para impedir regressão.
- **Governança (IGA):** recertificação periódica de acessos, SoD, processos de joiner-mover-leaver.

## Detalhes que merecem destaque

- **OAuth 2.0 ≠ autenticação.** OAuth é **autorização delegada**. Autenticação federada é o **OpenID Connect** (camada de identidade sobre OAuth), via **ID Token**.
- **Access token** (API), **refresh token** (renova junto ao AS, **nunca** vai ao RS) e **ID token** (prova de autenticação no OIDC) têm finalidades distintas.
- **JWS garante integridade/autenticidade, não sigilo.** Claims do JWT são **legíveis**; para confidencialidade, use **JWE** (nested JWT).
- **Sentido de `.well-known/openid-configuration`** (OIDC Discovery) e **AS Metadata (RFC 8414)**; de lá vem o `jwks_uri`.
- **PKCE** (RFC 7636): `code_verifier` (43–128 chars, alta entropia) → `code_challenge` via **S256** (SHA-256 + base64url); `plain` **não** deve ser usado. Protege o **authorization code** contra interceptação.
- **RFC 9700 (BCP de segurança OAuth, 2025):** **proíbe ROPC**, **desencoraja implicit**, exige **PKCE**, **exact match** de `redirect_uri`, **sender-constrained**/rotação de refresh tokens, `state`/`nonce`, proteção contra **mix-up**.
- **RFC 9068:** access token JWT deve ter `typ=at+jwt`, ser **assinado** (nunca `none`), e conter `iss`, `exp`, `aud`, `sub`, `client_id`, `iat`, `jti` (obrigatórios).
- **Validação de JWT é uma lista de verificação**: assinatura + algoritmo permitido + `iss` + `aud` + `exp`/`nbf` + `typ`, **sem** confiar em chaves vindas do header (`jku`/`jwk`/`x5u`/`x5c`).
- **`sub` do ID Token** pode ser **público** ou **pairwise (PPID)**; `azp` identifica a parte autorizada.
- **401 × 403:** 401 = não autenticado / credencial inválida (com `WWW-Authenticate`); 403 = autenticado, porém **sem permissão**.
- **Idempotência:** GET, HEAD, PUT, DELETE são idempotentes; **POST e PATCH não são** (na prática, PATCH pode ou não). Idempotência resolve retentativas/duplicidade.
- **MFA exige fatores de categorias diferentes**; senha + PIN não é MFA.
- **BOLA (nível de objeto) × BFLA (nível de função):** BOLA manipula **ID de objeto**; BFLA acessa **função/endpoint** indevido.
- **Spring Security:** `hasRole("X")` procura `ROLE_X`; `hasAuthority("ROLE_X")` é o valor literal. A **primeira regra que casa vence**. **Method security não vem ativada** pelo starter.
- **Spring Resource Server** valida `iss`/`exp`/`nbf` e assinatura; por padrão converte `scope` em autoridades **`SCOPE_*`**. `issuer-uri` habilita **discovery** e rotação automática de chaves.
- **CSRF:** necessário com **sessão em cookie**; dispensável em API stateless com Bearer token.
- **SemVer + `Deprecation`/`Sunset` (RFC 9745):** comunique descontinuação; só versione em *breaking changes*.
- **Contract-first + OpenAPI + contract tests** reduzem quebra de integração (Item 3.4 do edital).

## Comparações que a banca costuma cobrar (certo/errado)

| Conceito A | Conceito B | Diferença-chave |
| --- | --- | --- |
| Autenticação (AuthN) | Autorização (AuthZ) | AuthN = **quem é**; AuthZ = **o que pode fazer** |
| 401 Unauthorized | 403 Forbidden | 401 = não autenticado/credencial inválida; 403 = autenticado sem permissão |
| OAuth 2.0 | OpenID Connect | OAuth = **autorização** (access token); OIDC = **autenticação** sobre OAuth (ID token) |
| Access token | ID token | Access = acessa API (RS); ID = prova a autenticação do usuário (RP) |
| Access token | Refresh token | Access vai ao RS; refresh só ao AS para renovar |
| JWT (JWS) | JWE | JWS = assinado, **legível**; JWE = **cifrado**, sigiloso |
| Token opaco | JWT | Opaco exige introspecção no AS; JWT é validado localmente (autocontido) |
| Algoritmo simétrico (HS256) | Algoritmo assimétrico (RS256/ES256) | HS = mesma chave; RS/ES = privada assina, pública verifica (recomendado) |
| Public client | Confidential client | Public não guarda segredo (SPA/mobile); confidential guarda (servidor) |
| Authorization Code | Client Credentials | Code envolve usuário; Client Credentials é M2M (sem usuário) |
| RBAC | ABAC | RBAC = papéis; ABAC = atributos/políticas (mais granular) |
| BOLA (API1) | BFLA (API5) | BOLA = acesso a **objeto** de outro; BFLA = acesso a **função** indevida |
| IDOR | BOLA | IDOR é a manifestação clássica web; BOLA é o conceito em API (objeto) |
| Exposição excessiva de dados | Mass assignment | Exposição = **ler** demais; mass assignment = **gravar** campos indevidos |
| `hasRole("ADMIN")` | `hasAuthority("ADMIN")` | Role adiciona o prefixo **`ROLE_`**; authority é literal |
| `@PreAuthorize` | `@PostAuthorize` | Pre = antes de invocar; Post = após, examina o retorno (contra IDOR) |
| Proteção em request-level | Proteção em method-level | Request = grossa/central; method = fina/próxima ao domínio |
| `state` | `nonce` | state = anti-CSRF (OAuth); nonce = anti-replay/vincula sessão (OIDC) |
| Seguro (safe) | Idempotente | Safe = não altera estado; idempotente = repetição tem mesmo efeito |
| PUT | PATCH | PUT substitui o recurso inteiro; PATCH altera parcialmente |
| Versionamento na URI | Versionamento por media type/header | URI = visível/simples; header/media type = URI limpa, mais "REST" |
| API key | Autenticação de usuário | API key identifica a **aplicação**; não é login de usuário |
| `permitAll` | `denyAll` | permitAll libera; denyAll nega sempre (negação por padrão) |

## Pegadinhas e erros comuns

> Desconfie de termos absolutos ("sempre", "nunca", "exclusivamente") e da troca de papéis/tokens entre protocolos.

- Dizer que **"OAuth 2.0 autentica o usuário"** — OAuth é **autorização**; quem autentica é o **OIDC** (camada de identidade).
- Usar **access token como prova de autenticação** ou **ID token para chamar a API** — **cross-JWT confusion**.
- Afirmar que **JWT é criptografado** — JWS é apenas **assinado**; payload é base64url legível. Confidencialidade exige **JWE**.
- Achar que **JWT é sempre melhor que token opaco** — JWT facilita revogação? **Não**; ao contrário, dificulta (precisa de denylist/curta duração).
- Trocar **401 e 403** (401 = não autenticado; 403 = sem permissão).
- Confundir **autenticação** com **autorização** (inclusive ao afirmar "autenticado, logo autorizado").
- Supor que **POST é idempotente** (não é); ou que **PATCH é sempre idempotente**.
- Achar que **PUT e PATCH são equivalentes** (total × parcial).
- Dizer que **`alcance: none` é aceitável em produção** — jamais; também é risco a **confusão de algoritmo** (RS256 → HS256).
- **Confiar em `jku`/`jwk`/`x5u`/`x5c`** do header do token como fonte da chave de verificação (header é entrada não autenticada).
- Omitir a validação de **`iss`, `aud`, `exp`** — RFC 9068 exige.
- Achar que **API key autentica usuário** — ela identifica a **aplicação**; e **não** deve ir na URL.
- Confundir **RBAC com ABAC** e achar que "papel" e "permissão" são sinônimos.
- Confundir **BOLA (objeto)** com **BFLA (função)**; e **exposição excessiva (ler)** com **mass assignment (gravar)**.
- Achar que **segregação de funções (SoD)** é o mesmo que "separação de ambientes" (dev/prod) — é separação de **funções incompatíveis** por pessoa/papel.
- Em Spring: esquecer que **`hasRole("X")` verifica `ROLE_X`**; ou que a **primeira regra de `authorizeHttpRequests` que casa vence**; ou que **method security não vem ativada** pelo starter (métodos não anotados ficam abertos sem *catch-all*).
- Achar que **Spring Security desabilita CSRF por padrão** — ele **habilita**; em API stateless é preciso decidir conscientemente.
- Dizer que **PKCE se aplica só a apps mobile** — a recomendação atual é para **todos** os clientes; **`plain` não deve ser usado**.
- Confundir **refresh token** (usado com o AS) com **access token** (usado no RS); refresh **nunca** vai ao resource server.
- Achar que **implicit** ou **ROPC** são fluxos recomendados — a RFC 9700 os **proíbe/desencoraja**.
- Confundir **`state`** (anti-CSRF) com **`nonce`** (anti-replay/vincula sessão no OIDC).
- Achar que **MFA** é qualquer combinação de dois fatores (senha + PIN não é MFA).
- Dizer que **`/admin` no path** protege a função administrativa — a proteção tem de ser por **autorização**, não por convenção de URL.
- Achar que **versão na URI é obrigatória/sempre a melhor** — há trade-offs; header/media type são alternativas válidas.

## Notas atômicas relacionadas

```dataview
LIST FROM "20 - Notas"
WHERE disciplina = this.disciplina
  AND contains(tema, this.tema)
SORT file.name ASC
```

## Fontes

- https://owasp.org/API-Security/editions/2023/en/0x11-t10/ — OWASP API Security Top 10 (2023), lista e descrições dos riscos.
- https://owasp.org/API-Security/editions/2023/en/0xa1-broken-object-level-authorization/ — API1 BOLA.
- https://owasp.org/API-Security/editions/2023/en/0xa2-broken-authentication/ — API2 Broken Authentication.
- https://owasp.org/API-Security/editions/2023/en/0xa5-broken-function-level-authorization/ — API5 BFLA.
- https://cheatsheetseries.owasp.org/cheatsheets/REST_Security_Cheat_Sheet.html — OWASP REST Security Cheat Sheet (HTTPS, access control, JWT, métodos, status, CORS).
- https://cheatsheetseries.owasp.org/cheatsheets/JSON_Web_Token_Cheat_Sheet.html — OWASP JWT Cheat Sheet (estrutura, algoritmos, ataques, revogação, JWE).
- https://datatracker.ietf.org/doc/html/rfc7231 — RFC 7231, HTTP/1.1: Semantics and Content (métodos, safe/idempotente, status).
- https://datatracker.ietf.org/doc/html/rfc6749 — RFC 6749, The OAuth 2.0 Authorization Framework (papéis, grants, tokens).
- https://datatracker.ietf.org/doc/html/rfc6750 — RFC 6750, Bearer Token Usage (header Authorization, WWW-Authenticate, erros).
- https://datatracker.ietf.org/doc/html/rfc7519 — RFC 7519, JSON Web Token (claims, JOSE header, validação).
- https://datatracker.ietf.org/doc/html/rfc9068 — RFC 9068, JWT Profile for OAuth 2.0 Access Tokens (`typ=at+jwt`, `iss/aud/exp`, validação).
- https://datatracker.ietf.org/doc/html/rfc9700 — RFC 9700, Best Current Practice for OAuth 2.0 Security (PKCE, redirect URI, sender-constrained, ROPC proibido).
- https://datatracker.ietf.org/doc/html/rfc7636 — RFC 7636, PKCE (`code_verifier`/`code_challenge`, S256).
- https://openid.net/specs/openid-connect-core-1_0.html — OpenID Connect Core 1.0 (ID Token, claims, fluxos, UserInfo).
- https://datatracker.ietf.org/doc/html/rfc8725 — RFC 8725, JWT Best Current Practices (typing, substituição, confusão).
- https://datatracker.ietf.org/doc/html/rfc8705 — RFC 8705, Mutual-TLS Client Authentication and Certificate-Bound Access Tokens.
- https://datatracker.ietf.org/doc/html/rfc9449 — RFC 9449, OAuth 2.0 DPoP (Demonstrating Proof of Possession).
- https://datatracker.ietf.org/doc/html/rfc8414 — RFC 8414, OAuth 2.0 Authorization Server Metadata.
- https://datatracker.ietf.org/doc/html/rfc7662 — RFC 7662, OAuth 2.0 Token Introspection.
- https://datatracker.ietf.org/doc/html/rfc7009 — RFC 7009, OAuth 2.0 Token Revocation.
- https://datatracker.ietf.org/doc/html/rfc9457 — RFC 9457, Problem Details for HTTP APIs.
- https://datatracker.ietf.org/doc/html/rfc8594 — RFC 8594, The Sunset HTTP Header Field (depreciação de APIs).
- https://docs.spring.io/spring-security/reference/servlet/authorization/authorize-http-requests.html — Spring Security: Authorize HttpServletRequests.
- https://docs.spring.io/spring-security/reference/servlet/authorization/method-security.html — Spring Security: Method Security.
- https://docs.spring.io/spring-security/reference/servlet/oauth2/resource-server/jwt.html — Spring Security: OAuth 2.0 Resource Server JWT.
- https://docs.spring.io/spring-security/reference/servlet/architecture.html — Spring Security: arquitetura (filtros, SecurityContext).
- https://docs.spring.io/spring-security/reference/features/authentication/password-storage.html — Spring Security: armazenamento de senhas (PasswordEncoder).
