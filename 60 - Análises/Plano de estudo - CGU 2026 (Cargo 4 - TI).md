---
tipo: plano
banca: Cebraspe
data: "2026-10-16"
cargo: "CGU 2026 – Cargo 4 (AFFC TI / Desenvolvimento de Sistemas)"
prova: "2026-12-13"
tags:
  - plano
  - estudo
  - cgu-2026
  - TI
---

# Plano de estudo — CGU 2026 · Cargo 4 (AFFC TI / Desenvolvimento de Sistemas)

> **Hoje:** 16/10/2026 · **Prova (objetiva + discursiva):** 13/12/2026 · **Banca:** Cebraspe.
> **Janela:** ~8 semanas e 3 dias (16/10 → 13/12).
> **Base:** painel de incidência (`Incidência TI - Cruzamento provas x edital CGU 2026`), taxonomia E1–E4, edital (itens 7, 8, 9, 11, 15.2.2–15.2.4), análise de modelo/pontuação e estimativa de nota de corte. Todos os números vêm desses arquivos — ver **Fontes**.

---

## 0. Resumo executivo (leia primeiro)

1. **A P3 (específicos, 90 itens × 2 = 180 pts) é 69% dos pontos objetivos e tem o maior peso relativo.** É o núcleo do plano — ~55% do tempo.
2. **Na NFC, objetiva e discursiva valem o mesmo (10 cada).** `NFC = NFPO/26 + NFPD/10`. A **discursiva é 50% da classificação final** com apenas 2 questões → precisa de treino contínuo desde a semana 1.
3. **Erro anula acerto** (net scoring). Só marcar com convicção; **deixar em branco = 0** (nem ganha nem perde).
4. **Quatro mínimos eliminatórios** a garantir com folga: **P1 ≥ 8 · P2 ≥ 12 · P3 ≥ 54 · NFPO ≥ 78**; e **discursiva ≥ 50**.
5. **Meta realista de boa colocação:** NFC ≥ 15–16 (≈75–80% de aproveitamento líquido), dado o corte alto do TCU 2026 (Cebraspe, TI, ~71% no 15º/AC) e as poucas vagas do Cargo 4 (10 imediatas).

---

## 1. Diagnóstico

### 1.1 Estrutura e pesos (edital, itens 7 e 8)

| Prova | Área | Itens | Ponto/item | Máx. | % do objetivo | Turno |
|---|---|:--:|:--:|:--:|:--:|:--:|
| **P1** | Básicos | 40 | +1 / −1 | 40 | 15,4% | manhã |
| **P2** | Complementares | 40 | +1 / −1 | 40 | 15,4% | manhã |
| **P3** | Específicos (Cargo 4) | 90 | +2 / −2 | 180 | **69,2%** | manhã |
| **P4** | Discursiva (2 questões) | 2 | — | 100 | (50% da NFC) | tarde |

- Formato: **todos os 170 itens objetivos são Certo/Errado** (sem alternativas).
- Duração: objetivas **5 h** (manhã); discursiva **3 h 30** (tarde).
- `NFPO` máx = 260 · `NFPD` máx = 100 · `NFC = NFPO/26 + NFPD/10` (máx 20).

### 1.2 O que mais cai na P3 — cruzamento de 663 itens de 13 concursos Cebraspe

Blocos do edital (item 15.2.4), por volume:

| Bloco | Tema | Itens | % |
|---|---|--:|--:|
| **E4** | Desenvolvimento Seguro, Qualidade e Gestão da Entrega | 228 | 34% |
| **E3** | Persistência, Integração e Proteção de Dados | 199 | 30% |
| **E2** | Arquitetura e Integração de Sistemas | 190 | 29% |
| **E1** | Engenharia de Software e Programação | 46 | 7% |

Ranking por tema (cruzamento):

