# Análise de Clustering de Clientes da Olist

## Descrição

Este repositório contém um projeto de clustering de clientes da Olist, um e-commerce brasileiro. O objetivo do projeto é segmentar clientes usando técnicas de clustering para identificar padrões e comportamentos distintos entre os grupos de clientes.

## Sumário

1. [Introdução ao Clustering](#introdu%C3%A7%C3%A3o-ao-clustering)
2. [Sobre o Dataset](#sobre-o-dataset)
3. [Importação de Dados, Engenharia de Recursos e EDA](#importa%C3%A7%C3%A3o-de-dados-engenharia-de-recursos-e-eda)
4. [Clustering com K-Means](#clustering-com-k-means)
5. [Clustering com K-Means: Aplicação de PCA e Análise Adicional](#clustering-com-k-means-aplica%C3%A7%C3%A3o-de-pca-e-an%C3%A1lise-adicional)
6. [Pergunta Instigante](#pergunta-instigante)


## Introdução ao Clustering

### O que é Clustering?

Clustering é uma técnica de aprendizado de máquina não supervisionado que agrupa objetos em clusters com base na similaridade das características. O objetivo é que objetos dentro do mesmo cluster sejam mais semelhantes entre si do que com objetos de outros clusters.

### Por que é Importante?

- **Descoberta de Padrões:** Identifica padrões e estruturas nos dados que não são imediatamente aparentes.
- **Segmentação de Mercado:** Permite campanhas de marketing mais direcionadas e eficazes.
- **Análise Exploratória:** Facilita a identificação de grupos naturais e anomalias.

## Sobre o Dataset

### Descrição do Dataset

O dataset contém informações de 100 mil pedidos realizados entre 2016 e 2018 em múltiplos marketplaces no Brasil, incluindo status do pedido, preço, pagamento, desempenho do frete, localização do cliente, atributos do produto e avaliações dos clientes. Disponível no Kaggle.

### Objetivo do Projeto

Criar um algoritmo eficiente de clustering para segmentar os clientes da Olist e identificar padrões distintos entre os grupos.

## Importação de Dados, Engenharia de Recursos e EDA

### Importação de Dados

Importamos dados de quatro fontes distintas e realizamos a combinação dos DataFrames para análise.

## Engenharia de Recursos

Criamos novas features e tratamos valores nulos e duplicatas para melhorar a qualidade dos dados.

## Análise Exploratória de Dados (EDA)

Realizamos visualizações como a matriz de correlação e box plots para entender melhor os dados.

![correlation](https://github.com/Ito-Santana/Machine_Learning_Projects/blob/main/Clustering%20Customer%20E-commerce%20Olist/image_ignore/corr.png)

## Clustering com K-Means

### Introdução ao K-Means

O K-Means é um algoritmo que divide os dados em K clusters, minimizando a variância dentro de cada cluster.

### Análise do Erro Quadrático e Silhouette Score

Usamos o erro quadrático e o silhouette score para determinar o número ideal de clusters.
![metrics](https://github.com/Ito-Santana/Machine_Learning_Projects/blob/main/Clustering%20Customer%20E-commerce%20Olist/image_ignore/metrics.png)

### Escolha Inicial de Clusters

Começamos com 4 clusters e analisamos os resultados usando box plots e pair plots.

### Análise dos Resultados com Box Plots e Pair Plots

Observamos padrões de tempo de entrega e gastos, e visualizamos a distribuição dos clusters em diferentes dimensões.
![avg_time](https://github.com/Ito-Santana/Machine_Learning_Projects/blob/main/Clustering%20Customer%20E-commerce%20Olist/image_ignore/average_time_delivery.png)

![pair](https://github.com/Ito-Santana/Machine_Learning_Projects/blob/main/Clustering%20Customer%20E-commerce%20Olist/image_ignore/pairplot_kmeans.png)

## Clustering com K-Means: Aplicação de PCA e Análise Adicional

### Introdução ao PCA

A PCA reduz a dimensionalidade dos dados, mantendo a variabilidade. Aplicamos PCA e reexecutamos o K-Means com 6 clusters.
![pca_3d](https://github.com/Ito-Santana/Machine_Learning_Projects/blob/main/Clustering%20Customer%20E-commerce%20Olist/image_ignore/pca_3d_clusters.png)

### Análise dos Resultados com PCA
![pair_pca](https://github.com/Ito-Santana/Machine_Learning_Projects/blob/main/Clustering%20Customer%20E-commerce%20Olist/image_ignore/pair_plot_pca.png)


Observamos que o Cluster 4 apresentou características distintas, sugerindo um grupo de clientes com padrões diferentes.

![x](https://github.com/Ito-Santana/Machine_Learning_Projects/blob/main/Clustering%20Customer%20E-commerce%20Olist/image_ignore/otherxc4.png)

![x2](https://github.com/Ito-Santana/Machine_Learning_Projects/blob/main/Clustering%20Customer%20E-commerce%20Olist/image_ignore/otherxc4_3d.png)

## Pergunta Instigante

Isso nos leva a uma grande questão: será que o Cluster 4 representa um grupo de clientes extremamente atípicos ou é um conjunto de outliers que destaca padrões incomuns entre nossos dados?
