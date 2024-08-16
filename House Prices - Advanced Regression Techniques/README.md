# Projeto de Análise de Dados

Este repositório contém um projeto de análise de dados que inclui processamento e seleção de recursos para modelos preditivos. O objetivo é preparar os dados para modelagem e melhorar a qualidade do conjunto de dados.

## Estrutura do Projeto

- **`data/`**: Contém os conjuntos de dados brutos e processados.
- **`notebooks/`**: Jupyter notebooks para análise e visualização de dados.
- **`scripts/`**: Scripts Python para processamento de dados e modelagem.
- **`requirements.txt`**: Lista de dependências do projeto.

## Processamento de Dados

### 1. Pré-processamento de Dados

- **Tratamento de Valores Nulos**: Colunas com mais de 17% de valores nulos são removidas. Valores nulos nas colunas categóricas são preenchidos com base na frequência dos valores mais comuns.
  
  ```python
  def calculate_ratios(data, total_value):
      # Calcula as proporções para os 5 valores mais frequentes.
      ...
  
  def pre_processing_data(data):
      # Gera uma lista de valores para preencher os nulos.
      ...

