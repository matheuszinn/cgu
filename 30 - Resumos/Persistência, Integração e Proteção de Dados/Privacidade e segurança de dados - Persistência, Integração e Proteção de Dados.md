---
tipo: resumo
disciplina: "Persistência, Integração e Proteção de Dados"
tema: "Privacidade e segurança de dados"
status: novo
data: "2026-10-16"
tags: [resumo, persistencia-dados, cgu-2026]
---

# Resumo: Privacidade e segurança de dados

> [!info] MOC: [[Persistência, Integração e Proteção de Dados]]
> Edital nº 1/2026 – CGU – AFFC · **Conhecimentos específicos** · Cargo 4 (TI / Desenvolvimento de Sistemas) · Item 4 — *Privacidade e segurança de dados*.

## Escopo no edital (checklist)

- [x] 4.1 Minimização, finalidade, acesso e segregação.
- [x] 4.2 Criptografia em trânsito e repouso.
- [x] 4.3 Pseudonimização e risco de reidentificação.
- [x] 4.4 Retenção, descarte e proteção de cópias e registros.
- [x] 4.5 Compartilhamento e publicação com salvaguardas.
- [x] 4.6 Proteção de dados pessoais desde a concepção da aplicação.

## Resumo

Este item ancora-se na **LGPD (Lei nº 13.709/2018)** e nas práticas de **segurança da informação** aplicadas a dados pessoais. Os seis subitens formam uma cadeia de **proteção de ponta a ponta**:

1. **Princípios de tratamento** (art. 6º): **finalidade**, **adequação** e **necessidade** (minimização), **livre acesso**, **qualidade**, **transparência**, **segurança**, **prevenção**, **não discriminação** e **responsabilização**. A isso somam-se **controle de acesso** e **segregação** (menor privilégio, separação de funções).
2. **Criptografia em trânsito** (TLS) e **em repouso** (AES, criptografia de disco/banco), distinguindo também **hash** (não reversível) e **tokenização**.
3. **Pseudonimização** (reversível, art. 13 §4º) × **anonimização** (irreversível, art. 5º XI; dado anonimizado **não é dado pessoal**, art. 12) e o **risco de reidentificação** (ataques de ligação/inferência, k-anonimato).
4. **Retenção** (guardar só o necessário e pelo tempo devido) e **descarte seguro**, protegendo **cópias, backups e logs**.
5. **Compartilhamento e publicação** com salvaguardas: base legal, mínimo necessário, anonimização/agregação, acordos e controles.
6. **Privacy by design / by default** — proteção **desde a concepção** (art. 46 §2º da LGPD), com os sete princípios de Ann Cavoukian.

O fio condutor: **dado pessoal é a unidade protegida; cada decisão de arquitetura (coleta, armazenamento, trânsito, compartilhamento, descarte) precisa de justificativa de finalidade e de minimização.**

## 1. Minimização, finalidade, acesso e segregação (4.1)

### 1.1 Princípios da LGPD (art. 6º) que sustentam o subitem

- **Finalidade (I):** tratar para **propósitos legítimos, específicos, explícitos e informados** ao titular, sem uso posterior incompatível.
- **Adequação (II):** tratamento compatível com as finalidades informadas.
- **Necessidade / minimização (III):** limitação ao **mínimo necessário** para as finalidades (o coração da "minimização de dados").
- **Livre acesso (IV), qualidade dos dados (V), transparência (VI), segurança (VII), prevenção (VIII), não discriminação (IX), responsabilização e prestação de contas (X).**

### 1.2 Minimização e finalidade na prática

- Coletar **apenas** os campos necessários (não pedir CPF "por padrão"), com **base legal** (art. 7º) e **finalidade específica**.
- **Limitação de propósito:** não reutilizar dados para finalidade incompatível sem nova base/consentimento.
- **Armazenamento mínimo:** não reter além do necessário (liga ao item 4.4).
- **Privacidade por padrão:** por omissão, o tratamento é o **menos invasivo** possível (mínimo compartilhamento, mínima coleta).

### 1.3 Acesso e segregação