| # | Tema | Itens |
|--:|---|--:|
| 1 | **E4.5** Contratação e fiscalização de soluções | 84 |
| 2 | **E3.1** Modelagem e persistência | 73 |
| 3 | **E3.4** Privacidade e segurança de dados | 72 |
| 4 | **E2.5** Confiabilidade das aplicações | 71 |
| 5 | **E4.4** Gestão de produtos e governança | 69 |
| 6 | **E2.4** Integração com dados e IA | 62 |
| 7 | **E2.2** APIs e identidade | 35 |
| 8 | **E4.1** Segurança de aplicações | 33 |
| 9 | **E3.2** SQL e desempenho | 32 |
| 10 | **E3.3** Fluxos e interoperabilidade | 22 |
| 11 | **E4.3** Entrega e operação | 22 |
| 12 | **E4.2** Testes e qualidade | 20 |
| 13 | **E1.1** Problemas e requisitos | 18 |
| 14 | **E1.2** Programação e correção | 17 |
| 15 | **E2.1** Arquiteturas de aplicações | 16 |
| 16 | **E1.4** Interfaces e experiência do usuário | 9 |
| 17 | **E2.3** Comunicação e consistência | 6 |
| 18 | **E1.3** Concorrência e processamento | 1 |
| 19 | **E1.5** Manutenção e evolução | 1 |

**Leituras do painel:**
- O edital cobra **"engenharia de produto + dados + entrega"**, não TI clássica de infraestrutura.
- **Banco de dados é o núcleo técnico:** E3.1 + E3.2 + E3.3 = **127 itens (19%)**.
- **Segurança/privacidade:** E3.4 + E4.1 = **105 itens (16%)**.
- **Arquitetura/APIs:** E2.2 + E2.1 = 51 itens (OAuth/OIDC, tokens, Spring Security, versionamento).
- **IA/dados (E2.4 = 62)** é inflado por concursos com Ciência de Dados; interpretação estrita reduz ~37 itens. Ainda assim é item explícito e crescente.
- **Programação pura (E1.2 = 17) é minoria** nas provas de TI desses concursos — **mas é o que o edital do Cargo 4 detalha (Java/Vue); não descuidar**.

### 1.3 O que mais cai em P1 e P2 (incidência histórica Cebraspe)

**P2 — Complementares (40 itens):**

| # | Item do edital | Incidência |
|--:|---|:--:|
| 1 | Fundamentos de **Auditoria Governamental e Atuação Integrada da CGU** | Altíssima |
| 2 | Fundamentos de **Governança, Riscos e Integridade** (pública e privada) | Altíssima/Alta |
| 3 | Fundamentos de **Direito Público Aplicado, Controle e Responsabilização** | Alta |
| 4 | Fundamentos de **Transparência, Ouvidoria e Participação Social** | Média/Alta |
| 5 | Fundamentos de **Evidências, Dados e IA** | Média (tendência de alta) |

**P1 — Básicos (40 itens):**

| # | Item do edital | Incidência |
|--:|---|:--:|
| 1 | **Administração Pública e Fundamentos de Políticas Públicas** | Altíssima |
| 2 | **Ética Pública e Responsabilidade Profissional** | Muito alta |
| 3 | Estado, Democracia, Direitos e Ciência Política | Alta |
| 4 | Sociedade Brasileira, Desigualdades, Diversidade e Desenvolvimento | Média/Alta |

### 1.4 Incidência × peso → leitura estratégica

- **P3 concentra 69% dos pontos objetivos e o maior volume de incidência conhecida** → prioridade absoluta de tempo.
- **P1 e P2 valem só 15% cada, mas são eliminatórios** (8 e 12 pts) e **"pontos baratos"** quando o tema é de alta incidência (Administração Pública, Ética, Auditoria Governamental, Governança). Não sacrificar, mas não exagerar.
- **A discursiva tem 1 questão de complementares (30 pts) + 1 situação-problema de específicos (70 pts)** — ou seja, o treino de discursiva **puxa P2 e P3 ao mesmo tempo**.
- **Ressalva de método (não inventar):** o cruzamento (663 itens) mede o que a Cebraspe cobrou em **TI de controle/auditoria**; como o Cargo 4 é **desenvolvimento**, a análise de específicos (Raio-X Cebraspe) rebaixa E4.5 (contratação) para "média" e sobe Eng. Software/BD/Segurança. O plano **honra o cruzamento** (base do pedido) e **pondera** com essa ressalva — sinalizado na priorização.

---

## 2. Priorização (ordem de estudo)

