---
tipo: referência
banca: Cebraspe
tags:
  - cgu-2026
  - banco-de-questoes
  - direito
---

# Banco de questões — CGU 2026 · Direito

Banco montado a partir das **provas objetivas** de 17 concursos Cebraspe, com os itens de **Direito**
classificados pela taxonomia `50 - Questões/_taxonomia CGU 2026 (Direito).md` (recorte jurídico dos itens 15.2.2 e 15.2.3 do edital).

- **Arquivo único (consolidado):** `_banco_Direito_completo.json`
- **Por concurso:** `<concurso>.json` (17 arquivos)

## Números

- **1.400 itens** de Direito.
- **1.332 com gabarito** (C/E ou letra A–E) · **68 anulados** (`anulado: true`, `gabarito: null`).
- Distribuição de gabaritos: **C 524 · E 481** (Cebraspe ~50/50) + A 102 · B 97 · D 128 (múltipla escolha).

### Por tema
| Código | Tema | Itens |
|---|---|--:|
| D1 | Ordem constitucional, Estado e direitos | 288 |
| D5 | Controle e responsabilização | 251 |
| D9 | Licitações e contratos (Lei 14.133) | 247 |
| D3 | Administração pública e agentes | 186 |
| D8 | Governança, riscos e integridade | 116 |
| D4 | Decisão e processo administrativo | 91 |
| D2 | Ética pública e responsabilidade profissional | 62 |
| D6 | Transparência, acesso à informação e ouvidoria | 56 |
| D10 | Improbidade e anticorrupção | 54 |
| D7 | Proteção de dados pessoais (LGPD) | 49 |

### Por concurso
| Concurso | Itens | | Concurso | Itens |
|---|--:|---|---|--:|
| `anm_24` | 234 | | `tcu_25_aufc` | 58 |
| `seplad_df_22_auditor` | 175 | | `inpi_23` | 56 |
| `telebras_25` | 136 | | `tce_pr_24_auditor` | 51 |
| `CGE_CE_18` | 134 | | `tce_rs_25` | 45 |
| `tce_rn_25` | 125 | | `tce_mg_25` | 39 |
| `funpresp_26_jud` | 110 | | `sefaz_se_25_auditor` | 27 |
| `tce_ms_25` | 108 | | `sefaz_rn_25_auditor` | 24 |
| `tcu_25_tefc` | 71 | | `bcb_24` | 5 · `PREF_JP_17_CGM` | 2 |

## Formato de cada item

```json
{
  "id": "especificos-190",
  "concurso": "tcu_25_aufc",
  "tema": "D5",
  "assunto": "Controle externo e competências do TCU",
  "enunciado": "Texto completo do item...",
  "gabarito": "C",
  "anulado": false,
  "fonte": "TCU 2025 (AUFC) — Conhecimentos Específicos — item 190",
  "alternativas": {"A": "...", "B": "..."}   // só em provas de múltipla escolha
}
```

## Notas de qualidade

- Os `.md` vinham de PDF em **2 colunas** e estavam embaralhados; os agentes recuperaram o texto dos **PDFs originais** (`pdftotext -layout` / `-raw` / `-bbox`) e reconstruíram a numeração.
- Gabaritos conferidos contra os **gabaritos oficiais definitivos** (PDFs); `X` → anulado. Vários `.md` de gabarito estavam desalinhados/truncados e foram corrigidos pelo PDF (ex.: `sefaz_rn_25`, `tce_ms_25`, `tce_mg_25`, `seplad_df_22`).
- **Correções de numeração** aplicadas em: `tce_pr_24_auditor` (Cargo 6, 52–55), `sefaz_se_25` (48/51), `tce_mg_25`, `tce_ms_25` (CE1).
- **Ressalva de duplicação:** as provas de "conhecimentos gerais/básicos" se repetem entre grupos de cargos em vários concursos; os itens foram contados **por arquivo** (a incidência relativa por tema permanece válida).

## Uso

`_banco_Direito_completo.json` pode ser filtrado por `tema`/`concurso` ou embaralhado para gerar simulados no formato do edital (Certo/Errado e múltipla escolha).
