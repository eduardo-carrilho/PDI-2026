# Projeto PDI 2026 - Corretor Automático de Gabaritos

Este projeto consiste em um sistema de Processamento Digital de Imagens desenvolvido para realizar a correção automática de folhas de respostas. O código utiliza técnicas de binarização, detecção de contornos e análise de densidade de pixels para identificar as alternativas marcadas.

Todo o material necessário (código, imagens de teste e documentação) está centralizado no repositório oficial.

---

## 1. Configuração do Ambiente e Download (Passo a Passo)

Siga estas instruções para preparar um ambiente Linux (Ubuntu) do zero e obter os arquivos do projeto.

### 1.1 Preparação e Download do Projeto
Abra o terminal e execute os comandos para criar a pasta e clonar o repositório:
```bash
cd ~/Documents
mkdir pdi2026
cd pdi2026
git clone https://github.com/eduardo-carrilho/PDI-2026.git
cd PDI-2026/Trabalho-Final
```
### 1.2 Instalação do Miniconda3
Caso ainda não tenha o Conda instalado, execute:
```bash
sudo apt update
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh
```

* Atenção: Durante a instalação, digite "yes" para os termos de licença e pressione ENTER para confirmar o local padrão. Quando perguntado sobre o "conda init", selecione "yes".
* Após terminar: Feche o terminal e abra um novo para que as alterações tenham efeito.

### 1.3 Configuração do Ambiente Virtual (PDI26)
Crie e configure o ambiente da disciplina:
```bash
conda config --set auto_activate_base false
conda create --name PDI26 python -y
conda activate PDI26
```

### 1.4 Instalação das Bibliotecas Necessárias
Com o prefixo (PDI26) ativo, instale as dependências:
```bash
pip install opencv-python opencv-contrib-python pillow scikit-image
pip install numpy matplotlib scikit-learn
pip install jupyter ipython gdown
```
---

## 2. Procedimento de Execução

Após clonar o repositório e configurar o ambiente, siga os passos abaixo:

1. Acesse a pasta do trabalho final:
```bash
   cd ~/Documents/pdi2026/PDI-2026/Trabalho-Final
```

2. Ative o ambiente virtual:
```bash
   conda activate PDI26
```

3. Inicie o Jupyter Notebook:
```bash
   jupyter notebook
```
4. No navegador, abra o arquivo principal (extensão .ipynb) presente na pasta.

5. Fluxo de Processamento do Código:
    - O código realiza o pré-processamento (escala de cinza e binarização).
    - Localiza as âncoras de referência para corrigir eventuais rotações da imagem.
    - Segmenta a imagem nas coordenadas de cada questão do gabarito.
    - Calcula a densidade de pixels em cada alternativa para determinar a resposta marcada.
    - Exibe o resultado da correção e a nota final.

---

### 2.1 Como interagir com o Jupyter Notebook

Uma vez com o arquivo aberto no navegador, siga estas instruções:

1. **Execução Sequencial:** Clique na primeira célula de código e pressione **Shift + Enter** para executá-la e avançar para a próxima.
2. **Execução Total:** Para rodar todo o projeto de uma vez, vá no menu superior em **Cell** > **Run All** (ou **Célula** > **Executar Tudo**).
3. **Indicadores de Status:**
   - O símbolo `[*]` ao lado da célula indica que o processamento está em andamento.
   - O símbolo `[número]` (ex: `[1]`) indica que a execução daquela célula foi concluída.
4. **Visualização:** Os resultados das imagens processadas e a nota final aparecerão logo abaixo das respectivas células de código.

### 2.2 Pré-requisitos de Hardware e Preparação do Gabarito

Para que o sistema funcione corretamente, atente-se aos seguintes pontos:

1. **Webcam Obrigatória:** O sistema utiliza a câmera em tempo real para capturar a imagem do gabarito. Certifique-se de que sua webcam está conectada e funcional no Ubuntu.
2. **Uso do Gabarito Oficial:** O algoritmo está calibrado especificamente para o modelo gerado pelo próprio código. Não utilize folhas de respostas de outros modelos.
3. **Gerando a Folha de Respostas:** - Antes de iniciar a correção, execute a célula específica do notebook que contém o método de geração de gabarito.
   - O arquivo será salvo automaticamente na pasta `data/images` do projeto.
   - Imprima ou exiba este arquivo gerado para que a webcam possa realizar a leitura.

## 3. Requisitos de Software Adicionais (Opcional)
Para visualizar arquivos auxiliares ou editar scripts fora do ambiente Jupyter:
```bash
conda deactivate
sudo apt update
sudo apt install vlc geany -y
```