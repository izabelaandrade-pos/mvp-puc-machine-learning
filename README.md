# mvp-puc-machine-learning
Repositório para documentação do MVP produzido na Sprint de Machine Learning parte da pós graduação em Ciência de Dados e Analytics da PUC-RJ.

## 🚗 Previsão de Preços de Veículos Usados (Modelagem & Otimização)

Este repositório contém o projeto de **Machine Learning e Modelagem Preditiva** focado no mercado de carros usados dos EUA. O objetivo principal é construir, avaliar e otimizar modelos de regressão para automatizar a estimativa de preço de revenda, fornecendo uma ferramenta de apoio à decisão comercial rápida e precisa para vendedores individuais.

### 📌 Principais Funcionalidades & Insights

#### 🛠️ Engenharia de Atributos & Pré-processamento
* **Imputação Lógica e Higienização:** Correção de tipos de dados e preenchimento de valores ausentes baseado no conhecimento extraído do *dataset* e em regras de negócio, evitando o descarte de linhas.
* **Feature Engineering e Redução de Cardinalidade:** Criação da variável de idade do veículo, agrupamento estratégico de diversas variáveis com alta cardinalidade (como marcas e transmissões) e aplicação de *Target Encoding* para compactar os quase 1.900 modelos de carros.
* **Estabilização da Variância:** Aplicação de escala logarítmica na variável alvo preço e filtragem seletiva de *outliers* via IQR, preservando os extremos reais de potência dos motores.

#### 🤖 Modelagem & Otimização de Machine Learning
* **Pipeline Reprodutível e Isolado:** Centralização de todo o pré-processamento e modelagem em um fluxo unificado, eliminando qualquer risco de vazamento de dados (*data leakage*).
* **Torneio de Algoritmos:** Avaliação de 12 modelos concorrentes via validação cruzada (10-fold) que consolidou o domínio de *Ensembles* e revelou o *underfitting* severo das abordagens lineares.
* **Rejeição de Modelos Especialistas:** Validação experimental que refutou a divisão do projeto por *tiers* de marcas, provando que o ganho marginal não justificava o aumento de complexidade na arquitetura.
* **Otimização Híbrida e Eficiente:** Busca em duas etapas (*Random Search* + *Grid Search*) que localizou os melhores hiperparâmetros do XGBoost em menos de 2 minutos.

### 🛠 Tecnologias Utilizadas

* **Linguagem:** Python 3.x
* **Bibliotecas de Machine Learning:** Scikit-learn, XGBoost, Imbalanced-learn (para construção do pipeline de dados).
* **Análise e Visualização:** Pandas, NumPy, Matplotlib, Seaborn.
* **Ambiente:** Google Colab (executado integralmente em nuvem via CPU gratuita).

### 📂 Estrutura do Projeto

* `used_cars.csv`: Dataset original (espelhado do Kaggle/Cars.com).
* `Sprint3_MVP_Machine_Learning.ipynb`: Notebook principal com o pipeline completo de pré-processamento, treinamento e otimização.
* `README.md`: Documentação do projeto.

### 🚀 Critérios de Sucesso & Resultados Encontrados

O projeto foi balizado por metas de negócio em relação ao *baseline* estatístico ingênuo (Dummy Regressor baseado na mediana):

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

Apesar do sucesso preditivo nos segmentos de volume, o MVP apresenta limitações conhecidas que delimitam suas fronteiras de atuação. O modelo encontra dificuldades no segmento de carros de luxo e exóticos devido à forte oscilação de preços típica desse nicho e à ausência de variáveis qualitativas no dataset original (como o estado de conservação do veículo e o histórico de manutenção mecânica). Essa carência de informações explica por que o RMSE global foi impactado por esse nicho específico, gerando cenários onde o uso automatizado do modelo deve ser restrito ao mercado de massa e acompanhado por auditoria humana para veículos de alto padrão.

### 📜 Licença

Este projeto utiliza dados sob a licença Attribution 4.0 International (CC BY 4.0).
