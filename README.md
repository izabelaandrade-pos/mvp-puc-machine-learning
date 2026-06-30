# mvp-puc-machine-learning
Repositório para documentação do MVP produzido na Sprint de Machine Learning parte da pós graduação em Ciência de Dados e Analytics da PUC-RJ.

## 🚗 Previsão de Preços de Veículos Usados (Modelagem & Otimização)

Este repositório contém o projeto de **Engenharia de Machine Learning e Modelagem Preditiva** focado no mercado de carros usados dos EUA. O objetivo principal é construir, avaliar e otimizar modelos de regressão para automatizar a estimativa de preço de revenda, fornecendo uma ferramenta de apoio à decisão comercial rápida e precisa para vendedores individuais.

### 📌 Principais Funcionalidades & Insights

* **Pipelines de Produção Isolados:** Centralização de todas as etapas de pré-processamento via pipelines reprodutíveis para garantir o isolamento completo dos dados e evitar o vazamento de dados (*data leakage*).
* **Tratamento Avançado de Outliers:** Implementação de um transformador customizado baseado em IQR integrado ao fluxo de validação cruzada, tratando dados extremos de forma automatizada.
* **Tratamento de Alta Cardinalidade:** Resolução do desafio técnico da variável `model` (quase 1.900 classes) por meio da aplicação estratégica de *Target Encoding*, compactando a informação sem explodir a dimensionalidade.
* **Torneio de Algoritmos com Validação Cruzada:** Avaliação comparativa robusta utilizando validação cruzada em 10 *folds* envolvendo 12 algoritmos concorrentes, revelando o sob-ajuste (*underfitting*) das abordagens lineares.
* **Rejeição de Modelos Especialistas:** Validação experimental que refutou a hipótese de criar modelos separados por marca, provando que um modelo generalista unificado estabiliza melhor o aprendizado das regras de desvalorização.
* **Otimização Híbrida de Hiperparâmetros:** Estratégia em duas etapas utilizando *RandomizedSearchCV* para varredura ampla, seguida por *GridSearchCV* local, reduzindo o tempo de varredura computacional para menos de 2 minutos.
* **Apoio à Decisão via XGBoost:** Seleção do algoritmo campeão ponderando o erro comercial (MAPE de 23,20% no teste), controle de erros absolutos extremos (RMSE de USD 50.169,59) e tempo de treino de apenas 2 segundos.

### 🛠 Tecnologias Utilizadas

* **Linguagem:** Python 3.x
* **Bibliotecas principais:** Scikit-learn, XGBoost, Imbalanced-learn, Pandas, NumPy.
* **Ambiente:** Google Colab (executado integralmente em nuvem via CPU gratuita).

### 📂 Estrutura do Projeto

* `used_cars.csv`: Dataset original (espelhado do Kaggle/Cars.com).
* `Sprint3_MVP_Machine_Learning.ipynb`: Notebook principal com o pipeline completo de engenharia, treinamento e otimização.
* `README.md`: Documentação do projeto.

### 🚀 Critérios de Sucesso & Resultados Encontrados

O projeto foi balizado por metas rígidas de negócio em relação ao *baseline* estatístico ingênuo (Dummy Regressor baseado na mediana):

| Métrica | Meta de Sucesso | Baseline (Dummy) | XGBoost Otimizado (Teste) | Status |
| :--- | :--- | :--- | :--- | :--- |
| **MAPE** (Principal) | Abaixo de 25,00% | 94,67% | **23,20%** | **Atingida** |
| **RMSE** (Secundária) | Redução > 20,00% | USD 70.442,60 | **USD 50.169,59** ( -28,77% ) | **Atingida** |
| **Tempo de Treino** | Baixo custo computacional | ~1,5 segundos | **~2 segundos** | **Atingida** |

### 🔧 Como Executar

#### Passo 1: Clonar o Repositório

Execute o comando `git clone https://github.com/izabelaandrade-pos/mvp-puc-machine-learning.git` no seu terminal para baixar o projeto localmente.

#### Passo 2: Execução no Google Colab

Importe o arquivo `Sprint3_MVP_Machine_Learning.ipynb` diretamente para o ambiente do Google Colab. O notebook já está totalmente configurado para baixar o dataset via URL pública do GitHub de forma 100% automatizada e reprodutível, utilizando a semente fixa `SEED = 7`. Não há necessidade de uploads manuais ou chaves de API.

#### Passo 3: Execução em Ambiente Local

Caso prefira utilizar Jupyter Notebook ou VS Code localmente, certifique-se de ter o Python 3.x instalado junto com as bibliotecas contidas no ecossistema básico do Scikit-learn, além da biblioteca externa `xgboost`. O arquivo de dados `used_cars.csv` deve estar no mesmo diretório do notebook.

### 📝 Nota Técnica: Fronteiras de Atuação do MVP

Apesar do sucesso preditivo nos segmentos de volume, o MVP apresenta limitações conhecidas que delimitam suas fronteiras de atuação. Essa carência de dados explica por que o RMSE global foi severamente impactado pelo segmento de luxo. Isto ocorre devido à volatilidade inerente a esses ativos e à ausência de variáveis qualitativas no dataset original (como estado de conservação da pintura, tapeçaria e histórico de manutenção). Recomenda-se o uso automatizado do modelo para o segmento de volume e auditoria humana para veículos exóticos.

### 📜 Licença

Este projeto utiliza dados sob a licença Attribution 4.0 International (CC BY 4.0).
