---
tipo: moc
disciplina: "Operação, Governança e Gestão de Soluções de Dados e IA"
status: novo
data: "2026-11-03"
tags:
  - moc
  - especifico
  - cgu-2026
  - cargo-2
---

# Operação, Governança e Gestão de Soluções de Dados e IA

> **Conhecimentos específicos** — Cargo 2: TI / Ciência de Dados — Edital nº 1/2026 – CGU – AFFC.
> Texto integral do edital: [[Edital CGU 2026 (texto integral)]].

## Itens do edital (checklist)

### 1 Ciclo de vida e MLOps

- [x] 1.1 Versionamento de dados, código e modelos.
- [x] 1.2 Registro de experimentos.
- [x] 1.3 Pipelines, testes e integração e entrega contínuas.
- [x] 1.4 Reprodutibilidade.
- [x] 1.5 Disponibilização por APIs, implantação e reversão.
- [x] 1.6 Monitoramento de mudanças nas distribuições, nas relações e no desempenho.

### 2 Sustentação de soluções analíticas

- [x] 2.1 Serviços gerenciados e operação própria.
- [x] 2.2 Requisitos de processamento, memória, armazenamento e aceleradores.
- [x] 2.3 Custo, latência, disponibilidade e observabilidade de pipelines e inferência.
- [x] 2.4 Controle de acesso, proteção de segredos e continuidade das soluções.

### 3 Governança e responsabilidade

- [x] 3.1 Papéis, riscos e evidências sobre dados, modelos e decisões.
- [x] 3.2 Rastreabilidade, avaliação de impacto, revisão humana e contestação.
- [x] 3.3 Proteção de dados pessoais e informações sensíveis.
- [x] 3.4 Prevenção e tratamento de discriminação e de uso fora da finalidade.
- [x] 3.5 Avaliação de resultados e limites da automação.

### 4 Gestão de produtos de dados

- [x] 4.1 Alinhamento entre problema público, produto e resultado.
- [x] 4.2 Priorização, critérios de aceitação e indicadores.
- [x] 4.3 Descoberta de necessidades, entrega e ciclo de vida.
- [x] 4.4 Scrum e Kanban.
- [x] 4.5 Articulação com PDTIC, plano de transformação digital e plano de dados abertos.
- [x] 4.6 Comunicação dos resultados e das incertezas aos usuários.

### 5 Contratação e controle de soluções

- [x] 5.1 Estudo técnico preliminar e termo de referência.
- [x] 5.2 Viabilidade, dimensionamento e custo total de propriedade.
- [x] 5.3 Comparação entre desenvolvimento próprio, contratação e serviços de nuvem.
- [x] 5.4 Pesquisa de preços.
- [x] 5.5 Requisitos de qualidade, proteção e desempenho.
- [x] 5.6 Fiscalização e pagamento por entregas verificáveis.
- [x] 5.7 Propriedade intelectual, portabilidade, acesso a dados e modelos, dependência tecnológica e plano de saída.

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
