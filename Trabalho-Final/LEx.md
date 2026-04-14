# Relatório Técnico e Roteiro Experimental: Sistema de Correção OMR

**Equipe:** Eduardo Carrilho, Gabriel Figueiredo
**Disciplina:** MCZA018 - Processamento Digital de Imagens (UFABC)  
**Data:** 14/04/2026  

---

## 1. Introdução e Objetivos
Este documento descreve o desenvolvimento e a execução do **Sistema de Processamento Visual (SPV)** para correção automática de gabaritos (Optical Mark Recognition - OMR). O objetivo é aplicar conceitos de filtragem, binarização e segmentação morfológica para extrair informações de uma imagem capturada em tempo real via webcam.

---

## 2. Descrição Técnica do Projeto

Diferente de métodos de segmentação global simples, este sistema foi projetado para ser robusto em cenários reais de iluminação. O pipeline de processamento consiste em:

### 2.1 Detecção e Alinhamento (align_gabarito)
O sistema monitora o feed de vídeo em busca de **marcas de registro** (quatro quadrados pretos nos cantos). Através da função `cv2.getPerspectiveTransform`, a folha é "planificada" para uma resolução fixa de 600x800 pixels, corrigindo distorções de ângulo.

### 2.2 Pré-processamento Avançado (preprocess_image)
Para resolver os problemas de sombras identificados nos laboratórios iniciais, implementamos:
* **CLAHE (Contrast Limited Adaptive Histogram Equalization):** Equaliza o contraste em blocos de 8x8 para destacar a caneta mesmo em áreas escuras.
* **Limiarização Adaptativa (Gaussian):** Calcula o limiar de binarização localmente (janela de 71 pixels), ignorando gradientes de iluminação global.
* **Operações Morfológicas:** Aplicação de abertura (`MORPH_OPEN`) para eliminar ruídos de captura.

### 2.3 Segmentação e Correção (evaluate_respostas)
* **Algoritmo Watershed:** Utilizado para garantir a separação de bolhas caso o preenchimento do aluno tenha extrapolado os limites e unido dois círculos vizinhos.
* **Análise de Densidade:** O sistema conta pixels não nulos em cada bolha. Uma marcação é válida se ultrapassar o limiar de **1150 pixels**.
* **Feedback Visual:** O sistema indica em tempo real questões certas (Verde), erradas (Vermelho), anuladas por marcação dupla (Rosa) ou em branco (Ciano).

---

## 3. Laboratório Experimental (LEx)

Este roteiro permite a reprodução dos experimentos realizados pela equipe.

### 3.1 Materiais Necessários
* Webcam funcional e Python 3.10+.
* Dependências: `opencv-python`, `numpy`.
* Gabarito impresso ou gerado pela função `gerar_gabarito()`.

### 3.2 Procedimento Passo a Passo
1.  **Preparação:** Execute a função `gerar_gabarito()` para salvar o arquivo de teste `gabarito_teste.png`.
2.  **Inicialização:** Execute o script principal (`main(0)`).
3.  **Travamento de Alvo:** Aproxime o gabarito da câmera. Quando os 4 quadrados forem detectados, o contorno da folha ficará **Verde** com o aviso **"ALVO TRAVADO!"**.
4.  **Captura e Processamento:** Pressione a tecla **'C'**.
    * A janela **"Scanner Corretor"** exibirá o resultado final e a nota.
    * A janela **"DEBUG - Visao Binaria"** mostrará como os filtros adaptativos trataram a imagem.
5.  **Nova Leitura:** Pressione **'R'** para resetar o modo de captura e testar um novo gabarito.

---

## 4. Análise e Discussão dos Resultados

### 4.1 Superação do "Efeito Sombra"
Durante os testes com limiarização de Otsu (Lab 6), sombras densas causavam a perda de dados. Com a transição para a **Limiarização Adaptativa**, o sistema tornou-se capaz de ler o gabarito mesmo com iluminação lateral severa, pois o limiar de binarização "segue" a variação da luz sobre o papel.

### 4.2 Precisão da Segmentação
O uso do **Watershed** baseado na transformada de distância provou ser essencial. Em testes onde o círculo foi preenchido de forma grosseira, o algoritmo conseguiu encontrar os centros de massa individuais, evitando que o sistema pulasse questões por "contorno inválido".

---

## 5. Conclusões
O projeto atingiu os requisitos de um Sistema de Processamento Visual funcional. A combinação de transformações espaciais para alinhamento e técnicas de segmentação local resultou em um corretor de provas preciso e prático para o uso docente.

---

## 6. Referências
* GONZALEZ, R. C.; WOODS, R. E. **Digital Image Processing**. 4. ed. Pearson, 2018.
* OPENCV. **Image Thresholding**. Documentação Oficial.
* ZAMPIROLLI, F.; KURASHIMA, C. **Roteiros de Processamento Digital de Imagens**, UFABC, 2026.
