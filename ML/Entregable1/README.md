# Indiv-Modulo2
Trabajo de: Jose Edmundo Romo Castillo | Matricula: A01197772

## Descripcion de la problematica
La intencion es conocer el valor del ingreso per capita dependiendo del año el cual se introduzca conocer. Esta problematica se resuelve con un caso de regresion, y para esta situacion se eligio la regresion lineal.

## Descripcion del modelo
El algoritmo utilizado es Regresion Lineal,  se utiliza para predecir un valor continuo, como el precio de una casa o el riesgo de un préstamo, a partir de un conjunto de datos de valores continuos. El algoritmo utiliza una ecuación lineal para modelar la relación entre la variable dependiente y las variables independientes.

## Estructura del archivo
Este repositorio consta de 3 archivos:
- "main.ipynb", este sera el archvio a revisar, el cual contiene el algoritmo a evaluar.
- "Canada_per_capita_income (1).csv", este es el dataset que se utilizara.
- "README.md", es este documento donde se estara dando la descripcion del algoritmo como de la problematica.

## Dataset usado
Para esta actividad utilizare el dataset "Canada_per_capita_income.csv", obtenido de Kaggle.

De este link se obtuvo el dataset utilizado: https://www.kaggle.com/datasets/ananthu19/canada-per-capita-income-prediction 

El dataset se compone de 47 filas y 2 columnas:
- La columna "year" que es de tipo int.
- La columnas "income" que es de tipo float.

## Predicciones de prueba
En el archivo "Codigo.ipynb" se utiliza una lista con distintos años para probar las predicciones, dentro de esa lista hay valores ya existentes por lo cual se creo otra lista con esos valores existentes para buscar en el data set con la funcion .isin() y mostrar el valor real.


## Conclusiones
La efectividad del modelo no es buena, se intento hacer varios ajustes con el alpha o el numero de iteraciones en el algoritmo, pero nada de ello ayudo a mejorar el resultado esperado.
