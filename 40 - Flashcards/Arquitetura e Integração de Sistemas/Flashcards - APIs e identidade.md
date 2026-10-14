---
tipo: flashcard
disciplina: "Arquitetura e Integração de Sistemas"
tema: "APIs e identidade"
data: "2026-10-14"
tags:
  - flashcard
---

# Flashcards: APIs e identidade

> Deck baseado no resumo [[APIs e identidade - Arquitetura e Integração de Sistemas]].
> Formato: cards de linha única do plugin Spaced Repetition (pergunta e resposta no mesmo parágrafo).

## REST: origem e restrições

O que é REST? :: Um estilo arquitetural (não norma nem protocolo) descrito por Roy Fielding em 2000; sigla de Representational State Transfer.

Quais restrições definem um sistema REST? :: Cliente–servidor, sem estado, cacheável, interface uniforme, sistema em camadas e código sob demanda (opcional).

O que significa ser "sem estado" (stateless) no REST? :: Cada requisição contém toda a informação necessária; o servidor não guarda estado de sessão — o "estado" do acrônimo é o estado do recurso.

Quais são os níveis do Modelo de Maturidade de Richardson e o que é HATEOAS? :: 0 = POX/RPC; 1 = recursos; 2 = verbos HTTP + status; 3 = hypermedia (HATEOAS). HATEOAS fornece links que guiam as transições de estado, e a maioria das APIs do mercado está no nível 2.

O que é uma representação em REST? :: A captura do estado atual ou desejado do recurso (ex.: JSON), transferida via HTTP.

## Recursos, URIs e métodos HTTP

O que a URI deve identificar e quais as boas práticas de path? :: Um substantivo (recurso), não uma ação; plural para coleções, hierarquia para sub-recursos e kebab-case minúsculo, evitando verbos, snake_case e camelCase.

Quais métodos HTTP são seguros e o que isso significa? :: GET, HEAD e OPTIONS; seguro (safe) = não altera o estado do recurso (somente leitura).

Quais métodos HTTP são idempotentes e o que isso significa? :: GET, HEAD, OPTIONS, PUT e DELETE; idempotente = repetir a operação N vezes produz o mesmo efeito que uma vez.

Qual a diferença entre PUT, PATCH e POST e como mitigar duplicidade? :: PUT substitui o recurso inteiro, PATCH modifica parcialmente e POST cria ou processa; POST não é idempotente, e a mitigação é o cabeçalho Idempotency-Key com resposta cacheada.

## Status codes e representações

A que correspondem os status 200, 201, 202 e 204? :: 200 OK; 201 Created (traz Location); 202 Accepted (processamento assíncrono); 204 No Content.

Qual a diferença entre 401 e 403? :: 401 é falta de autenticação ou credencial inválida (com WWW-Authenticate); 403 é autenticado porém sem permissão.

A que correspondem 406, 415, 422, 409 e 429? :: 406 Not Acceptable; 415 Unsupported Media Type; 422 Unprocessable Entity (validação semântica); 409 Conflict; 429 Too Many Requests (com Retry-After).

O que é a RFC 9457 e o que ela sucede? :: Problem Details for HTTP APIs, com Content-Type application/problem+json e campos type, title, status, detail e instance; sucede a RFC 7807, e não se deve vazar stack traces.

Como funciona a negociação de conteúdo e com que erros se relaciona? :: Via Accept (cliente) e Content-Type (corpo), com JSON como formato predominante; nenhum formato aceitável gera 406 e mídia não suportada gera 415. Não copie o Accept direto para o Content-Type da resposta (risco de MIME sniffing).

## Contratos e versionamento de APIs

O que é o contrato de uma API e o que é a OpenAPI Specification? :: O contrato descreve endpoints, parâmetros, schemas, respostas e erros; a OpenAPI (antes Swagger) é o padrão de facto para APIs REST, com Swagger UI, Redoc e geradores de código, usando JSON Schema para validação.

Para que servem AsyncAPI e Pact, e o que é design-first? :: AsyncAPI descreve APIs assíncronas/eventos; Pact é contract testing (consumer-driven), em que o consumidor define expectativas e o provedor as verifica em build; design-first começa pelo contrato e code-first gera o contrato a partir do código.

Quais são as formas de versionar uma API e o trade-off da versão na URI? :: URI, query param, cabeçalho customizado (X-API-Version) e media type (content negotiation). A URI é simples e visível, mas mistura a versão com o recurso e "polui" a URI.

