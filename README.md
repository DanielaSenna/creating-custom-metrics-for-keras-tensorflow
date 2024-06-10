# **Criando Métricas Personalizadas Para Keras/Tensorflow**

Você pode implementar sua própria métrica e usá-la como objetivo e na busca de hiperparâmetros.


Nesse notebook, iremos implementar com o Keras/Tensorflow duas métricas do Scikit-Learn para avaliar o desempenho de uma Rede Neural Convolucional (CNN):

* F1-Score
* Balanced Accuracy Score

Essas métricas são úteis para avaliar o desempenho de modelos de classificação, especialmente quando o conjunto de dados é desbalanceado.

#### **Métricas Personalizadas**

Se precisar de uma métrica que não faça parte da API Keras, você poderá criar facilmente métricas personalizadas criando uma subclasse da classe **keras.metrics.Metric**. Você precisará implementar 4 métodos:

1) Inicialização (__init__):
    * **__init__(self)**, em que você criará variáveis ​​de estado para sua métrica. 
    * Todas as variáveis ​​de estado devem ser criadas neste método chamando self.add_weight() como: self.var = self.add_weight(...)
2) Atualização do Estado (update_state):
    * **update_state(self, y_true, y_pred, sample_weight=None)**, que usa os alvos y_true e as previsões do modelo y_pred para atualizar as variáveis ​​de estado. 
    * Possui todas as atualizações nas variáveis ​​de estado como: self.var.assign_add(...).
3) Resultado (result):
    * **result(self)**, que usa as variáveis ​​de estado para calcular os resultados finais.
    * Calcula e retorna um valor escalar ou um ditado de valores escalares para a métrica das variáveis ​​de estado.
4) Reinicialização dos Estados (reset_states):
    * **reset_state(self)**, que reinicializa o estado da métrica.

A atualização do estado e o cálculo dos resultados são mantidos separados (em update_state() e result(), respectivamente) porque, em alguns casos, o cálculo dos resultados pode ser muito caro e só seria feito periodicamente.

[Custom Metrics](https://keras.io/guides/training_with_built_in_methods/)
[Base Metric Class](https://keras.io/api/metrics/base_metric/)