Ordem por **retorno esperado = incidência × peso × aderência ao cargo "desenvolvimento"**.

### Grupo A — Núcleo de altíssimo retorno (≈50–55% do tempo)

| Ordem | Tema (E-código) | Por que |
|:--:|---|---|
| A1 | **E3.1 Modelagem e persistência** (73) + **E3.2 SQL e desempenho** (32) | Núcleo técnico de BD (127 itens com E3.3); 2º e 9º no cruzamento; "Muito alta" na análise de específicos |
| A2 | **E3.4 Privacidade e segurança de dados** (72) + **E4.1 Segurança de aplicações** (33) | Segurança/privacidade = 105 itens; OWASP/LGPD "figurinha carimbada"; perfil auditoria |
| A3 | **E4.5 Contratação e fiscalização de soluções** (84) | **1º no cruzamento**; decisiva na discursiva (SLA, TCO, lock-in, plano de saída) — ressalva: menos "desenvolvimento" |
| A4 | **E2.5 Confiabilidade das aplicações** (71) | 4º no cruzamento; cloud/containers/observabilidade ("Média-alta/Alta" na análise) |
| A5 | **E4.4 Gestão de produtos e governança** (69) | 5º no cruzamento; **Scrum 26,46%** no Raio-X; PDTIC/plano de dados abertos = marca CGU |
| A6 | **E1.1 Problemas e requisitos** (18) + **E1.2 Programação e correção / Java** (17) | Edital detalha Java/Vue; análise aponta Eng. Software como disciplina mais cobrada |

### Grupo B — Segundo anel (≈30% do tempo)

| Ordem | Tema | Por que |
|:--:|---|---|
| B1 | **E2.2 APIs e identidade** (35) | Item explícito: REST, OAuth 2.0, OIDC, JWT, Spring Security, permissões excessivas |
| B2 | **E2.4 Integração com dados e IA** (62) | 6º no cruzamento; RAG/embeddings/agentes/prompt injection — novo e crescente |
| B3 | **E2.1 Arquiteturas** (16) + **E2.3 Comunicação e consistência** (6) | Microsserviços/eventos/Saga/idempotência; "coração técnico" |
| B4 | **E4.2 Testes e qualidade** (20) + **E4.3 Entrega e operação** (22) | Testes/CI-CD/DevSecOps/containers |

### Grupo C — Cauda e cobertura integral (≈15% do tempo)

| Ordem | Tema | Por que |
|:--:|---|---|
| C1 | **E3.3 Fluxos e interoperabilidade** (22) | ETL/ELT, CSV/JSON/XML/Parquet, Spring Batch — cobre o edital e a discursiva |
| C2 | **E1.4 Interfaces/UX (Vue.js)** (9) | Item explícito e novo; baixa frequência |
| C3 | **E1.3 Concorrência** (1) e **E1.5 Manutenção** (1) | Baixa incidência, mas cobrem o edital (e o "teste de borda" mental) |

> **P2 (ordem):** Auditoria Governamental → Governança/Riscos/Integridade → Direito Público Aplicado/Controle → Transparência/LAI×LGPD → Evidências/Dados/IA.
> **P1 (ordem):** Administração Pública/Políticas Públicas → Ética → Estado/Democracia/Direitos → Sociedade/Desigualdades.

---

## 3. Cronograma semanal (16/10 → 13/12/2026)

### 3.1 Grade-base (≈30 h/semana — ajuste à sua disponibilidade)

- **2ª a 6ª (4 h/dia = 20 h):** 2 h teoria P3 · 1 h questões P3 (Certo/Errado) · 0,5 h P2 **ou** P1 · 0,5 h flashcards/revisão.
- **Sáb (5 h):** 3 h P2 · 2 h P1 · questões intercaladas.
- **Dom (5 h):** 3 h simulado/revisão dirigida · 2 h discursiva (redação + autocorreção).

> Se o tempo disponível for menor, **preserve a proporção** (P3 ≈ 55%, P2 ≈ 20%, P1 ≈ 15%, discursiva ≈ 10%), não a carga absoluta.

### 3.2 Bloco 0 — 16 a 18/10 (6ª a dom, ~10 h) — Onboarding e diagnóstico

