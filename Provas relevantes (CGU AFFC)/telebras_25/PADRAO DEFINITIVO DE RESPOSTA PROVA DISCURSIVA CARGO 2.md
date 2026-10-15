---
tipo: prova
concurso: "telebras_25"
arquivo_origem: "Provas Cebraspe/telebras_25/PADRAO DEFINITIVO DE RESPOSTA PROVA DISCURSIVA CARGO 2.pdf"
tags:
  - prova
  - cebraspe
  - cgu-2026
---

# PADRAO DEFINITIVO DE RESPOSTA PROVA DISCURSIVA CARGO 2

TELECOMUNICAÇÕES BRASILEIRAS S.A.
ESPECIALISTA EM GESTÃO DE TELECOMUNICAÇÕES – ANALISTA
DE TECNOLOGIA DA INFORMAÇÃO
Prova Discursiva
Aplicação: 8/2/2026
PADRÃO DE RESPOSTA DEFINITIVO
A integridade referencial estabelece que todo valor presente em uma chave estrangeira deve, obrigatoriamente,
corresponder a um valor existente na chave primária da tabela referenciada, ou então assumir um valor nulo, quando permitido
pela modelagem. Dessa forma, evita-se a ocorrência de registros órfãos, isto é, dados que fazem referência a entidades
inexistentes, o que comprometeria a coerência lógica do banco de dados. A integridade referencial, portanto, contribui para a
confiabilidade das informações, para a correta interpretação dos dados pelos sistemas e para a geração de relatórios consistentes
e precisos. A integridade referencial também pode ser corretamente caracterizada como uma relação de dependência lógica e de
consistência entre tabelas, na qual registros associados a chaves estrangeiras dependem da existência e da estabilidade dos
registros correspondentes, identificados por chaves primárias, de modo a evitar inconsistências e referências inválidas.
O sistema gerenciador de banco de dados (SGBD) aplica automaticamente as restrições definidas no esquema do banco
de dados. Ao executar operações de manipulação de dados, como inserções ( INSERT), atualizações (UPDATE) e exclusões
(DELETE), o SGBD realiza verificações internas para assegurar que as regras de integridade sejam respeitadas. Caso uma tentativa
de inserção utilize um valor de chave estrangeira inexistente na tabela referenciada, o sistema impedirá a operação. Da mesma
forma, ao tentar excluir ou alterar um registro que é referenciado por outras tabelas, o SGBD pode adotar diferentes políticas,
como RESTRICT ou NO ACTION, que bloqueiam a operação, CASCADE, que propaga a alteração ou exclusão para os registros
dependentes, e SET NULL ou SET DEFAULT, que ajustam os valores das chaves estrangeiras. O SGBD aplica automaticamente
essas restrições durante operações de manipulação de dados, impedindo inserções incoerentes, bloqueando alterações ou
exclusões que violem relações existentes ou propagando tais operações conforme definido no esquema, ainda que sem a
enumeração formal de comandos DML ou de políticas referenciais específicas.
QUESITOS AVALIADOS
Quesito 2.1 – Relação entre integridade referencial e chaves primárias e chaves estrangeiras em um banco de dados
relacional
Conceito 0 – Não atendeu o quesito ou o fez de maneira totalmente equivocada.
Conceito 1 – Explicou, de forma parcialmente correta, a relação entre a integridade referencial e apenas um dos tipos de chave:
primária ou estrangeira.
Conceito 2 – Explicou corretamente a relação entre a integridade referencial e apenas um dos tipos de chave.
Conceito 3 – Explicou, de forma parcialmente correta, a relação entre a integridade referencial e os dois tipos de chave.
Conceito 4 – Explicou corretamente a relação entre a integridade referencial e os dois tipos de chave.
Quesito 2.2 – Papel do SGBD na garantia da integridade referencial
Conceito 0 – Não atendeu o quesito ou o fez de maneira totalmente equivocada.
Conceito 1 – Mencionou, de forma superficial, o papel do SGDB na garantia da integridade referencial, sem explicar como as
restrições são aplicadas automaticamente durante as operações de manipulação de dados (DML).
Conceito 2 – Abordou, corretamente, apenas um dos dois aspectos: (i) papel do SGDB na garantia da integridade referencial; (ii)
forma como as restrições são aplicadas automaticamente durante as operações de manipulação de dados (DML).
Conceito 3 – Abordou, de forma parcialmente correta, os dois aspectos.
Conceito 4 – Abordou, corretamente, os dois aspectos.
