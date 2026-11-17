---
tipo: moc
disciplina: "Estado, Democracia, Direitos e Ciência Política"
status: novo
data: "2026-10-13"
tags:
  - moc
  - basico
  - cgu-2026
---

# Estado, Democracia, Direitos e Ciência Política

> **Conhecimentos básicos** — Edital nº 1/2026 – CGU – AFFC (Cargo 2 – TI/Ciência de Dados).
> Texto integral do edital: [[Edital CGU 2026 (texto integral)]].

## Itens do edital (checklist)

### 1 Estado e legitimidade

- [x] 1.1 Estado, governo e administração
- [x] 1.1 Autoridade, legitimidade e poder
- [x] 1.1 Interesse público, pluralismo e conflitos distributivos

### 2 Democracia e representação

- [x] 2.1 Representação e participação
- [x] 2.1 Responsabilização democrática
- [x] 2.1 Relações entre Executivo, Legislativo e Judiciário
- [x] 2.1 Governabilidade e controles recíprocos

### 3 Federalismo e capacidades estatais

- [x] 3.1 Autonomia, coordenação e cooperação federativa
- [x] 3.1 Capacidades administrativas e políticas
- [x] 3.1 Burocracia, discricionariedade e implementação de direitos

### 4 Ordem constitucional e direitos

- [x] 4.1 Fundamentos e objetivos da República
- [x] 4.1 Direitos fundamentais, sociais e políticos
- [x] 4.1 Igualdade, devido processo e limites ao exercício do poder
- [x] 4.1 Princípios da administração pública

### 5 Valor público e controle

- [x] 5.1 Resultados socialmente relevantes
- [x] 5.1 Legitimidade, confiança e direitos
- [x] 5.1 Controle interno, externo e social em perspectiva institucional
- [x] 5.1 Tensões entre eficiência, equidade e garantias

### 6 Corrupção como fenômeno político e social

- [x] 6.1 Abuso do poder confiado e apropriação de decisões públicas em benefício particular
- [x] 6.1 Dimensões política, administrativa e público-privada
- [x] 6.2 Distinções entre corrupção, falha de gestão, conflito de interesses e ilícitos específicos
- [x] 6.2 Relações e diferenças entre clientelismo, patronagem, nepotismo e captura

### 7 Mecanismos de reprodução e captura

- [x] 7.1 Assimetrias de poder e informação, incentivos e oportunidades
- [x] 7.1 Relações principal-agente e problemas de ação coletiva
- [x] 7.1 Normas sociais, tolerância organizacional e redes de favorecimento
- [x] 7.2 Captura de políticas e influência indevida
- [x] 7.2 Distinção entre representação legítima de interesses e favorecimento

### 8 Consequências e respostas à corrupção

- [x] 8.1 Efeitos sobre direitos, desigualdades, competição, alocação de recursos, qualidade dos serviços e confiança institucional.
- [x] 8.2 Relações entre prevenção, detecção, responsabilização e reparação
- [x] 8.2 Controles democráticos, participação e capacidades estatais
- [x] 8.3 Avaliação crítica das respostas e de seus efeitos não pretendidos, preservados o devido processo e a continuidade de serviços essenciais.

### 9 Estado e modelos de desenvolvimento econômico

- [x] 9.1 Arranjos de desenvolvimento com diferentes combinações de mercado, planejamento, regulação, provisão pública e atuação empresarial do Estado
- [x] 9.1 Industrialização, inovação e transformação produtiva
- [x] 9.2 Papel das empresas estatais no investimento de longo prazo, na infraestrutura, no financiamento e na prestação de serviços públicos.
- [x] 9.3 Relações entre finalidade pública, concorrência, universalização, sustentabilidade fiscal e socioambiental
- [x] 9.3 Capacidades estatais, riscos de captura e efeitos distributivos
- [x] 9.4 Fundamentos constitucionais da atuação econômica do Estado e comparação de alternativas institucionais à luz de objetivos, evidências e resultados.

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
