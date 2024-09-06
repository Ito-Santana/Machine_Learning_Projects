# Detecção de Fraudes em Cartões de Crédito - 0.8776


## Objetivo

O objetivo deste projeto é desenvolver um modelo de aprendizado de máquina para identificar transações fraudulentas em um conjunto de dados de transações de cartões de crédito. Detectar fraudes é crucial para garantir que os clientes não sejam cobrados por transações que não realizaram.

## Descrição do Conjunto de Dados

- **Período:** Setembro de 2013
- **Total de Transações:** 284.807
- **Fraudes:** 492 (0,172% do total)
- **Características:**
  - **V1 a V28:** Componentes principais obtidos via PCA. Essas características são transformações das variáveis originais e não podem ser interpretadas diretamente.
  - **Tempo:** Tempo em segundos desde a primeira transação.
  - **Valor:** Valor da transação.
  - **Classe:** Variável alvo (0 para não-fraude e 1 para fraude).

## Desafios

O conjunto de dados é altamente desequilibrado, com a classe positiva (fraudes) representando apenas 0,172% das transações. Isso torna a acurácia tradicional uma métrica menos confiável. 
[Link para o dataset no Kaggle](https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud)

## Importação de Dados e Bibliotecas

O primeiro passo no projeto é a importação dos dados e das bibliotecas necessárias. Os dados utilizados neste projeto são provenientes de transações de cartões de crédito, e as bibliotecas incluem ferramentas para análise de dados, pré-processamento e modelagem.

## Análise Exploratória de Dados (EDA)

Durante a Análise Exploratória de Dados, foram realizadas as seguintes etapas:

1. **Matriz de Correlação:** Plotei a matriz de correlação e observei que as variáveis possuem uma correlação linear entre si. Isso pode indicar que algumas variáveis estão relacionadas e podem ter impacto na detecção de fraudes.


2. **Distribuição das Transações:** Analisei a distribuição das transações fraudulentas e não fraudulentas para entender a diferença entre essas classes. Essa análise ajuda a visualizar a desproporção entre as transações fraudulentas e não fraudulentas.
 ![Distribuição das Transações](https://github.com/Ito-Santana/Machine_Learning_Projects/blob/main/Credit_card_fraud_detection/ignore/newplot%20(8).png)


3. **Violin Plot das Transações Fraudulentas:** Criei um violin plot para visualizar a distribuição dos valores das transações fraudulentas. Este gráfico fornece uma visão detalhada da dispersão e da densidade dos valores das transações fraudulentas.
![Violin Plot das Transações Fraudulentas](https://github.com/Ito-Santana/Machine_Learning_Projects/blob/main/Credit_card_fraud_detection/ignore/newplot%20(9).png)

## Resultados do Pré-processamento de Dados

Os resultados das análises de pré-processamento de dados indicam que o melhor recall foi alcançado quando os dados foram escalonados usando `StandardScaler`, os outliers foram deixados intocados e o método de peso de classe foi aplicado.

## Seleção de Modelo
. A escolha do recall como métrica principal foi motivada pelo desequilíbrio significativo no conjunto de dados, onde as transações fraudulentas representam uma fração muito pequena das transações totais. Em cenários de desequilíbrio como este, o recall é crucial, pois mede a capacidade do modelo de identificar corretamente as instâncias positivas (neste caso, as fraudes).

Utilizei a validação cruzada estratificada K-Fold para treinar e avaliar vários modelos, com foco na métrica de recall devido ao desequilíbrio dos dados.

### Modelos Avaliados:

1. **Regressão Logística**
   - **Recall Scores:** [0.91525424, 0.93220339, 0.91525424, 0.88135593, 0.88135593]
   - **Mean Recall:** 0.9051

2. **Random Forest**
   - **Recall Scores:** [0.50847458, 0.47457627, 0.47457627, 0.59322034, 0.49152542]
   - **Mean Recall:** 0.5085

3. **SVC**
   - **Recall Scores:** [0.69491525, 0.71186441, 0.62711864, 0.72881356, 0.69491525]
   - **Mean Recall:** 0.6915

4. **AdaBoost**
   - **Recall Scores:** [0.50847458, 0.47457627, 0.47457627, 0.59322034, 0.49152542]
   - **Mean Recall:** 0.5085

**Melhor Modelo:** Regressão Logística

### Ajuste de Hiperparâmetros da Regressão Logística

Utilizei o Optuna para ajustar os hiperparâmetros da Regressão Logística e obter o melhor desempenho em termos de recall.

- **Recall Score no Conjunto de Teste:** 0.8776

### Matriz de Confusão

A matriz de confusão do melhor modelo é mostrada abaixo:

![Matriz de Confusão](https://github.com/Ito-Santana/Machine_Learning_Projects/blob/main/Credit_card_fraud_detection/ignore/cmfinal.png)
