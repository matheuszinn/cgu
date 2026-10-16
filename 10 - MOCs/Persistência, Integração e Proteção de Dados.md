---
tipo: moc
disciplina: "Persistência, Integração e Proteção de Dados"
status: novo
data: "2026-10-13"
tags:
  - moc
  - especifico
  - cgu-2026
---

# Persistência, Integração e Proteção de Dados

> **Conhecimentos específicos** — Cargo 4: TI / Desenvolvimento de Sistemas — Edital nº 1/2026 – CGU – AFFC.
> Texto integral do edital: [[Edital CGU 2026 (texto integral)]].

## Itens do edital (checklist)

### 1 Modelagem e persistência

- [x] 1.1 Modelagem relacional, normalização e integridade.
- [x] 1.2 Bancos documentais, chave-valor e vetoriais.
- [x] 1.3 Cache e busca textual.
- [x] 1.4 Escolha de armazenamento conforme uso.
- [x] 1.5 Transações, concorrência, consistência e evolução de esquemas.
- [x] 1.6 Persistência em Java com JPA: mapeamento de entidades e relacionamentos, ciclo de vida das entidades, contexto de persistência, consultas e transações.
- [x] 1.7 Estratégias de carregamento e seus efeitos sobre correção e desempenho.
- [x] 1.8 Spring Data JPA: repositórios, consultas e paginação.
- [x] 1.9 Integração da camada de persistência às regras de negócio.

### 2 SQL e desempenho

- [x] 2.1 Definição e manipulação de dados, controle de acesso e transações.
- [x] 2.2 Consultas com filtros, junções, agregações, subconsultas e expressões de tabela comuns.
- [x] 2.3 Índices, planos de execução, valores nulos e duplicações.
- [x] 2.4 Diagnóstico de consultas e efeitos sobre o desempenho da aplicação.

### 3 Fluxos e interoperabilidade

- [x] 3.1 Ingestão, transformação e carga.
- [x] 3.2 ETL e ELT.
- [x] 3.3 Processamento em lote e fluxo, completo e incremental.
- [x] 3.4 APIs, contratos e formatos CSV, JSON, XML e Parquet.
- [x] 3.5 Qualidade, rastreabilidade, conciliação e repetição segura de processamento.
- [x] 3.6 Spring Batch: organização de trabalhos e etapas de processamento (jobs e steps).
- [x] 3.7 Leitura, processamento e escrita de registros.
- [x] 3.8 Controle transacional, registro do estado de execução e reinício após falhas.
- [x] 3.9 Prevenção de perdas e duplicações no reprocessamento.

### 4 Privacidade e segurança de dados

- [x] 4.1 Minimização, finalidade, acesso e segregação.
- [x] 4.2 Criptografia em trânsito e repouso.
- [x] 4.3 Pseudonimização e risco de reidentificação.
- [x] 4.4 Retenção, descarte e proteção de cópias e registros.
- [x] 4.5 Compartilhamento e publicação com salvaguardas.
- [x] 4.6 Proteção de dados pessoais desde a concepção da aplicação.

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
