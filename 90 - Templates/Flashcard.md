---
tipo: flashcard
disciplina: "<% tp.system.prompt("Disciplina", "Direito Administrativo") %>"
tema: "<%* const tema = tp.system.prompt("Assunto", ""); const slug = (tema.normalize("NFD").replace(/[\u0300-\u036f]/g, "").toLowerCase().replace(/[^a-z0-9]+/g, "-").replace(/^-+|-+$/g, "")) || "geral"; tR += tema %>"
data: "<% tp.date.now("YYYY-MM-DD") %>"
tags:
  - flashcard/<%* tR += slug %>
---

# <% tp.file.title %>

<% tp.file.cursor() %>
?
Resposta

<!--SR:!<% tp.date.now("YYYY-MM-DD") %>,1,250-->
