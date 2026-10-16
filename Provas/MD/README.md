# Provas e Gabaritos em Markdown — Concursos Cebraspe

> Versão **`.md`** (texto extraído dos PDFs) das provas e gabaritos baixados de concursos da Cebraspe similares à **CGU AFFC**.
> Conversão/reescrita feita com `pdftotext` em **15/10/2026**. **Total: 550 arquivos `.md`**.
>
> **Formatação aplicada:** cabeçalhos/rodapés de página removidos; itens das provas re-fluxados (número em **negrito**); enunciados-comando ("Julgue…") em _itálico_; seções como títulos (`##`); provas de múltipla escolha com `### QUESTÃO N`; **gabaritos convertidos em tabela Markdown** (`| Item | Gabarito |`).
>
> **Limitação:** a ordem dos itens pode não ser perfeita em algumas provas, por causa do layout em **duas colunas** do PDF (limitação da extração de texto). Os PDFs originais estão em `Provas/PDF/`.
> Os PDFs originais estão em `Provas/PDF/`. Aqui o conteúdo é **pesquisável e linkável no Obsidian**.

## Estrutura
Cada arquivo `.md` traz um cabeçalho (frontmatter) com `tipo: prova`, o `concurso` (slug), o `arquivo_origem` (PDF) e a tag `#cebraspe` — e, abaixo, o texto da prova/gabarito.

## Concursos convertidos

| Pasta (slug) | Concurso | Arquivos `.md` |
|---|---|:--:|
| `anm_24` | ANM | 104 |
| `tce_rn_25` | TCE-RN | 70 |
| `telebras_25` | Telebrás | 62 |
| `tce_mg_25` | TCE-MG | 42 |
| `inpi_23` | INPI | 41 |
| `funpresp_26_jud` | FUNPRESP-JUD 26 | 32 |
| `tce_ms_25` | TCE-MS | 28 |
| `tce_pr_24_auditor` | TCE-PR | 26 |
| `sefaz_se_25_auditor` | SEFAZ-SE | 24 |
| `tce_rs_25` | TCE-RS | 21 |
| `seplad_df_22_auditor` | SEPLAD-DF (CGDF) | 20 |
| `CGE_CE_18` | CGE-CE | 16 |
| `bcb_24` | Banco Central | 15 |
| `PREF_JP_17_CGM` | Pref. João Pessoa/CGM | 15 |
| `cd_25_ns` | Câmara dos Deputados 25 | 10 |
| `sefaz_rn_25_auditor` | SEFAZ-RN | 7 |
| `tcu_25_aufc` | **TCU 25 AUFC (Auditoria de TI)** | 6 |
| `cd_26_pl` | Câmara 26 Policial | 6 |
| `tcu_25_tefc` | TCU 25 TEFC | 5 |
| | **TOTAL** | **550** |

## Provas com foco no mesmo assunto (prioridade de estudo)
Conforme [[Concursos similares (Cebraspe)]] (seção "Como aproveitar essas provas"):

1. **Específicos de TI (Desenvolvimento):** `tcu_25_aufc`, `bcb_24`, `funpresp_26_jud`.
2. **Controle interno / integridade:** `CGE_CE_18`, `seplad_df_22_auditor`, `PREF_JP_17_CGM`.
3. **Controle externo / tribunais:** `tce_rn_25`, `tce_rs_25`, `tce_mg_25`, `tce_ms_25`, `tce_pr_24_auditor`.
4. **Fiscal / finanças:** `sefaz_se_25_auditor`, `sefaz_rn_25_auditor`.

> Dica: no Obsidian, use a busca global (ou o painel de busca) por termos como "Julgue", "OWASP", "Spring", "LGPD", "improbidade" para localizar rapidamente os itens.
