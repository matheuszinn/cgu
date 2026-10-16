---
tipo: prova
concurso: "tce_rn_25"
arquivo_origem: "Provas/PDF/tce_rn_25/PADRAO DEFINITIVO DE RESPOSTA PROVA DISCURSIVA CARGO 4.pdf"
tags:
  - prova
  - cebraspe
  - cgu-2026
---

# PADRAO DEFINITIVO DE RESPOSTA PROVA DISCURSIVA CARGO 4

TRIBUNAL DE CONTAS DO ESTADO DO RIO GRANDE DO
NORTE
CARGO 4: ANALISTA ADMINISTRATIVO – ESPECIALIDADE:
TECNOLOGIA DA INFORMAÇÃO (DESENVOLVIMENTO DE SISTEMAS
E INTELIGÊNCIA DA INFORMAÇÃO)
Prova Discursiva
Aplicação: 12/4/2026
PADRÃO DE RESPOSTA DEFINITIVO
O modelo conceitual tem como objetivo representar a realidade do negócio de forma abstrata, independentemente de
tecnologia, identificando entidades, atributos, relacionamentos e regras de negócio. Essa etapa permite o alinhamento do
entendimento entre usuários e equipe técnica, o que favorece a redução de ambiguidades e a correta captura dos requisitos. Pode
ser representado por diagramas como o modelo entidade-relacionamento (DER), amplamente utilizado na fase de análise. O
modelo lógico, por sua vez, traduz o modelo conceitual para uma estrutura formal compatível com um paradigma de banco de
dados, geralmente o modelo relacional. Nesse nível, são definidas tabelas, chaves primárias e estrangeiras, restrições de
integridade, além de processos de normalização que visam eliminar redundâncias e evitar anomalias. A normalização pode ser
expressa por meio das formas normais (como 1FN, 2FN e 3FN), que tratam dependências funcionais e estruturais. Conforme a
abordagem adotada, o modelo lógico pode também contemplar decisões, como desnormalização controlada, visando atender
requisitos específicos de desempenho. Já o modelo físico corresponde à implementação concreta no sistema gerenciador de
banco de dados (SGBD), envolvendo a definição de tipos de dados, índices, estruturas de armazenamento, particionamento,
compressão e estratégias de acesso. Inclui também a definição de constraints adicionais, como NOT NULL, UNIQUE e regras
de domínio. Nessa etapa, considerações, como volume de dados, concorrência, padrões de consulta e características do hardware
tornam-se determinantes para a eficiência do sistema.
A modelagem adequada contribui diretamente para a integridade dos dados, especialmente por meio da definição de
chaves primárias, que garantem unicidade, e chaves estrangeiras, que asseguram a integridade referencial. A correta aplicação
dessas restrições evita inconsistências, como registros órfãos ou duplicidades indevidas. Além disso, a normalização reduz
redundâncias e previne anomalias de inserção, atualização e exclusão. Esses mecanismos são operacionalizados por constraints
e validações automáticas no SGBD, o que garante consistência ao longo do ciclo de vida dos dados. Por outro lado, em
determinados cenários, pode-se optar por desnormalização controlada, desde que acompanhada de mecanismos que preservem
a consistência.
No contexto de desempenho em larga escala, a modelagem física exerce papel fundamental, pois a criação de índices
adequados pode reduzir significativamente o tempo de resposta de consultas, embora implique custo adicional em operações de
escrita. O particionamento de tabelas permite distribuir grandes volumes de dados, melhorando o desempenho de consultas
segmentadas e facilitando operações de manutenção. A utilização dessas técnicas envolve trade-offs, devendo ser aplicada de
forma criteriosa conforme padrões de acesso e carga do sistema. Estratégias, como uso de tabelas particionadas, clusters,
materialização de visões e ajuste de parâmetros do SGBD também podem ser adotadas para otimização.
QUESITOS AVALIADOS
Quesito 2.1 – Características e finalidades dos modelos conceitual, lógico e físico
Conceito 0 – Não atendeu ao solicitado ou o fez de forma totalmente equivocada.
Conceito 1 – Descreveu corretamente as características e finalidades de apenas um dos seguintes modelos: (i) conceitual; (ii)
lógico; e (iii) físico.
Conceito 2 – Descreveu corretamente as características e finalidades de apenas dois dos modelos enumerados.
Conceito 3 – Descreveu as características e finalidades dos três modelos, mas de forma incompleta ou parcialmente correta.
Conceito 4 – Descreveu, de forma completa e correta, as características e finalidades dos três modelos.
Quesito 2.2 – Contribuição da modelagem adequada para a integridade dos dados e para a redução de inconsistências
em sistemas corporativos
Conceito 0 – Não atendeu ao solicitado ou o fez de forma totalmente equivocada.
Conceito 1 – Descreveu corretamente apenas um dos aspectos a seguir: (i) como a modelagem adequada contribui para a
integridade dos dados; e (ii) como ela contribui para a redução de inconsistências em sistemas corporativos.
Conceito 2 – Descreveu os dois aspectos anteriormente enumerados, mas de forma incompleta ou parcialmente correta.
Conceito 3 – Descreveu, de forma completa e correta, os dois aspectos enumerados.
Quesito 2.3 – Relação entre a modelagem física e a otimização de desempenho em bancos de dados, considerados os
índices, o particionamento e a organização de armazenamento
Conceito 0 – Não atendeu ao solicitado ou o fez de forma totalmente equivocada.
Conceito 1 – Discorreu corretamente sobre a relação entre a modelagem física e a otimização de desempenho em bancos de
dados, mas não considerou nenhum dos seguintes aspectos: (i) índices; (ii) particionamento; (iii) organização de armazenamento.
Conceito 2 – Discorreu corretamente sobre a relação entre a modelagem física e a otimização de desempenho em bancos de
dados e considerou apenas um dos aspectos anteriormente enumerados.
Conceito 3 – Discorreu corretamente sobre a relação entre a modelagem física e a otimização de desempenho em bancos de
dados e considerou apenas dois dos aspectos enumerados.
Conceito 4 – Discorreu corretamente sobre a relação entre a modelagem física e a otimização de desempenho em bancos de
dados e considerou os três aspectos enumerados.
