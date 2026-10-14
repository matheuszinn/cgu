# Guia do Vault — Segundo Cérebro CGU

Este vault é um "segundo cérebro" para os estudos do concurso da CGU, organizado no Obsidian com o método de **Mapas de Conteúdo (MOCs)**.

## 1. Estrutura de pastas

| Pasta | Para que serve |
|---|---|
| `00 - Início/` | Home (dashboard), Edital (kanban), Guia |
| `10 - MOCs/` | Um MOC por disciplina (índice do edital + painéis Dataview) |
| `20 - Notas/` | Notas atômicas: uma ideia/conceito por nota (subpastas por disciplina) |
| `30 - Resumos/` | Documentos longos, visão geral de um assunto (subpastas por disciplina) |
| `40 - Flashcards/` | Revisão ativa (Spaced Repetition) — subpastas por disciplina |
| `50 - Questões/` | Questões de provas antigas + análise de erros (subpastas por disciplina) |
| `90 - Templates/` | Modelos do Templater |
| `99 - Arquivo/` | Material desatualizado (mover para cá, não apagar) |

## 2. Plugins da comunidade (instalar uma única vez)

A configuração já está pronta em `.obsidian/`. Instale os plugins abaixo em **Configurações → Plugins da comunidade → Explorar** e depois habilite:

1. **Templater** — `templater-obsidian` (modelos dinâmicos)
2. **Dataview** — `dataview` (painéis automáticos)
3. **Kanban** — `obsidian-kanban` (quadro do edital)
4. **Spaced Repetition** — `obsidian-spaced-repetition` (revisão espaçada)
5. **Linter** — `obsidian-linter` (formatação automática)
6. **Obsidian Git** — `obsidian-git` (backup automático via git)

Para instalar plugins da comunidade, o modo de plugins restrito precisa estar desativado: **Configurações → Plugins da comunidade → Ativar plugins da comunidade**.

> Dica: os `data.json` de cada plugin já foram criados com configurações sensatas. Se o Obsidian sobrescrever, os valores padrão ainda funcionam bem.

## 3. Convenções

- **Frontmatter (YAML)** em toda nota: `tipo`, `disciplina`, `tema`, `status`, `data`, `tags`
- **Status**: `novo` (acabou de criar) → `estudando` (em desenvolvimento) → `dominado` (revisado e dominado)
- **Tags principais**: `#nota`, `#resumo`, `#flashcard`, `#questão`, `#pendente`, `#moc`
- **`disciplina`** deve ter exatamente o mesmo nome do MOC (ex: `Direito Administrativo`) — é isso que conecta nota ↔ MOC via Dataview
- **Organização em subpastas**: em `20 - Notas/`, `30 - Resumos/`, `40 - Flashcards/` e `50 - Questões/`, os arquivos ficam em subpastas com o **nome exato da disciplina** (ex: `Arquitetura e Integração de Sistemas/`). Os painéis Dataview são **recursivos**, então continuam listando tudo normalmente.

## 4. Fluxo de estudo

1. **Estudar** → criar Nota (detalhe) ou Resumo (macro) com Templater
2. **Vincular** ao MOC da disciplina (o Dataview lista automaticamente)
3. **Flashcards**: pontos-chave viram flashcards no formato `Pergunta :: Resposta` (separador de linha única do Spaced Repetition) e o plugin agenda as revisões
4. **Questões**: resolver questões antigas e registrar erros com tag `#pendente`
5. **Kanban**: mover tópicos do edital entre colunas conforme evolui
6. **Revisar**: usar a Home e os MOCs para revisar e atualizar o `status` para `dominado`

## 5. Backups (Obsidian Git)

O vault é um repositório git. O plugin `obsidian-git` pode fazer commit/push automáticos em intervalos configurados. Se quiser backup remoto, crie um repositório vazio no GitHub e configure o remoto:

```bash
git remote add origin <url-do-repositorio>
```

## 6. Atalhos úteis

- `Ctrl/Cmd + P` → paleta de comandos (inserir template, abrir painel do Spaced Repetition, etc.)
- `Ctrl/Cmd + O` → abrir nota rapidamente (Quick switcher)
- `Ctrl/Cmd + N` → nova nota (criada em `20 - Notas/` por padrão)