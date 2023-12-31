---
title: "Reporte Final"
author: "José Romo - A01197772"
date: "2023-09-06"
output:
  pdf_document: default
  html_document: default
---

# Reporte final de "El precio de los autos"

## Resumen
Una empresa automovilística china aspira a entrar en el mercado estadounidense. Desea establecer allí una unidad de fabricación y producir automóviles localmente para competir con sus contrapartes estadounidenses y europeas. Contrataron una empresa de consultoría de automóviles para identificar los principales factores de los que depende el precio de los automóviles, específicamente, en el mercado estadounidense, ya que pueden ser muy diferentes del mercado chino. Lo que se busco en un inicio fue identificar las variables que mayor correlacion se tuviera con el valor de precio, una vez ya haciendo eso se encontro que dichas variables son: enginesize, cubrweight, horsepower, carwidth, cylindernumber y citympg.

## Introduccion
Cuando se trata de entrar a un nuevo mercado, sobretodo si este es en otro pais donde la cultura es muy diferente, las costumbres son otras y el estilo de vida de las personas puede ser muy diferente, no se puede entrar con el mismo catalogo y precios que uno ya hace en el pais de origen. 

Podemos tomar como ejemplo a Estados Unidos, donde 4 de sus 5 vehiculos mas vendidos son camionetas tipo Pick-Up. Tambien esta el caso de Mexico donde se vende mas los automoviles de tipo sedan. Este tipo de circunstancias son aquellos que se deben de tomar en cuenta a la hora de adentrarse a un mercado nuevo que tambien se necestia competir arduamente para tener un pedazo del pastel que ya otras compañias controlan desde hace tiempo.

Para esto este analisis tratara de ayudar a identificar cuales son los parametros necesarios para poder calcular el precio de los vehiculos que se ofreceran al nuevo mercado, siguiendo como ejemplo las ventas de otros vehiculos similares para encontrar el precio justo para la ventan de los automoviles.

## Analisis de los resultados
```{r}
knitr::opts_chunk$set(echo = FALSE)
library(ggplot2)
library(corrplot)
library(tidyr)
library(Hmisc)
library(GGally)

data <- read.csv("precios_autos.csv")
#data
```

```{r}
knitr::opts_chunk$set(echo = FALSE)

data$cylindernumber <- ifelse(data$cylindernumber == "four", 4, data$cylindernumber)

data$cylindernumber <- ifelse(data$cylindernumber == "five", 5, data$cylindernumber)

data$cylindernumber <- ifelse(data$cylindernumber == "six", 6, data$cylindernumber)

data$cylindernumber <- ifelse(data$cylindernumber == "two", 2, data$cylindernumber)

data$cylindernumber <- ifelse(data$cylindernumber == "three", 3, data$cylindernumber)

data$cylindernumber <- ifelse(data$cylindernumber == "twelve", 12, data$cylindernumber)

data$cylindernumber <- ifelse(data$cylindernumber == "eight", 8, data$cylindernumber)

data$cylindernumber <- as.numeric(data$cylindernumber)

```

```{r}
knitr::opts_chunk$set(echo = FALSE)
columnas_cuantitativas <- data[, sapply(data, is.numeric)] #Se almacenan en un dataset todas las variables cuantitativas

```

*Coeficiente de correlacion*
```{r}
knitr::opts_chunk$set(echo = FALSE)
cor(columnas_cuantitativas, data$price)
```
```{r}
knitr::opts_chunk$set(echo = FALSE)
columnas_usar <- data[, c("carwidth", "citympg", "curbweight", "cylindernumber", "enginesize", "horsepower", "price")]
#columnas_usar
```

```{r,warning=FALSE}
knitr::opts_chunk$set(echo = FALSE)
Rc = rcorr(as.matrix(columnas_usar))
#Rc
```

```{r}
knitr::opts_chunk$set(echo = FALSE)
A2 = lm(data$price ~ data$carwidth + data$citympg + data$curbweight + data$cylindernumber + data$enginesize + data$horsepower)
#A2
```

