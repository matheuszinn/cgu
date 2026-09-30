---
tipo: questão
disciplina: "<% tp.system.prompt("Disciplina", "Direito Administrativo") %>"
tema: "<% tp.system.prompt("Assunto", "") %>"
fonte: "<% tp.system.prompt("Fonte (ex: CESPE 2023)", "") %>"
resultado: "<% tp.system.prompt("Acertou/Errou?", "") %>"
data: "<% tp.date.now("YYYY-MM-DD") %>"
tags:
  - questão
  - "<% tp.system.prompt("Errou? adicione tag: pendente", "") %>"
---

# <% tp.file.title %>

## Enunciado

<% tp.file.cursor() %>

## Alternativas

- [ ] A)
- [ ] B)
- [ ] C)
- [ ] D)
- [ ] E)

## Meu raciocínio

-

## Gabarito e comentário

> **Gabarito:** ...
> **Por que acertei/errei:** ...