Quando versionar uma API e que mudanças são compatíveis? :: Só em mudanças incompatíveis; compatível = adicionar campo opcional, novo endpoint ou novo valor de enum tratável; breaking = remover/renomear campo, mudar tipo, tornar campo obrigatório ou alterar semântica/status code.

Quais cabeçalhos comunicam depreciação de uma API? :: Deprecation e Sunset (RFC 8594 e RFC 9745).

## Boas práticas de design

Quais recursos de consulta e proteção uma API REST deve oferecer? :: Paginação (page/size ou cursor), filtros, ordenação, sparse fieldsets, limites de payload (413), rate limiting (429 + Retry-After), timestamps em ISO 8601/UTC e restrição de métodos por allowlist (405).

## Autenticação e autorização

Qual a diferença entre autenticação e autorização, e o que são identidade e credencial? :: AuthN verifica quem é o sujeito; AuthZ decide o que ele pode fazer; identidade é o conjunto de atributos de uma entidade e credencial é a evidência apresentada para prová-la.

Quais são as categorias de fatores de autenticação e o que é MFA? :: Algo que você sabe, tem, é e, em modelos modernos, o local/contexto; MFA exige dois ou mais fatores de categorias diferentes (senha mais PIN não é MFA).

Como senhas devem ser armazenadas e protegidas contra credential stuffing? :: Nunca em texto claro; usar hash com salt e algoritmos lentos (bcrypt, scrypt, Argon2, PBKDF2); contra credential stuffing, rate limiting, lockout, CAPTCHA e verificação de senhas vazadas.

Sessão no servidor × token stateless (JWT), e o que um cookie deve ter? :: A sessão guarda estado no servidor, é fácil de invalidar e exige proteção CSRF; o JWT é escalável, mas dificulta a revogação. O cookie de sessão deve usar HttpOnly, Secure, SameSite e prefixos __Host- ou __Secure-.

O que é autenticação federada, SSO/SLO, SCIM e JIT provisioning? :: Federada delega a um IdP externo (OIDC, SAML 2.0, WS-Federation), com a RP confiando na asserção; SSO autentica uma vez e acessa vários serviços, SLO encerra todas as sessões; SCIM (RFC 7643/7644) padroniza usuários/grupos e JIT provisioning cria o usuário no primeiro login. A federação cria dependência do IdP como ponto único de falha.

## Modelos de autorização e autenticação de clientes

O que são DAC, MAC e RBAC? :: DAC = o dono do recurso concede o acesso; MAC = rótulos de segurança e níveis de classificação com decisão central (ambientes militares/governamentais); RBAC = permissões atribuídas a papéis, com o problema da explosão de papéis.

O que são ABAC e ReBAC, e quais policy engines existem? :: ABAC decide por atributos de sujeito, recurso, ação e ambiente via políticas (mais granular); ReBAC decide por relações (ex.: "usuário é dono do recurso"), como Zanzibar e OpenFGA; policy engines: OPA/Rego e XACML.

O que é uma API key e quais formas autenticam clientes machine-to-machine? :: API key identifica a aplicação (não o usuário), é fácil de vazar, não tem granularidade e não deve ir na URL; M2M também usa mTLS, OAuth 2.0 client credentials, HMAC/signature-based (AWS SigV4) e private_key_jwt.

## OAuth 2.0

O que é OAuth 2.0, quais suas RFCs e quais são seus quatro papéis? :: Um framework de autorização delegada (RFC 6749; bearer tokens na RFC 6750) que dá acesso limitado em nome do dono do recurso sem compartilhar a senha; papéis: Resource Owner, Client, Authorization Server (AS) e Resource Server (RS).

Onde cada token trafega: access, refresh e ID? :: O access token vai ao resource server; o refresh token é usado só com o AS (nunca vai ao RS); o ID token (OIDC) vai à RP. Nenhum token deve ir na URL.

Qual grant type é o principal e o que é PKCE? :: Authorization Code, em que o cliente troca um código por tokens no token endpoint, sem os tokens passarem pelo user-agent; PKCE (RFC 7636) envia o code_challenge (S256) e apresenta o code_verifier (43–128 chars), sendo obrigatório para public clients e recomendado para todos.

Por que Implicit, ROPC e plain não devem ser usados, e o que é Client Credentials? :: O Implicit expõe o token em URL/fragmento/histórico; o ROPC expõe credenciais ao cliente e é incompatível com MFA (proibido pela RFC 9700); plain no PKCE não deve ser usado. Client Credentials é o cliente agindo em nome próprio, sem usuário (M2M).

