---
tipo: moc
disciplina: "Engenharia, Arquitetura e Governança de Dados"
status: novo
data: "2026-11-03"
tags:
  - moc
  - especifico
  - cgu-2026
  - cargo-2
---

# Engenharia, Arquitetura e Governança de Dados

> **Conhecimentos específicos** — Cargo 2: TI / Ciência de Dados — Edital nº 1/2026 – CGU – AFFC.
> Texto integral do edital: [[Edital CGU 2026 (texto integral)]].

## Itens do edital (checklist)

### 1 Modelagem e arquiteturas

- [x] 1.1 Modelos relacional, documental, chave-valor, multidimensional e vetorial; normalização e integridade; transações e consistência.
- [x] 1.2 Data warehouse, data mart, data lake e lakehouse; produtos de dados, responsabilidade por domínios, autosserviço e governança federada em data mesh.

### 2 SQL e consultas analíticas

- [x] 2.1 Definição e manipulação de dados, controle de acesso e transações; filtros, junções, agregações, subconsultas, expressões de tabela comuns e funções de janela.
- [x] 2.2 Índices, planos de execução e desempenho; valores nulos, duplicações e erros de interpretação em consultas.

### 3 Ingestão e integração

- [x] 3.1 ETL e ELT; processamento em lote e fluxo, completo e incremental; APIs e contratos de dados; formatos CSV, JSON, XML e Parquet; interoperabilidade semântica e técnica; falhas, repetição de processamento e consistência.

### 4 Processamento distribuído

- [x] 4.1 Particionamento, paralelismo, movimentação de dados e execução distribuída de transformações e junções.
- [x] 4.2 Escalabilidade, tolerância a falhas e custo.
- [x] 4.3 Planos de execução.
- [x] 4.4 Assimetria entre partições e resultados inconsistentes.

### 5 Qualidade e rastreabilidade

- [x] 5.1 Metadados, catálogo e linhagem.
- [x] 5.2 Completude, consistência, validade, unicidade, acurácia e atualidade.
- [x] 5.3 Perfilamento, deduplicação, vinculação de registros e enriquecimento.
- [x] 5.4 Conciliação de fontes.
- [x] 5.5 Riscos de correspondências incorretas entre pessoas ou entidades.

### 6 Compartilhamento e proteção

- [x] 6.1 Minimização, segregação de ambientes e privilégios.
- [x] 6.2 Retenção e descarte.
- [x] 6.3 Anonimização, pseudonimização e reidentificação.
- [x] 6.4 Publicação, reutilização e compartilhamento controlados.
- [x] 6.5 Proteção de dados pessoais e equilíbrio entre utilidade analítica, abertura e proteção de pessoas.

## Notas atômicas

```dataview
TABLE status AS "Status", tema AS "Tema"
FROM "20 - Notas"
WHERE disciplina = this.disciplina
SORT status ASC, file.name ASC
```

## Resumos

```dataview
TABLE status AS "Status", tema AS "Tema"
FROM "30 - Resumos"
WHERE disciplina = this.disciplina
SORT file.name ASC
```

## Flashcards

```dataview
LIST FROM "40 - Flashcards"
WHERE disciplina = this.disciplina
SORT file.name ASC
```

## Questões

```dataview
TABLE resultado AS "Resultado", fonte AS "Fonte"
FROM "50 - Questões"
WHERE disciplina = this.disciplina
SORT file.name ASC
```

## Pendências

- [ ]
