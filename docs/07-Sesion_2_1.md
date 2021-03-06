# De numeros aleatorios, distribuciones y probabilidades

<style> body {text-align: justify} </style> <!-- Justify text. -->

En R, existen funciones para la generacion de numeros aleatorios, es decir, podremos generar cualquier numero de 0 a infinito de forma automatica. Para esto, debemos especificar la distribucion de probabilidad de la cual queremos obtener estos numeros aleatorios.

Una distribucion de probabilidad describe la gama de resultados que podemos obtener. De esta manera, la probabilidad de que obtengamos un valor dependera de la distribucion de probabilidad.

**Ejemplo:**

**La probabilidad de los dados:**

<p>&nbsp;</p>
<img src="dice2.png" width="100%" />
<p>&nbsp;</p>

Un dado convencional se caracteriza por poseer 6 lados, y cada lado representa un valor de 1 al 6. Frecuentemente en juegos de mesa como el parques, mientras mas alto sea el numero, mas podremos avanzar y ganar. Al lanzar el dado para poder avanzar, existe una probabilidad fija de obtener cualquiera de los 6 lados. Ya que esta probabilidad es la misma para cada lado (1/6), podriamos decir que la distribucion de los numeros de un dado pertenece a la distribucion uniforme.

## Distribucion uniforme:

En nuestro ejemplo del dado, planteamos que la distribucion de los numeros de cada lado del dado tiene una distribucion uniforme, debido a que la probabilidad de de obtener cada lado es la misma. Vamos a explorar un poco esto en R.

Para obtener un numero aleatorio n que viene de una distribucion uniforme utilizamos runif()

__*Estructura de la funcion*__

*runif(n, min, max)*

###### Para maas informacion ejecute ?runif

Vamos a escoger 10 numeros aleatorios del 1 al 6 que vienen de una distribucion uniforme


```r
ru1 <- runif(n = 10, min = 1, max = 6) #los numeros que obtendremos tienen decimales
hist(ru1)
```

<img src="07-Sesion_2_1_files/figure-html/unnamed-chunk-1-1.png" width="672" />

Segun nuestro histograma, y dependiendo de los numeros que nos toque, puede que obtengamos mas veces un numero que otro, ¿entonces la probabilidad no es la misma?


```r
ru2 <- runif(n =100, min = 1, max = 6) 
hist(ru2)
```

<img src="07-Sesion_2_1_files/figure-html/unnamed-chunk-2-1.png" width="672" />


```r
ru3 <- runif(n =1000, min = 1, max = 6) 
hist(ru3)
```

<img src="07-Sesion_2_1_files/figure-html/unnamed-chunk-3-1.png" width="672" />

¡Ahora nuestro histograma parece mas uniforme!. Cuando trabajamos con datos, siempre es una buena practica tener una muestra grande, con esto evitamos el sesgo en nuestros analisis.

## Distribucion normal:

La distribucion normal es una de las más importantes, ya que se ajusta a muchos datos que representan procesos en la vida real. Su representacion se asemeja a la de una campana, la campana de Gauss.

<img src="campana.png" width="100%" />

Para obtener un numero aleatorio n que viene de una distribuion normal utilizamos rnorm()

__*Estructura de la funcion*__

*rnorm(n, mean, sd)*

###### Para maas informacion ejecute ?rnorm


```r
rnorm(n = 4, mean = 100, sd = 5)
```

```
## [1]  99.62558  95.79660  91.21621 101.25875
```

######?set.seed para reproducir los mismos numeros


```r
set.seed(6)
rnorm(n = 10, mean = 5, sd = 5)
```

```
##  [1]  6.348030  1.850073  9.343299 13.635978  5.120938  6.840126 -1.546021
##  [8]  8.693110  5.224365 -0.241986
```


```r
set.seed(6)
rnorm(n = 10, mean = 5, sd = 5)
```

```
##  [1]  6.348030  1.850073  9.343299 13.635978  5.120938  6.840126 -1.546021
##  [8]  8.693110  5.224365 -0.241986
```


```r
set.seed(4)
rnorm(n = 10, mean = 5, sd = 5)
```

```
##  [1]  6.083774  2.287537  9.455723  7.979903 13.178090  8.446377 -1.406233
##  [8]  3.934277 14.482699 13.884316
```

**Distribucion normal estandar**


```r
rnorm(n = 100)
```

