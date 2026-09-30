---
tipo: dashboard
tags:
  - moc
---

# Segundo Cérebro — CGU

> Página inicial do vault. Painéis automáticos atualizados pelo Dataview.

## Disciplinas (MOCs)

```dataview
TABLE status AS "Status", date(date) AS "Atualizado"
FROM "10 - MOCs"
WHERE tipo = "moc"
SORT file.name ASC
```

## Estado geral por tipo de documento

```dataview
TABLE length(rows) AS "Total", rows.status AS "Status"
FROM "20 - Notas" OR "30 - Resumos" OR "40 - Flashcards" OR "50 - Questões"
WHERE tipo
GROUP BY tipo
SORT key ASC
```

## Pendências (tarefas abertas)

```dataview
TASK FROM "20 - Notas" OR "30 - Resumos" OR "40 - Flashcards" OR "50 - Questões"
WHERE !completed
LIMIT 20
```

## Mapas rápidos

- [[Edital]] — quadro kanban de acompanhamento do edital
- [[Guia do Vault]] — como usar este vault
- [[MOCs/_Índice]] — todas as disciplinas