| Dia | Bloco | Tema | Carga |
|---|---|---|---:|
| 6ª 16/10 | Fundação | Ler edital 15.2.4 (Cargo 4) + painel de incidência; montar **caderno de erros** e **baralho de flashcards** por tema | 3 h |
| Sáb 17/10 | Fundação | Panorama E1–E4; criar pastas de flashcards (ver `40 - Flashcards/`) | 3 h |
| Dom 18/10 | **Simulado-diagnóstico** | Prova-alvo (TCU 2026 TI **ou** FUNPRESP-JUD 2026 Dev. Sistemas) + correção; registrar baseline | 4 h |

### 3.3 Semana 1 — 19 a 25/10 — Núcleo A1 (E4.5) + A3 (E3.1) · P2-1 · P1-1

| Dia | Bloco | Tema | Carga |
|---|---|---|---:|
| 2ª 19/10 | P3 | E4.5 — necessidade, ETP, termo de referência | 3 h |
| 3ª 20/10 | P3 | E4.5 — próprio × contratação × compartilhamento; TCO, pesquisa de preços | 3 h |
| 4ª 21/10 | P3 | E3.1 — modelagem relacional, normalização, integridade | 3 h |
| 5ª 22/10 | P3 | E3.1 — NoSQL (documento/chave-valor/vetorial), cache, ACID/transações | 3 h |
| 6ª 23/10 | P3 | E4.5 — SLA, entregas verificáveis, fiscalização/pagamento, PI, plano de saída | 3 h |
| Sáb 24/10 | P2 + P1 | P2 Auditoria Governamental (três linhas/COSO) · P1 Administração Pública/Políticas Públicas | 5 h |
| Dom 25/10 | Sim + Disc | **Mini-simulado P3 (E4.5+E3.1)** + correção · discursiva 30 linhas (complementares) | 5 h |

### 3.4 Semana 2 — 26/10 a 1/11 — A2 (E3.4 + E4.1) + E3.2 · P2-2 · P1-2

| Dia | Bloco | Tema | Carga |
|---|---|---|---:|
| 2ª 26/10 | P3 | E3.4 — minimização, finalidade, criptografia (trânsito/repouso) | 3 h |
| 3ª 27/10 | P3 | E3.4 — pseudonimização, retenção/descarte, privacy by design | 3 h |
| 4ª 28/10 | P3 | E4.1 — ameaças/vulnerabilidades (OWASP: SQLi, XSS), validação de entradas | 3 h |
| 5ª 29/10 | P3 | E4.1 — segredos/dependências, testes de segurança, vazamentos, evidências | 3 h |
| 6ª 30/10 | P3 | E3.2 — DDL/DML, joins, agregações, subconsultas, CTEs, índices, planos | 3 h |
| Sáb 31/10 | P2 + P1 | P2 Governança/Riscos/Integridade (COSO, risco residual, Lei 12.813/2013) · P1 Ética Pública | 5 h |
| Dom 1/11 | Sim + Disc | **Mini-simulado P3 (E3.4+E4.1+E3.2)** + correção · discursiva 30 linhas | 5 h |

### 3.5 Semana 3 — 2 a 8/11 — A4 (E2.5) + E4.3 + E4.2 · P2-3 · P1-3

| Dia | Bloco | Tema | Carga |
|---|---|---|---:|
| 2ª 2/11 | P3 | E2.5 — contêineres, nuvem, serverless | 3 h |
| 3ª 3/11 | P3 | E2.5 — logs/métricas/rastreamento; latência, disponibilidade, tolerância a falhas | 3 h |
| 4ª 4/11 | P3 | E4.3 — CI/CD, versionamento, automação de build/teste/deploy | 3 h |
| 5ª 5/11 | P3 | E4.3 — DevSecOps, cadeia de dependências, ambientes, reversão, observabilidade | 3 h |
| 6ª 6/11 | P3 | E4.2 — testes unitário/integração/contrato/aceitação, análise estática, cobertura | 3 h |
| Sáb 7/11 | P2 + P1 | P2 Direito Público Aplicado/Controle (Lei 9.784, arts. 70–74 CF, PAD×PAR) · P1 Estado/Democracia/Direitos | 5 h |
| Dom 8/11 | **Simulado 1** | **P3 completo (90 itens, 3 h)** + correção · discursiva | 5 h |

