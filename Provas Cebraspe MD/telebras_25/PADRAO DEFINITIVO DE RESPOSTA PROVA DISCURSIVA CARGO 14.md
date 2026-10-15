---
tipo: prova
concurso: "telebras_25"
arquivo_origem: "Provas Cebraspe/telebras_25/PADRAO DEFINITIVO DE RESPOSTA PROVA DISCURSIVA CARGO 14.pdf"
tags:
  - prova
  - cebraspe
  - cgu-2026
---

# PADRAO DEFINITIVO DE RESPOSTA PROVA DISCURSIVA CARGO 14

TELECOMUNICAÇÕES BRASILEIRAS S.A.
ESPECIALISTA EM GESTÃO DE TELECOMUNICAÇÕES
ENGENHEIRO – SUBATIVIDADE: ENGENHEIRO ELETRICISTA
Prova Discursiva
Aplicação: 8/2/2026
PADRÃO DE RESPOSTA DEFINITIVO
No sistema SCADA descrito, a codificação de fonte tem como objetivo principal reduzir a redundância dos dados
medidos nas subestações, comprimindo as medições, sem perda de conteúdo relevante. Isso permite otimizar a utilização do
canal limitado em banda e reduzir a quantidade de bits transmitidos. Por outro lado, a codificação de canal adiciona redundância
controlada para possibilitar a detecção e correção de erros introduzidos pelo ruído térmico e pelas interferências eletromagnéticas
presentes no ambiente industrial. Essa codificação garante maior confiabilidade na transmissão de sinais críticos, o que reduz a
probabilidade de falhas no sistema de supervisão.
Quanto à modulação por pulsos, o sistema pode adotar diferentes técnicas, conforme o requisito de robustez e
eficiência. Na técnica PAM (pulse amplitude modulation), a amplitude de cada pulso varia proporcionalmente ao sinal de
informação, o que permite implementação relativamente simples, mas torna o sistema mais vulnerável ao ruído, pois qualquer
variação de amplitude afeta diretamente o dado recebido. Na técnica PWM (pulse width modulation), a largura do pulso é
proporcional ao sinal de informação, oferecendo maior imunidade a ruído em amplitude, mas exigindo maior complexidade de
geração e detecção. Por sua vez, a técnica PPM (pulse position modulation) codifica a informação na posição temporal do pulso,
o que proporciona excelente imunidade a ruído e eficiência energética, porém requer sincronização precisa e circuitos mais
complexos.
Para evitar interferência intersimbólica (ISI), é fundamental aplicar o critério de Nyquist que determina a largura de
banda mínima necessária para transmissão de símbolos sem sobreposição temporal e espectral. A limitação de banda impõe um
compromisso entre a taxa de transmissão de símbolos e a qualidade do sinal recebido: uma largura de banda insuficiente resulta
em distorção dos pulsos e em aumento da taxa de erro, mesmo com codificação de canal eficiente. Portanto, a combinação de
codificação de fonte e canal, de modulação por pulsos adequada e de aplicação dos critérios de Nyquist é essencial para garantir
transmissão confiável e eficiente no sistema SCADA, mesmo em um ambiente industrial ruidoso e com restrições de canal. Além
disso, para garantir simultaneamente a ausência de ISI e de aliasing, a taxa de amostragem deve ser superior ao dobro da maior
frequência presente no sinal. Essa condição — também fundamentada no critério de Nyquist — assegura que o sinal seja
representado fielmente no domínio discreto, evitando sobreposição espectral (aliasing) e preservando a integridade dos pulsos
transmitidos. Assim, a adoção de uma taxa de amostragem maior que duas vezes a maior frequência do sinal não é apenas uma
recomendação teórica, mas um requisito essencial para manter a fidelidade da informação e a robustez da comunicação.
QUESITOS AVALIADOS
Quesito 2.1 – Contribuições da codificação de fonte e da codificação de canal
Conceito 0 – Não atendeu ao quesito ou o fez de forma totalmente equivocada.
Conceito 1 – Esclareceu sobre a codificação de canal e(ou) a codificação de fonte, mas não explicitou sua contribuição para a
eficiência da transmissão e para a mitigação dos efeitos do ruído e das interferências presentes no ambiente industrial.
Conceito 2 – Esclareceu, corretamente, sobre apenas uma contribuição (eficiência da transmissão ou mitigação dos efeitos do
ruído e das interferências presentes no ambiente industrial) de uma das codificações somente.
Conceito 3 – Esclareceu, corretamente, sobre as contribuições (eficiência da transmissão e mitigação dos efeitos do ruído e das
interferências presentes no ambiente industrial) de uma das codificações somente.
Conceito 4 – Esclareceu, corretamente, sobre apenas uma contribuição (eficiência da transmissão ou mitigação dos efeitos do
ruído e das interferências presentes no ambiente industrial) de ambas as codificações.
Conceito 5 – Esclareceu, corretamente, sobre as contribuições (eficiência da transmissão e mitigação dos efeitos do ruído e das
interferências presentes no ambiente industrial) de ambas as codificações.
Quesito 2.2 – Pulsos PAM, PWM e PPM
Quesito 2.2.1 – PAM: eficiência espectral, complexidade de implementação e suscetibilidade ao ruído
Conceito 0 – Não abordou a técnica PAM ou o fez de forma totalmente equivocada.
Conceito 1 – Comentou sobre a técnica PAM, mas não a avaliou quanto a nenhum dos aspectos solicitados (eficiência espectral,
complexidade de implementação e suscetibilidade ao ruído).
Conceito 2 – Avaliou a técnica PAM, corretamente, quanto a apenas um dos aspectos solicitados.
Conceito 3 – Avaliou a técnica PAM, corretamente, quanto a apenas dois dos aspectos solicitados.
Conceito 4 – Avaliou a técnica PAM, corretamente, quanto aos três aspectos solicitados.
Quesito 2.2.2 – PWM: eficiência espectral, complexidade de implementação e suscetibilidade ao ruído
Conceito 0 – Não abordou a técnica PWM ou o fez de forma totalmente equivocada.
Conceito 1 – Comentou sobre a técnica PWM, mas não a avaliou quanto a nenhum dos aspectos solicitados (eficiência espectral,
complexidade de implementação e suscetibilidade ao ruído).
Conceito 2 – Avaliou a técnica PWM, corretamente, quanto a apenas um dos aspectos solicitados.
Conceito 3 – Avaliou a técnica PWM, corretamente, quanto a apenas dois dos aspectos solicitados.
Conceito 4 – Avaliou a técnica PWM, corretamente, quanto aos três aspectos solicitados.
Quesito 2.2.3 – PPM: eficiência espectral, complexidade de implementação e suscetibilidade ao ruído
Conceito 0 – Não abordou a técnica PPM ou o fez de forma totalmente equivocada.
Conceito 1 – Comentou sobre a técnica PPM, mas não a avaliou quanto a nenhum dos aspectos solicitados (eficiência espectral,
complexidade de implementação e suscetibilidade ao ruído).
Conceito 2 – Avaliou a técnica PPM, corretamente, quanto a apenas um dos aspectos solicitados.
Conceito 3 – Avaliou a técnica PPM, corretamente, quanto a apenas dois dos aspectos solicitados.
Conceito 4 – Avaliou a técnica PPM, corretamente, quanto aos três aspectos solicitados.
Quesito 2.3 – Aplicação dos critérios de Nyquist
Conceito 0 – Não atendeu ao quesito ou o fez de forma totalmente equivocada.
Conceito 1 – Comentou sobre os critérios de Nyquist, mas não explicitou como evitar a interferência intersimbólica.
Conceito 2 – Abordou corretamente o impacto da adoção dos critérios de Nyquist para evitar a interferência intersimbólica.
