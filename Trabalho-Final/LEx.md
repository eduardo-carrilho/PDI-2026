# Laboratório Experimental do SPV (LEx): Sistema de Correção OMR

**Projeto:** Digitalizador e Corretor Automático de Gabaritos

**Equipe:** Eduardo Carrilho, Gabriel Figueiredo

**Data:** 14/04/2026

---

## 1. Introdução: Como o sistema funciona?
O nosso Sistema de Processamento Visual (SPV) foi desenvolvido para automatizar a correção de provas de múltipla escolha. Ele utiliza a câmara do computador para identificar um gabarito, alinhar a imagem e extrair as respostas marcadas pelo aluno.

### A Interface e Operação:
* **Janela de Visualização:** Mostra o feed da webcam em tempo real. Um **retângulo verde** aparecerá automaticamente assim que o sistema detetar as bordas da folha de papel.
* **Mensagem de Status:** Exibe "ALVO TRAVADO!" quando a folha está posicionada corretamente para leitura.
* **Janela de Resultados:** Após o processamento, uma janela secundária exibe o gabarito com a correção (certo/errado) e a nota final.

---

## 2. Procedimento Experimental (Instruções ao Usuário)
Siga estes passos detalhados para executar o experimento:

1.  **Preparação:** Utilize um gabarito impresso e preencha as bolhas de alternativas utilizando uma caneta de cor escura (preta ou azul).
2.  **Ambiente:** Certifique-se de que a folha está bem iluminada e sem sombras pesadas sobre as bolhas.
3.  **Alinhamento:** Posicione o gabarito em frente à webcam até que o retângulo verde de deteção fique estável.
4.  **Captura (Tecla 'C'):** Quando o sistema travar no alvo, pressione a tecla **'C'**. O software irá capturar o frame, corrigir a perspetiva e realizar a binarização da imagem.
5.  **Coleta de Resultados:** Observe na tela de correção a nota atribuída e se as marcações detetadas correspondem ao que você preencheu.
6.  **Reinício (Tecla 'R'):** Para escanear uma nova prova, pressione **'R'** na janela principal.



---

## 3. Questionário Didático
*Responda após realizar o experimento para validar o aprendizado:*

1.  O sistema conseguiu processar a imagem corretamente mesmo se o papel estivesse ligeiramente inclinado ou torto em relação à câmara?
2.  Ao observar a imagem binarizada (preto e branco), o que representam os pontos brancos na tela?
3.  Você notou alguma falha na leitura quando existiam sombras muito fortes sobre o papel? Como isso afetou o resultado?

---

## 4. Enquete Subjetiva de Opinião
**Escala de 1 a 5 (1 = Discordo Totalmente / 5 = Concordo Totalmente):**
1.  As instruções do sistema são claras para um utilizador leigo? ( )
2.  O sistema de "travamento" automático da folha facilitou a captura? ( )
3.  A velocidade de correção foi satisfatória? ( )

**Perguntas Abertas:**
1.  Qual foi a sua percepção sobre a utilidade deste sistema em uma sala de aula real?
2.  Que sugestão de melhoria você daria para a interface do programa?

---

## 5. Descrição Técnica (Documentação do Projeto)

### 🚀 Metodologia de Processamento
O sistema opera através de quatro pilares de Visão Computacional:
1.  **Warp Perspective (Alinhamento):** Utiliza a deteção de contornos para encontrar os quatro cantos da folha e aplica uma transformação matemática para "esticar" a imagem, removendo distorções de ângulo.
2.  **Binarização de Otsu Invertida:** Calcula o limiar ideal para separar o papel (fundo) da tinta (objeto), convertendo a caneta em pixels brancos (valor 255).
3.  **Filtragem de Áreas:** O software segmenta apenas os objetos que possuem tamanho e proporção circular compatíveis com as bolhas do gabarito.
4.  **Análise de Densidade:** O sistema conta os pixels brancos dentro de cada uma das 5 alternativas de cada questão. A alternativa com maior densidade de pixels é registada como a escolha do aluno.

### 🛠️ Tecnologias e Dependências
* **Linguagem:** Python 3.10+
* **Bibliotecas:** OpenCV (Processamento), NumPy (Matrizes), Matplotlib (Gráficos).