### 3.6 Semana 4 — 9 a 15/11 — A5 (E4.4) + B2 (E2.4) · P2-4 · P1-4

| Dia | Bloco | Tema | Carga |
|---|---|---|---:|
| 2ª 9/11 | P3 | E4.4 — descoberta, ciclo de vida de produto, **Scrum e Kanban** | 3 h |
| 3ª 10/11 | P3 | E4.4 — priorização, critérios de aceitação, indicadores, **PDTIC/plano de dados abertos** | 3 h |
| 4ª 11/11 | P3 | E2.4 — consumo de serviços de dados/LLM, embeddings, busca semântica, **RAG** | 3 h |
| 5ª 12/11 | P3 | E2.4 — agentes/ferramentas, avaliação de respostas, **prompt injection**, supervisão | 3 h |
| 6ª 13/11 | P3 | Revisão ativa E4.4 + E2.4 (flashcards + questões) | 3 h |
| Sáb 14/11 | P2 + P1 | P2 Transparência/Ouvidoria (LAI×LGPD, Lei 13.460) · P1 Sociedade/Desigualdades | 5 h |
| Dom 15/11 | **Simulado 2** | **P3 + P2 (130 itens)** + correção · discursiva (situação-problema 60 linhas) | 5 h |

### 3.7 Semana 5 — 16 a 22/11 — B1 (E2.2) + B3 (E2.1/E2.3) + A6 (E1.1/E1.2) · P2-5

| Dia | Bloco | Tema | Carga |
|---|---|---|---:|
| 2ª 16/11 | P3 | E2.2 — design/contratos/versionamento REST; autenticação × autorização | 3 h |
| 3ª 17/11 | P3 | E2.2 — **OAuth 2.0, OIDC, tokens, Spring Security**, permissões excessivas | 3 h |
| 4ª 18/11 | P3 | E2.1 + E2.3 — microsserviços/eventos; mensageria, idempotência, Saga, contratos | 3 h |
| 5ª 19/11 | P3 | E1.1 — requisitos funcionais/não funcionais, critérios de aceitação, desenho centrado nas pessoas | 3 h |
| 6ª 20/11 | P3 | E1.2 — Java/POO, coleções, genéricos, exceções, estruturas/algoritmos, complexidade | 3 h |
| Sáb 21/11 | P2 + revisão P1 | P2 Evidências/Dados/IA · revisão de flashcards P1 | 5 h |
| Dom 22/11 | **Simulado 3** | **Completo (170 itens) + discursiva (30+60 linhas)**, cronometrado | 5 h |

### 3.8 Semana 6 — 23 a 29/11 — C (E3.3 + E1.4/E1.3/E1.5) + revisão do núcleo

| Dia | Bloco | Tema | Carga |
|---|---|---|---:|
| 2ª 23/11 | P3 | E3.3 — ingestão/transformação/carga, ETL×ELT, formatos CSV/JSON/XML/Parquet | 3 h |
| 3ª 24/11 | P3 | E3.3 — **Spring Batch** (jobs/steps, transacional, restart, idempotência) | 3 h |
| 4ª 25/11 | P3 | E1.4 — usabilidade, acessibilidade, **JavaScript/Vue.js** | 3 h |
| 5ª 26/11 | P3 | E1.3 + E1.5 — concorrência; débito técnico, legado, interoperabilidade | 3 h |
| 6ª 27/11 | P3 | Revisão núcleo (E3.1, E3.4, E4.1, E2.5) — só questões e erros | 3 h |
| Sáb 28/11 | P2 + P1 | Revisão geral P2/P1 (flashcards + 40 questões) | 5 h |
| Dom 29/11 | **Simulado 4** | **Completo (170 itens) + discursiva**, em condições reais (5 h + 3h30) | 5 h |

### 3.9 Semana 7 — 30/11 a 6/12 — Revisão por incidência + Simulado

