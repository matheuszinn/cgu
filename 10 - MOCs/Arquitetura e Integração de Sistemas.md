---
tipo: moc
disciplina: "Arquitetura e Integração de Sistemas"
status: novo
data: "2026-10-13"
tags:
  - moc
  - especifico
  - cgu-2026
---
/
# Arquitetura e Integração de Sistemas

> **Conhecimentos específicos** — Cargo 4: TI / Desenvolvimento de Sistemas — Edital nº 1/2026 – CGU – AFFC.
> Texto integral do edital: [[Edital CGU 2026 (texto integral)]].

## Itens do edital (checklist)

### 1 Arquiteturas de aplicações

- [x] 1.1 Monolitos, microsserviços e arquiteturas orientadas a eventos.
- [x] 1.2 Distribuição de responsabilidades, acoplamento e dependências.
- [x] 1.3 Desempenho, escalabilidade, segurança e custo.
- [x] 1.4 Escolha de arquitetura conforme restrições.
- [x] 1.5 Aplicações Java com Spring Framework e Spring Boot: organização de componentes, inversão de controle e injeção de dependências.
- [x] 1.6 Configuração e autoconfiguração.
- [x] 1.7 Construção de serviços REST e separação entre apresentação, regras de negócio e acesso a dados.

### 2 APIs e identidade

- [x] 2.1 Design, contratos e versionamento de APIs REST.
- [x] 2.2 Autenticação e autorização.
- [x] 2.3 OAuth 2.0 para autorização e OpenID Connect para autenticação federada.
- [x] 2.4 Uso, validação e proteção de tokens.
- [x] 2.5 Controle de acesso e segregação de funções nas aplicações.
- [x] 2.6 Spring Security: configuração e avaliação de mecanismos de autenticação e autorização.
- [x] 2.7 Proteção de endpoints e métodos.
- [x] 2.8 Identificação e correção de permissões excessivas e falhas de controle de acesso.

### 3 Comunicação e consistência

- [x] 3.1 Mensageria, eventos e persistência.
- [x] 3.2 Falhas, repetição de requisições, idempotência e consistência.
- [x] 3.3 Integração entre sistemas e coordenação de operações.
- [x] 3.4 Evolução de contratos e migração de esquemas.

### 4 Integração com dados e IA

- [x] 4.1 Consumo e disponibilização de serviços de dados e modelos de linguagem.
- [x] 4.2 Representações vetoriais, busca semântica e recuperação de informação para geração de respostas.
- [x] 4.3 Agentes e ferramentas.
- [x] 4.4 Avaliação funcional de respostas e fontes.
- [x] 4.5 Limites de autorização, supervisão e proteção contra instruções maliciosas em conteúdo externo.

### 5 Confiabilidade das aplicações

- [x] 5.1 Contêineres, serviços de nuvem e processamento serverless como ambientes de implantação.
- [x] 5.2 Logs, métricas e rastreamento.
- [x] 5.3 Latência, disponibilidade, capacidade e tolerância a falhas.
- [x] 5.4 Diagnóstico de integrações e dependências.
- [x] 5.5 Continuidade, recuperação e degradação de serviços.

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
