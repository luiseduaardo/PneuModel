# 🫁 | PneuModel: Classificação de imagens na análise de exames de Raio-X torácico para identificação de Pneumonia

O **PneuModel** é um modelo de inteligência artificial baseado em visão computacional que realiza a classificação de imagens de raio-x para retornar a probabilidade de infecção por pneumonia. Essa solução visa otimizar o tempo de triagem, ofertando suporte técnico e uma alternativa diagnóstica para a análise de exames torácicos.

## 📂 | Arquitetura do projeto

```
├── notebooks/
│   ├── eda.ipynb           # Análise exploratória e visualização do dataset.
│   ├── treinamento.ipynb   # Pipeline de pré-processamento, Transfer Learning e Fine-tuning.
│   └── inferencia.ipynb    # Carregamento do modelo salvo e geração de submissão (Kaggle).
├── dataset/                # (Criado na execução) Armazena as imagens de treino/validação.
├── requirements.txt        # Dependências do projeto
├── modelo.keras            # Artefato do modelo treinado (gerado após o treino).
├── submission.csv          # Submissão final do Kaggle (gerado após a inferência).
└── README.md               # Documentação do projeto.
```

## ⚙️ | Instruções de execução
### 💻 | Escolha de ambiente e dependências
Para executar o projeto, é recomendado usar o Google Colab (com aceleração de GPU para agilizar o treinamento) para facilitar a instalação das dependências e o download automático do dataset via API do Google Drive, além de permitir a exportação e importação do modelo no Drive nos notebooks de treinamento e inferência, respectivamente.

Além disso, para garantir a reprodutibilidade do projeto, os notebooks foram estruturados de forma que a configuração do ambiente ocorra de maneira totalmente automatizada. Ao iniciar a execução de qualquer um dos arquivos na pasta notebooks/, o sistema realiza automaticamente o clone do repositório oficial do GitHub e a instalação de todas as dependências necessárias através do comando `pip install -r requirements.txt`.

### 🧠 | Treinamento do modelo
1. Abra o arquivo notebooks/treinamento.ipynb.
2. Execute as células para realizar o pré-processamento das imagens e o treinamento do modelo.
3. O modelo treinado será salvo automaticamente na raiz do projeto e exportado para o Google Drive.

Observação: caso os notebooks sejam executados em outro ambiente que não o Google Colab, a célula de exportação para o Google Drive não funcionará da maneira devida, mas o modelo estará na raiz do projeto. Nesse caso, para executar o notebook de inferência, será necessário trocar os caminhos do arquivo.

Para realizar essa troca, basta removar a importação do drive (`from google.colab import drive`) na 4ª célula e na 5ª célula, remover o `drive.mount` e mudar o caminho da variável `model_path_drive` para o caminho `./modelo.keras`.

### 📄 | Geração do arquivo .csv de submissão
1. Abra o arquivo `notebooks/inferencia.ipynb`.
2. Este notebook carregará o modelo salvo no Google Drive (caso esteja sendo usado o Google Colab) e processará as imagens da pasta de teste da competição.
3. O script exportará um arquivo .csv formatado com os campos exigidos na submissão do Kaggle.
4. Faça o upload do modelo no Kaggle para obter o seu resultado da submissão.

## 📊 | Métrica de Avaliação do Modelo
O desempenho do modelo é mensurado primariamente pela métrica **ROC AUC** (Receiver Operating Characteristic - Area Under the Curve), que mede a capacidade do modelo em distinguir entre as classes (Normal vs. Pneumonia), isto é, quanto maior o AUC, melhor o modelo é em prever casos de pneumonia como pneumonia e casos normais como normais.

| Métrica | Valor (0-1) | Valor (%) | Local |
|------|---------|--------|--------|
| ROC-AUC de Treinamento | 0.99960 | 99,960% | Treinamento |
| ROC-AUC de Validação   | 0.99800 | 99,800% | Treinamento | 
| ROC-AUC de Inferência  | 0.99034 | 99,034% | Inferência/Kaggle |

## 🛠️ | Tecnologias utilizadas
- Framework de Visão Computacional: TensorFlow / Keras.
- Arquitetura Base: EfficientNetB0 e ResNet50 (tentativa inicial).
- Processamento de Imagem: OpenCV e Matplotlib.
- Interpretabilidade (xAI): tf-explain (Grad-CAM) para visualização das áreas de ativação do pulmão.