Quais grants atendem dispositivos, troca de tokens e server-to-server? :: Device Authorization Grant (RFC 8628), Token Exchange (RFC 8693) e JWT Bearer (RFC 7523).

Para que servem escopos, state, nonce e redirect_uri? :: Escopo limita o acesso (string separada por espaços, ex.: openid profile email); state é anti-CSRF vinculado à sessão; nonce, no OIDC, é anti-replay e vincula a requisição ao ID Token; redirect_uri exige comparação exata (exact match) com o pré-registrado.

Quais exigências de segurança a RFC 9700 (BCP do OAuth, 2025) traz? :: Proíbe ROPC, desencoraja implicit, exige PKCE e exact match de redirect_uri, sender-constrained/rotação de refresh tokens, state/nonce e proteção contra mix-up.

O que são tokens sender-constrained e o que é o mix-up attack? :: São tokens amarrados à posse de uma chave, via mTLS (RFC 8705) ou DPoP (RFC 9449); o mix-up confunde o cliente sobre qual AS emitiu a resposta, e mitiga-se com o iss (RFC 9207) e URIs distintas.

Para que serve o Authorization Server Metadata (RFC 8414)? :: Para o discovery dos endpoints e chaves do AS; o CORS não deve ser usado no authorization endpoint, apenas nos endpoints acessados diretamente pela SPA (token, jwks).

## OpenID Connect

O que é OpenID Connect (OIDC), como é acionado e quais seus fluxos? :: Uma camada de identidade sobre o OAuth 2.0 que permite à RP verificar a identidade do usuário com base na autenticação do OP, acionada pelo escopo openid; fluxos: Authorization Code (code, recomendado), Implicit (id_token, obsoleto) e Hybrid (code id_token).

O que são o UserInfo Endpoint, o Discovery e os escopos padrão do OIDC? :: O UserInfo é recurso protegido que, com o access token, devolve claims do usuário; o Discovery é o .well-known/openid-configuration, que publica endpoints e o jwks_uri; escopos: openid (obrigatório), profile, email, address, phone e offline_access.

O que é o ID Token e quais suas claims? :: Um JWT emitido pelo OP com claims sobre o evento de autenticação; obrigatórias: iss, sub, aud (com o client_id da RP), exp e iat; opcionais/contextuais: auth_time, nonce, acr, amr e azp.

Como o ID Token deve ser protegido e validado? :: Deve ser assinado (JWS) e pode ser assinado e cifrado (JWE, nested JWT); valida-se assinatura, iss, aud (= client_id), exp e nonce quando aplicável.

O que é o sub pairwise (PPID) e qual a diferença entre OAuth 2.0 e OIDC? :: PPID é um identificador pseudônimo por RP que evita correlação do usuário entre serviços; OAuth 2.0 é autorização delegada e emite access token, enquanto OIDC é autenticação federada sobre OAuth e emite ID token (mais access token).

Por que não usar o access token como prova de autenticação nem o ID token para acessar APIs? :: Porque são tokens com finalidades distintas; a confusão gera cross-JWT confusion.

## Tokens: estrutura, validação e proteção

Token opaco × JWT? :: O opaco exige introspecção no AS (RFC 7662) e permite revogação imediata; o JWT é autocontido e validado localmente pela chave pública, mas dificulta a revogação e pode expor dados.

Qual o formato de um JWT e o que contém seu header? :: base64url(header).base64url(payload).base64url(signature); o JOSE Header traz alg, typ, kid e, opcionalmente, jku/jwk/x5c/x5u e cty (nested JWT); as claims registradas são iss, sub, aud, exp, nbf, iat e jti.

O que o JWS garante e quais algoritmos existem? :: O JWS garante integridade e autenticidade, mas não confidencialidade (payload base64url legível; sigilo exige JWE); HS256/384/512 são simétricos (mesma chave) e RS256, PS256, ES256 e EdDSA são assimétricos (chave privada assina, pública verifica — recomendados). Nunca usar none.

O que a RFC 9068 exige do access token JWT? :: typ igual a at+jwt, assinatura (nunca none) e as claims iss, exp, aud, sub, client_id, iat e jti obrigatórias.

Qual o checklist de validação de um JWT? :: Verificar typ, validar a assinatura pelo JWKS, conferir iss exatamente, aud (deve conter o RS), exp/nbf com tolerância de clock skew, escolher a chave pelo kid, usar allowlist de algoritmos e respeitar escopos.

