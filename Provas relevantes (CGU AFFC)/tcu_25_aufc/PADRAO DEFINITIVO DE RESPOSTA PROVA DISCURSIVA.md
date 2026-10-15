---
tipo: prova
concurso: "tcu_25_aufc"
arquivo_origem: "Provas Cebraspe/tcu_25_aufc/PADRAO DEFINITIVO DE RESPOSTA PROVA DISCURSIVA.pdf"
tags:
  - prova
  - cebraspe
  - cgu-2026
---

# PADRAO DEFINITIVO DE RESPOSTA PROVA DISCURSIVA

TRIBUNAL DE CONTAS DA UNIÃO
AUDITOR FEDERAL DE CONTROLE EXTERNO – ÁREA DE CONTROLE
EXTERNO/ORIENTAÇÃO: AUDITORIA DE TECNOLOGIA DA
INFORMAÇÃO
Prova Discursiva – Questão 1
Aplicação: 22/2/2026
PADRÃO DE RESPOSTA DEFINITIVO
A responsabilidade civil objetiva do Estado por danos causados por seus agentes a terceiros é prevista no art. 37, § 6.º,
da Constituição Federal de 1988 (CF). Seu fundamento reside na teoria do risco administrativo, segundo a qual o Estado tem a
obrigação de indenizar o terceiro lesado, bastando a comprovação dos seguintes elementos: a ação ou omissão administrativa; a
ocorrência do dano; o nexo causal entre o dano e a ação ou omissão administrativa; e a ausência de causa de excludente da
responsabilidade estatal (caso fortuito ou força maior, culpa exclusiva da vítima ou culpa exclusiva de terceiro). Não se exige
que o particular prove a culpa ou o dolo do agente, pois a responsabilidade é objetiva (independe de elemento subjetivo). A
finalidade é garantir uma reparação do dano mais rápida e eficaz ao particular lesado. Admite-se, ainda, a menção à
responsabilidade subjetiva do Estado em casos de omissão genérica (teoria da culpa do serviço/falta do serviço) e à teoria do
risco integral em situações excepcionais, como no caso de danos nucleares. Ademais, consagra-se a tese da dupla garantia fixada
pelo STF, segundo a qual a ação indenizatória deve ser ajuizada contra o ente público ou prestador de serviço, sendo o agente
público parte ilegítima para responder diretamente à demanda do lesado.
O direito de regresso é a prerrogativa do Estado de, após ter indenizado a vítima do dano causado por seu agente, ajuizar
ação contra o responsável pelo dano, com vistas ao ressarcimento do valor pago. Essa ação tem natureza subjetiva, sendo
imprescindível que o Estado demonstre o dolo ou a culpa do agente na causação do prejuízo.
O TCU, no exercício do controle externo (art. 71 da CF), atuando em auxílio ao Congresso Nacional, detém competência
constitucional para julgar irregularidades de que resulte prejuízo ao erário (art. 71, inciso II, da CF) e determinar o ressarcimento
integral do dano ao erário. Essa competência é exercida, geralmente, no julgamento das contas (anuais ou por tomadas de contas
especiais), ocasião em que o TCU julga a legalidade e a economicidade dos atos do responsável. Ao constatar débito irregular,
o TCU condena o agente público a devolver o valor. A decisão definitiva do TCU que impõe o ressarcimento tem eficácia de
título executivo, podendo ser executada judicialmente, garantindo-se, assim, a recomposição do patrimônio público lesado, sem,
contudo, interferir no julgamento das demais sanções na esfera da administrativa (independência mitigada das instâncias).
QUESITOS AVALIADOS
Quesito 2.1 – Teoria do risco administrativo e direito de regresso do Estado
Conceito 0 – Não abordou a teoria do risco administrativo nem o direito de regresso do Estado, ou o fez de maneira totalmente
equivocada.
Conceito 1 – Abordou, de forma correta e suficiente, apenas um dos seguintes aspectos: (i) a responsabilidade civil do Estado é
objetiva por danos causados a terceiros por seus agentes; (ii) o direito brasileiro adota a teoria do risco administrativo; (iii) é
necessária a comprovação de determinados elementos (para cumprir esse aspecto, o(a) candidato(a) deve ter citado no mínimo
dois dos seguintes elementos: ação ou omissão, ocorrência do dano, nexo causal e ausência de excludente da responsabilidade
estatal); (iv) o Estado tem a prerrogativa de ajuizar ação contra o agente público para ressarcimento de indenização paga pelo
Estado ao particular em razão do dano causado por aquele agente público.
Conceito 2 – Abordou, de forma correta e suficiente, apenas dois dos aspectos enumerados.
Conceito 3 – Abordou, de forma correta e suficiente, apenas três dos aspectos enumerados.
Conceito 4 – Abordou, de forma correta e suficiente, todos os aspectos enumerados.
Quesito 2.2 – Competência do TCU para atuar nos casos em que irregularidade cometida por agente público resulte em
prejuízo ao erário
Conceito 0 – Não abordou a competência do TCU ou o fez de maneira totalmente equivocada.
Conceito 1 – Abordou, de forma correta e suficiente, apenas um dos seguintes aspectos: (i) o TCU exerce o controle externo; (ii)
o TCU tem competência para julgar as irregularidades que resultem em prejuízo ao erário; (iii) o TCU tem competência para
determinar o ressarcimento integral do dano ao erário.
Conceito 2 – Abordou, de forma correta e suficiente, apenas dois dos aspectos enumerados.
Conceito 3 – Abordou, de forma correta e suficiente, todos os aspectos enumerados.
TRIBUNAL DE CONTAS DA UNIÃO
AUDITOR FEDERAL DE CONTROLE EXTERNO – ÁREA DE CONTROLE
EXTERNO/ORIENTAÇÃO: AUDITORIA DE TECNOLOGIA DA
INFORMAÇÃO
Prova Discursiva – Questão 2
Aplicação: 22/2/2026
PADRÃO DE RESPOSTA DEFINITIVO
A situação descrita apresenta múltiplas falhas de configuração diretamente relacionadas à perda de confidencialidade
dos dados. A primeira falha é a permissão excessiva de acesso atribuída ao contêiner de inferência (violação do princípio
do menor privilégio), que consegue consultar buckets fora do escopo autorizado, indicando ausência de controle granular de
IAM/políticas por recurso (bucket/prefixo/ação) e de isolamento adequado entre serviços. Também há falha no processo de
atualização/promoção do modelo generativo, realizada sem revisão, validação ou “gates” de segurança no ciclo de vida
do modelo e no deploy (governança deficiente de mudanças no pipeline), o que permite que artefatos potencialmente
inseguros sejam executados no pipeline. Outra falha relevante está na configuração incorreta do deploy e das políticas de
execução/segmentação, que resulta em chamadas automáticas da pipeline para recursos não autorizados (ex.: egress não
controlado), demonstrando ausência de regras de restrição de rede (allowlist/NetworkPolicies), políticas de acesso e validação
de parâmetros. Ademais, os logs revelam comportamento anômalo do sistema, o que evidencia falta de monitoramento
preventivo e mecanismos de detecção de uso indevido. Somam-se, ainda, a inexistência ou a deficiência de política de
classificação/rotulagem dos dados e/ou DLP (Data Loss Prevention) para documentos sensíveis (“documentos internos não
rotulados”), o que impede a aplicação consistente de controles proporcionais de acesso e proteção e facilita exposição indevida
quando há erro de permissão ou roteamento do pipeline. Em conjunto, essas falhas de configuração comprometem diretamente
a confidencialidade dos documentos sensíveis, facilitando o acesso indevido e ampliando o risco de vazamento de
informações.
A mitigação exige a implementação integrada de controles técnicos e administrativos em todas as camadas do pipeline
MLOps. Por exemplo, Deve-se realizar a aplicação do princípio do mínimo privilégio, com permissões IAM estritamente
delimitadas por serviço, políticas granulares por bucket/prefixo/ação, abordagem deny-by-default e segregação por
contas/projetos/roles, usando identidades/contas de serviço dedicadas por workload (ex.: por pod) para evitar permissões
excessivas e acesso fora do escopo, além do uso de service accounts dedicadas para cada pod e segregação lógica do ambiente
por meio de namespaces, policies de rede, mecanismos de admissão como PSP/OPA e hardening sistemático das imagens. No
fluxo MLOps, No DevSecOps/segurança no pipeline, recomenda-se instituir gates formais de aprovação/revisão e gestão de
mudanças (incluindo validações automatizadas), adotar IaC (policy-as-code) para reduzir erro de deploy e, quando pertinente,
recomenda-se aplicar controles de supply chain, incluindo-se gestão segura de dependências, versionamento rastreável de
datasets e modelos, validação de integridade, varredura (scans) automáticos de vulnerabilidades em código, contêineres e
artefatos, além de assinatura e verificação do conteúdo (artefatos) antes da promoção de versões. No ambiente de contêineres, é
essencial fortalecer isolamento e políticas com Network Policies/segmentação, admission controls (ex.: OPA) e/ou policy-ascode, com controle explícito de egress (allowlist) para impedir chamadas automáticas a destinos não autorizados. Também se
sugere instituir políticas de aprovação formal de modelos antes do deploy, com testes de segurança orientados a dados — como
validação robusta de entradas, detecção de drift malicioso e prevenção de data leakage. Na etapa de entrega, recomenda-se o
uso de estratégias seguras de implantação, como shadow deployment e canary release, a fim de garantir monitoramento
controlado do comportamento do modelo antes da exposição total. A proteção das feature stores requer controle de acesso
granular, logging estruturado e trilhas de auditoria para rastrear consultas, gravações e acessos não autorizados. Como
mitigação de confidencialidade, pode-se adotar criptografia em repouso e em trânsito, com gestão adequada de chaves (KMS,
rotação e controle de acesso às chaves), desde que bem fundamentada como medida de redução de impacto em caso de acesso
indevido. Adicionalmente, deve-se prever classificação/rotulagem de dados e mecanismos de DLP, vinculando controles
proporcionais aos rótulos de sensibilidade (incluindo bloqueios/alertas de exfiltração), especialmente para endereçar o cenário
de “documentos internos não rotulados”. Por fim, recomenda-se fortalecer monitoramento/detecção e alertas baseados em logs
de auditoria, com capacidade de identificar e bloquear acessos fora do escopo (ex.: consultas a buckets não autorizados),
apoiando resposta rápida a incidentes. No pós-deploy, o monitoramento contínuo do comportamento do modelo, aliado à
detecção de anomalias, completa a defesa do pipeline, reduzindo a superfície de ataque e mitigando riscos de escalonamento de
privilégios, acessos indevidos e vazamento de dados sensíveis em ambiente de nuvem.
QUESITOS AVALIADOS
Quesito 2.1 – Falhas de configuração da segurança
Conceito 0 – Não abordou o quesito ou o fez de maneira totalmente equivocada.
Conceito 1 – Identificou apenas uma falha de configuração que compromete a confidencialidade e a descreveu de forma
superficial, incompleta, com alguma imprecisão conceitual e(ou) sem relação direta com o cenário.
Conceito 2 – Identificou duas falhas corretamente, mas as descreveu de forma incompleta, com alguma imprecisão conceitual
e(ou) sem relação direta com o cenário.
Conceito 3 – Identificou e descreveu, corretamente, duas ou mais falhas de configuração diretamente ligadas à perda de
confidencialidade no cenário descrito.
Quesito 2.2 – Medidas corretivas de segurança
Conceito 0 – Não abordou o quesito ou o fez de maneira totalmente equivocada.
Conceito 1 – Apresentou apenas uma medida de segurança relacionada ao pipeline MLOps, mas de forma superficial,
incompleta e(ou) sem relação adequada com a proteção da confidencialidade e a redução do risco de vazamento de dados em
pipelines MLOps.
Conceito 2 – Apresentou apenas uma medida correta e sua adequada relação com a proteção da confidencialidade e a redução
do risco de vazamento de dados em pipelines MLOps.
Conceito 3 – Apresentou duas medidas corretas, porém com detalhamento técnico parcialmente inconsistente, incompleto
e(ou) sem relação adequada com a proteção da confidencialidade e a redução do risco de vazamento de dados em pipelines
MLOps.
Conceito 4 – Apresentou duas ou mais medidas corretas, com detalhamento técnico consistente, demonstrando compreensão
clara de como cada controle contribui diretamente para a proteção da confidencialidade e a redução do risco de vazamento.
TRIBUNAL DE CONTAS DA UNIÃO
AUDITOR FEDERAL DE CONTROLE EXTERNO – ÁREA DE CONTROLE
EXTERNO/ORIENTAÇÃO: AUDITORIA DE TECNOLOGIA DA
INFORMAÇÃO
Prova Discursiva – Questão 3
Aplicação: 22/2/2026
PADRÃO DE RESPOSTA DEFINITIVO
Na situação descrita, há uma clara desconformidade nos papéis ou nas responsabilidades/accountabilities do
framework Scrum. O product owner falha em sua missão de maximizar o valor do produto, pois sua responsabilidade central
refere-se à gestão e priorização do product backlog e à priorização de itens, e não à remoção de impedimentos técnicos. Esta
última função compete ao scrum master, que deve atuar como líder servidor, ou verdadeiro líder que serve, e facilitador do
processo. Com a inversão dessas atribuições, comprometem-se a visão de negócio e a fluidez operacional, gerando-se um risco
de execução para a administração pública.
Quanto às práticas de engenharia, a afirmação da equipe de que utiliza TDD é tecnicamente falsa ou
incompatível/inadequada. O conceito fundamental do TDD é o desenvolvimento orientado a testes (test-first), que exige a
escrita do teste antes do código funcional no ciclo red-green-refactor ou ciclo vermelho-verde-refatorar/refatoração. A
realização de testes após a codificação desvirtua a prática, tornando-a um teste de qualidade convencional. Ademais, o foco em
interface negligencia o DDD, que é essencial para um auditor verificar a aderência do sistema às regras de negócio. O DDD
foca a modelagem do domínio e a linguagem ubíqua (ou seja, o alinhamento terminológico entre especialistas de negócio e
desenvolvedores), garantindo que o software respeite com precisão os requisitos legais e as complexas normas do setor
público, assegurando a entrega de valor real.
QUESITOS AVALIADOS
Quesito 2.1 – Papéis do product owner e do scrum master
Conceito 0 – Não avaliou a conformidade dos papéis solicitados ou afirmou que eles estão de acordo com o Guia Scrum.
Conceito 1 – Identificou o erro na situação, mas não definiu corretamente as atribuições do product owner (valor e backlog) nem do scrum
master (facilitação do processo e remoção de impedimentos).
Conceito 2 – Identificou a inversão de papéis e definiu corretamente as atribuições apenas do product owner ou do scrum master.
Conceito 3 – Identificou a inversão de papéis e definiu, de forma parcialmente correta, as atribuições do product owner e do scrum master.
Conceito 4 – Identificou a inversão de papéis e definiu corretamente as atribuições do product owner e do scrum master.
Quesito 2.2 – Engenharia e valor (TDD e DDD)
Conceito 0 – Não concluiu que a prática relatada é incompatível com TDD nem explicou a importância do DDD para a auditoria, ou o fez de
forma totalmente equivocada.
Conceito 1 – Mencionou e desenvolveu, corretamente, apenas um dos seguintes aspectos: (i) desenvolvimento orientado a testes (test-first),
que exige a escrita do teste antes do código funcional no ciclo red-green-refactor; (ii) relação do DDD com a verificação da aderência do
sistema às regras de negócio e com a entrega de valor real; (iii) DDD: foco na modelagem do domínio e na linguagem ubíqua.
Conceito 2 – Mencionou e desenvolveu, corretamente, apenas dois dos aspectos citados.
Conceito 3 – Mencionou e desenvolveu, corretamente, todos os aspectos citados.
TRIBUNAL DE CONTAS DA UNIÃO
AUDITOR FEDERAL DE CONTROLE EXTERNO – ÁREA DE CONTROLE
EXTERNO/ORIENTAÇÃO: AUDITORIA DE TECNOLOGIA DA
INFORMAÇÃO
Prova Discursiva – Peça de Natureza Prática
Aplicação: 22/2/2026
PADRÃO DE RESPOSTA DEFINITIVO
Achado 1 (irregularidade). O achado revela falhas graves no planejamento. A escolha da solução de TI deve
considerar o custo total de propriedade (TCO), abrangendo todo o ciclo de vida (implantação, migração, treinamento, suporte e
descontinuidade), e não apenas o custo de aquisição, devendo haver justificativa técnica e econômica para a preterição de
soluções de software livre disponíveis ou de soluções estruturantes de governo, como o Sistema Eletrônico de Informações
(SEI) no âmbito do Processo Eletrônico Nacional (PEN), conforme diretrizes da IN SGD/ME n.º 94/2022 e do Portal do
Software Público Brasileiro. A pesquisa de preços violou o art. 23, § 1.º, da Lei n.º 14.133/2021 e a IN SEGES/ME n.º
65/2021, que estabelecem a prioridade dos parâmetros públicos (painel de preços, contratações similares nos últimos 12 meses)
sobre orçamentos de fornecedores, a fim de se evitar sobrepreço, e cuja utilização exclusiva exige justificativa de
impossibilidade.
Achado 2 (irregularidade). A modelagem de pagamento fixo sem vinculação a resultados viola a Lei n.º
14.133/2021 (art. 144) e a IN SGD/ME n.º 94/2022. É obrigatória a definição de acordos de nível de serviço (SLA) ou
Instrumentos de Medição de Resultado (IMR) com mecanismos de glosa no pagamento proporcional ou sanções pecuniárias
proporcionais à indisponibilidade ou baixa qualidade. A ausência de cláusulas de reversibilidade e portabilidade cria risco
inaceitável de aprisionamento tecnológico (vendor lock-in). Além disso, consoante a LGPD, o tratamento de dados pessoais
sensíveis exige garantias de segurança, soberania de dados e jurisdição nacional, devendo o contrato definir os papéis de
controlador e operador e assegurar a localização do armazenamento preferencialmente em território nacional, e conformidade
na transferência ou no armazenamento em nuvem.
Achado 3 (irregularidade). Houve violação ao princípio da segregação de funções (art. 5.º da Lei n.º 14.133/2021).
A IN SGD/ME n.º 94/2022 determina papéis distintos para o fiscal técnico, o fiscal administrativo e o gestor, vedando a
acumulação que comprometa o controle, especialmente entre as funções técnica e administrativa. Observa-se, ainda, erro na
nomenclatura, pois a fase de gestão exige a designação de “fiscais” e não de “integrantes”, que são próprios da fase de
planejamento. A designação de servidor sem a devida qualificação técnica viola o princípio da eficiência e o art. 117 da Lei n.º
14.133/2021, que exige gestão por competência. Diante da alegação formal de insuficiência técnica, incumbe à administração
promover a capacitação do servidor ou prover apoio especializado de terceiros.
Conclusão. Conclui-se pela irregularidade dos três achados. Deve-se recomendar ao órgão que anule ou , suspenda ou
saneie os atos viciados para: refazer o ETP (incluindo TCO) e a pesquisa de preços; ajustar a minuta contratual (inserir SLAs/
IMRs, glosas e cláusulas de saída portabilidade/LGPD e definição de controlador/operador); e designar nova equipe de
fiscalização com a devida segregação de funções e qualificação técnica e providências de capacitação. Subsidiariamente, o
TCU poderá assinar prazo para o cumprimento da lei ou comunicar o Congresso Nacional para fins de sustação do contrato.
QUESITOS AVALIADOS
Quesito 2.1 – Análise do achado 1: irregularidade no ETP e na pesquisa de preços
Conceito 0 – Não analisou o achado 1 ou indicou sua regularidade ou o fez de forma totalmente equivocada, sem atender aos
aspectos de coesão, concisão e clareza, demonstrando falta de capacidade de análise e argumentação.
Conceito 1 – Afirmou a irregularidade do achado 1, mas não a justificou corretamente.
Conceito 2 – Afirmou a irregularidade do achado 1, abordando, corretamente, apenas um dos elementos da resposta,
demonstrando capacidade superficial de análise e argumentação.
Conceito 3 – Afirmou a irregularidade do achado 1, abordando, corretamente, apenas dois dos elementos da resposta,
demonstrando capacidade mediana de análise e argumentação.
Conceito 4 – Afirmou a irregularidade do achado 1, abordando, corretamente, todos os elementos da resposta, demonstrando
adequada capacidade de análise e argumentação quanto às falhas no planejamento: 1) escolha da solução deve considerar o
custo total de propriedade (TCO), abrangendo todo o ciclo de vida, e não apenas o custo de aquisição; 2) justificativa técnica e
econômica para a preterição de soluções de software livre disponíveis ou de governo (SEI/PEN); e 3) a pesquisa de preços ter
violado o art. 23, § 1.º, da Lei n.º 14.133/2021, que estabelece a prioridade dos parâmetros públicos (painel de preços,
contratações similares) sobre orçamentos de fornecedores, a fim de se evitar sobrepreço, em conformidade com os
procedimentos de priorização de parâmetros públicos da IN SEGES/ME n.º 65/2021.
Quesito 2.2 – Análise do achado 2: irregularidade na falta de SLA e no pagamento fixo; riscos de lock-in e violação à
LGPD; segurança em nuvem
Conceito 0 – Não analisou o achado 2 ou indicou sua regularidade ou o fez de forma totalmente equivocada, sem atender aos
aspectos de coesão, concisão e clareza, demonstrando falta de capacidade de análise e argumentação.
Conceito 1 – Afirmou a irregularidade do achado 2, mas não a justificou corretamente.
Conceito 2 – Afirmou a irregularidade do achado 2, abordando, corretamente, apenas um dos elementos da resposta,
demonstrando capacidade superficial de análise e argumentação.
Conceito 3 – Afirmou a irregularidade do achado 2, abordando, corretamente, apenas dois dos elementos da resposta,
demonstrando capacidade mediana de análise e argumentação.
Conceito 4 – Afirmou a irregularidade do achado 2, abordando, corretamente, todos os elementos da resposta, demonstrando
adequada capacidade de análise e argumentação (a modelagem de pagamento fixo sem vinculação a resultados viola a Lei n.º
14.133/2021 – art. 144 –, a Súmula TCU n.º 269 e a IN SGD/ME n.º 94/2022; é obrigatória a definição de acordos de nível de
serviço – SLA/IMR – com mecanismos de glosa no pagamento proporcional à indisponibilidade ou baixa qualidade ou sanções
proporcionais; a ausência de cláusulas de reversibilidade/portabilidade cria risco inaceitável de aprisionamento tecnológico
(lock-in) e, conforme a LGPD, o tratamento de dados pessoais sensíveis exige garantias de segurança e soberania, localização e
definição de papéis (controlador/operador).
Quesito 2.3 – Análise do achado 3: violação da segregação de funções e da qualificação técnica
Conceito 0 – Não analisou o achado 3 ou indicou sua regularidade ou o fez de forma totalmente equivocada, sem atender aos
aspectos de coesão, concisão e clareza, demonstrando falta de capacidade de análise e argumentação.
Conceito 1 – Afirmou a irregularidade do achado 3, mas não a justificou corretamente.
Conceito 2 – Afirmou a irregularidade do achado 3, abordando, corretamente, apenas um dos elementos da resposta,
demonstrando capacidade superficial de análise e argumentação.
Conceito 3 – Afirmou a irregularidade do achado 3, abordando, corretamente, apenas dois dos elementos da resposta,
demonstrando capacidade mediana de análise e argumentação.
Conceito 4 – Afirmou a irregularidade do achado 3, abordando, corretamente, todos os elementos da resposta, demonstrando
adequada capacidade de análise e argumentação (há violação ao princípio da segregação de funções – art. 5.º da Lei n.º
14.133/2021 –; os papéis do fiscal técnico, do fiscal administrativo e do gestor são distintos, sendo vedada a acumulação que
comprometa o controle e identifique a impropriedade na nomenclatura dos papéis, de acordo com a IN SGD/ME n.º 94/2022; a
designação de servidor sem a devida qualificação técnica viola o princípio da eficiência e o art. 117 da Lei n.º 14.133/2021,
que exige gestão por competência, ressaltando o dever de capacitação ou apoio técnico pela administração).
Quesito 2.4 – Conclusão: síntese da análise dos achados e recomendação de saneamento ou anulação
Conceito 0 – Não concluiu o parecer ou o fez de maneira totalmente equivocada, ou o fez de forma totalmente equivocada, sem
atender aos aspectos de coesão, concisão e clareza, demonstrando falta de capacidade de análise e argumentação.
Conceito 1 – Apresentou conclusão correta quanto a apenas um dos elementos da resposta, demonstrando capacidade
superficial de análise e argumentação.
Conceito 2 – Apresentou conclusão correta quanto a apenas dois dos elementos da resposta, demonstrando capacidade mediana
de análise e argumentação.
Conceito 3 – Apresentou conclusão correta quanto a todos os elementos da resposta, demonstrando capacidade adequada de
análise e argumentação (irregularidade dos três achados; recomendação ao órgão que anule, suspenda ou saneie os atos
viciados, admitindo-se ritos processuais do TCU, como assinatura de prazo, cautelares ou comunicação ao Congresso, para:
refazer o ETP – incluindo-se TCO – e a pesquisa de preços, ajustar a minuta contratual (inserir SLAs, glosas e cláusulas de
saída portabilidade/LGPD) e designar nova equipe de fiscalização com a devida segregação de funções e capacitação).
