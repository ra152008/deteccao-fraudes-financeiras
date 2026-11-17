# Resumo de métricas para dados desbalanceados


Responsável: Henrique



Projeto: IEEE – Detecção de Fraudes Financeiras



O dataset Credit Card Fraud Detection reúne 284.807 transações, das quais apenas 492 são fraudes, o que corresponde a cerca de 0,172% do total. Esses números constam na descrição pública da base e serão conferidos no arquivo creditcard.csv. Em um conjunto com essa proporção, a classe de interesse é raríssima, e é justamente ela que o modelo precisa identificar.



Essa característica compromete o uso da acurácia, definida como a fração de previsões corretas sobre o total. Um modelo que classifica todas as transações como legítimas acerta cerca de 99,83% dos casos e, ainda assim, não detecta nenhuma fraude. O valor é alto, mas o modelo é inútil na prática, pois a acurácia é dominada pela classe majoritária e oculta o desempenho sobre a classe minoritária. Por essa razão, neste projeto a acurácia poderá ser reportada, mas não será adotada como critério principal de avaliação.



Para analisar o comportamento do modelo de forma adequada, parte-se da matriz de confusão, que separa os resultados em quatro categorias. Considerando a fraude como classe positiva, o verdadeiro positivo (VP) é a fraude corretamente identificada, o falso positivo (FP) é a transação legítima apontada indevidamente como fraude, o falso negativo (FN) é a fraude que passou despercebida e o verdadeiro negativo (VN) é a transação legítima corretamente liberada. Os dois tipos de erro têm custos distintos: o falso positivo gera um alarme falso e causa transtorno ao cliente, enquanto o falso negativo representa o prejuízo efetivo e é o erro mais caro.



Dessas quatro contagens derivam as métricas utilizadas. A precisão, dada por VP / (VP + FP), indica a proporção de alertas emitidos que de fato eram fraudes. A revocação (recall), dada por VP / (VP + FN), indica a proporção das fraudes existentes que o modelo conseguiu encontrar. As duas métricas tendem a variar em sentidos opostos: um modelo que marca todas as transações como fraude obtém revocação máxima e precisão muito baixa, e o inverso também ocorre. O F1 combina ambas por meio da média harmônica, só assume valores altos quando precisão e revocação são razoáveis ao mesmo tempo e, por isso, será calculado para a classe fraude, e não como média entre as classes.



Essas métricas dependem do limiar de decisão, que na regressão logística é, por padrão, 0,5. Reduzi-lo aumenta a revocação e diminui a precisão, e a escolha adequada depende do custo relativo entre falsos negativos e falsos positivos. A AUPRC, área sob a curva precisão-revocação, resume o desempenho do modelo em todos os limiares possíveis e é mais informativa que a AUROC quando a classe positiva é rara, porque não é inflada pela grande quantidade de transações legítimas.



No desenvolvimento do projeto, a regressão logística será comparada ao baseline por meio da precisão, da revocação e do F1 da classe fraude, da matriz de confusão e da AUPRC, mantendo-se a acurácia apenas como informação complementar. Recomenda-se ainda que a divisão entre treino e teste seja estratificada, de modo que a proporção de fraudes se mantenha nos dois conjuntos.



Fonte de estudo: documentação do scikit-learn, seção Model Evaluation.