- **Controle de acesso:** **menor privilégio**, **negação por padrão**, **need-to-know** — cada usuário/sistema acessa só o indispensável. Aplica-se a banco, arquivos, logs, APIs (ver Item 2 de "Arquitetura e Integração de Sistemas").
- **Segregação de funções (SoD):** quem **aprova** ≠ quem **executa**; quem **cadastra** ≠ quem **libera**; papéis administrativos separados de operacionais.
- **Segregação lógica/física:** separar dados pessoais (ou dados sensíveis) de outros dados/ambientes (multitenancy, bancos/ambientes separados, *data masking* por papel).
- **Dados sensíveis** (art. 5º II: origem racial/étnica, convicção religiosa, opinião política, saúde, vida sexual, dado genético/biométrico) têm regime **mais restrito** (art. 11) e merecem controles extras.

### 1.4 Bases legais (art. 7º) e agentes de tratamento

**Bases legais do tratamento (art. 7º):** consentimento, cumprimento de **obrigação legal/regulatória**, execução de **políticas públicas** (administração pública), **estudos por órgão de pesquisa**, **execução de contrato**, **exercício regular de direitos** (processo judicial/administrativo), **proteção da vida**/incolumidade física, **tutela da saúde**, **interesse legítimo** (do controlador ou terceiro, sem prevalecer direitos do titular) e **proteção ao crédito**.

> **Pontos que caem:** o **consentimento é apenas uma** das bases, não a única; dados sensíveis (art. 11) exigem consentimento **específico e destacado** (ou hipóteses mais restritas); a administração pública trata dados para políticas públicas com **finalidade específica**.

**Agentes de tratamento (art. 5º):** **Titular** (pessoa a quem o dado se refere), **Controlador** (decide sobre o tratamento), **Operador** (executa em nome do controlador), **Encarregado/DPO** (canal com titulares e ANPD). O **controlador responde** e pode ser responsabilizado; a **ANPD** é a autoridade nacional fiscalizadora.

## 2. Criptografia em trânsito e repouso (4.2)

### 2.1 Em trânsito (in transit)

- **TLS** (Transport Layer Security) protege dados em movimento pela rede. Usar **TLS 1.2/1.3** (RFC 8446), **não** SSL 2/3/TLS 1.0/1.1 (obsoletos).
- Aplica-se a HTTP (**HTTPS**), conexões de banco, filas, e-mail e chamadas entre serviços (mTLS para autenticação mútua).
- Também: **VPN/IPsec** para enlaces, **SSH** para acesso remoto, criptografia de tráfego em **redes internas** (zero trust — não confiar só no perímetro).

### 2.2 Em repouso (at rest)

- Protege dados **armazenados**: criptografia de disco (full-disk — LUKS, BitLocker), de banco (**TDE** — Transparent Data Encryption), de arquivos/backups, de objetos (S3-SSE).
- Algoritmo simétrico padrão: **AES** (FIPS 197), com **AES-256** recomendado para dados sensíveis; modos com autenticação (GCM) para integridade.
- **Gerenciamento de chaves** é o ponto crítico: rotação, guarda em **HSM/KMS**, separação da chave e do dado.

### 2.3 Criptografia × hash × tokenização

| Técnica | Reversível? | Uso típico |
| --- | --- | --- |
| **Criptografia simétrica** (AES) | Sim (com a chave) | Dados em trânsito/repouso |
| **Criptografia assimétrica** (RSA/ECC) | Sim (com a chave privada) | Troca de chave, assinatura |
| **Hash** (SHA-256, bcrypt/Argon2) | **Não** | Senhas, integridade, fingerprint |
| **Tokenização** | Sim (via *vault*) | Substituir dado sensível por token (ex.: cartão) |

- **Senha nunca se "descriptografa"**: usa-se **hash + salt** com função lenta (**bcrypt, scrypt, Argon2, PBKDF2**). Hash simples (MD5/SHA-1) é inadequado.
- **Hash ≠ criptografia**: hash é one-way e não "protege" dado que precise ser lido de volta.
- **Criptografia ≠ pseudonimização** (ver 4.3), embora possam se combinar.

## 3. Pseudonimização e risco de reidentificação (4.3)

### 3.1 Definições legais

