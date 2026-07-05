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
* **Torneio de Algoritmos:** Avaliação de 12 modelos concorrentes via validação cruzada (10-fold) que consolidou o domínio de *Ensembles* e revelou a insuficiência preditiva das abordagens lineares.
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
| **MAPE** (Principal) | Abaixo de 25,00% | 94,67% | **23,81%** | **Atingida** |
| **RMSE** (Secundária) | Redução > 20,00% | USD 70.442,60 | **USD 47.446,68** ( -32,6% ) | **Atingida** |
| **Tempo de Treino** | Baixo custo computacional | ~2 segundos | **~2,5 segundos** | **Atingida** |

### 🔧 Como Executar

* **Opção 1 (Via Google Colab):** Clique no arquivo `Sprint3_MVP_Machine_Learning.ipynb` aqui no repositório. Na pré-visualização que se abrirá, clique no botão **Open in Colab** no topo da página para executar o projeto na nuvem de forma 100% automatizada e reprodutível.

* **Opção 2 (Ambiente Local):** Caso prefira rodar localmente (Jupyter ou VS Code), baixe o notebook e o arquivo `used_cars.csv` para o mesmo diretório e garanta a instalação do ecossistema do *Scikit-Learn* e da biblioteca *XGBoost*.

### 📝 Nota Técnica: Fronteiras de Atuação do MVP

Apesar do sucesso preditivo nos segmentos de volume, o MVP apresenta limitações conhecidas que delimitam suas fronteiras de atuação. O modelo encontra dificuldades no segmento de carros de luxo e exóticos devido à forte oscilação de preços típica desse nicho e à ausência de variáveis qualitativas no dataset original (como o estado de conservação do veículo e o histórico de manutenção mecânica). Essa carência de informações explica por que o RMSE global foi impactado por esse nicho específico, gerando cenários onde o uso automatizado do modelo deve ser restrito ao mercado de massa e acompanhado por auditoria humana para veículos de alto padrão.

### 📜 Licença

Este projeto utiliza dados sob a licença Attribution 4.0 International (CC BY 4.0).
