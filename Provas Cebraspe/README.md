# Provas e Gabaritos — Concursos Cebraspe (similares à CGU AFFC)

> Baixados automaticamente das páginas oficiais da Cebraspe (API `apis.cebraspe.org.br` + CDN `cdn.cebraspe.org.br`) em **15/10/2026**.
> Cada subpasta corresponde a um concurso e contém os PDFs de **prova** e **gabarito** publicados.
> **Total: 550 PDFs válidos** (integridade verificada: assinatura `%PDF`).

## Concursos com provas/gabaritos baixados

| Pasta (slug) | Concurso | PDFs |
|---|---|:--:|
| `anm_24` | Agência Nacional de Mineração (ANM) | 104 |
| `tce_rn_25` | TCE-RN (Auditor de Controle Externo) | 70 |
| `telebras_25` | Telebrás (Analista de TI, entre outros) | 62 |
| `tce_mg_25` | TCE-MG (Controle Externo) | 42 |
| `inpi_23` | INPI (Analista, inclui TI) | 41 |
| `funpresp_26_jud` | FUNPRESP-JUD 26 (inclui Desenvolvimento de Sistemas) | 32 |
| `tce_ms_25` | TCE-MS (Controle Externo) | 28 |
| `tce_pr_24_auditor` | TCE-PR (Auditor de Controle Externo) | 26 |
| `sefaz_se_25_auditor` | SEFAZ-SE (Auditor Fiscal) | 24 |
| `tce_rs_25` | TCE-RS (Auditor/Oficial de Controle Externo) | 21 |
| `seplad_df_22_auditor` | SEPLAD-DF / CGDF (Auditor de Controle Interno) | 20 |
| `CGE_CE_18` | CGE-CE (Auditor de Controle Interno — inclui TI) | 16 |
| `bcb_24` | Banco Central (Analista — TI) | 15 |
| `PREF_JP_17_CGM` | Prefeitura de João Pessoa / CGM (Auditor de Controle Interno) | 15 |
| `cd_25_ns` | Câmara dos Deputados 25 (Analista/Técnico Legislativo) | 10 |
| `sefaz_rn_25_auditor` | SEFAZ-RN (Auditor Fiscal) | 7 |
| `tcu_25_aufc` | **TCU 25 AUFC (Auditoria de TI)** | 6 |
| `cd_26_pl` | Câmara dos Deputados 26 (Policial Legislativo) | 6 |
| `tcu_25_tefc` | TCU 25 TEFC (Técnico de Controle Externo) | 5 |
| | **TOTAL** | **550** |

## Concursos ainda SEM prova/gabarito publicado (em 15/10/2026)

| Slug | Concurso | Motivo |
|---|---|---|
| `cgu_26_affc` | **CGU 26 AFFC** (o próprio) | prova em **13/12/2026** — ainda não aplicada |
| `tce_ma_26` | TCE-MA | prova/gabarito ainda não publicados |
| `sefaz_al_26` | SEFAZ-AL 26 | inscrições/prova em andamento |
| `cd_26_analista` | Câmara dos Deputados 26 (Analista) | prova/gabarito ainda não publicados |

> Quando esses concursos publicarem prova/gabarito, basta rodar novamente o script (`/tmp/opencode/baixar_cebraspe.sh <slug>`).

## Como foi feito
1. API da Cebraspe: `https://apis.cebraspe.org.br/cebraspe/eventos/<slug>` (retorna `arquivosGabarito` e `arquivosEdital`).
2. Download: `https://cdn.cebraspe.org.br/concursos/<slug>/arquivos/<nomeArquivo>`.
3. Script: `/tmp/opencode/baixar_cebraspe.sh` (baixa os PDFs cujas descrições começam por `PROVA`, `GABARITO` ou `PADRÃO`).

## Nomes de arquivo
Os arquivos foram renomeados a partir da descrição oficial (ex.: `PROVA OBJETIVA CONHECIMENTOS ESPECIFICOS.pdf`, `GABARITO DEFINITIVO CONHECIMENTOS BASICOS.pdf`, `PADRAO DEFINITIVO DE RESPOSTA PROVA DISCURSIVA.pdf`). Acentos foram removidos para evitar problemas de compatibilidade.

## Fonte
- Página geral de concursos da Cebraspe: <https://www.cebraspe.org.br/concursos>
- Lista de concursos similares: [[Concursos similares (Cebraspe) - CGU AFFC]]
