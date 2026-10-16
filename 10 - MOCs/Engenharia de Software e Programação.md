---
tipo: moc
disciplina: "Engenharia de Software e Programação"
status: novo
data: "2026-10-13"
tags:
  - moc
  - especifico
  - cgu-2026
---

# Engenharia de Software e Programação

> **Conhecimentos específicos** — Cargo 4: TI / Desenvolvimento de Sistemas — Edital nº 1/2026 – CGU – AFFC.
> Texto integral do edital: [[Edital CGU 2026 (texto integral)]].

## Itens do edital (checklist)

### 1 Problemas e requisitos

- [x] 1.1 Necessidades de usuários.
- [x] 1.2 Requisitos funcionais e não funcionais.
- [x] 1.3 Restrições e critérios de aceitação.
- [x] 1.4 Desenho centrado nas pessoas.
- [x] 1.5 Relações entre problema público, processo de trabalho e solução digital.

### 2 Programação e correção

- [x] 2.1 Linguagem Java: tipos de dados, estruturas de controle, métodos, classes e objetos.
- [x] 2.2 Encapsulamento, interfaces, herança e polimorfismo.
- [x] 2.3 Coleções e tipos genéricos.
- [x] 2.4 Igualdade de objetos, mutabilidade, tratamento de exceções e leitura e escrita de arquivos.
- [x] 2.5 Estruturas de dados, algoritmos e pseudocódigo.
- [x] 2.6 Leitura, depuração e testes de borda.
- [x] 2.7 Complexidade em decisões de desempenho.
- [x] 2.8 Modularidade e padrões de projeto aplicados à manutenção.

### 3 Concorrência e processamento

- [x] 3.1 Concorrência, paralelismo e assincronia.
- [x] 3.2 Condições de corrida e sincronização.
- [x] 3.3 Compartilhamento de estado, bloqueios e falhas.
- [x] 3.4 Correção e desempenho sob requisições concorrentes.

### 4 Interfaces e experiência do usuário

- [x] 4.1 Usabilidade, prototipagem e desenho responsivo.
- [x] 4.2 Acessibilidade e barreiras digitais.
- [x] 4.3 Componentes de interface e reaproveitamento.
- [x] 4.4 Validação com usuários e prevenção de erros no uso dos serviços.
- [x] 4.5 Desenvolvimento de interfaces com JavaScript e Vue.js: componentes, reatividade, tratamento de eventos e consumo de APIs.

### 5 Manutenção e evolução

- [x] 5.1 Débito técnico, documentação, modularidade e acoplamento.
- [x] 5.2 Sustentação e modernização de sistemas legados.
- [x] 5.3 Interoperabilidade e compatibilidade.
- [x] 5.4 Impactos das mudanças e das falhas sobre a continuidade e a qualidade dos serviços.

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