- **Pseudonimização** (art. 13 §4º): tratamento pelo qual o dado **perde a possibilidade de associação** direta ou indireta a um indivíduo, **senão pelo uso de informação adicional** mantida **separadamente** pelo controlador, em **ambiente controlado e seguro**. → **Reversível** (a chave/tabela de correspondência existe, mas separada).
- **Anonimização** (art. 5º XI): uso de **meios técnicos razoáveis e disponíveis** pelos quais o dado **perde a possibilidade de associação**, direta ou indireta, a um indivíduo. → **Irreversível**.
- **Art. 12:** **dado anonimizado não é considerado dado pessoal**, **salvo** se o processo de anonimização puder ser **revertido** com esforços razoáveis ou meios próprios. → Anonimização "mal feita" continua sendo dado pessoal.

### 3.2 Risco de reidentificação

- Pseudonimização **reduz** o risco, mas **não elimina** (o dado continua sendo **dado pessoal** enquanto a associação for possível).
- **Ataques de ligação (linking):** cruzar bases (ex.: CEP + data de nascimento + gênero) para reidentificar. **Ataque de inferência:** deduzir atributos a partir de outros.
- **Quase-identificadores** (quasi-identifiers): atributos que, sozinhos, não identificam, mas em combinação, sim (CEP, idade, sexo).
- Técnicas de anonimização: **generalização** (idade em faixa), **supressão** (remover campo), **perturbação** (ruído/arredondamento), **k-anonimato** (cada combinação aparece ≥ k vezes), **l-diversidade** (variedade de valores sensíveis), **t-closeness** (distribuição próxima da global). Nenhuma é à prova de balas; é análise **contínua** de risco.

> **Exemplo clássico:** uma base "anonimizada" com `(CEP, data de nascimento, sexo)` é cruzada com o cadastro eleitoral e reidentifica a pessoa — os três campos são **quase-identificadores**. Por isso publicar só "agregado" não basta: é preciso **generalizar/suprimir** até que cada combinação atenda ao k desejado e ainda testar ataques de ligação/inferência.

## 4. Retenção, descarte e proteção de cópias e registros (4.4)

### 4.1 Retenção

- **Minimização temporal:** guardar só enquanto a **finalidade** existir e enquanto a **base legal/obrigação** exigir.
- **Art. 16:** dados devem ser **eliminados após o término do tratamento**, admitida a conservação para: **obrigação legal/regulatória**, **estudo por órgão de pesquisa** (com anonimização sempre que possível), **uso exclusivo do controlador** (vedado acesso de terceiros) e **transferência a terceiro**.
- Definir **política de retenção** (prazos por categoria) e **revisão periódica**.

### 4.2 Descarte seguro

- **Eliminação (art. 5º XIV):** exclusão de dado ou conjunto armazenado, independentemente do meio.
- **Descarte seguro:** sobrescrita, **destruição criptográfica** (apagar a chave), desmagnetização/destruição física de mídia. "Deletar" arquivo (apagar referência) **não** é descarte seguro.
- **Anonimização** como alternativa de retenção quando ainda há valor analítico.

### 4.3 Proteção de cópias e registros

- **Backups** guardam dados pessoais por mais tempo — devem entrar na política de retenção e ser **criptografados** e **eliminados** junto.
- **Logs** podem conter dados pessoais (IP, CPF, conteúdo) — minimizar o que se loga, mascarar, controlar acesso e retenção.
- **Réplicas, caches, filas, snapshots, ambientes de teste**: todas as **cópias** contam. Cuidado com **dados reais em dev/test** (usar mascaramento/sintéticos) e com **cópias em object storage** esquecidas.

## 5. Compartilhamento e publicação com salvaguardas (4.5)

### 5.1 Compartilhamento (uso compartilhado, art. 5º XVI)

- Exigir **base legal** (art. 7º/11) e **finalidade legítima**; compartilhar o **mínimo necessário**.
- **Acordos/instrumentos** entre controlador e operador/terceiros (contratos, cláusulas de proteção), responsabilização e **registro** do compartilhamento.
- **Transferência internacional** (arts. 33-36) tem regras próprias (garantias, cláusulas-padrão, decisão de adequação).
- **Administração pública** (art. 23-26): uso compartilhado para **políticas públicas**, com finalidade específica e salvaguardas — relevante para a CGU.

### 5.2 Publicação com salvaguardas

- **Anonimizar/agregar** antes de publicar (relatórios, dados abertos, dashboards); evitar **quase-identificadores** que permitam reidentificar.
- **Minimizar campos** e aplicar **mascaramento** (ex.: exibir só os 4 últimos dígitos, faixas etárias).
- **Controle de acesso** à publicação (público × restrito) e **revisão** antes da divulgação (evitar vazamento em PDFs/metadados/imagens).