```
##   [1]  0.56660450  0.01571945  0.38305734 -0.04513712  0.03435191  0.16902677
##   [7]  1.16502684 -0.04420400 -0.10036844 -0.28344457  1.54081498  0.16516902
##  [13]  1.30762236  1.28825688  0.59289694 -0.28294368  1.25588403  0.90983915
##  [19] -0.92802811  1.24018084  0.15346418  1.05193258 -0.75421121 -1.48218912
##  [25]  0.86113187 -0.40451983 -0.22740542  0.93409617 -0.46589588 -0.63754350
##  [31]  1.34370863  0.18153538  1.29251234 -1.68804858 -0.82099358 -0.86214614
##  [37]  0.09884369 -0.37565514  0.72390416 -1.79738202 -0.66374314 -0.62372649
##  [43] -0.07963243  0.43562476  1.97090097 -0.59675867 -0.55250721  0.69596663
##  [49] -0.15566396  1.34889820 -1.06852307  1.06445075 -1.31272176  2.06369470
##  [55]  0.13138301 -0.23168845 -0.39735552  0.88943208  0.52616904 -0.17127324
##  [61]  0.15867690 -0.48566507 -0.95890607  0.18051729  0.72173428 -0.36954048
##  [67]  0.23753831 -0.66592211 -0.79680751 -0.05169693  1.28692833 -0.21414966
##  [73] -0.57474546 -1.47072704 -1.03273843 -1.30652486 -0.83825241 -1.13065368
##  [79]  0.36874818 -0.20180302 -1.27765990 -0.79801248  0.15908242  0.61479763
##  [85]  0.68794796 -0.04705101  2.33032168 -0.57756599  0.96847913 -0.27753563
##  [91]  0.68480194 -0.11511351 -0.35647518 -0.10577161  0.04488279 -1.72617323
##  [97]  1.55578702  0.77641269 -1.09850751 -1.72801975
```

Distribucion normal con media de 5 y distribucion estandar de 2

```r
rn<-rnorm(n = 100, mean = 5, sd = 2)
hist(rn)
```

<img src="07-Sesion_2_1_files/figure-html/unnamed-chunk-9-1.png" width="672" />

```r
mean(rn)
```

```
## [1] 4.900487
```

```r
sd(rn)
```

```
## [1] 2.075452
```

Distribucion normal con media de 5 y distribucion estandar de 2
Aumente n: 1000, 10000, 100000


```r
r<-rnorm(1000000, mean=5, sd=2)
hist(r)
```

<img src="07-Sesion_2_1_files/figure-html/unnamed-chunk-10-1.png" width="672" />

```r
mean(r)
```

```
## [1] 4.999633
```

```r
sd(r)
```

```
## [1] 1.997775
```

**Ejemplo:**

Vamos a cargar un conjunto de datos que contiene dos medidas del sepalo y petalo de diferentes especies de flores


```r
data(iris)
hist(iris$Sepal.Length)
```

<img src="07-Sesion_2_1_files/figure-html/unnamed-chunk-11-1.png" width="672" />

```r
hist(iris$Sepal.Width)
```

<img src="07-Sesion_2_1_files/figure-html/unnamed-chunk-11-2.png" width="672" />

```r
hist(iris$Petal.Length)
```

<img src="07-Sesion_2_1_files/figure-html/unnamed-chunk-11-3.png" width="672" />

```r
hist(iris$Petal.Width)
```

<img src="07-Sesion_2_1_files/figure-html/unnamed-chunk-11-4.png" width="672" />

¿Cual dato representa mejor una distribucion normal?

### Ggplot

library(ggplot2)


```r
library(ggplot2)
ggplot(iris, aes(Sepal.Width)) +
  geom_bar(stat = "count")
```

<img src="07-Sesion_2_1_files/figure-html/unnamed-chunk-12-1.png" width="672" />

**Ejercicios:**

**1.** Cree un vector v1 que contenga una muestra de 1000 numeros aleatorios que vengan de una distribucion normal con media de 112 y desviacion estandar  de 35. Grafique los valores en un histograma

**2.** Cree un vector v2 que contenga una muestra de 1000 numeros aleatorios que vengan de una distribucion normal con media de 34 y desviacion estandar de 3. Grafique los valores en un histograma

**3.** Multiplique v1 con v2 y grafique el resutado en un histograma. ¿Cual es la diferencia de este histograma con los anteriores?

**4.** Cree un vector "x" que contenga 14 numeros entre 1 y 50 que vengan de una distribucion uniforme. Cree otro vector "y" que contenga los valores de "x" pero dos veces mas grande. Suma a cada valor de "y" un valor constante de 7. Ahora grafiquelo mostrando "y" sobre "x" : plot(x,y)

## Probabilidad en distribución nomral

Para calcular la probabilidad de obtener un valor que viene de una distribucion normal, utilizamos la funcion pnorm()

__*Estructura de la funcion*__

*pnorm(q, mean, sd)*

###### Para maas informacion ejecute ?pnorm

¿Cual es la probabilidad de obtener un valor menor que -2 que venga de la distribucion normal? (mean = 2, sd = 2)?


```r
pnorm(q = 9, mean = 2, sd = 2)
```

```
## [1] 0.9997674
```

¿Cual es la probabilidad de obtener un valor mayor que -2 que venga de la distribucion normal mencionada anteriormente (mean = 2, sd = 2)?


```r
1-pnorm(-2,mean=2,sd=2)
```

```
## [1] 0.9772499
```

## Mas ejercicios

¿Cual es la probabilidad de obtener un valor menor que 5 que venga de la distribucion normal mencionada anteriormente (mean = 5, sd = 2)?

¿Cual es la probabilidad de obtener un valor entre 2 y 8?


