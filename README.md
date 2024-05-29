# Projeto de Detecção de Fraudes em Transações de Cartão de Crédito

Fraudes em cartões de crédito são um problema significativo para bancos e fintechs. No Brasil, mais de 12 milhões de pessoas foram vítimas de fraudes financeiras no ano de 2022, causando um prejuízo de R$ 1,8 bilhões. Com o crescimento do comércio eletrônico, a detecção eficiente de fraudes em tempo real é crucial para proteger os consumidores e as instituições financeiras. 

Investir em Inteligência Artificial para detectar fraudes em transações de cartões de crédito representa uma oportunidade valiosa em Data Science, com potencial para economizar milhões de Reais. O desafio é aprimorar constantemente os algoritmos para prevenir ou detectar transações fraudulentas de forma mais eficaz, reduzindo os falsos positivos e os prejuízos.

## Objetivo do Projeto
O objetivo do projeto é desenvolver modelos preditivos precisos que possam distinguir entre as transações legítimas e as fraudulentas, usando algoritmos de Machine Learning como Regressão Logística e Árvores de Decisão. Antes de construir o modelo, são realizadas análises para lidar com dados faltantes, verificar correlações, fazer descrições estatísticas e garantir o balanceamento de classes. Em seguida, veremos os passos para a construção e comparação de modelos de Machine Learning para resolver esse problema.

## Sobre os Dados
Os dados utilizados foram fornecidos por empresas europeias de cartão de crédito, representando dois dias de transações com 492 fraudes em cerca de 290 mil transações, resultando em um desbalanceamento acentuado, com fraudes representando apenas 0,17%. As características do dataset são todas numéricas e foram descaracterizadas para proteger a privacidade, representadas por [V1, V2, V3... V28], passando por uma transformação chamada Análise de Componentes Principais (PCA) para redução da dimensionalidade enquanto mantém a informação essencial.

## Criando um Conjunto de Validação
15% dos dados do DataFrame original foram separados para um conjunto de validação. Após criar e ajustar os modelos de Machine Learning, esses dados são usados para testar e avaliar sua eficácia com dados novos, nunca antes vistos pelos modelos.

## Dicionário de Variáveis
- **Time**: intervalo de tempo em segundos entre cada transação.
- **Amount**: valor da transação.
- **Class**: indica se a transação é fraudulenta (1) ou legítima (0).
- **V1, V2, V3...V28**: variáveis ocultas por questões de privacidade.

## Análise Exploratória
Na análise inicial dos dados, observamos que as colunas Time e Amount permanecem com seus valores originais, enquanto as colunas transformadas pela PCA são numeradas em um intervalo de -1 a 1. A coluna Class é a variável alvo, onde 0 representa uma transação real e 1 representa uma transação fraudulenta. As transações reais representam aproximadamente 99,83% do total, e as fraudes apenas 0,17%, evidenciando um desbalanceamento significativo.

### Análise dos Valores da Coluna Amount:
- Média das transações: 88,61
- Mediana: 22
- Desvio padrão: 247,65
- 75% dos valores abaixo de: 77,58
- Valor máximo da transação: 19656,53

Felizmente, o conjunto de dados não possui valores ausentes, eliminando a necessidade de tratamentos adicionais para valores nulos. No entanto, devido ao grande desbalanceamento entre as classes, será necessário realizar um rebalanceamento antes da modelagem.

## Modelagem e Preparação de Dados
A padronização dos dados envolve calcular a média e o desvio padrão dos dados, subtraindo a média de cada valor e dividindo pelo desvio padrão. Utilizamos a função `StandardScaler` da biblioteca Scikit-Learn para padronizar as colunas Amount e Time. Após a transformação, os dados de "std_amount" e "std_time" estão no mesmo padrão das variáveis V1-V28, todas em uma mesma escala.

Os dados foram então divididos em conjuntos de Treino (75%) e Teste (25%), utilizando os parâmetros `Stratify` e `Shuffle` para manter a distribuição das classes e evitar viés nos dados.

### Balanceamento de Classes
Para lidar com o desbalanceamento, utilizamos o método de Undersampling da biblioteca `imblearn`, balanceando os dados para evitar o Overfitting. Após o balanceamento, verificamos que as classes estão distribuídas de maneira mais equilibrada, o que melhora a capacidade do modelo de generalizar para novos dados.

## Construção dos Modelos
Testamos dois algoritmos de classificação: Regressão Logística e Árvore de Decisão.

### Regressão Logística
- A Regressão Logística é usada para prever a probabilidade de uma variável pertencer a uma classe com base em variáveis independentes.
- Nos dados de validação, a Regressão Logística alcançou uma acurácia de 97% e uma previsão de fraudes de 93%.

### Árvore de Decisão
- A Árvore de Decisão modela relações e decisões com base em uma estrutura de árvore, dividindo os dados em subconjuntos específicos usando características ou atributos.
- Nos dados de validação, a Árvore de Decisão apresentou uma acurácia de 90% e uma previsão de fraudes de 92%.

## Comparação dos Modelos
Para comparar os modelos, utilizamos a curva ROC (Receiver Operating Characteristic), que representa graficamente a taxa de verdadeiros positivos em relação à taxa de falsos positivos. A Regressão Logística apresentou um Recall de 97%, enquanto a Árvore de Decisão teve um Recall de 90%. Assim, a Regressão Logística é o melhor modelo para detectar fraudes em transações de cartão de crédito.

## Conclusão
O projeto de detecção de fraudes em transações de cartão de crédito envolveu várias etapas cruciais, desde a análise exploratória dos dados até a construção e avaliação de modelos de Machine Learning. Através de uma análise detalhada e de transformações adequadas, foi possível desenvolver um modelo preditivo eficaz, destacando a Regressão Logística como a melhor opção para o problema em questão.
