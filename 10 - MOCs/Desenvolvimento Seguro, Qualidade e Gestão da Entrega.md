---
tipo: moc
disciplina: "Desenvolvimento Seguro, Qualidade e Gestão da Entrega"
status: novo
data: "2026-10-13"
tags:
  - moc
  - especifico
  - cgu-2026
---

# Desenvolvimento Seguro, Qualidade e Gestão da Entrega

> **Conhecimentos específicos** — Cargo 4: TI / Desenvolvimento de Sistemas — Edital nº 1/2026 – CGU – AFFC.
> Texto integral do edital: [[Edital CGU 2026 (texto integral)]].

## Itens do edital (checklist)

### 1 Segurança de aplicações

- [x] 1.1 Ameaças e vulnerabilidades em aplicações e interfaces.
- [x] 1.2 Validação de entradas e controles de acesso.
- [x] 1.3 Proteção de segredos e dependências.
- [x] 1.4 Testes de segurança autorizados.
- [x] 1.5 Prevenção de vazamentos.
- [x] 1.6 Registros, preservação de evidências e tratamento de falhas de segurança, inclusive em integrações com IA.

### 2 Testes e qualidade

- [x] 2.1 Testes unitários, de integração, de contrato e de aceitação.
- [x] 2.2 Análise estática, cobertura e revisão de código.
- [x] 2.3 Automação e dados de teste.
- [x] 2.4 Limites das métricas de qualidade.
- [x] 2.5 Verificação de requisitos funcionais, segurança, desempenho e acessibilidade.

### 3 Entrega e operação

- [x] 3.1 Versionamento, integração e entrega contínuas.
- [x] 3.2 DevSecOps e segurança da cadeia de dependências.
- [x] 3.3 Automação de build, teste e implantação.
- [x] 3.4 Configuração e segregação de ambientes.
- [x] 3.5 Mudanças, reversão e observabilidade.
- [x] 3.6 Manutenção da continuidade durante entregas e incidentes.

### 4 Gestão de produtos e governança

- [x] 4.1 Descoberta de necessidades, entrega e ciclo de vida de produtos digitais.
- [x] 4.2 Scrum e Kanban.
- [x] 4.3 Priorização, critérios de aceitação e indicadores de resultado.
- [x] 4.4 PDTIC, plano de transformação digital e plano de dados abertos aplicados a produtos e integrações.
- [x] 4.5 Riscos, responsabilidades e evidências de efetividade de controles.

### 5 Contratação e fiscalização de soluções

- [x] 5.1 Necessidade, estudo técnico preliminar e termo de referência.
- [x] 5.2 Comparação entre desenvolvimento próprio, contratação e compartilhamento.
- [x] 5.3 Viabilidade, dimensionamento, custo total de propriedade e pesquisa de preços.
- [x] 5.4 Qualidade, níveis de serviço e entregas verificáveis.
- [x] 5.5 Fiscalização e pagamento.
- [x] 5.6 Propriedade intelectual, portabilidade, acesso a código e dados, dependência tecnológica e plano de saída.

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
