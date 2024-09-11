# Dogecoin Price Prediction

Este projeto tem como objetivo prever os preços do Dogecoin usando técnicas de aprendizado de máquina. Ele envolve a análise de dados históricos, extração de características, treinamento de um modelo de regressão linear, e a implementação de uma estratégia de investimento baseada nas previsões.

## Índice

- [Imports](#imports)
- [Data Description](#data-description)
- [Exploratory Data Analysis (EDA)](#exploratory-data-analysis-eda)
- [Data Preprocessing and Metrics Explanation](#data-preprocessing-and-metrics-explanation)
- [Linear Regression - Tuning, Testing, and Plotting](#linear-regression---tuning-testing-and-plotting)
- [Importing Dogecoin Data from April 2024 to September 2024](#importing-dogecoin-data-from-april-2024-to-september-2024)
- [Investment Strategy](#investment-strategy)

## Imports

Nesta seção, todas as bibliotecas e pacotes necessários são importados:

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
import plotly.express as px
import numpy as np
from plotly.subplots import make_subplots

from sklearn.model_selection import train_test_split
from sklearn.preprocessing import PolynomialFeatures,StandardScaler,MinMaxScaler
from sklearn.pipeline import Pipeline
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error, mean_absolute_error,r2_score
from sklearn.linear_model import Lasso, Ridge, ElasticNet
from sklearn.ensemble import GradientBoostingRegressor
from sklearn.neighbors import KNeighborsRegressor
from sklearn.svm import SVR
from sklearn.model_selection import cross_val_score, KFold
```
## Data Description

O conjunto de dados inclui informações históricas do Dogecoin, com as seguintes variáveis principais:

- **Date**: Data da observação.
- **Open**: Preço de abertura do Dogecoin no início do período.
- **High**: Preço máximo alcançado pelo Dogecoin no período.
- **Low**: Preço mínimo alcançado pelo Dogecoin no período.
- **Close**: Preço de fechamento do Dogecoin no final do período.
- **Volume**: Volume de Dogecoin negociado durante o período.

Os dados cobrem um intervalo de tempo específico e são usados para treinar e testar o modelo de previsão de preços.

## Exploratory Data Analysis (EDA)

Nesta seção, exploramos o comportamento do preço de fechamento do Dogecoin ao longo do tempo, identificando tendências e variações significativas. A análise está dividida nas seguintes partes:

### 1. Visualização do Preço de Fechamento ao Longo do Tempo
![Gráfico do fechamento dogecoin](https://github.com/Ito-Santana/Machine_Learning_Projects/blob/main/Dogecoin_Close_Prediction/image_ignore/0.png)

Iniciamos com uma visualização do preço de fechamento (`Close`) do Dogecoin ao longo de todo o período de dados disponível. Observamos que o preço de fechamento foi relativamente constante entre 2017 e 2021. Portanto, focamos a análise no período após 01/01/2021, quando as variações se tornaram mais significativas.

![Gráfico do fechamento dogecoin](https://github.com/Ito-Santana/Machine_Learning_Projects/blob/main/Dogecoin_Close_Prediction/image_ignore/1.jpeg)

### 2. Identificação de Picos de Preço

Durante o período analisado, identificamos que o preço de fechamento atingiu seu valor máximo em 07/05/2021 e seu valor mínimo em 01/01/2021. Essa identificação ajuda a entender os momentos de maior volatilidade do ativo.

### 3. Análise das Tendências

Dividimos o período pós-2021 em quatro principais tendências de preço:

- **Tendência Ascendente (fevereiro 2021 - maio 2021)**: O preço de fechamento do Dogecoin apresentou um aumento significativo, culminando no valor máximo em maio de 2021.
- **Tendência Descendente (maio 2021 - agosto 2021)**: Após o pico, observou-se uma queda acentuada nos preços.
- **Tendência Descendente (outubro 2021 - outubro 2022)**: Outro período de queda, onde o preço continuou a diminuir de forma mais moderada.
- **Tendência Ascendente (janeiro 2024 - março 2024)**: No início de 2024, o preço do Dogecoin voltou a subir, indicando uma possível recuperação.

Em cada uma dessas tendências, analisamos as variações diárias no preço, identificando dias com variações positivas e negativas e somando a variação total durante o período.

### 4. Matriz de Correlação
![Matriz de correlação](https://github.com/Ito-Santana/Machine_Learning_Projects/blob/main/Dogecoin_Close_Prediction/image_ignore/corr.png)

Geramos uma matriz de correlação para entender as relações entre as variáveis principais: `Open`, `High`, `Low`, e `Close`. A análise mostrou que essas variáveis são altamente correlacionadas, o que é esperado em dados financeiros como estes. Isso nos ajuda a entender como essas variáveis influenciam o modelo de previsão.

---

Com essas análises, obtemos uma compreensão mais profunda dos dados, permitindo que as etapas subsequentes de modelagem e estratégia de investimento sejam baseadas em insights sólidos.

## Pré-processamento de Dados e Explicação das Métricas

### Métricas

#### Erro Quadrático Médio (RMSE)
- **Definição**: O RMSE é uma métrica amplamente utilizada para avaliar o desempenho de modelos de regressão. Ele mede a raiz quadrada da média dos quadrados das diferenças entre os valores preditos e os valores reais.
- **Fórmula**: 
 
  ![Fórmula do RMSE](https://github.com/Ito-Santana/Machine_Learning_Projects/blob/main/Dogecoin_Close_Prediction/image_ignore/rmse.png)
- **Por que usar RMSE**:
  - **Sensibilidade a Erros Grandes**: O RMSE dá mais peso a erros grandes devido ao quadrado das diferenças. Isso é útil quando erros grandes são indesejáveis e devem ser penalizados mais severamente.
  - **Dependente de Escala**: O RMSE está na mesma unidade da variável alvo, o que facilita a interpretação no contexto dos dados.
  - **Comparação entre Modelos**: Permite a comparação direta dos erros de previsão entre diferentes modelos, assumindo que as unidades de medida sejam consistentes.

#### Erro Absoluto Médio (MAE)
- **Definição**: O MAE é outra métrica para avaliar modelos de regressão. Ele mede a magnitude média dos erros nas previsões, sem considerar a direção dos erros.
- **Fórmula**:
  
  ![Fórmula do MAE](https://github.com/Ito-Santana/Machine_Learning_Projects/blob/main/Dogecoin_Close_Prediction/image_ignore/mae.png)
- **Por que usar MAE**:
  - **Simplicidade**: O MAE é simples de entender e interpretar, pois fornece a média das diferenças absolutas entre os valores preditos e os valores reais.
  - **Robusto a Outliers**: Ao contrário do RMSE, o MAE é menos sensível a outliers, pois não eleva os erros ao quadrado. Isso pode ser vantajoso se o conjunto de dados contiver pontos de dados ruidosos ou anômalos.
  - **Dependente de Escala**: Assim como o RMSE, o MAE está na mesma unidade da variável alvo, facilitando a interpretação.

### Melhores Modelos Avaliados

#### Regressão Linear
#### GradientBoostingRegressor

## Linear Regression - Tuning, Testing and Plotting
![Resultado na base de teste](https://github.com/Ito-Santana/Machine_Learning_Projects/blob/main/Dogecoin_Close_Prediction/image_ignore/testing.png)

## Testando os dados para os meses de aril a setembro de 2024
![Teste com dados de 2024](https://github.com/Ito-Santana/Machine_Learning_Projects/blob/main/Dogecoin_Close_Prediction/image_ignore/testing%202024%20error.png)

## Estratégias de Investimento e Resultados

Para avaliar o desempenho de diferentes estratégias de investimento no projeto de previsão de preços do Dogecoin, utilizamos quatro abordagens distintas:

### 1. Moving Average Crossover
- **Descrição**: Utiliza duas médias móveis (curta e longa) para gerar sinais de compra e venda baseados nos pontos de cruzamento.
- **Resultado**: A estratégia apresentou um valor final do investimento de R$611,06, resultando em um prejuízo de R$388,94.

### 2. Momentum
- **Descrição**: Baseia-se na continuidade de tendências, gerando sinais de compra quando a mudança no preço é positiva e sinais de venda quando é negativa.
- **Resultado**: A estratégia gerou um valor final do investimento de R$743,05, com um prejuízo de R$256,95.

### 3. Mean Reversion
- **Descrição**: Assume que os preços retornam à média histórica, gerando sinais de compra quando o preço está abaixo da média e sinais de venda quando está acima.
- **Resultado**: Esta estratégia obteve um valor final do investimento de R$1073,94, resultando em um lucro de R$73,94.

### 4. Dynamic Allocation
- **Descrição**: Ajusta a alocação do investimento com base na volatilidade do mercado, aumentando a exposição quando a volatilidade é baixa e reduzindo quando é alta.
- **Resultado**: O valor final do investimento foi de R$1041,91, com um lucro de R$41,91.

Esses resultados demonstram que a estratégia de **Mean Reversion** foi a mais lucrativa, seguida pela estratégia de **Dynamic Allocation**. As estratégias de **Moving Average Crossover** e **Momentum** apresentaram desempenho negativo.
