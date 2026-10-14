---
tipo: flashcard
disciplina: "Arquitetura e Integração de Sistemas"
tema: "Integração com dados e IA"
data: "2026-10-14"
tags:
  - flashcard
---

# Flashcards: Integração com dados e IA

> Deck baseado no resumo [[Integração com dados e IA - Arquitetura e Integração de Sistemas]].
> Cada card traz a pergunta e a resposta na mesma linha.

## Serviços de dados (consumo e disponibilização)

O que significa consumir um serviço de dados? :: Integrar-se a uma API/interface (REST/HTTP, gRPC, GraphQL, mensageria) respeitando o contrato e as restrições do provedor.

O que define o contrato de uma API REST? :: Nome do recurso, formato (JSON/XML), semântica dos campos e códigos de status; costuma ser descrito por OpenAPI/Swagger.

Como tratar versionamento, paginação, limites e resiliência? :: Breaking changes exigem nova versão (como /v1 e /v2); iterar todas as páginas; respeitar o status 429, o cabeçalho Retry-After e o backoff; timeouts, retry com jitter, circuit breaker e cache; POST pode exigir idempotency key.

O que é disponibilizar um serviço de dados? :: Expor os dados da organização como um serviço consumível (por aplicações, analistas e LLMs), tratando a API como produto, com versionamento e depreciação planejada.

O que envolve governança, segurança e formatos na exposição de dados? :: Governança com classificação, dono do dado (data owner), linhagem e qualidade; segurança com escopo mínimo e auditoria; SLA e observabilidade; formato JSON (padrão), protobuf/gRPC (alto desempenho) ou GraphQL (flexível).

## Modelos de linguagem como serviço

O que é um token e o que é a janela de contexto? :: Token é a unidade de texto processada (input/prompt e output); o custo é medido por token e a janela de contexto limita o total de entrada mais saída.

Quais são os papéis de mensagem (chat roles)? :: system (instruções de mais alta prioridade), user (entrada do usuário) e assistant (resposta do modelo).

Quais os principais parâmetros de geração? :: temperature (aleatoriedade; 0 = mais determinístico), top_p (nucleus sampling), max_tokens (limite de saída) e stop/seed (término e reprodutibilidade aproximada).

O que são streaming e saídas estruturadas? :: Streaming entrega a resposta em pedaços via SSE, reduzindo a latência percebida; JSON mode/structured outputs e function/tool calling devolvem dados em schema previsível.

O que é alucinação e por que a geração é estocástica? :: O modelo pode gerar conteúdo plausível e falso (mitiga-se com grounding/RAG); a mesma entrada pode produzir saídas diferentes, o que impacta testes e avaliação.

Boas práticas no consumo responsável e na disponibilização de IA? :: Segredos em cofre com rotação (nunca no cliente), gateway de LLM, controle de custo/latência (cache semântico e roteamento), privacidade/LGPD e fallback; expor o modelo em endpoint REST/gRPC com autenticação, cotas, schema, telemetria, sandbox e limites de recursos.

## Embeddings

O que é um embedding e qual sua propriedade fundamental? :: Uma função que mapeia texto/imagem/áudio para um vetor denso de números reais, capturando significado (semântica) e não a forma literal; itens semanticamente próximos ficam próximos no espaço vetorial.

Modelos de embeddings e a dimensionalidade? :: text-embedding-3-small (1536 dim.) e text-embedding-3-large (3072 dim.) da OpenAI, all-MiniLM-L6-v2; mais dimensões dão mais capacidade de representação, mas mais custo.

O que é um embedding normalizado e qual seu risco? :: Norma 1 torna o produto interno equivalente ao cosseno; embeddings não são interpretáveis e podem sofrer inversão (embedding inversion), revelando o texto original.

## Métricas de similaridade e distância

O que medem a similaridade de cosseno e o produto interno? :: Cosseno mede o ângulo entre vetores (de -1 a 1), ignorando a magnitude; o produto interno considera magnitude e direção e equivale ao cosseno quando os vetores são normalizados.

Quando usar a distância euclidiana (L2) e as métricas binárias? :: A L2 (reta entre pontos) é sensível à magnitude e adequada quando escala importa; Hamming e Jaccard servem a vetores binários.

Qual a regra de ouro da métrica e quais operadores o pgvector usa? :: Usar a mesma métrica com que o modelo foi treinado; no pgvector, <-> (L2), <#> (produto interno negativo), <=> (cosseno), <+> (L1), <~> (Hamming) e <%> (Jaccard).

## Busca semântica, ANN e pgvector

Busca lexical e busca semântica, como se diferenciam? :: A lexical usa termos exatos (TF-IDF, BM25) e não entende sinônimos; a semântica usa embeddings e vizinhos mais próximos, entendendo paráfrases.

