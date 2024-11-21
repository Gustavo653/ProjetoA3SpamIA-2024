# Relatório Final: Classificação de SMS como Spam ou Não Spam

## 1. Introdução
**Objetivo do Projeto**:  
O objetivo deste projeto é desenvolver um agente inteligente capaz de classificar SMS como spam ou não spam utilizando técnicas de aprendizado de máquina.

**Problema e Importância**:  
A classificação de SMS como spam é uma tarefa importante para melhorar a eficiência e a segurança no uso de SMS, ajudando a filtrar SMS indesejados e garantindo que as mensagens legítimas cheguem ao destinatário.

---

## 2. Definição do Problema
**Definição do Problema**:  
O objetivo é classificar SMS como spam ou não spam, com base no conteúdo da mensagem.

**Objetivo do Agente Inteligente**:  
O agente inteligente deve ser capaz de aprender a partir de um conjunto de dados rotulados e classificar SMS novos em tempo real.

---

## 3. Coleta de Dados
**Fonte dos Dados**:  
O conjunto de dados utilizado foi o "SMS Spam Collection Dataset" disponível no repositório do PyCon 2016.
- Link: [Dataset SMS Spam Collection](https://raw.githubusercontent.com/justmarkham/pycon-2016-tutorial/master/data/sms.tsv)

**Descrição do Conjunto de Dados**:  
O conjunto contém duas colunas:
- **label**: 'spam' ou 'ham' (não spam).
- **message**: o conteúdo do SMS.

**Pré-processamento dos Dados**:  
- Substituição de valores de 'spam' por 1 e 'ham' por 0.
- Divisão do conjunto de dados em treinamento (80%) e teste (20%).
- Aplicação do **TfidfVectorizer** para transformar os textos em uma representação numérica.

---

## 4. Modelos Testados

### 4.1 Algoritmos Utilizados
- **K-Nearest Neighbors (KNN)**: Algoritmo que classifica dados com base na proximidade dos vizinhos mais próximos.
- **Árvore de Decisão**: Modelo de classificação que utiliza uma estrutura hierárquica de decisões baseadas em atributos dos dados.
- **Random Forest**: Modelo de classificação que utiliza múltiplas árvores de decisão para melhorar a precisão e evitar o overfitting.

### 4.2 Processo de Treinamento e Avaliação
- **Treinamento**: Todos os modelos foram treinados utilizando o conjunto de dados de treinamento transformado com **TfidfVectorizer**.
- **Métricas de Avaliação**: As métricas utilizadas para avaliar o desempenho dos modelos foram:
  - **Acurácia**: Proporção de previsões corretas.
  - **Precisão**: Proporção de positivos preditivos corretos.
  - **Recall**: Proporção de reais positivos corretamente identificados.
  - **F1 Score**: Média harmônica entre precisão e recall.

---

## 5. Resultados e Análise

### 5.1 Resultados Obtidos
A tabela a seguir apresenta as métricas de desempenho para cada modelo:

| Modelo              | Acurácia | Precisão | Recall | F1 Score |
|---------------------|----------|----------|--------|----------|
| K-Nearest Neighbors  | 91,30%       | 100%       | 34,89%     | 51,74%       |
| Árvore de Decisão    | 96,86%       | 90,71%       | 85,23%     | 87,88%       |
| Random Forest        | 98,11%       | 100%       | 85,90%     | 92,41%       |

### 5.2 Visualização dos Resultados
Abaixo está um gráfico que compara o desempenho dos algoritmos em todas as métricas:

![image](https://github.com/user-attachments/assets/5bef3aee-139f-4ddf-9991-5e817a8f8234)

### 5.3 Análise do Desempenho
- **Random Forest** foi o melhor modelo, apresentando as melhores métricas de **acurácia**, **precisão** e **F1 score**.
- **KNN** teve o pior desempenho entre os modelos testados, com uma acurácia mais baixa e maior taxa de erro.
- **Árvore de Decisão** teve desempenho semelhante ao **Random Forest**, mas ficou um pouco atrás na métrica de **recall**, provavelmente devido ao overfitting em dados mais complexos.

---

## 6. Justificativa para o Desempenho do Random Forest
- O **Random Forest** se destacou devido à sua natureza de **predição**, utilizando múltiplas árvores de decisão para melhorar a generalização e reduzir o overfitting.
- A **acurácia** elevada indica que o modelo conseguiu classificar corretamente a maioria dos SMS.
- **Precisão** alta significa que o **Random Forest** foi eficaz em identificar SMS realmente spam, sem classificar erroneamente muitos SMS não spam como spam.
- O **F1 score** elevado também mostra que o **Random Forest** manteve um bom equilíbrio entre **precisão** e **recall**, resultando em uma performance geral superior.

---

## 7. Conclusão
- O projeto teve sucesso em desenvolver um agente inteligente capaz de classificar SMS como spam ou não spam.
- O modelo **Random Forest** obteve os melhores resultados, superando os outros modelos testados em todas as métricas.
- Apesar dos bons resultados, o projeto pode ser aprimorado com a experimentação de novos modelos e técnicas de ajuste de hiperparâmetros, visando uma maior precisão e eficiência na classificação de spam.

---

## 8. Referências
- Fonte dos dados: [Repository SMS Spam Collection](https://github.com/justmarkham/pycon-2016-tutorial)