## 6. Proteção desde a concepção — privacy by design (4.6)

### 6.1 Base legal

- **Art. 46 §2º:** as medidas de segurança devem ser observadas **"desde a fase de concepção do produto ou do serviço até a sua execução"** → é o fundamento da **privacy by design** e **by default** na LGPD.
- **Art. 46 caput:** agentes devem adotar **medidas de segurança técnicas e administrativas** aptas a proteger dados pessoais.

### 6.2 Privacy by design (Ann Cavoukian) — sete princípios

1. **Proativo, não reativo** (prevenir antes de remediar).
2. **Privacidade como padrão (default).**
3. **Privacidade embutida no design** (não um "add-on").
4. **Funcionalidade total — soma positiva** (privacidade sem abrir mão da função).
5. **Segurança de ponta a ponta** (ciclo de vida completo).
6. **Visibilidade e transparência.**
7. **Respeito pela privacidade do usuário** (centralidade no titular).

### 6.3 Aplicação prática no desenvolvimento

- **Avaliação de impacto (RIPD/DPIA)** para tratamentos de alto risco (art. 5º XVII, art. 38 e 55-J, XIII).
- **Threat modeling** e requisitos de privacidade no backlog; **code review** de segurança; **testes** de controle de acesso e criptografia.
- **DPO/Encarregado** (art. 5º VIII) participa do ciclo; **registro das operações de tratamento**.
- **Ciclo de vida completo:** da coleta ao descarte, com minimização em cada etapa (liga todos os subitens).

## Detalhes que merecem destaque

- **Finalidade (art. 6º I)** exige propósitos legítimos, específicos, explícitos e informados; **necessidade (III)** é a **minimização**.
- **Bases legais (art. 7º):** consentimento, obrigação legal, políticas públicas, estudos/órgão de pesquisa, execução de contrato, exercício regular de direitos, proteção da vida, tutela da saúde, interesse legítimo, proteção ao crédito.
- **Dado sensível (art. 5º II)** tem regime **mais restrito** (art. 11) — consentimento específico e destacado.
- **Anonimização (art. 5º XI) é irreversível; pseudonimização (art. 13 §4º) é reversível** (informação adicional separada e segura).
- **Art. 12:** anonimizado **não é dado pessoal**, salvo se **reversível** com esforços razoáveis.
- **TLS 1.2/1.3 em trânsito; AES(-256) em repouso; chave em HSM/KMS.**
- **Hash (bcrypt/Argon2) ≠ criptografia** — hash é one-way; senha se armazena como hash+salt.
- **K-anonimato/l-diversidade/t-closeness** mitigam reidentificação, mas exigem análise contínua.
- **Art. 16:** eliminação após o término do tratamento, com hipóteses de conservação.
- **Art. 46 §2º:** proteção **desde a concepção** (privacy by design/by default).
- **Backups/logs/réplicas também são dados pessoais** e entram na retenção/descarte.
- **Compartilhamento** exige base legal + mínimo necessário + acordos + registro.

## Comparações que a banca costuma cobrar (certo/errado)

| Conceito A | Conceito B | Diferença-chave |
| --- | --- | --- |
| Anonimização | Pseudonimização | Anonimização é **irreversível**; pseudonimização é **reversível** (chave separada) |
| Dado anonimizado | Dado pseudonimizado | Anonimizado **não é dado pessoal** (art. 12); pseudonimizado **continua sendo** |
| Criptografia | Hash | Criptografia é reversível (chave); hash é **one-way** |
| Criptografia | Tokenização | Criptografia cifra o valor; tokenização troca por token via vault |
| Em trânsito | Em repouso | Trânsito = TLS em movimento; repouso = AES/TDE armazenado |
| Finalidade | Necessidade (minimização) | Finalidade = por que tratar; necessidade = tratar o **mínimo** |
| Controlador | Operador | Controlador decide o tratamento; operador executa em nome dele |
| Encarregado (DPO) | Controlador | DPO é ponte com titulares/ANPD; controlador é o decisor |
| Dado pessoal | Dado sensível | Sensível (art. 5º II) tem regime mais restrito (art. 11) |
| Retenção | Descarte | Retenção = quanto tempo guarda; descarte = como elimina com segurança |
| Eliminação | Bloqueio | Eliminação exclui; bloqueio suspende o tratamento temporariamente |
| Menor privilégio | Segregação de funções | Menor privilégio = mínimo acesso; SoD = separar funções incompatíveis |
| Privacy by design | Privacy by default | By design = embutido na arquitetura; by default = mínimo por padrão |

