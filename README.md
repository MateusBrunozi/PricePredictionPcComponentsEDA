Previsão de Preços de Componentes de Computador

Este é um projeto de Machine Learning que visa desenvolver e avaliar modelos de regressão para prever o preço de componentes de hardware de PC com base em suas especificações técnicas.

O projeto foi desenvolvido como parte da disciplina de Inteligência Artificial do Curso Ciência da Computação do IFGoiano Campus Iporá e cobre um pipeline completo, desde a coleta e limpeza de dados até a otimização de hiperparâmetros e análise de resultados.

---

Objetivos

O objetivo principal deste trabalho foi construir um modelo que pudesse estimar o valor (em Reais - BRL) de um componente de PC. Os objetivos específicos incluíram:

* **Coleta de Dados:** Carregar e consolidar múltiplos arquivos CSV de diferentes categorias de produtos em um único dataset.
* **Análise Exploratória (EDA):** Entender a distribuição dos dados, identificar a assimetria dos preços e justificar a transformação logarítmica.
* **Pré-processamento:** Implementar um pipeline robusto para tratar valores ausentes (NaNs) e converter dados categóricos em numéricos (One-Hot Encoding).
* **Modelagem (Baseline):** Estabelecer um modelo base de `Regressão Linear` para medir a melhoria futura.
* **Modelagem (Avançada):** Implementar um modelo `Random Forest` e avaliá-lo usando Validação Cruzada (K-Fold).
* **Refinamento:** Otimizar os hiperparâmetros do `Random Forest` com `RandomizedSearchCV` para encontrar o melhor desempenho possível.
* **Análise de Performance:** Interpretar os resultados do modelo final, analisando o gráfico de Resíduos (erros) e o gráfico de Importância de Features (especificações mais relevantes).

---

Dataset Utilizado(Créditos)

Este projeto não seria possível sem o dataset público disponibilizado no Kaggle.

* **Título Original:** PC components data set (computer data)
* **Autor:** [sudhanshuy17](https://www.kaggle.com/sudhanshuy17)
* **Fonte:** Kaggle
* **Link:** [https://www.kaggle.com/datasets/sudhanshuy17/pccomponents](https://www.kaggle.com/datasets/sudhanshuy17/pccomponents)

Para este projeto, a coluna de preço `MRP` (em Rúpias Indianas - INR) foi limpa e convertida para Reais (BRL), usando uma taxa de câmbio estática para fins de análise.

---

Metodologia e Pipeline

O notebook principal (`.ipynb`) segue um fluxo de trabalho estruturado:

1.  **Carga dos Dados:** O notebook clona o próprio repositório GitHub para acessar os arquivos CSV da pasta `DataSetPcComponents` (anteriormente `Trabalho IA`).
2.  **Limpeza e EDA:** A variável alvo (preço) é limpa e transformada (`np.log1p`) para corrigir a assimetria.
3.  **Pré-processamento:**
    * NaNs numéricos são preenchidos com `0` (interpretados como "não aplicável").
    * NaNs categóricos são preenchidos com `"missing"`.
    * Colunas categóricas são convertidas via `pd.get_dummies`.
4.  **Validação de Modelos:** Os modelos são avaliados usando `cross_val_score` (K=5) sobre o conjunto de treino para uma métrica de MAE (Erro Médio Absoluto) mais robusta.
5.  **Otimização:** O `RandomizedSearchCV` (CV=3, n_iter=10) é usado para "tunar" o Random Forest.
6.  **Análise Final:** O melhor modelo é usado para gerar previsões no conjunto de teste (`X_test`), e os gráficos de Resíduos e Importância de Features são gerados.

---

Principais Resultados

O modelo final (Random Forest Otimizado) demonstrou ser significativamente superior ao baseline de Regressão Linear.

* **Métrica (MAE):** O modelo otimizado atingiu um **Erro Médio Absoluto (MAE) de R$ [PREENCHA O MAE FINAL AQUI, ex: R$ 45,80]** no conjunto de teste.
* **Feature Mais Importante:** A análise de `feature_importances_` revelou que a **Categoria** do produto (ex: `Category_GPU`, `Category_Motherboard`) é, de longe, o fator mais determinante para o preço.
* **Análise de Resíduos:** O gráfico de resíduos mostrou que o modelo é **altamente preciso para itens de baixo e médio custo**, mas apresenta heteroscedasticidade, tendendo a **subestimar** (chutar para baixo) o preço de itens *high-end* (muito caros).

---

Como Executar

Este projeto está contido em um único notebook Jupyter e é configurado para ser totalmente reprodutível.

1.  **Clone o repositório:**
    ```bash
    git clone [https://github.com/MateusBrunozi/PricePredictionPcComponentsEDA.git](https://github.com/MateusBrunozi/PricePredictionPcComponentsEDA.git)
    ```
2.  **Abra o Notebook:**
    Carregue o arquivo `.ipynb` no **Google Colab** (recomendado) ou em um ambiente Jupyter local.
3.  **Execute:**
    O notebook está configurado (Bloco 2) para clonar este próprio repositório e ler os dados da pasta `DataSetPcComponents`. Basta executar todas as células em ordem.

---

Ferramentas Utilizadas

* Python 3
* Pandas
* Numpy
* Matplotlib & Seaborn
* Scikit-learn (para `LinearRegression`, `RandomForestRegressor`, `cross_val_score`, `RandomizedSearchCV`)
* Google Colab

---

## 👨‍💻 Autor

* **Mateus Brunozi** - [GitHub](https://github.com/MateusBrunozi)