Busca exata (k-NN) e aproximada (ANN), como se diferenciam? :: A exata compara com todos os vetores, com recall perfeito e custo alto; a ANN troca um pouco de recall por velocidade.

Como funciona o índice HNSW? :: É um grafo multinível, com a melhor relação velocidade-recall de consulta, mas construção mais lenta e mais uso de memória; parâmetros m, ef_construction e ef_search.

Como funciona o índice IVFFlat? :: Usa listas invertidas, com construção mais rápida e menos memória, mas menor desempenho de consulta; parâmetros lists (semear após carregar os dados) e probes.

O que é o pgvector e como lidar com filtro e multitenancy? :: Extensão do PostgreSQL que mantém vetores junto aos dados relacionais, herdando ACID, JOINs, replicação e RLS; o filtro por metadados é aplicado depois da varredura do índice (mitigar com iterative scans ou particionamento), e o índice compartilhado pode afetar recall entre tenants, isolando-se por particionamento.

## RAG (Retrieval-Augmented Generation)

O que é RAG? :: Recuperar trechos relevantes de fontes externas e injetá-los no prompt como contexto fundamentado, em vez de confiar só no conhecimento paramétrico do modelo.

Qual o pipeline típico de RAG? :: Ingestão, extração/limpeza, chunking, embeddings, indexação, consulta, retrieval top-k, re-ranking, montagem do prompt, geração e pós-processamento.

O que é chunking e por que é o ajuste de maior alavancagem? :: Dividir documentos em pedaços; tamanho e sobreposição (overlap) são os botões principais — chunks grandes diluem o sinal e gastam contexto, pequenos perdem contexto; ajuda incluir título/seção.

O que é retrieval top-k e re-ranking? :: Top-k busca os vizinhos mais similares; o re-ranking reordena candidatos com cross-encoder (avalia consulta e documento juntos), em uma arquitetura de dois estágios, sendo mais preciso que a similaridade vetorial.

O que é busca híbrida e Reciprocal Rank Fusion (RRF)? :: Combinar busca densa (vetorial) com lexical (BM25); o RRF funde listas somando um sobre k mais a posição de cada documento, ou seja, por posição e não por score bruto.

O que é HyDE e query augmentation? :: HyDE gera uma resposta hipotética e a usa como consulta; outras formas são múltiplas consultas (multi-query) e reescrita de consulta.

RAG e fine-tuning, como se complementam? :: O RAG injeta conhecimento/atualização em tempo de execução; o fine-tuning ajusta comportamento/estilo/formato com dados de treino — são frequentemente complementares.

Quais as limitações e riscos do RAG? :: Alucinação residual, knowledge conflict, lost in the middle, injeção indireta de prompt, envenenamento do índice (poisoning) e behavior alteration.

## Agentes e ferramentas

O que é um LLM aumentado (augmented LLM)? :: A unidade básica: um modelo com recuperação (retrieval), ferramentas (tools) e memória, que gera consultas, escolhe ferramentas e decide o que reter.

Workflow e agente, como se diferenciam? :: O workflow orquestra LLMs e ferramentas por caminhos de código predefinidos (determinístico); o agente dirige dinamicamente seu próprio processo e uso de ferramentas.

O que é o loop agêntico e o padrão ReAct? :: Perceber, planejar, agir (chamar ferramenta), observar e repetir até uma condição de parada; ReAct intercala raciocínio (Reasoning) e ação (Acting).

Quais são os padrões de workflow (Anthropic)? :: Prompt chaining (com portões), routing, parallelization (sectioning e voting), orchestrator-workers e evaluator-optimizer.

Como funciona o function/tool calling e onde o código roda? :: O desenvolvedor define funções com nome, descrição e input_schema; o modelo devolve um bloco tool_use, a aplicação executa e devolve o tool_result. Client tools rodam na sua aplicação; server tools, na infraestrutura do provedor.

O que é o MCP? :: Model Context Protocol, um padrão aberto ("USB-C para aplicações de IA") em arquitetura cliente-servidor para conectar IA a dados, ferramentas e workflows; o risco é ampliar a superfície de ataque, exigindo menor privilégio e allowlist.

## Memória e multiagentes

Memória e riscos em agentes e multiagentes? :: Curto prazo é o contexto da conversa; longo prazo é persistida e alvo de memory poisoning. Multiagentes têm falhas em cascata, escalada de privilégio e propagação de injeções, exigindo fronteiras de confiança e autenticação entre agentes.

## Avaliação funcional

Quais as três frentes da avaliação funcional? :: Recuperação, geração e, para agentes, ações/ferramentas.

O que medem Precision@k e Recall@k? :: Precision@k é a fração dos k itens recuperados que é relevante; Recall@k é a fração dos itens relevantes que foi recuperada.

O que medem MRR e NDCG? :: MRR (Mean Reciprocal Rank) mede quão alto está o primeiro acerto; NDCG mede a qualidade do ranqueamento com ganho descontado pela posição.

