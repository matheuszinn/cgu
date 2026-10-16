---
tipo: moc
disciplina: "Sociedade Brasileira, Desigualdades, Diversidade e Desenvolvimento"
status: novo
data: "2026-10-13"
tags:
  - moc
  - basico
  - cgu-2026
---

# Sociedade Brasileira, Desigualdades, Diversidade e Desenvolvimento

> **Conhecimentos básicos** — Edital nº 1/2026 – CGU – AFFC (Cargo 4 – TI/Desenvolvimento de Sistemas).
> Texto integral do edital: [[Edital CGU 2026 (texto integral)]].

## Itens do edital (checklist)

### 1 Fundamentos sociológicos

- [ ] 1.1 Instituições, socialização e ação coletiva
- [ ] 1.1 Estratificação e mobilidade social
- [ ] 1.1 Redes, poder, discriminação e reprodução das desigualdades

### 2 Formação social e cidadania no Brasil

- [ ] 2.1 Heranças da escravidão, hierarquias sociais e construção da cidadania
- [ ] 2.1 Transformações nas relações entre Estado e sociedade
- [ ] 2.1 Mecanismos de inclusão e exclusão institucional

### 3 População, território e trabalho

- [ ] 3.1 Transição demográfica, envelhecimento e cuidado
- [ ] 3.1 Desigualdades regionais, urbanas e rurais
- [ ] 3.1 Estrutura produtiva, informalidade e mudanças tecnológicas no trabalho

### 4 Diversidade e acesso a direitos

- [ ] 4.1 Relações étnico-raciais, gênero e sexualidade
- [ ] 4.1 Pessoas com deficiência
- [ ] 4.1 Idade
- [ ] 4.1 Povos indígenas e comunidades tradicionais
- [ ] 4.1 Interseccionalidade, acessibilidade e barreiras administrativas e digitais

### 5 Desenvolvimento e realidade brasileira

- [ ] 5.1 Pobreza, renda e proteção social
- [ ] 5.1 Educação, saúde, saneamento e habitação como problemas públicos
- [ ] 5.1 Sustentabilidade e vulnerabilidade climática
- [ ] 5.1 Leitura contextual de indicadores e desigualdades

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
