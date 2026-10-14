---
tipo: moc
disciplina: "Fundamentos de Evidências, Dados e Inteligência Artificial"
status: novo
data: "2026-10-13"
tags:
  - moc
  - complementar
  - cgu-2026
---

# Fundamentos de Evidências, Dados e Inteligência Artificial

> **Conhecimentos complementares** — Edital nº 1/2026 – CGU – AFFC (Cargo 4 – TI/Desenvolvimento de Sistemas).
> Texto integral do edital: [[Ed_1_2026_CGU_Abertura]].

## Itens do edital (checklist)

### 1 Perguntas e fontes

- [ ] 1.1 Relação entre problema, pergunta e informação necessária
- [ ] 1.1 Fontes documentais, administrativas, estatísticas e de participação social
- [ ] 1.2 Distinção entre dado, evidência, interpretação e juízo de valor
- [ ] 1.2 Verificação de origem e confronto de fontes

### 2 Leitura de dados e indicadores

- [ ] 2.1 Interpretação de tabelas, gráficos, proporções, taxas e medidas descritivas
- [ ] 2.1 Denominadores, qualidade e comparabilidade
- [ ] 2.2 Distinção entre indicadores de percepção, experiência, denúncias, detecção e sanções na análise da corrupção
- [ ] 2.2 Subnotificação e limites de inferência sobre sua ocorrência

### 3 Inferências e erros de raciocínio

- [ ] 3.1 Associação e causalidade
- [ ] 3.1 Seleção e representatividade
- [ ] 3.1 Explicações alternativas e incerteza
- [ ] 3.2 Generalizações indevidas, falácia ecológica e viés de confirmação
- [ ] 3.2 Falsos positivos e falsos negativos

### 4 Integridade da evidência e proteção

- [ ] 4.1 Rastreabilidade e verificação de informações
- [ ] 4.1 Comunicação proporcional dos resultados e limites
- [ ] 4.2 Escuta sem indução, confidencialidade e risco de identificação indireta.
- [ ] 4.3 Distinção entre as condições e os regimes de proteção de entrevistados em auditoria, participantes de pesquisa e denunciantes.

### 5 Uso responsável de inteligência artificial

- [ ] 5.1 Possibilidades de classificação, busca, síntese e apoio à análise
- [ ] 5.1 Escolha entre IA, solução simples e revisão humana
- [ ] 5.2 Erros, conteúdo não sustentado, vieses e efeitos sobre grupos
- [ ] 5.2 Proteção de informações, supervisão, rastreabilidade e contestação
- [ ] 5.3 Verificação de fontes e limites da automação de decisões que afetam direitos.

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
