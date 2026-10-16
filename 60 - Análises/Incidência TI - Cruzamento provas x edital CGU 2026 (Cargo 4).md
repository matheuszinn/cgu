---
tipo: análise
banca: Cebraspe
data: "2026-10-16"
tags:
  - analise
  - incidencia
  - cgu-2026
  - TI
---

# Incidência TI — Cruzamento provas × edital CGU 2026 (Cargo 4)

> **Método:** leitura apenas das **provas objetivas específicas de TI** (sem gabaritos) de 13 concursos Cebraspe, classificando cada item na taxonomia do **item 15.2.4 do Edital nº 1/2026 – CGU – AFFC (Cargo 4: TI/Desenvolvimento de Sistemas)**.
> Itens de assunto alheio ao edital (redes/infra, SO, ITIL/COBIT/PMBOK, ISO 27001/27002, gestão de projetos, Office, etc.) foram **descartados**.
> Taxonomia: `50 - Questões/TI/Taxonomia - TI.md` · Dados brutos: `50 - Questões/TI/Incidência/`.

## 1. Números gerais

- **13 concursos** com prova específica de TI.
- **663 itens de TI** selecionados (de ≈ 850 itens numerados lidos).
- Distribuição por bloco do edital:

| Bloco | Tema | Itens | % |
|---|---|--:|--:|
| **E4** | Desenvolvimento Seguro, Qualidade e Gestão da Entrega | **228** | 34% |
| **E3** | Persistência, Integração e Proteção de Dados | **199** | 30% |
| **E2** | Arquitetura e Integração de Sistemas | **190** | 29% |
| **E1** | Engenharia de Software e Programação | **46** | 7% |

## 2. Ranking por tema (todos os concursos)

| # | Tema | Itens |
|--:|---|--:|
| 1 | **E4.5** Contratação e fiscalização de soluções | **84** |
| 2 | **E3.1** Modelagem e persistência | **73** |
| 3 | **E3.4** Privacidade e segurança de dados | **72** |
| 4 | **E2.5** Confiabilidade das aplicações | **71** |
| 5 | **E4.4** Gestão de produtos e governança | **69** |
| 6 | **E2.4** Integração com dados e IA | **62** |
| 7 | **E2.2** APIs e identidade | **35** |
| 8 | **E4.1** Segurança de aplicações | **33** |
| 9 | **E3.2** SQL e desempenho | **32** |
| 10 | **E3.3** Fluxos e interoperabilidade | **22** |
| 11 | **E4.3** Entrega e operação | **22** |
| 12 | **E4.2** Testes e qualidade | **20** |
| 13 | **E1.1** Problemas e requisitos | **18** |
| 14 | **E1.2** Programação e correção | **17** |
| 15 | **E2.1** Arquiteturas de aplicações | **16** |
| 16 | **E1.4** Interfaces e experiência do usuário | **9** |
| 17 | **E2.3** Comunicação e consistência | **6** |
| 18 | **E1.3** Concorrência e processamento | **1** |
| 19 | **E1.5** Manutenção e evolução | **1** |

## 3. Por concurso

| Concurso | Itens TI | Destaques |
|---|--:|---|
| `funpresp_26_jud` (emp. 9–11) | 115 | E3.4(28), E2.5(19), E3.1(17), E4.1(9), E3.2(8) |
| `anm_24` (cargos 24–26) | 87 | E2.4(28), E4.5(11), E2.5(10), E1.1(8) |
| `tce_rn_25` (cargos 4, 5, 12) | 71 | E4.5(14), E3.1(11), E4.4(8), E3.4(7) |
| `tcu_25_aufc` (Auditoria de TI) | 71 | E4.5(13), E2.2(9), E2.4(8), E2.5(7), E4.3(7) |
| `tce_rs_25` (cargo 4) | 58 | E3.4(9), E4.4(9), E3.1(7), E1.2(5) |
| `inpi_23` (cargos 9–11) | 46 | E4.1(9), E3.4(8), E4.4(8), E4.2(5) |
| `tce_ms_25` (cargo 5) | 44 | E4.5(20), E3.1(7), E3.2(4) |
| `tce_pr_24_auditor` (cargo 5) | 38 | E4.4(6), E2.4(5), E2.5(5), E3.4(5), E4.5(5) |
| `telebras_25` (cargo 2) | 35 | E4.5(10), E4.4(8), E3.1(4) |
| `bcb_24` (cargo 2) | 32 | E2.5(13), E1.2(3), E2.3(3), E3.1(3), E4.4(3) |
| `tce_mg_25` (cargo 1) | 30 | E3.1(6), E2.4(5), E4.4(5), E3.2(4) |
| `sefaz_se_25_auditor` (esp. 2) | 27 | E4.5(5), E2.4(4), E2.5(4), E4.4(4) |
| `CGE_CE_18` (cargo 3) | 9 | E2.1(2), E4.2(2) |

## 4. Leitura para a estratégia

1. **O edital cobra "engenharia de produto + dados + entrega"**, não a TI clássica de infraestrutura. Contratação de soluções (**E4.5**, 84 itens — 1º lugar), persistência (**E3.1**, 73), privacidade/LGPD (**E3.4**, 72), confiabilidade/cloud/contêineres (**E2.5**, 71) e governança/PDTIC/Scrum (**E4.4**, 69) dominam.
2. **Banco de dados é o núcleo técnico:** E3.1 + E3.2 + E3.3 = **127 itens** (19%).
3. **Segurança/privacidade:** E3.4 + E4.1 = **105 itens** (16%).
4. **Arquitetura/APIs:** E2.2 + E2.1 = 51 itens; OAuth/OIDC, tokens, Spring Security e versionamento de API aparecem bastante (E2.2).
5. **IA/dados:** E2.4 com 62 itens — em grande parte por causa do `anm_24` (3 cargos de TI, incl. Ciência de Dados). Ver ressalva abaixo.
6. **Programação pura (Java/Vue/estruturas) é minoria** (E1.2 = 17) nas provas destes concursos — mas é justamente o que o edital do Cargo 4 detalha; não descuidar.

## 5. Ressalvas e decisões de método

- **IA/ML → E2.4:** itens de *teoria* de ML/mineração foram classificados em E2.4 (único código de IA). O edital trata E2.4 como **integração** com dados/LLM (RAG, agentes, vetores). Interpretação estrita reduziria E2.4 em ~37 itens (→ "fora"), afetando principalmente `anm_24`, `tce_pr_24_auditor`, `tce_mg_25` e `sefaz_se_25_auditor`.
- **Perda de itens na extração:** os `.md` vêm de PDF em 2 colunas e alguns enunciados ficaram sem numeração/mesclados. Vários agentes recuperaram o texto do PDF original. Ainda assim, os totais são **piso**, não teto (ex.: `funpresp_26_jud`, `anm_24`, `tce_rs_25`).
- **Numeração repetida:** em `inpi_23` e `funpresp_26_jud` a numeração reinicia por prova; os itens foram prefixados por cargo/emprego.
- **Fora do edital (descartados):** redes/infra, SO, ITIL/COBIT/PMBOK/MPS.BR, ISO 27001/27002/27005, gestão de projetos, Office, hardware, ciência de dados pura etc.

## Fontes

- Edital nº 1/2026 – CGU – AFFC, item **15.2.4** (Conhecimentos Específicos – Cargo 4).
- Provas em `Provas/Relevantes (CGU AFFC)/`; cruzamentos em `50 - Questões/TI/Incidência/`.
