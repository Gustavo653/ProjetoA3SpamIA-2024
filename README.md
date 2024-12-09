# Relatório Final: Classificação de SMS como Spam ou Não-Spam

## 1. Descrição do Problema

O objetivo deste projeto foi desenvolver um modelo de machine learning para classificar mensagens de SMS como **spam** ou **não-spam (ham)**. Isso é relevante para prevenir fraudes, proteger a privacidade dos usuários e melhorar a experiência em sistemas de mensagens.

### Dataset
- **Fonte:** [SMS Spam Collection Dataset](https://raw.githubusercontent.com/justmarkham/pycon-2016-tutorial/master/data/sms.tsv)
- **Descrição:** O dataset contém mensagens de texto SMS rotuladas como:
  - **spam:** Mensagens indesejadas ou fraudulentas.
  - **ham:** Mensagens legítimas.
- **Distribuição dos Dados:**  
  - `spam`: 13.4%  
  - `ham`: 86.6%
  
### Pré-Processamento
1. **Leitura e Limpeza:**  
   O dataset foi carregado no formato `.tsv`, e os rótulos foram mapeados para:
   - `1` para spam
   - `0` para ham
2. **Divisão em Conjuntos de Treino e Teste:**  
   - 80% para treinamento e 20% para teste.
3. **Vetorização dos Dados:**  
   Utilizou-se o **TF-IDF Vectorizer** para transformar os textos em vetores numéricos, ignorando palavras comuns por meio do parâmetro `stop_words='english'`.

---

## 2. Resultados dos Modelos

### Modelos Testados
Foram treinados os seguintes modelos para comparação inicial:
- **K-Nearest Neighbors (KNN)**
- **Decision Tree**
- **Random Forest**

### Métricas de Avaliação
Os modelos foram avaliados usando:
- **Accuracy**: Proporção de classificações corretas.
- **Precision**: Proporção de mensagens classificadas como spam que realmente eram spam.
- **Recall**: Proporção de mensagens de spam corretamente identificadas.
- **F1 Score**: Média harmônica entre precisão e recall.

### Resultados dos Modelos Base
| Modelo                | Accuracy  | Precision | Recall  | F1 Score |
|-----------------------|-----------|-----------|---------|----------|
| **K-Nearest Neighbors** | 0.913004  | 1.000000  | 0.348993 | 0.517413 |
| **Decision Tree**      | 0.968610  | 0.907143  | 0.852349 | 0.878893 |
| **Random Forest**      | 0.981166  | 1.000000  | 0.859060 | 0.924188 |

![image](https://github.com/user-attachments/assets/9da3044d-239c-4178-a5b0-3d7001ea9268)

### Justificativa para o Melhor Modelo
O **Random Forest** superou os outros modelos devido às seguintes razões:
1. **Robustez**: Como é um modelo de ensemble, combina os resultados de várias árvores de decisão, reduzindo o overfitting.
2. **Balanceamento Entre Variância e Viés**: Oferece uma boa combinação entre alta precisão e generalização.
3. **Desempenho em Recall e F1 Score**: Apesar de alcançar precisão perfeita (1.0), também manteve um alto recall (0.859), resultando no maior F1 Score (0.924).

---

## 3. Comparação de Hiperparâmetros no Random Forest

Inicialmente, buscamos melhorar o desempenho do **Random Forest** ajustando hiperparâmetros. Foram testadas diferentes combinações de configurações, conforme a tabela abaixo:

| Hiperparâmetros                                | Accuracy  | Precision | Recall  | F1 Score |
|------------------------------------------------|-----------|-----------|---------|----------|
| **n_estimators=50, max_depth=10, min_samples_leaf=1**  | 0.898655  | 1.0       | 0.241611 | 0.389189 |
| **n_estimators=100, max_depth=20, min_samples_leaf=2** | 0.951570  | 1.0       | 0.637584 | 0.778689 |
| **n_estimators=200, max_depth=30, min_samples_leaf=3** | 0.965919  | 1.0       | 0.744966 | 0.853846 |
| **Configuração Original (n_estimators=100, max_depth=None, min_samples_leaf=1)** | **0.981166**  | **1.0**   | **0.859060** | **0.924188** |

![image](https://github.com/user-attachments/assets/15bb3f78-270f-43af-9d26-e83864077181)

### Análise dos Resultados
- A configuração original do modelo superou todas as combinações testadas em termos de **accuracy**, **recall** e **F1 Score**.  
- **Recall:** As configurações ajustadas apresentaram valores inferiores, indicando que o modelo ajustado identificou menos mensagens de spam corretamente.  
- **F1 Score:** O modelo original apresentou o melhor equilíbrio entre precisão e recall.  

Além disso, ao analisar as matrizes de confusão, foi possível observar que o Random Forest padrão teve o melhor desempenho geral, com o maior número de acertos e o menor número de erros. Abaixo está a comparação entre o modelo padrão e o ajustado com 200 estimadores:
### Comparação das Matrizes de Confusão
![image](https://github.com/user-attachments/assets/71d19d2f-7176-485f-83b2-e66f26e1bbd7)
- **Modelo Padrão (n_estimators=100, max_depth=None, min_samples_leaf=1)**:
  - **Mensagens legítimas (Ham)**: O modelo identificou quase todas corretamente, com poucos falsos positivos.
  - **Mensagens de spam**: Maior número de acertos entre todas as configurações, com o menor número de falsos negativos.
- **Modelo Ajustado (n_estimators=200, max_depth=30, min_samples_leaf=3)**:
  - Embora tenha apresentado desempenho bom, o número de falsos negativos (mensagens de spam não identificadas) foi maior do que no modelo padrão, resultando em um recall inferior.

### Justificativa para utilizar os Hiperparâmetros Originais
As tentativas de ajuste nos hiperparâmetros não resultaram em melhorias no desempenho. O desempenho do modelo original já era ótimo devido à sua flexibilidade:  
1. **n_estimators=100:** Número suficiente de árvores para garantir robustez e estabilidade sem aumentar desnecessariamente o custo computacional.  
2. **max_depth=None:** Permitiu que as árvores explorassem toda a profundidade necessária para capturar padrões complexos.  
3. **min_samples_leaf=1:** Garantiu que o modelo identificasse até mesmo padrões raros, aumentando o recall.

Com base nisso, concluímos que a configuração original ofereceu o melhor desempenho possível para este problema. Optar por mantê-la evita overfitting e garante uma solução eficiente e bem balanceada.

---

## 4. Limitações e Melhorias Futuras

### Limitações
1. **Dataset Desequilibrado:** Apenas 13.4% das mensagens são spam, o que pode afetar o recall de mensagens minoritárias.
2. **Análise de Texto Limitada:** O modelo atual não leva em consideração o contexto ou relações semânticas entre palavras.

### Melhorias Futuras
1. **Balanceamento de Classes:** Implementar técnicas como **oversampling** ou **under-sampling** para lidar com o desbalanceamento.
2. **Modelos Avançados:** Utilizar algoritmos baseados em deep learning, como **Transformers (BERT)**, que captam contextos mais complexos.

---

## 5. Conclusão

O modelo **Random Forest** foi escolhido como o melhor classificador para identificar mensagens de spam. Ele demonstrou excelente desempenho, especialmente com seus **hiperparâmetros padrões**, superando todas as combinações testadas em termos de precisão e recall. Embora ajustes de hiperparâmetros tenham sido testados, os valores padrão (n_estimators=100, max_depth=None, min_samples_leaf=1) garantiram um desempenho superior, com o melhor equilíbrio entre acurácia e identificação de spam. Melhorias futuras podem incluir o balanceamento do dataset e o uso de modelos mais avançados para explorar ainda mais o potencial do classificador.