| Dia | Bloco | Tema | Carga |
|---|---|---|---:|
| 2ª 30/11 | Revisão | Top 5 do cruzamento (E4.5, E3.1, E3.4, E2.5, E4.4) — mapas mentais + questões | 3 h |
| 3ª 1/12 | Revisão | P3 2º anel (E2.2, E2.4, E2.1/E2.3, E4.2/E4.3) | 3 h |
| 4ª 2/12 | Discursiva | 2 redações cronometradas (30 + 60 linhas) + autocorreção pela fórmula NQ | 4 h |
| 5ª 3/12 | Revisão | Caderno de erros + flashcards (revisão espaçada) | 3 h |
| 6ª 4/12 | P1 + P2 | Bateria de 40 questões P1 + 40 P2 | 3 h |
| Sáb 5/12 | **Simulado 5** | **Completo (170 itens) + discursiva** | 5 h |
| Dom 6/12 | Correção | Análise do simulado; ajuste final das metas | 3 h |

### 3.10 Semana 8 — 7 a 13/12 — Reta final (reduzir carga, não zerar)

| Dia | Bloco | Tema | Carga |
|---|---|---|---:|
| 2ª 7/12 | Revisão leve | Tabelas de distinções conceituais (P1/P2) + siglas de frameworks (P3) | 3 h |
| 3ª 8/12 | Revisão leve | Lei seca citada (Lei 12.813/2013 arts. 3º–5º, 8º, 10; Lei 9.784/1999 arts. 18–21) | 3 h |
| 4ª 9/12 | Revisão leve | Fórmulas (NQ1, NQ2, NFC) + estrutura-modelo de redação | 2 h |
| 5ª 10/12 | Sim leve | Mini-simulado de 30–40 itens (só os temas mais fortes) | 3 h |
| 6ª 11/12 | Logística | Descanso ativo; conferir local/horário; separar documento e caneta preta | 1 h |
| Sáb 12/12 | Descanso | Revisão muito leve de flashcards; dormir cedo | 2 h |
| Dom 13/12 | **PROVA** | Objetivas (manhã, 5 h) + discursiva (tarde, 3h30) | — |

---

## 4. Metas semanais de questões e flashcards

Formato **Certo/Errado** com apuração **líquida** = (acertos − erros) ÷ total. Registre no caderno de erros por **motivo**: conceito · norma/lei · detalhe de ferramenta.

| Semana | Questões C/E | Simulado | Flashcards novos | Foco de revisão |
|---|:--:|---|:--:|---|
| Bloco 0 | 40 | Diagnóstico | 20 | — |
| 1 | 80 | Mini P3 | 40 | E4.5, E3.1 |
| 2 | 80 | Mini P3 | 45 | E3.4, E4.1, E3.2 |
| 3 | 90 | — | 45 | E2.5, E4.3, E4.2 |
| 4 | 90 | Simulado 1 (P3 90) | 50 | E4.4, E2.4 |
| 5 | 100 | Simulado 2 (130) | 50 | E2.2, E2.1/E2.3, E1 |
| 6 | 110 | Simulado 3 (170 + disc) | 40 | E3.3, E1.4 |
| 7 | 120 | Simulado 4 (170 + disc) | 60 | revisão geral |
| 8 | — | Simulado 5 (leve) | 80 | revisão final |
| **Total** | **≈ 710** | **5 simulados + 3 mini** | **≈ 430** | — |

**Rotina de flashcards (revisão espaçada):** D+1 · D+7 · D+30. Use `40 - Flashcards/` (crie uma pasta por tema do edital). Cada par de conceitos que a Cebraspe confunde vira um card: ética×moral, eficiência×eficácia×efetividade, descentralização×desconcentração, impedimento×suspeição, COSO×Três Linhas, risco inerente×residual, OAuth2×OIDC, lazy×eager, ACID×BASE.

---

## 5. Estratégia de prova

### 5.1 Regra de pontuação (item 8.11.2) — "uma errada anula uma certa"

| Prova | Acerto | Erro | Branco ou dupla (C e E) |
|---|:--:|:--:|:--:|
| P1 | +1,00 | −1,00 | 0,00 |
| P2 | +1,00 | −1,00 | 0,00 |
| P3 | **+2,00** | **−2,00** | 0,00 |

