# Documentação Unificada: Laboratório 6 e Roteiro Experimental (LEx)

**Disciplina:** MCZA018 - Processamento Digital de Imagens (2026.1)

**Equipe:** Eduardo Carrilho, Gabriel Figueiredo

**Data:** 14/04/2026

---

## PARTE 1: Relatório do Laboratório 6 (Limiarização)

### 1. Introdução
O objetivo deste relatório é descrever as atividades de segmentação por limiarização (*thresholding*). A técnica consiste em converter uma imagem de tons de cinzento para binário, isolando objetos de interesse do fundo. Exploramos métodos manuais e automáticos (Otsu) em imagens estáticas, vídeo em tempo real e no protótipo do nosso Projeto Final.

### 2. Procedimentos Experimentais
* **Fotos e Avatares:** Testamos a binarização manual nas fotos da equipe para encontrar o ponto ideal de separação no histograma.
* **Webcam em Tempo Real:** Implementamos um script que alterna entre limiarização manual (fixa em 150) e automática (Otsu) através da tecla 'C'.
* **Aplicação no Projeto Final:** Utilizamos a binarização de Otsu invertida para extrair as marcações de caneta em gabaritos de testes.

### 3. Análise de Resultados e Discussão
Identificamos que o método de Otsu é superior ao manual em condições de luz controlada. No entanto, ao testarmos o gabarito do nosso projeto com iluminação irregular, observamos que sombras densas são interpretadas incorretamente como "objetos" (tinta), causando manchas na binarização global.



**Conclusão:** A limiarização global é sensível a gradientes de luz. Para o sucesso do sistema de correção de gabaritos em ambientes reais, é imperativo o uso de pré-processamentos como equalização de histograma (CLAHE) ou limiares adaptativos.

---

## PARTE 2: Laboratório Experimental (LEx) - Guia do Usuário

Este guia foi elaborado para que um usuário externo consiga operar o **Sistema de Processamento Visual (SPV)** de correção de gabaritos.

### 1. Introdução ao Sistema
O sistema utiliza visão computacional para ler e corrigir provas automaticamente. Através da webcam, o software identifica a folha, alinha a imagem e conta as marcações feitas nas bolhas.
* **Interface:** Rectângulo verde indica detecção da folha; Janela secundária exibe a correção.

### 2. Procedimento Passo a Passo
1. **Preparação:** Preencha o gabarito com caneta preta ou azul escura.
2. **Execução:** Inicie o programa e posicione a folha frente à câmera.
3. **Travamento:** Aguarde o sistema exibir a mensagem **"ALVO TRAVADO!"** (contorno verde estável).
4. **Captura:** Pressione a tecla **'C'**. O sistema processará a imagem e abrirá a tela com a nota.
5. **Reset:** Pressione **'R'** para limpar a memória e ler uma nova prova.

### 3. Questionário Didático (Avaliação do Usuário)
* **Q1:** Conseguiu entender a diferença entre a imagem original e a imagem binarizada (preta e branca) na tela?
* **Q2:** O sistema identificou corretamente todas as bolhas que você preencheu?
* **Q3:** Como o sistema se comportou quando você inclinou ligeiramente a folha?

### 4. Enquete Subjetiva de Opinião
**Escala de 1 a 5 (1 - Muito Ruim / 5 - Excelente):**
1. Facilidade de uso da interface: [ ]
2. Velocidade de resposta do sistema: [ ]
3. Utilidade prática do corretor: [ ]

**Pergunta Aberta:** * Qual melhoria você sugeriria para facilitar o uso por um professor em sala de aula?

---

## PARTE 4: Descrição Técnica do Projeto (GitHub/README)

### 🚀 O que o Sistema Faz
O software é um sistema de **Reconhecimento de Marcas Ópticas (OMR)**. Ele automatiza a correção de provas utilizando processamento de vídeo em tempo real.

### 🛠️ Lógica de Implementação
1. **Warp Perspective:** Alinha a folha para remover distorções de ângulo, garantindo que o computador veja o papel de cima.
2. **Otsu Invertido:** Binariza a imagem transformando a tinta em pixels brancos e o papel em preto para facilitar a detecção de contornos.
3. **Segmentação por Densidade:** O sistema conta a quantidade de pixels brancos dentro de cada bolha; a alternativa com maior densidade é considerada a marcada.

### 📋 Referências Consultadas
* Gonzalez, R. C., & Woods, R. E. (2018). *Digital Image Processing*.
* Documentação OpenCV: *Image Thresholding Tutorial*.
* Material Didático: Prof. Francisco Zampirolli e Prof. Celso Kurashima (UFABC).
