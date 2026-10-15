---
tipo: prova
concurso: "tce_rn_25"
arquivo_origem: "Provas Cebraspe/tce_rn_25/PADRAO DEFINITIVO DE RESPOSTA PROVA DISCURSIVA CARGO 11.pdf"
tags:
  - prova
  - cebraspe
  - cgu-2026
---

# PADRAO DEFINITIVO DE RESPOSTA PROVA DISCURSIVA CARGO 11

TRIBUNAL DE CONTAS DO ESTADO DO RIO GRANDE DO
NORTE
CARGO 11: AUDITOR DE CONTROLE EXTERNO – ESPECIALIDADE:
ESTATÍSTICA
Prova Discursiva – Estudo de caso
Aplicação: 11/4/2026
PADRÃO DE RESPOSTA DEFINITIVO
Dada uma realização amostral x1, ..., xn extraída da distribuição de Laplace, a função de log-verossimilhança pode ser
|x μ|
representada sob a forma l(μ, σ) = – nln(2) – nln(σ) − ∑ni=1 i . Para se obter o EMV de μ, fixando-se σ, observe-se que
σ
maximizar l(μ, σ) equivale a minimizar ∑ni=1|xi μ|. É um resultado clássico em que essa soma é minimizada pela mediana
amostral, de modo que μ = mediana (x1, ..., xn). Logo, μ = mediana (0, 0, 1, 1, 2, 2, 3, 4, 5, 10) = 2.
|x μ|
∂l μ,σ
n
∑ni=1 i 2 .
Para se obter o EMV de σ, fixa-se μ e deriva-se a log-verossimilhança em relação a σ,
∂σ
σ
σ
∑n |x μ|. Os desvios absolutos em torno da mediana
Igualando-se a zero, e combinando-se com a solução μ, obtém-se σ
n i=1 i
são 3, 1, 0, 1, 8, 0, 2, 2, 2, 1, cuja soma é 20. Assim, σ = 20/10 = 2.
Para amostras grandes, os erros-padrão podem ser estimados pela teoria assintótica. No caso de 𝜇̂ , usa-se a distribuição
assintótica da mediana amostral. Como a densidade da Laplace no ponto central vale 𝑓 𝜇
1/ 2𝜎 , obtém-se √𝑛 𝜇̂ 𝜇
→ 𝑁 0, 𝜎 , de modo que o erro-padrão assintótico de 𝜇̂ é aproximadamente 𝜎/√𝑛, sendo usual substituí-lo por 𝜎/√𝑛. Para 𝜎,
pode-se usar a informação de Fisher ou a expansão assintótica do estimador; obtendo-se √𝑛 𝜎 𝜎 → 𝑁 0, 𝜎 , de modo que
o erro-padrão assintótico de 𝜎 também é aproximadamente 𝜎/√𝑛, estimado na prática por 𝜎/√𝑛. Logo, os erros-padrão de
ambos são iguais a 2/√10.
QUESITOS AVALIADOS
Quesito 2.1 – EMV de μ
Conceito 0 – Não apresentou a estimativa ou o fez de forma totalmente equivocada.
Conceito 1 – Apresentou a estimativa de forma parcialmente correta.
Conceito 2 – Apresentou corretamente a estimativa.
Quesito 2.2 – EMV de 𝝈
Conceito 0 – Não apresentou a estimativa ou o fez de forma totalmente equivocada.
Conceito 1 – Apresentou a estimativa de forma parcialmente correta.
Conceito 2 – Apresentou corretamente a estimativa.
Quesito 2.3 – Erros-padrão desses estimadores para 𝒏 grande
Conceito 0 – Não apresentou o cálculo de nenhum dos erros-padrão solicitados ou o fez de forma totalmente equivocada.
Conceito 1 – Apresentou corretamente o cálculo de apenas um dos erros-padrão solicitados.
Conceito 2 – Apresentou corretamente o cálculo de ambos os erros-padrão solicitados.
