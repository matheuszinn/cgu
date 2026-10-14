---
tipo: dashboard
tags:
  - moc
  - concurso
---

# CGU 2026 — Auditor Federal de Finanças e Controle (AFFC)

> Painel inicial do vault para o **Edital nº 1 – CGU – AFFC, de 8 de outubro de 2026**.
> Alvo: **Cargo 4 — TI / Desenvolvimento de Sistemas**.

## 📄 Edital

- [[Ed_1_2026_CGU_Abertura|Edital nº 1/2026 — texto integral]]
- Banca: **Cebraspe** · <http://www.cebraspe.org.br/concursos/cgu_26_affc>
- Validade do concurso: **2 anos**, contados da publicação do resultado final.

## Dados do cargo

| Item | Informação |
|---|---|
| Cargo | Auditor Federal de Finanças e Controle (AFFC) |
| Especialidade | Tecnologia da Informação – **Desenvolvimento de Sistemas** (Cargo 4) |
| Requisito | Curso superior em qualquer área |
| Subsídio inicial | R$ 20.000,00 |
| Jornada | 40 horas semanais |
| Taxa de inscrição | R$ 170,00 |
| Vagas imediatas | 10 |
| Limite de aprovados | 54 (inclui cadastro de reserva) |
| Lotação | Órgão Central – DF |

## Provas

| Prova | Área de conhecimento | Itens | Caráter |
|---|---|---|---|
| P1 | Conhecimentos básicos | 40 | Eliminatório e classificatório |
| P2 | Conhecimentos complementares | 40 | Eliminatório e classificatório |
| P3 | Conhecimentos específicos | 90 | Eliminatório e classificatório |
| P4 | Discursiva — 2 questões (30 + 70 pontos) | 2 | Eliminatório e classificatório |

- Prova objetiva: **260 pontos**, duração de 5 horas (turno da manhã).
- Prova discursiva: **100 pontos**, duração de 3 h 30 min (turno da tarde).
- Nota final: `NFC = NFPO/26 + NFPD/10`.

## Datas-chave (Anexo I — cronograma previsto)

| Data | Etapa |
|---|---|
| 10 a 16/10/2026 | Solicitação de isenção da taxa de inscrição |
| 10/10 a 4/11/2026 | Período de inscrições |
| 6/11/2026 | Data final para pagamento da taxa |
| 2/12/2026 | Divulgação dos locais de prova |
| **13/12/2026** | **Aplicação das provas objetivas e discursiva** |
| 15 a 17/12/2026 | Consulta aos gabaritos preliminares |
| 14/1/2027 | Resultado final nas provas objetivas |
| 15/4/2027 | Resultado final no concurso público |

## Conteúdo programático

### Conhecimentos básicos

- Estado, Democracia, Direitos e Ciência Política
- Sociedade Brasileira, Desigualdades, Diversidade e Desenvolvimento
- Ética Pública e Responsabilidade Profissional
- Administração Pública e Fundamentos de Políticas Públicas

### Conhecimentos complementares

- Fundamentos de Governança, Riscos e Integridade Pública e Privada
- Fundamentos de Transparência, Ouvidoria e Participação Social
- Fundamentos de Direito Público Aplicado, Controle e Responsabilização
- Fundamentos de Evidências, Dados e Inteligência Artificial
- Fundamentos de Auditoria Governamental e Atuação Integrada da CGU

### Conhecimentos específicos — Desenvolvimento de Sistemas

- Engenharia de Software e Programação
- Arquitetura e Integração de Sistemas
- Persistência, Integração e Proteção de Dados
- Desenvolvimento Seguro, Qualidade e Gestão da Entrega

## Disciplinas (MOCs)

```dataview
TABLE status AS "Status", date(data) AS "Atualizado"
FROM "10 - MOCs"
WHERE tipo = "moc"
SORT file.name ASC
```

## Estado geral por tipo de documento

```dataview
TABLE length(rows) AS "Total", rows.status AS "Status"
FROM "20 - Notas" OR "30 - Resumos" OR "40 - Flashcards" OR "50 - Questões"
WHERE tipo
GROUP BY tipo
SORT key ASC
```

## Pendências (tarefas abertas)

```dataview
TASK FROM "20 - Notas" OR "30 - Resumos" OR "40 - Flashcards" OR "50 - Questões"
WHERE !completed
LIMIT 20
```

## Mapas rápidos

- [[Edital]] — quadro kanban do conteúdo programático
- [[Guia do Vault]] — como usar este vault
- [[MOCs/_Índice]] — todas as disciplinas
