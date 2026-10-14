---
tipo: flashcard
disciplina: "<% tp.system.prompt("Disciplina", "Direito Administrativo") %>"
tema: "<% tp.system.prompt("Assunto", "") %>"
data: "<% tp.date.now("YYYY-MM-DD") %>"
tags:
  - flashcard
---

# <% tp.file.title %>

<% tp.file.cursor() %>
?
Resposta

<!--SR:!<% tp.date.now("YYYY-MM-DD") %>,1,250-->