- **Nota da prova** = soma das notas de todos os itens (8.11.3).
- **Máximos:** P1 = 40 · P2 = 40 · P3 = 180 → **NFPO máx = 260**.

### 5.2 Gestão de risco (net scoring)

- **Regra do valor esperado:** marcar só rende **se a convicção de acerto > 50%**. Com aversão a risco (corte alto), marque apenas com **~60–65%+ de segurança**.
- **Em dúvida genuína → deixe em branco** (0,00: não ganha, mas não perde). Isso é parte da estratégia, não fraqueza.
- **Nunca marque dupla (C e E)** nem rasure — vira 0,00 ou marcação indevida (8.3, 8.5).
- **Termos absolutos** ("sempre", "nunca", "exclusivamente", "apenas", "todos") são **candidatos a ERRADO** — salvo transcrição literal de lei.
- A banca mantém ~**50% certos / 50% errados**; não "corrija" sua folha para bater 50/50, mas desconfie de sequências longas iguais.

### 5.3 Os 4 mínimos eliminatórios (item 8.11.4)

| Condição | Mínimo | % do máximo |
|---|:--:|:--:|
| P1 (básicos) | **≥ 8,00** | 20% de 40 |
| P2 (complementares) | **≥ 12,00** | 30% de 40 |
| P3 (específicos) | **≥ 54,00** | 30% de 180 |
| **NFPO = P1+P2+P3** | **≥ 78,00** | 30% de 260 |
| Discursiva (NFPD) | **≥ 50,00** | 50% de 100 |

- Quem falha em qualquer um **é eliminado e não tem classificação alguma**.
- **Metas de trabalho (com folga):** P1 ≈ 26–30/40 · P2 ≈ 28–32/40 · P3 ≈ 135–153/180 (75–85%) · NFPO ≈ 195–220/260 · NFPD ≈ 75–85.

### 5.4 Discursiva (item 9) — 50% da NFC

**Estrutura:** (a) questão discursiva de **complementares** — até **30 linhas**, **30 pts**; (b) **situação-problema** de **específicos** — até **60 linhas**, **70 pts**. Manuscrito, caneta preta, sem marca de identificação.

**Fórmulas (9.7.5 e 9.7.6):**

- `NQ1 = NC − 6 × NE ÷ TL` (máx NC = 30)
- `NQ2 = NC − 14 × NE ÷ TL` (máx NC = 70)
- `NFPD = NQ1 + NQ2` (máx 100) · **aprovação: NFPD ≥ 50**
- Nota **zero** se `NQ < 0`, **fuga ao tema** ou **sem texto**.

**Leitura estratégica da fórmula:** o coeficiente (6 ou 14) é proporcional ao valor da questão (30 ou 70) — nos dois casos a penalidade é **~20% da nota máxima × (NE/TL)**. Consequências práticas:
1. **Escreva até o limite de linhas** (30 e 60): quanto maior **TL**, menor o peso de cada erro gramatical. Ex.: 6 erros → −1,4 pt com TL=60, mas −2,8 pt com TL=30.
2. **Norma culta é dinheiro:** cada erro gramatical (grafia, morfossintaxe, propriedade vocabular) desconta. Revise antes de passar a limpo.
3. **Estrutura dissertativa** (introdução → desenvolvimento → conclusão), **coerência e coesão**, atendendo integralmente ao comando.
4. **Conteúdo (NC)** exige responder ao tema — treine os temas transversais: riscos/controles, integridade, acesso à informação × proteção de dados, proteção do denunciante, evidência/achado/conclusão, uso responsável de IA, e (na situação-problema) arquitetura/segurança/contratação de TI (SaaS, SLA, lock-in).

**Treino:** 1–2 redações por semana desde a Semana 1; pelo menos 4 em condições cronometradas. Autocorrija com as fórmulas (conteúdo + contagem de erros).

---

## 6. Marcos de simulado e metas de desempenho

