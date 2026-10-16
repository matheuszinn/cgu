---
tipo: moc
disciplina: "Fundamentos de Transparência, Ouvidoria e Participação Social"
status: novo
data: "2026-10-13"
tags:
  - moc
  - complementar
  - cgu-2026
---

# Fundamentos de Transparência, Ouvidoria e Participação Social

> **Conhecimentos complementares** — Edital nº 1/2026 – CGU – AFFC (Cargo 4 – TI/Desenvolvimento de Sistemas).
> Texto integral do edital: [[Edital CGU 2026 (texto integral)]].

## Itens do edital (checklist)

### 1 Acesso à informação

- [x] 1.1 Transparência ativa e passiva
- [x] 1.1 Finalidade de pedidos e recursos
- [x] 1.1 Publicidade como regra e motivação das restrições
- [x] 1.2 Distinção conceitual entre informação classificada, sigilos previstos em lei, informação pessoal e documento preparatório
- [x] 1.2 Acesso parcial e comunicação clara da decisão

### 2 Transparência e proteção de dados

- [x] 2.1 Compatibilização entre acesso à informação e proteção de dados pessoais
- [x] 2.1 Finalidade, necessidade e salvaguardas
- [x] 2.2 Diferença entre dados pessoais e dados pessoais sensíveis
- [x] 2.2 Noções de tarjamento, anonimização e risco de reidentificação

### 3 Ouvidoria e proteção das pessoas

- [x] 3.1 Finalidades das manifestações
- [x] 3.1 Acolhimento, encaminhamento e resposta ao usuário
- [x] 3.1 Acessibilidade e linguagem cidadã
- [x] 3.2 Proteção da identidade e prevenção de retaliação.
- [x] 3.3 Distinção entre receber um relato, apurar fatos e decidir sobre responsabilidade.

### 4 Participação e melhoria de serviços

- [x] 4.1 Participação e controle social
- [x] 4.1 Conselhos, consultas e escuta de usuários
- [x] 4.1 Representatividade e barreiras à participação
- [x] 4.2 Recorrências em manifestações como sinais de problemas.
- [x] 4.2.1 Subnotificação.
- [x] 4.3 Transparência ativa, dados abertos e Portal da Transparência como meios de acesso e controle
- [x] 4.3 Qualidade, atualização, cobertura e limites da informação
- [x] 4.4 Papel da CGU na orientação e no monitoramento da transparência e do acesso à informação, em nível de finalidade institucional.

### 5 Integridade da informação e comunicação

- [x] 5.1 Confiabilidade e contexto das fontes
- [x] 5.1 Distinção entre fato, alegação e interpretação
- [x] 5.2 Desinformação e efeitos sobre políticas públicas
- [x] 5.2 Comunicação de incertezas e correção de erros
- [x] 5.3 Liberdade de expressão e pluralismo.
- [x] 5.3.1 Distinção entre crítica legítima e desinformação.

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
