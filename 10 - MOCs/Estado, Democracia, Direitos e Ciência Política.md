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

> **Conhecimentos básicos** — Edital nº 1/2026 – CGU – AFFC (Cargo 4 – TI/Desenvolvimento de Sistemas).
> Texto integral do edital: [[Edital CGU 2026 (texto integral)]].

## Itens do edital (checklist)

### 1 Estado e legitimidade

- [ ] 1.1 Estado, governo e administração
- [ ] 1.1 Autoridade, legitimidade e poder
- [ ] 1.1 Interesse público, pluralismo e conflitos distributivos

### 2 Democracia e representação

- [ ] 2.1 Representação e participação
- [ ] 2.1 Responsabilização democrática
- [ ] 2.1 Relações entre Executivo, Legislativo e Judiciário
- [ ] 2.1 Governabilidade e controles recíprocos

### 3 Federalismo e capacidades estatais

- [ ] 3.1 Autonomia, coordenação e cooperação federativa
- [ ] 3.1 Capacidades administrativas e políticas
- [ ] 3.1 Burocracia, discricionariedade e implementação de direitos

### 4 Ordem constitucional e direitos

- [ ] 4.1 Fundamentos e objetivos da República
- [ ] 4.1 Direitos fundamentais, sociais e políticos
- [ ] 4.1 Igualdade, devido processo e limites ao exercício do poder
- [ ] 4.1 Princípios da administração pública

### 5 Valor público e controle

- [ ] 5.1 Resultados socialmente relevantes
- [ ] 5.1 Legitimidade, confiança e direitos
- [ ] 5.1 Controle interno, externo e social em perspectiva institucional
- [ ] 5.1 Tensões entre eficiência, equidade e garantias

### 6 Corrupção como fenômeno político e social

- [ ] 6.1 Abuso do poder confiado e apropriação de decisões públicas em benefício particular
- [ ] 6.1 Dimensões política, administrativa e público-privada
- [ ] 6.2 Distinções entre corrupção, falha de gestão, conflito de interesses e ilícitos específicos
- [ ] 6.2 Relações e diferenças entre clientelismo, patronagem, nepotismo e captura

### 7 Mecanismos de reprodução e captura

- [ ] 7.1 Assimetrias de poder e informação, incentivos e oportunidades
- [ ] 7.1 Relações principal-agente e problemas de ação coletiva
- [ ] 7.1 Normas sociais, tolerância organizacional e redes de favorecimento
- [ ] 7.2 Captura de políticas e influência indevida
- [ ] 7.2 Distinção entre representação legítima de interesses e favorecimento

### 8 Consequências e respostas à corrupção

- [ ] 8.1 Efeitos sobre direitos, desigualdades, competição, alocação de recursos, qualidade dos serviços e confiança institucional.
- [ ] 8.2 Relações entre prevenção, detecção, responsabilização e reparação
- [ ] 8.2 Controles democráticos, participação e capacidades estatais
- [ ] 8.3 Avaliação crítica das respostas e de seus efeitos não pretendidos, preservados o devido processo e a continuidade de serviços essenciais.

### 9 Estado e modelos de desenvolvimento econômico

- [ ] 9.1 Arranjos de desenvolvimento com diferentes combinações de mercado, planejamento, regulação, provisão pública e atuação empresarial do Estado
- [ ] 9.1 Industrialização, inovação e transformação produtiva
- [ ] 9.2 Papel das empresas estatais no investimento de longo prazo, na infraestrutura, no financiamento e na prestação de serviços públicos.
- [ ] 9.3 Relações entre finalidade pública, concorrência, universalização, sustentabilidade fiscal e socioambiental
- [ ] 9.3 Capacidades estatais, riscos de captura e efeitos distributivos
- [ ] 9.4 Fundamentos constitucionais da atuação econômica do Estado e comparação de alternativas institucionais à luz de objetivos, evidências e resultados.

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
