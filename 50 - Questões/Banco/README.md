---
tipo: referência
banca: Cebraspe
tags:
  - cgu-2026
  - banco-de-questoes
  - TI
---

# Banco de questões — CGU 2026 · Cargo 4 (TI / Desenvolvimento de Sistemas)

Banco de questões montado a partir das **provas específicas de TI** de 13 concursos Cebraspe,
classificadas pela taxonomia do edital (`50 - Questões/_taxonomia CGU 2026 (Cargo 4 - TI).md`).

- **Arquivo único (consolidado):** `_banco_TI_completo.json`
- **Por concurso:** `<concurso>.json` (13 arquivos)

## Números

- **663 itens** de TI (todos os que casam com o edital do Cargo 4).
- **626 com gabarito** (C/E ou letra A–E) · **37 anulados** (`anulado: true`, `gabarito: null`).
- Distribuição de gabaritos: **C 276 · E 275** (Cebraspe ~50/50) + A 28 · B 26 · D 21 (múltipla escolha).

### Por bloco do edital
| Bloco | Itens |
|---|--:|
| **E4** Desenvolvimento Seguro, Qualidade e Entrega | 228 |
| **E3** Persistência, Integração e Proteção de Dados | 199 |
| **E2** Arquitetura e Integração de Sistemas | 190 |
| **E1** Engenharia de Software e Programação | 46 |

### Por tema
| Tema | Itens |
|---|--:|
| E4.5 Contratação e fiscalização | 84 |
| E3.1 Modelagem e persistência | 73 |
| E3.4 Privacidade e segurança de dados | 72 |
| E2.5 Confiabilidade das aplicações | 71 |
| E4.4 Gestão de produtos e governança | 69 |
| E2.4 Integração com dados e IA | 62 |
| E2.2 APIs e identidade | 35 |
| E4.1 Segurança de aplicações | 33 |
| E3.2 SQL e desempenho | 32 |
| E3.3 Fluxos e interoperabilidade | 22 |
| E4.3 Entrega e operação | 22 |
| E4.2 Testes e qualidade | 20 |
| E1.1 Problemas e requisitos | 18 |
| E1.2 Programação e correção | 17 |
| E2.1 Arquiteturas de aplicações | 16 |
| E1.4 Interfaces e experiência do usuário | 9 |
| E2.3 Comunicação e consistência | 6 |
| E1.3 Concorrência e processamento | 1 |
| E1.5 Manutenção e evolução | 1 |

### Por concurso
| Concurso | Itens |
|---|--:|
| `funpresp_26_jud` (emp. 9–11) | 115 |
| `anm_24` (cargos 24–26) | 87 |
| `tce_rn_25` (cargos 4, 5, 12) | 71 |
| `tcu_25_aufc` | 71 |
| `tce_rs_25` (cargo 4) | 58 |
| `inpi_23` (cargos 9–11) | 46 |
| `tce_ms_25` (cargo 5) | 44 |
| `tce_pr_24_auditor` (cargo 5) | 38 |
| `telebras_25` (cargo 2) | 35 |
| `bcb_24` (cargo 2) | 32 |
| `tce_mg_25` (cargo 1) | 30 |
| `sefaz_se_25_auditor` (esp. 2) | 27 |
| `CGE_CE_18` (cargo 3) | 9 |

## Formato de cada item

```json
{
  "id": "C4-100",
  "concurso": "tce_rn_25",
  "tema": "E3.1",
  "assunto": "Modelagem relacional e normalização",
  "enunciado": "Texto completo do item...",
  "gabarito": "C",
  "anulado": false,
  "fonte": "TCE-RN 2025 — Cargo 4 — item 100",
  "alternativas": [{"letra": "A", "texto": "..."}]   // só em provas de múltipla escolha
}
```

## Notas de qualidade

- Os `.md` de várias provas vinham de PDF em **2 colunas** e estavam embaralhados; os agentes recuperaram o texto dos **PDFs originais** (`pdftotext -layout`).
- Gabaritos conferidos contra os **gabaritos oficiais definitivos**; `X` → anulado.
- **Correções aplicadas** (itens que o cruzamento havia trocado): `tce_mg_25` (itens 48/53), `tce_ms_25` (44/45, 91/96, 74/77/80) e `tce_pr_24_auditor` (89/94).
- Ressalvas: 8 itens têm enunciado muito curto (< 60 caracteres) e podem ser artefato de extração; a interpretação de **E2.4** segue frouxa para IA/ML (ver ressalva no painel de incidência).

## Uso

O arquivo `_banco_TI_completo.json` pode ser filtrado por `tema`, `concurso` ou embaralhado para gerar simulados no formato do edital (Certo/Errado).
