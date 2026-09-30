---
tipo: índice
tags:
  - moc
---

# Índice de Disciplinas (MOCs)

> Quando souber o conteúdo do edital, crie um MOC por disciplina usando o template `MOC.md` (comando do Templater). Os painéis Dataview dentro dele listam notas, resumos, flashcards e questões automaticamente.

## Como criar um MOC

1. Pressione `Ctrl/Cmd + P` e procure por "Templater: Insert template"
2. Escolha `MOC.md`, informe a disciplina (ex: "Direito Administrativo")
3. Cole no topo os itens do edital daquela matéria
4. Quando criar notas/resumos, preencha `disciplina` com o mesmo nome

## Disciplinas

```dataview
TABLE status AS "Status"
FROM "10 - MOCs"
WHERE tipo = "moc"
SORT file.name ASC
```