| Data | Simulado | Escopo | Meta de desempenho |
|---|---|---|---|
| Dom 18/10 | Diagnóstico | Prova-alvo completa | Baseline (sem meta) |
| Dom 25/10 | Mini 1 | P3 (E4.5+E3.1) | ≥ 55% líquido no recorte |
| Dom 1/11 | Mini 2 | P3 (E3.4+E4.1+E3.2) | ≥ 55% líquido no recorte |
| Dom 8/11 | **Simulado 1** | P3 completo (90) | ≥ 55–60% (≈50–54/90) |
| Dom 15/11 | **Simulado 2** | P3 + P2 (130) | P3 ≥ 65% · P2 ≥ 60% |
| Dom 22/11 | **Simulado 3** | Completo 170 + discursiva | NFPO ≥ 60% (156/260) |
| Dom 29/11 | **Simulado 4** | Completo + discursiva (real) | NFPO ≥ 70% (182/260) · P3 ≥ 70% · disc ≥ 65 |
| Sáb 5/12 | **Simulado 5** | Completo + discursiva | NFPO ≥ 75% (195/260) · P3 ≥ 75% (135/180) · disc ≥ 75 |
| Qui 10/12 | Sim leve | 30–40 itens (temas fortes) | Confiança/ritmo (sem meta) |

**Meta final:** **NFC ≥ 15–16** (≈75–80% líquido), visando ficar confortavelmente dentro das vagas (referência: corte do TCU 2026 TI ≈ 71%; Cargo 4 com apenas 10 vagas imediatas).

**Cenários de referência (estimativa de nota de corte):** mínimo p/ não ser eliminado ≈ NFC 8 (40%) · aprovação CR ≈ 12–14 (60–70%) · boa colocação (top 5–10) ≈ 15–17 (75–85%) · topo ≈ 17–19 (85–95%).

---

## 7. Fontes

**Arquivos do vault (base deste plano)**
- `60 - Análises/Incidência TI - Cruzamento provas x edital CGU 2026 (Cargo 4).md` — painel de incidência (663 itens / 13 concursos).
- `50 - Questões/TI/Taxonomia - TI.md` — taxonomia E1–E4.
- `Ed_1_2026_CGU_Abertura.md` — itens 7, 8 (8.11), 9 (9.7), 11, 12 e 15.2.2/15.2.3/15.2.4 (Cargo 4).
- `60 - Análises/Análise - Modelo e pontuação da prova (CGU 2026).md` — estrutura, pontuação, mínimos, discursiva, NFC.
- `60 - Análises/Estimativa de nota de corte - CGU 2026 (Cargo 4).md` — cenários de NFC e metas por prova.
- `60 - Análises/Incidência CEBRASPE - Conhecimentos Básicos.md` · `...Complementares.md` · `...Específicos (Cargo 4 - TI).md` · `Análise de Incidência CEBRASPE - CGU 2026 (visão geral).md`.
- `50 - Questões/TI/Incidência/` — dados brutos do cruzamento. `40 - Flashcards/` — baralhos existentes.

**Edital e concurso (oficial)**
- Edital nº 1/2026 – CGU – AFFC: <https://cdn.cebraspe.org.br/concursos/cgu_26_affc/arquivos/C7A60D15CB0DDDFA92233056D728C555505D6B935D7048646D49445EB346F825.pdf>
- Página oficial (Cebraspe): <https://www.cebraspe.org.br/concursos/cgu_26_affc>

**Provas-alvo para questões e simulados (Cebraspe)**
- TCU 2015 e 2026 (AUFC – Auditoria de TI); FUNPRESP-JUD 2026 (Dev. de Sistemas); BANRISUL 2022; BDMG 2025; Bacen 2024; TCE-MG/RN/RS/MS/PR 2024–2026; TELEBRAS 2025; INPI 2023; CGU 2021 (FGV, referência de "o que a CGU gosta").

**Referências de incidência citadas nos arquivos-fonte**
- Estratégia — Raio-X "TCU – Auditor de TI" (Cebraspe 2021–2025) e "TI: temas quentes Cebraspe".
- QConcursos / TecConcursos / Gran Questões — distribuição por disciplina e priorização de assuntos.
- Decorando a Lei Seca — artigos mais cobrados (LAI/LGPD, Lei 9.784, Lei 8.429).
- IIA — Modelo das Três Linhas (2020); CGU — IN SFC/CGU nº 3/2017 (Normas de Auditoria Interna).