## Pegadinhas e erros comuns

> Cuidado com termos absolutos ("sempre", "nunca", "exclusivamente") e com a troca de requisitos.

- Dizer que **pseudonimização torna o dado não-pessoal** — ela é **reversível**; o dado continua **pessoal** (o anonimizado é que sai do escopo, art. 12).
- Confundir **anonimização com pseudonimização** (irreversível × reversível).
- Achar que **toda anonimização é definitiva** — se **reversível com esforços razoáveis**, volta a ser dado pessoal (art. 12).
- Dizer que **criptografar dado equivale a anonimizar** — são coisas distintas.
- Afirmar que **hash "criptografa" senha** — hash é **one-way**; e senha exige hash **lento + salt** (bcrypt/Argon2), não MD5/SHA-1.
- Supor que **TLS 1.0/1.1 são aceitáveis** — obsoletos; usar TLS 1.2/1.3.
- Achar que **criptografia em repouso dispensa controle de acesso** — são camadas **complementares** (defesa em profundidade).
- Confundir **base legal com consentimento** — consentimento é **uma** das bases (art. 7º); não é a única nem sempre a adequada.
- Supor que **dado sensível e dado pessoal têm o mesmo regime** — sensível é **mais restrito** (art. 11).
- Dizer que **"apagar o arquivo" é descarte seguro** — exige sobrescrita/destruição criptográfica; e **backups/logs/réplicas também contam**.
- Achar que **minimização é só "coletar pouco"** — inclui retenção mínima, acesso mínimo e compartilhamento mínimo.
- Supor que **privacy by design é um "add-on" no fim** — é **desde a concepção** (art. 46 §2º), proativo e como padrão.
- Confundir **controlador com operador** ou **encarregado (DPO) com controlador**.
- Achar que **publicar dado agregado é sempre seguro** — quase-identificadores podem permitir reidentificação.

## Notas atômicas relacionadas

```dataview
LIST FROM "20 - Notas"
WHERE disciplina = this.disciplina
  AND contains(tema, this.tema)
SORT file.name ASC
```

## Fontes

- https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709.htm — Lei nº 13.709/2018 (LGPD), texto compilado oficial no Planalto.
- https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709.htm#art6 — LGPD, art. 6º (princípios: finalidade, adequação, necessidade, segurança, prevenção...).
- https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709.htm#art7 — LGPD, art. 7º (bases legais do tratamento).
- https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709.htm#art11 — LGPD, art. 11 (tratamento de dados sensíveis).
- https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709.htm#art46 — LGPD, art. 46 (medidas de segurança e proteção desde a concepção).
- https://www.gov.br/anpd/pt-br — ANPD (Autoridade Nacional de Proteção de Dados), guias e orientações.
- https://www.ufrgs.br/proprivacidade/anonimizacao — Anonimização e pseudonimização (LGPD) — comparação didática com critérios de reidentificação.
- https://ico.org.uk/media/about-the-ico/documents/4018606/chapter-2-anonymisation-draft.pdf — ICO: guia de anonimização (referência internacional em reidentificação).
- https://datatracker.ietf.org/doc/html/rfc8446 — RFC 8446: TLS 1.3 (criptografia em trânsito).
- https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.197.pdf — FIPS 197: AES (Advanced Encryption Standard, criptografia em repouso).
- https://cheatsheetseries.owasp.org/cheatsheets/Cryptographic_Storage_Cheat_Sheet.html — OWASP Cryptographic Storage Cheat Sheet (algoritmos, chaves, repouso).
- https://cheatsheetseries.owasp.org/cheatsheets/Transport_Layer_Security_Cheat_Sheet.html — OWASP Transport Layer Security Cheat Sheet (TLS em trânsito).
- https://www.ipc.on.ca/wp-content/uploads/Resources/7foundationalprinciples.pdf — Ann Cavoukian: os 7 princípios do Privacy by Design.
- https://en.wikipedia.org/wiki/K-anonymity — k-anonimato (e l-diversidade/t-closeness) no contexto de reidentificação.
