---
tipo: moc
disciplina: "<% tp.system.prompt("Disciplina", "Direito Administrativo") %>"
status: novo
data: "<% tp.date.now("YYYY-MM-DD") %>"
tags:
  - moc
---

# <% tp.file.title %>

> Mapa de Conteúdo da disciplina **<% tp.file.title %>**. Cole abaixo o índice do edital desta matéria e vá marcando o progresso.

## Itens do edital (checklist)

- [ ] <% tp.file.cursor() %>

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