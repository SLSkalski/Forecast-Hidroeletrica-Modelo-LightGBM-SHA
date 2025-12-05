mae = metrics['mae']
rmse = metrics['rmse']
r2 = metrics['r2']
mape = metrics['mape']

readme_content = f"""# Forecasting de Geração Hidrelétrica com LightGBM e SHAP

Este projeto demonstra um pipeline completo para previsão de séries temporais de geração hidrelétrica (em MW) utilizando o modelo LightGBM. O foco está na criação de features temporais robustas, validação temporal e, crucialmente, na explicabilidade do modelo através da biblioteca SHAP, permitindo entender como as variáveis influenciam as previsões.

## Key Features

-   **Feature Engineering**: Criação automática de features temporais (dia da semana, mês, cíclicas), lags da variável alvo e de variáveis externas, e estatísticas móveis (médias, desvios padrão).
-   **LightGBM**: Treinamento de um modelo LightGBM para regressão, otimizado para séries temporais com validação cruzada temporal (TimeSeriesSplit) e early stopping.
-   **Evaluation**: Avaliação abrangente do modelo usando métricas como MAE, RMSE, R² e MAPE, acompanhada de visualizações de previsões e análise de resíduos.
-   **SHAP (eXplainable AI)**: Análise detalhada da importância e do impacto das features nas previsões do modelo através de diversos gráficos SHAP (Summary, Bar, Dependence, Waterfall, Force plots).

## Performance do Modelo

Após o treinamento e avaliação no conjunto de teste, o modelo obteve as seguintes métricas de desempenho:

-   **MAE (Mean Absolute Error)**: 82.40 MW
-   **RMSE (Root Mean Squared Error)**: 102.77 MW
-   **R² (Coefficient of Determination)**: 0.9188
-   **MAPE (Mean Absolute Percentage Error)**: 4.47%

Esses resultados indicam um desempenho muito forte, com o modelo explicando aproximadamente 92% da variância na geração de energia e um erro percentual médio de apenas 4.47%.

## Visualizações e Análise SHAP

O pipeline inclui diversas visualizações para avaliar o desempenho do modelo e entender suas decisões:

-   **Gráfico de Previsões**: Compara os valores reais com os previstos ao longo do tempo e em um gráfico de dispersão.
-   **Análise de Resíduos**: Exibe a distribuição dos erros de previsão e sua variação ao longo do tempo para identificar vieses.
-   **SHAP Summary Plot**: Mostra a importância geral de cada feature e como seus valores (baixos em azul, altos em vermelho) impactam a previsão (negativamente à esquerda, positivamente à direita).
-   **SHAP Bar Plot**: Um ranking da importância média de cada feature.
-   **SHAP Dependence Plots**: Ilustram a relação entre o valor de uma feature e o impacto marginal na previsão do modelo.
-   **SHAP Waterfall/Force Plots**: Explicam a contribuição de cada feature para uma previsão individual, mostrando como se chega ao valor previsto a partir de uma base.

## Como Usar o Projeto

Para utilizar este pipeline com seus próprios dados, siga os passos abaixo:

### Carregando Seus Dados Reais

Atualmente, o notebook utiliza dados simulados para demonstração. Para usar seus próprios dados, você precisará substituir o bloco de código de simulação pela leitura do seu arquivo de dados. As instruções detalhadas sobre como fazer isso, incluindo a conversão da coluna de data e as colunas esperadas, são explicadas nas células de texto `Mk5vGrk7bIas` e `W7zTKGjiblyj` do notebook.

Seu DataFrame deve conter minimamente as colunas:
-   `data`: Coluna de data/timestamp (em formato `datetime`).
-   `geracao_mw`: Sua variável alvo (geração de energia em MW).
-   Variáveis externas como `vazao_afluente`, `precipitacao`, `nivel_reservatorio` (ou outras relevantes para o seu caso).

### Configurando Variáveis Externas

Se os nomes das suas colunas de variáveis externas forem diferentes dos exemplos (`vazao_afluente`, `precipitacao`, `nivel_reservatorio`), você deve atualizar a lista `external_cols` na chamada da função `prepare_features`. Um exemplo de como fazer isso está na célula de texto `3X3VN2A2bx9Y` do notebook.

### Rodando o Pipeline

Após carregar e configurar seus dados, basta executar todas as células do notebook em sequência. O pipeline se encarregará da engenharia de features, treinamento, avaliação e análise de explicabilidade.

### Salvando os Gráficos

As funções de plotagem atualmente exibem os gráficos (`plt.show()`). Para salvar os gráficos, você pode substituir `plt.show()` por `plt.savefig('nome_do_arquivo.png')` dentro das funções de plotagem relevantes e adicionar `plt.close()` após salvar para evitar que eles sejam exibidos e liberar memória.
"""

