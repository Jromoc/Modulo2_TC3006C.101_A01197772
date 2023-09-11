# Mod_2_Analisis_y_Reporte
Trabajo de: Jose Edmundo Romo Castillo
Matricula: A01197772

## Descripcion de la problematica
Se busca crear un modelo que pueda identificar cual tipo de Iris pertence dependiendo de ciertas caracteristicas, y siendo este un problema donde se busca obtener un classificacion para conocer esto se utilizar el algoritmo de DecisionTreeClassifier para ayudar a conocer estos resultados.

## Descripcion de los modelos
### Arbol de Decisiones
DecisionTreeClassifier es un algoritmo utilizado para el aprendizaje supervisado, el cual se usa para clasificar una serie de datos y poder predecir que rumbo tomaran los datos con respecto a ciertos parametros. La estructura de este modelo se divide en:

- El arbol de decisiones, donde los datos que se clasificaran tendran una serie de atributos o etiquetas.
- Luego esta la division de los datos, donde el algoritmo esta separando los datos en subconjuntos mas pequeños los cuales estan categorizados por las etiquetas, el objetivo de este paso es limpiar las impurezas que puedan existir.
- Luego estan los criterios de division, se tienen varios como la ganancia de informacion, indice de Gini y el error de clasificacion. El objetivo de estos es revisar la pureza de la division de los datos.
- Luego se tiene la profundidad del arbol, estos arboles pueden llegar a ser muy profundos si no se controla o limita su crecimiento. Para evitar un sobreajuste, se suele establecer limites en la profundidad maxima la cual puede alcanzar un arbol de decisiones.
- Una vez ya creado el arbol, se puede seguir el camino para crear una prediccion y al final cada respuesta que se le de a cada creterio de cada nodo guiara a la respuesta final en una de las hoja creadas.

## Estructura
- El archivo "iris.data" contiene los datos que se utilizaron para hacer las pruebas.
- El archivo "decision_tree.ipynb" es donde se estara utilizando el algoritmo de Arbol de decisiones. Este sera el archivo principal a revisar

## Obtencion del dataset
El dataset se obtuvo de los archivos ofrecidos por el modulo Machine Learning de la materia.

## Descripcion del dataset

El dataset "iris.data" contiene 5 columnas y 150 filas. Los nombres de las columnas son:
- sepal length
- sepal width
- petal length
- petal width
- class

*Cantidad de datos*
La cantidad de registros son 150

*Num de clases*
Hay 3 clases:
- Iris-setosa
- Iris-versicolor
- Iris-virginica

En este link se encuentra el dataset: https://experiencia21.tec.mx/courses/406127/files/149476499?module_item_id=24950857

## Arboles
Se crearon 3 arboles, dos para hacer el entrenamiento y el pruebas, y un tercero donde se busca la validacion. Cada uno de los dos primeros arboles cuenta con unos parametros disntitnos con la busqueda del mejor resultado.

myTree1 -- criterion = "gini"
- Socre: 0.93 
- Accuracy: 0.93
- F1-score: 0.93
Matriz de confucion:
[[12 0 0]
 [0 8 1]
 [0 1 8]]

myTree2 -- criterion = "entropy" y max_depth = 3
- Socre: 0.97
- Accuracy: 0.93
- F1-score: 0.93
Matriz de confucion:
[[12 0 0]
 [0 8 1]
 [0 1 8]]

### Validacion para escoger el modelo final 
## Conclusiones
Al momento de incluir los parametros de myTree2, el cual fue con el que se obtuvo mejores resultados no hicieron lo mismo al momento de hacer la validacion, ya que se obtuvieron los mismos resultados que myTree1. Aunque la matriz de confusion si salio un tanto distinta.

myTree_valid -- criterion = "entropy" y max_depth = 3
- Socre: 1
- Accuracy: 0.93
- F1-score: 0.93
Matriz de confucion:
[[6 0 0]
 [0 4 1]
 [0 0 4]]
