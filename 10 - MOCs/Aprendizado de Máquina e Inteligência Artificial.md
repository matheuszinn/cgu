---
tipo: moc
disciplina: "Aprendizado de Máquina e Inteligência Artificial"
status: novo
data: "2026-11-03"
tags:
  - moc
  - especifico
  - cgu-2026
  - cargo-2
---

# Aprendizado de Máquina e Inteligência Artificial

> **Conhecimentos específicos** — Cargo 2: TI / Ciência de Dados — Edital nº 1/2026 – CGU – AFFC.
> Texto integral do edital: [[Edital CGU 2026 (texto integral)]].

## Itens do edital (checklist)

### 1 Seleção e construção de modelos

- [x] 1.1 Aprendizado supervisionado e não supervisionado; noções e limites de abordagens semissupervisionadas e por reforço.
- [x] 1.2 Regressão, classificação, agrupamento, redução de dimensionalidade e detecção de anomalias; regularização, ensembles, sobreajuste e subajuste; comparação com soluções simples.

### 2 Validação e generalização

- [x] 2.1 Separação de treino, validação e teste.
- [x] 2.2 Validação cruzada e temporal.
- [x] 2.3 Vazamento de informação.
- [x] 2.4 Viés e variância.
- [x] 2.5 Generalização e estabilidade dos resultados.
- [x] 2.6 Comparação de modelos e adequação ao uso pretendido.

### 3 Métricas e efeitos das decisões

- [x] 3.1 Precisão, sensibilidade, especificidade, calibração e métricas de regressão.
- [x] 3.2 Custos dos falsos positivos e falsos negativos.
- [x] 3.3 Desempenho por grupos, discriminação e incerteza.
- [x] 3.4 Explicabilidade e interpretabilidade.
- [x] 3.5 Limites do uso de escores para priorização e tomada de decisão.

### 4 Redes neurais

- [x] 4.1 Perceptron e redes multicamadas.
- [x] 4.2 Funções de ativação e perda, otimização, retropropagação e regularização em nível conceitual e de interpretação de resultados.
- [x] 4.3 Redes convolucionais, recorrentes e transformers.
- [x] 4.4 Adequação ao tipo de dado, custo, limitações e alternativas.
- [x] 4.5 Transferência de aprendizado e ajuste de modelos.

### 5 Linguagem natural e modelos generativos

- [x] 5.1 Pré-processamento e classificação de textos.
- [x] 5.2 Representações vetoriais, embeddings e similaridade semântica.
- [x] 5.3 Modelos de linguagem e LLMs.
- [x] 5.4 Prompts, recuperação de informação para geração de respostas e ajuste de modelos.
- [x] 5.5 Avaliação de respostas, fontes, alucinações e limitações.

### 6 Agentes e uso seguro de ferramentas

- [x] 6.1 Agentes de IA e integração com ferramentas e fontes.
- [x] 6.2 Autorização, rastreabilidade e supervisão.
- [x] 6.3 Proteção contra instruções maliciosas em conteúdo externo, exposição de dados e uso indevido de ferramentas.
- [x] 6.4 Avaliação dos resultados e limites de autonomia.

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
