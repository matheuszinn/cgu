---
tipo: moc
disciplina: "Estatística, Programação e Análise de Dados"
status: novo
data: "2026-11-03"
tags:
  - moc
  - especifico
  - cgu-2026
  - cargo-2
---

# Estatística, Programação e Análise de Dados

> **Conhecimentos específicos** — Cargo 2: TI / Ciência de Dados — Edital nº 1/2026 – CGU – AFFC.
> Texto integral do edital: [[Edital CGU 2026 (texto integral)]].

## Itens do edital (checklist)

### 1 Exploração e descrição

- [x] 1.1 Tipos de dados e variáveis; distribuições de frequências, medidas de posição e dispersão; exploração e visualização; comparação de grupos e períodos; identificação de padrões, anomalias e limites das fontes.

### 2 Probabilidade e inferência

- [x] 2.1 Probabilidade e distribuições em aplicações; amostragem, estimação, intervalos de confiança e testes de hipóteses.
- [x] 2.2 Pressupostos, incerteza e erros de inferência; significância estatística e relevância prática.

### 3 Relações entre variáveis

- [x] 3.1 Correlação, regressão e análise de variância; pressupostos, tamanho de efeito e interpretação de resultados.
- [x] 3.2 Associação, predição e causalidade; seleção, representatividade e explicações alternativas em dados administrativos.

### 4 Programação para análise

- [x] 4.1 Python 3: estruturas de dados, controle de fluxo, funções, módulos, arquivos e exceções; leitura, análise e depuração de rotinas de manipulação de dados; organização modular, testes e reprodutibilidade de análises.

### 5 Preparação e transformação

- [x] 5.1 Valores ausentes, inconsistências, duplicações, outliers e desbalanceamento; transformação, codificação, normalização e padronização; engenharia e seleção de atributos; prevenção de vazamento de informação na preparação dos dados.

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