```{r}
knitr::opts_chunk$set(echo = FALSE)
b0 = A2$coefficients[1]
b1 = A2$coefficients[2]
b2 = A2$coefficients[3]
b3 = A2$coefficients[4]
b4 = A2$coefficients[5]
b5 = A2$coefficients[6]
b6 = A2$coefficients[7]
#cat("Precio =", b0, "+", b1, "Carwidth", "+", b2, "citympg", "+", b3 , "curbweight", "+", b4, "cylindernumber", "+", b5, "enginesize", "+", b6,"horsepower")
``` 

```{r}
knitr::opts_chunk$set(echo = FALSE)
pairs(columnas_usar,labels=c("carwidth", "citympg", "curbweight", "cylindernumber", "enginesize", "horsepower", "price" ),main="Matriz de dispersión",pch=20)
```

```{r,message="FALSE",warning=FALSE}
knitr::opts_chunk$set(echo = FALSE)
ggpairs(columnas_usar,lower = list(continuous = "smooth"),
        diag = list(continuous = "barDiag"), axisLabels = "none")
```
Como se puede ver en la Matriz de dispersion y en la grafica anterior es que vemos como 5 de las 6 variables cuando tienen un valor mayor estas suben el precio tambien sube por la correlacion de cada una de estas. Diciendo que si el automovil es mas ancho, mas pesado, con mayor cilindraje, con un motor mas grande y con un numero de caballaje mas alto, el precio total del automovil debera de ser mas elevado en comparacion con otros automoviles de caracteristicas inferiores.

```{r}
knitr::opts_chunk$set(echo = FALSE)
Y = function(x){b0+b1+b2+b3+b4+b5+b6*x}

colores = c('blue')
plot(data$price, data$carwidth + data$citympg + data$curbweight + data$cylindernumber + data$enginesize + data$horsepower, col=colores, pch=20,ylab="Todas las variables",xlab="Precio",main="Relacion del Precio vs las variables")
x = seq(100000,500000,10000)
lines(x,Y(x), col="blue", lwd=3)
```
Aqui se puede apreciar lo anterior mencionado, el como todas las variables juntas tienden a subir con respecto al precio.

```{r}
knitr::opts_chunk$set(echo = FALSE)
R3a=lm(data$price~data$carwidth + data$curbweight +data$enginesize + data$horsepower,data=columnas_usar)
S=summary(R3a)
#S
```
```{r}
knitr::opts_chunk$set(echo = FALSE)
E=R3a$residuals
Y=R3a$fitted.values

qqnorm(E)
qqline(E,col="red")

hist(E,col="lightcyan",freq=FALSE,main="Histograma de Residuos",ylim=c(0,0.0002),xlab="",ylab="Densidad")
lines(density(E),col="red")
curve(dnorm(x,mean=mean(E),sd=sd(E)), add=TRUE, col="blue",lwd=2)
```
Lo que se mostro en la explicacion anterior se puede apreciar como se tiene un sesgo positvo, ya que la media se carga a la derecha. Y en el grafico superior tenemos un sesgo y heterocedasticidad.

## Conclusion

Lo que se encontro fue que las variables: enginesize, cubrweight, horsepower, carwidth, cylindernumber y citympg; las cuales tienen una gran correlacion con la variable dinero, se pudo determinar que las que mayor impacto se tiene de estas 6 variables son : "carwidth", "curbweight", "enginesize" y "horsepower". Estas 4 variables representan una relacion con la subida de precios, entre mayor sea el valor de las variables, el precio subira. 

Por lo tanto si se tiene un automovil mas ancho, mas peso, con mayor caballaje y un motor mas grande, se tendria que tener un precio superior que si se tuviera todo lo contrario. Y lo que podemos concluir es que los automoviles posiblemente los SUV o Pick Ups por sus dimensiones, y que tengan un motor muy potenten gracias a sus caballos de fuerza, son muy apreciados en el pais objetivo. Esto demostrando que se busca un automovil grande y comodo, que estas dos palabras cuando se trata de automoviles van de la mano, y que tenga una gran fuerza.
