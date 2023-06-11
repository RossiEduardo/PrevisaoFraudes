# PrevisaoFraudes
Esse projeto tem como objetivo fazer um estudo de uma base de fraudes em
compras com cartões de crédito e tentar criar um modelo que ajude a mitigar tal
problema. Os dados de treinamento estão disponíveis no arquivo train.csv e os
de teste no arquivo test.csv

Primeiro identificamos a variável resposta do problema e criamos um histograma mostrando a sua distribuição.
Depois identificamos a variável que é um metadado para não utilizarmos ela nos modelos.
Feito isso comparamos as métricas acurácia e AUC para essa base de dados simulando os seguintes modelos:
  * ○ Modelo que classifica aleatoriamente (50% chance de dizer que é
  * fraude e 50% de dizer que não é);
  * ○ Modelo que classifica todos os casos como fraude; 
  * ○ Modelo que classifica todos os casos como não fraude
E chegamos a conclusão que se deve usar a AUC.

Depois usando a a classe RandomForestClassifier do scikit-learn fazemos um 3-fold
cross-validation para comparar todas as combinações dos seguintes valores
de hiperparâmetros e depois refazemos usando class_weight=’balanced’:
 * n_estimators = [10, 50, 100, 200];
 * max_depth = [2, 3, 4, 5]
  
Feito isso calculamos o lucro que o modelo traria no seguinte cenário:
 * As top-1% transações com maior chance de fraude (de acordo com os scores
do modelo) seriam impedidas de acontecer;
 * Cada fraude evitada em média evita um prejuízo (gera um lucro) de R$ 100 e
 * Cada não-fraude bloqueada gera em média um prejuízo de R$ 2.