Quais ataques e antipadrões ameaçam tokens? :: alg none (forja completa); confusão de algoritmo (RS256 trocado por HS256 usando a chave pública como segredo HMAC); confiar em jku/jwk/x5u/x5c do header (entrada não autenticada); confusão de emissor/audiência; cross-JWT confusion; replay; vazamento em URL/logs/localStorage e segredo HMAC fraco (mínimo igual ao output, 256 bits no HS256).

Como proteger e revogar tokens? :: TLS ponta a ponta; access tokens de vida curta (até 1 hora, idealmente minutos) e refresh tokens com rotação e reuse detection; armazenar em cofre de segredos ou cookie HttpOnly + Secure + SameSite (evitar localStorage); enviar como Authorization: Bearer, não logar, e revogar por introspecção, denylist por jti/iss ou Token Status List.

## Controle de acesso e segregação de funções

O que é menor privilégio e negação por padrão? :: Menor privilégio = conceder o mínimo necessário pelo menor tempo necessário; negação por padrão = tudo proibido, salvo o explicitamente permitido (allowlist). Aplica-se também a service accounts, containers e exige defesa em profundidade.

O que é segregação de funções (SoD)? :: Nenhuma pessoa deve concentrar funções incompatíveis — quem autoriza não é quem executa, quem cadastra não é quem aprova; a SoD estática usa papéis mutuamente exclusivos e a dinâmica permite ter os papéis, mas não exercê-los ao mesmo tempo.

Em que níveis o controle de acesso atua? :: Endpoint/função (evita BFLA), objeto (evita BOLA/IDOR), propriedade/campo (evita BOPLA e mass assignment), dado/linha (tenant/órgão) e operação (leitura, escrita, exclusão).

Qual a diferença entre papel e autoridade no Spring Security? :: Papel é conceito de negócio; autoridade (GrantedAuthority) é o que o framework verifica — hasRole("ADMIN") checa a autoridade ROLE_ADMIN.

Como funciona o controle de acesso em microserviços? :: Autenticar centralmente no IdP e autorizar localmente em cada serviço, sob o modelo Zero Trust, com mTLS e tokens de audiência específica, distinguindo "em nome de" (usuário) de "em nome próprio" (serviço) e evitando o confused deputy.

## Spring Security

Qual a arquitetura de filtros e de contexto do Spring Security? :: Uma filter chain (SecurityFilterChain) gerenciada pelo FilterChainProxy via DelegatingFilterProxy, com o AuthorizationFilter como último filtro por padrão; o SecurityContextHolder guarda o SecurityContext (por padrão em ThreadLocal) com o objeto Authentication.

O que o Authentication contém e qual o fluxo de autenticação? :: principal (o usuário), credentials (senha/token, geralmente apagados), authorities (GrantedAuthority) e isAuthenticated(); o fluxo vai de AuthenticationManager para ProviderManager e deste para AuthenticationProvider (ex.: DaoAuthenticationProvider) usando UserDetailsService e PasswordEncoder (BCrypt/Argon2, nunca NoOpPasswordEncoder).

Qual método substitui o antigo authorizeRequests e como as regras são avaliadas? :: authorizeHttpRequests; as regras são avaliadas em ordem e vale a primeira que casa — do mais específico ao mais genérico, com denyAll() como catch-all; permitAll libera e denyAll nega sempre.

Qual a diferença entre hasRole e hasAuthority no Spring? :: hasRole("X") verifica a autoridade ROLE_X (adiciona o prefixo); hasAuthority("X") verifica o valor literal.

Como habilitar e usar a segurança em métodos no Spring? :: Com EnableMethodSecurity; PreAuthorize checa antes de invocar e PostAuthorize depois, examinando returnObject (útil contra IDOR), além de PreFilter/PostFilter para coleções; há JSR-250 (RolesAllowed, PermitAll, DenyAll), Secured e RoleHierarchy. Atenção: o starter não ativa method security por padrão, então métodos não anotados ficam desprotegidos sem um catch-all no HttpSecurity.

Como configurar o OAuth2 Resource Server no Spring Security? :: Com oauth2ResourceServer().jwt() e a propriedade issuer-uri, que descobre o AS pelo .well-known e obtém o jwks_uri; o JwtDecoder (NimbusJwtDecoder) valida assinatura e claims (RS256 por padrão) e JwtValidators validam iss, exp e nbf.

Como o scope vira autoridade e como proteger por escopo no Spring? :: O JwtGrantedAuthoritiesConverter converte o claim scope em autoridades com o prefixo SCOPE_; hasScope é o atalho de OAuth2AuthorizationManagers para proteger por escopo.

