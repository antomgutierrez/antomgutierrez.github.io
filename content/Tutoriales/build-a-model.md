---
date: 2013-10-16
title: "Tutoriales RapidMiner: Build a model"
category: Tutoriales
---

## Tutoriales RapidMiner: Build a model

### Modeling
El objetivo de este tutorial es explorar distintos modelos de clasificacion (*Decision Tree*, *Naive Bayes* y *Rule Induction*)

Se inicia con el dataset provisto por RapidMiner *Titanic Training*, que ya cuenta con los ajustes realizados en el tutorial de *Prepare data* y esta listo para ser usado para el entrenamiento, como su nombre lo indica.

Luego de agregar los tres modelos, el proceso resultante es el siguiente

![](images/UT2_PD2_1.jpeg)

Al ejecutarlo, podemos ver varios datos interesantes:
- El hombre tiene en general menos posibilidades de supervivencia

![](images/UT2_PD2_1_1.jpeg)

- La cantidad de familiares en el barco y el *Passenger Fare* parecen ser determinante al momento de determinar la supervivencia de las mujeres

![](images/UT2_PD2_1_2.jpeg)

En resumen, se aplicaron tres modelos al dataset con el objetivo de lograr entender e interpretar quién tuvo más posibilidades de sobrevivir.

### Scoring
El objetivo de este tutorial es mostrar como realizar predicciones. Se ultilizará el modelo de *Naive Bayes* para intentar predecir si nuevos pasajeros sobrevivirán o no.

Utilizando nuevamente el dataset *Titanic Training* y aplicando el modelo correspondiente, el proceso resultante es el siguiente:

![](images/UT2_PD2_2.jpeg)

Y al ejecutarlo podemos ver que para aquellos registros de *Titanic Unlabeled* (es decir, sin contar con la columna correspondiente a la variable objetivo), podemos ver que se realizaron las predicciones con su respectivos niveles de confianza:

![](images/UT2_PD2_2_1.jpeg)

Y de esta forma finaliza el tutorial.

### Tests Splits and Validation
El objetivo de este tutorial es ver y medir que tan bien se comportan los modelos, y que tan bien se comportaran ante nuevos escenarios.
Para validarlo, es necesario poder probar el modelo con datos reales, es decir, *labeled data*.
Para ello, debemos reservar parte de los registros de entrenamiento para ser usados para testear el modelo.

El operador *Split Data* nos permite dividir un dataset en varias particiones. En este caso usaremos el 70% para el entrenamiento y el 30% restante para testing.

Finalmente, luego de aplicar el modelo, se añade el operador *Performance* que va a permitir visualizar globalmente la exactitud (accuracy) del modelo.

![](images/UT2_PD2_3.jpeg)

Al ejecutar el proceso, podemos ver:

1) El resultado de aplicar el modelo a los datos que cuentan con label, podemos comparar uno a uno para ver el comportamiento. Similar al resultado del tutorial anterior.
![](images/UT2_PD2_3_1.jpeg)

2) La matriz de performance del modelo:
![](images/UT2_PD2_3_2.jpeg)

Podemos ver que se cuenta con un *80.36*% de accuracy. Este % se podria aumentar variando las proporciones de sapleo del dataset original o mediante la ultilizacion de otro modelo.

### Cross Validation
El objetivo de este tutorial es hacer uso del operador *Cross Validation*. En el tutorial anterior se vio que dividiendo el dataset para obtener conjuntos de entrenamiento y tests puede ser un buen acercamiento, pero todo depende de como se realice dicha division. Es posible que estos conjuntos tengan diferencias significativas, haciendo que el conjunto de entrenamiento sea mas "facil" o "dificil".

La idea del *Cross Validation* es que cada registro del conjunto original sea usado tanto para entrenamiento como para pruebas del modelo. Como default realiza 10 divisiones y 10 ejecuciones. Para cada ejecucion se utilizan 9/10 divisiones para entrenas y 1/10 para testear.

El proceso resultante es el siguiente:
![](images/UT2_PD2_4.jpeg)
![](images/UT2_PD2_4_1.jpeg)

Y al ejecutarlo:
![](images/UT2_PD2_4_2.jpeg)

Podemos ver que se cuenta con un *80.35*% de accuracy, similar al resultado obtenido con el *Split data*, pero dependiendo del dataset y modelo utilizado puede ser mas conveniente usar uno u otro.

### Visual Model Comparison
El objetivo de este tutorial es hacer uso del operador *Compare ROCs* (Receiver Operating Characteristics). Muestra qué tan bien funciona un modelo binario de aprendizaje automático. Muestra la tasa de verdaderos positivos (TPR) frente a la tasa de falsos positivos (FPR) para diferentes umbrales de confianza del modelo.

El operador *Compare ROCs* realiza internamente un *Cross Validation*

El proceso resultante es el siguiente:

![](images/UT2_PD2_5.jpeg)
![](images/UT2_PD2_5_1.jpeg)

Y al ejecutarlo:
![](images/UT2_PD2_5_2.jpeg)

Podemos ver que todos son mas efectivos que elegir aleatoriamente un valor. En orden de efectividad, el mejor para este caso seria el arbol de decision, y el peor Naive Bayes