O que é faithfulness/groundedness e o que é a RAG Triad? :: Faithfulness é a razão entre claims suportadas pelo contexto e o total de claims (métrica central de alucinação); a tríade tem relevância do contexto, fidelidade e relevância da resposta.

O que é o RAGAS e quais métricas clássicas existem? :: RAGAS é uma suíte de métricas reference-free (Context Precision, Context Recall etc.); as clássicas são BLEU, ROUGE, CHRF, Exact Match e String Presence.

Como avaliar agentes, fontes e o LLM-as-a-judge? :: Agentes: Tool Call Accuracy, Tool Call F1, Agent Goal Accuracy e Topic Adherence; fontes: procedência, atualidade, atribuição e conflito; o juiz automático tem viés e exige rubricas.

## Limites de autorização e supervisão

O que são menor privilégio e mediação completa? :: Dar ao modelo/agente o mínimo de ferramentas e permissões; a autorização é feita fora do modelo, no sistema de destino, a cada requisição.

O que é confused deputy e fail closed? :: Usar privilégio indevidamente em nome de outro — evita-se executando a ação no contexto do usuário; fail closed é negar quando a verificação falha ou a ferramenta é desconhecida.

O que é human-in-the-loop e quais controles de supervisão existem? :: Exigir aprovação humana para ações de alto impacto/irreversíveis, vinculada à ação exata e de uso único; registrar chamadas e decisões com redação, ter kill switch e limites de iteração/tokens/custo (evita Denial of Wallet).

## Injeção de prompt

O que é prompt injection? :: Uma vulnerabilidade em que entradas fazem o LLM se comportar de forma não intencionada; a causa-raiz é instruções e dados processados juntos, sem separação clara.

Injeção direta e indireta, como se diferenciam? :: A direta vem do próprio usuário; a indireta vem de conteúdo externo (web, documentos, e-mails, comentários, RAG) e é o risco-chave em agentes.

O que é jailbreak? :: Uma forma de injeção que faz o modelo ignorar suas salvaguardas, usando personas como "DAN" ou cenários hipotéticos.

Quais técnicas de ataque a banca pode citar? :: Codificação/ofuscação (Base64, hex, Unicode invisível), typoglycemia, payload splitting, adversarial suffix, best-of-N, injeção multimodal e RAG poisoning.

Quais as mitigações de injeção (defesa em profundidade)? :: Separar instrução de dado (rótulos não são fronteira de segurança), restringir o comportamento do modelo, validar entrada/saída e sanitizar conteúdo remoto, usar guardrails, menor privilégio e HITL.

O que é o padrão Dual-LLM/CaMeL? :: Separar um LLM privilegiado (planeja, não vê dados não confiáveis) de um LLM em quarentena (lê o conteúdo suspeito, mas sem acesso a ferramentas), rastreando fluxo de dados e capabilities.

## OWASP Top 10 for LLM Applications (2025)

O que são LLM01 e LLM02? :: LLM01 Prompt Injection (direta e indireta; RAG e fine-tuning não eliminam); LLM02 Sensitive Information Disclosure (vazamento de PII, segredos e dados proprietários).

O que são LLM03 e LLM04? :: LLM03 Supply Chain (dependências, modelos, provedores, dados de treino); LLM04 Data and Model Poisoning (pré-treino, fine-tuning, embeddings).

O que são LLM05 e LLM06? :: LLM05 Improper Output Handling (saída sem validação, gera XSS e injeções downstream); LLM06 Excessive Agency (funcionalidade, permissões ou autonomia em excesso).

O que são LLM07, LLM08 e LLM09? :: LLM07 System Prompt Leakage (não colocar segredos no prompt); LLM08 Vector and Embedding Weaknesses (inversão, poisoning, vazamento); LLM09 Misinformation (alucinação).

O que é LLM10? :: Unbounded Consumption: consumo ilimitado, gerando custo/DoS (Denial of Wallet).

## Comparações e pegadinhas

O RAG elimina alucinação e prompt injection? :: Não; ele reduz a alucinação, mas não a elimina, e não elimina a injeção de prompt.

Produto interno e cosseno são sempre iguais? :: Não; só são equivalentes quando os vetores são normalizados.

Embedding, banco vetorial e busca semântica são a mesma coisa? :: Não; o embedding é a representação, o banco vetorial é o armazenamento/índice e a busca semântica é a operação.

O function calling executa a função no provedor e temperature zero garante determinismo? :: Não; em client tools a sua aplicação executa a função, e temperature zero reduz a variação mas não garante reprodutibilidade total.

Qual a diferença entre faithfulness e correctness? :: Faithfulness é adesão ao contexto recuperado; correctness é verdade factual — uma resposta pode ser fiel a um contexto errado.