Quando habilitar ou desabilitar CSRF e como configurar CORS? :: O CSRF vem habilitado por padrão, é essencial com sessão em cookie e dispensável em API stateless com Bearer token (SessionCreationPolicy.STATELESS); o CORS deve declarar origens explícitas, sem curinga com credenciais.

O que verificar ao avaliar uma configuração do Spring Security? :: Rotas sem regra, permitAll amplo, method security desativada, CSRF desabilitado indevidamente, alg none aceito, validação de iss/aud ausente e hasRole/hasAuthority trocados.

## Proteção de endpoints e métodos

Qual a diferença entre proteção em request-level e em method-level? :: Request-level dá granularidade grossa e configuração centralizada no HttpSecurity; method-level dá granularidade fina e lógica próxima ao domínio (usa Authentication, parâmetros e retorno); o ideal é combinar um catch-all com regras finas por método.

Como o Spring Security casa requisições? :: Por path (não por query string), com matchers Ant (/recurso/**), variáveis de path, Regex, método HTTP e dispatcher type; cuidado com padronização de barra e com verb tampering.

Por que PostAuthorize não é recomendado para escritas e que proteções extras um endpoint precisa? :: Porque a alteração pode ocorrer antes da checagem — o correto é ler primeiro, checar e só então escrever; além disso: restringir métodos (allowlist, 405), validar entrada e limite de payload (413), validar Content-Type (415), rate limiting (429 + Retry-After), CORS/CSRF/headers, DTOs contra mass assignment e endpoints de gestão fora da internet.

## OWASP API Security Top 10 e falhas de controle de acesso

Quais riscos formam o OWASP API Security Top 10 (2023)? :: API1 BOLA, API2 Broken Authentication, API3 BOPLA, API5 BFLA, API6 acesso irrestrito a fluxos de negócio sensíveis, API8 Security Misconfiguration e API9 gerência inadequada de inventário.

O que é BOLA (API1) e o que é IDOR? :: BOLA (Broken Object Level Authorization) ocorre quando o endpoint recebe um ID de objeto e não valida se o solicitante pode acessá-lo; IDOR (Insecure Direct Object Reference) é a manifestação clássica no lado web/app. Previne-se com checagem em nível de objeto em toda função que acessa dado por ID, IDs imprevisíveis (UUID) e testes automatizados — não basta comparar o sub do token com o ID.

O que é BFLA (API5)? :: Broken Function Level Authorization, em que usuário autenticado (ou anônimo) chama função que não deveria; previne-se negando por padrão, exibindo grants explícitos por função e revisando os endpoints contra o modelo de negócio.

O que é BOPLA (API3) e o que abrange? :: Broken Object Property Level Authorization, que abrange exposição excessiva de dados (ler demais) e mass assignment (gravar campos indevidos, como "role":"admin"); previne-se com DTOs, serialização explícita, checagem de propriedade e validação de entrada.

Como identificar e corrigir falhas de controle de acesso? :: Identificar: mapear endpoints/versões/hosts (inventário), testes manuais e automatizados de autorização (trocar IDs e métodos, verb tampering), revisão de código/config, testes de token (alg none, expirado, aud errado, outro emissor, ID token como access token), revisão de papéis e scanners DAST (ZAP). Corrigir: negar por padrão, centralizar a autorização, checar em nível de objeto, aplicar menor privilégio e SoD, usar DTOs, validar tokens, rotacionar credenciais, monitorar decisões de acesso, ter testes de regressão no CI e recertificar permissões (IGA).

## Comparações e pegadinhas

Por que "OAuth 2.0 autentica o usuário" e "JWT é criptografado" estão errados? :: OAuth 2.0 é autorização delegada — quem autentica é o OpenID Connect; e o JWS apenas assina, deixando o payload base64url legível, de modo que sigilo exige JWE.

JWT facilita a revogação, e MFA pode ser senha mais PIN? :: Não; o JWT dificulta a revogação (exige denylist/curta duração, enquanto o token opaco a facilita via introspecção), e senha mais PIN não é MFA, pois falta reunir categorias de fatores diferentes.

Exposição excessiva de dados × mass assignment e IDOR × BOLA? :: Exposição excessiva é ler demais; mass assignment é gravar campos indevidos; IDOR é a manifestação clássica web e BOLA é o conceito equivalente no nível de objeto da API.

Basta o path /admin para proteger uma função administrativa, e a versão na URI é sempre a melhor? :: Não para ambos; a proteção deve ser por autorização explícita (não por convenção de URL) e o versionamento tem trade-offs, sendo query param, header e media type alternativas válidas.
