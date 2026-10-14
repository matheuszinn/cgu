---
tipo: moc
disciplina: "Fundamentos de Governança, Riscos e Integridade Pública e Privada"
status: novo
data: "2026-10-13"
tags:
  - moc
  - complementar
  - cgu-2026
---

# Fundamentos de Governança, Riscos e Integridade Pública e Privada

> **Conhecimentos complementares** — Edital nº 1/2026 – CGU – AFFC (Cargo 4 – TI/Desenvolvimento de Sistemas).
> Texto integral do edital: [[Ed_1_2026_CGU_Abertura]].

## Itens do edital (checklist)

### 1 Governança e responsabilidades

- [ ] 1.1 Distinção entre direção, gestão, controle e prestação de contas
- [ ] 1.1 Papéis, supervisão, transparência e responsabilização
- [ ] 1.1 Relação entre decisões organizacionais, finalidade pública e direitos

### 2 Riscos e controles essenciais

- [ ] 2.1 Risco, causa, consequência e controle
- [ ] 2.1 Prevenção e detecção
- [ ] 2.1 Proporcionalidade dos controles, segregação de funções e risco residual
- [ ] 2.2 Identificação de vulnerabilidades e de controles compatíveis com situações usuais, a partir dos dados fornecidos.

### 3 Integridade pública

- [ ] 3.1 Finalidades dos programas e medidas de integridade
- [ ] 3.1 Compromisso da liderança, orientação ética, identificação de riscos, canais de relato e acompanhamento de ações
- [ ] 3.2 Prevenção de favorecimento, assédio e discriminação
- [ ] 3.2 Ambiente seguro e não retaliação

### 4 Integridade privada

- [ ] 4.1 Finalidades dos programas de integridade e sua relação com o poder público
- [ ] 4.1 Compromisso da direção, registros confiáveis, controles, diligência proporcional sobre terceiros, canais de relato e remediação
- [ ] 4.2 Diferença entre existência documental, implementação e efetividade dos mecanismos.

### 5 Prevenção e melhoria institucional

- [ ] 5.1 Cultura, incentivos e confiança
- [ ] 5.1 Diferenças de capacidade entre organizações
- [ ] 5.1 Orientação e medidas proporcionais
- [ ] 5.2 Denúncias e resultados de controle como insumos de melhoria.
- [ ] 5.3 Distinção entre baixa ocorrência e baixa detecção de problemas
- [ ] 5.3 Leitura de evidências simples sobre funcionamento e resultados das medidas

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
