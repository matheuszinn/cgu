---
tipo: resumo
disciplina: "<% tp.system.prompt("Disciplina", "Direito Administrativo") %>"
tema: "<% tp.system.prompt("Assunto geral (ex: Licitações)", "") %>"
status: novo
data: "<% tp.date.now("YYYY-MM-DD") %>"
tags:
  - resumo
---

# Resumo: <% tp.file.title %>

> [!info] MOC: [[<% tp.frontmatter.disciplina %>]]

## Visão geral

<% tp.file.cursor() %>

## Estrutura do assunto

1.
2.
3.

## Detalhes que merecem destaque

-

## Notas atômicas relacionadas

```dataview
LIST FROM "20 - Notas"
WHERE disciplina = this.disciplina
  AND contains(tema, this.tema)
SORT file.name ASC
```

## Próximos passos

- [ ] Revisar pontos fracos e converter em flashcards