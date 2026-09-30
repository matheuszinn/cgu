---
tipo: nota
disciplina: "<% tp.system.prompt("Disciplina", "Direito Administrativo") %>"
tema: "<% tp.system.prompt("Assunto", "") %>"
status: germinar
data: "<% tp.date.now("YYYY-MM-DD") %>"
tags:
  - nota
---

# <% tp.file.title %>

> [!info] MOC: [[<% tp.frontmatter.disciplina %>]]

## Conceito

<% tp.file.cursor() %>

## Pontos-chave e Exceções

-

## Conexões

- Ver também: [[...]]

## Próximos passos

- [ ] Gerar flashcards a partir desta nota