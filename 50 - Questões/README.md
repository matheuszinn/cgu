---
tipo: índice
tags:
  - cgu-2026
  - questoes
---

# 50 - Questões

Organização por **disciplina**, e dentro de cada uma por **etapa do pipeline**.

```
50 - Questões/
├── TI/
│   ├── Taxonomia - TI.md          ← taxonomia do edital (E1–E4, Cargo 4)
│   ├── Incidência/                ← cruzamento provas × edital, por concurso (.md + .json)
│   └── Banco/                     ← banco de questões (itens com enunciado + gabarito)
│       ├── _banco_TI_completo.json
│       ├── <concurso>.json
│       └── README.md
├── Direito/
│   ├── Taxonomia - Direito.md     ← taxonomia jurídica do edital (D1–D10)
│   ├── Incidência/                ← cruzamento provas × edital, por concurso (.md + .json)
│   └── Banco/                     ← banco de questões (itens com enunciado + gabarito)
│       ├── _banco_Direito_completo.json
│       ├── <concurso>.json
│       └── README.md
└── README.md
```

## Como usar

- **Quer saber o que mais cai?** → `Incidência/` (por concurso) + os painéis consolidados em `60 - Análises/`.
- **Quer treinar?** → `Banco/` (`_banco_*_completo.json` tem tudo; os arquivos por concurso permitem filtrar).
- **Quer classificar algo novo?** → `Taxonomia - *.md`.

## Números

| Disciplina | Itens | Com gabarito | Anulados | Arquivos por concurso |
|---|--:|--:|--:|--:|
| **TI** (E1–E4) | 663 | 626 | 37 | 13 |
| **Direito** (D1–D10) | 1.400 | 1.332 | 68 | 17 |

> Painéis consolidados: `60 - Análises/Incidência TI - …md` e `60 - Análises/Incidência Direito - …md`.
