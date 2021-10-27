# Introducción a la programación con R

<style> body {text-align: justify} </style> <!-- Justify text. -->

Comenzaremos con las operaciones básicas ejecutadas en la línea de comandos en R o terminal. Este será nuestro espacio de trabajo en el cual ejecutaremos las ordenes cuyos resultados se mostrarán en la consola.  

Todo lo que siga después de un numeral (#) será considerado como un comentario, que al ejecutar será omitido. Para ejecutar el código en R podemos utilizar el botón "run" que disponemos arriba a la derecha, o utilizar un atajo:

 + **Command + Enter (Mac)**
 + **Control + Enter (Windows, Linux)**
 
## La línea de comandos (Terminal) 

Línea de comandos como calculadora:


```r
2+5
- [1] 7
7-3
- [1] 4
(2+3)*5
- [1] 25
(2+3)/((2+3)*5)
- [1] 0.2
```

Se pueden ejecutar varias operaciones utilizando punto y coma (;):


```r
2+5; 4+6
- [1] 7
- [1] 10
```

Dispone de diferentes funciones como raíz cuadrada o logaritmo:


```r
?Arithmetic
sqrt(9) # raíz cuadrada
- [1] 3
log(1)  # logaritmo
- [1] 0
log10(10) # logaritmo base 10
- [1] 1
3^2 # potenciación (exponente 2)
- [1] 9
```

Las letras y variables más importantes estan disponibles en R:


```r
?Constants
pi
- [1] 3.141593
letters
-  [1] "a" "b" "c" "d" "e" "f" "g" "h" "i" "j" "k" "l" "m" "n" "o" "p" "q" "r" "s"
- [20] "t" "u" "v" "w" "x" "y" "z"
LETTERS
-  [1] "A" "B" "C" "D" "E" "F" "G" "H" "I" "J" "K" "L" "M" "N" "O" "P" "Q" "R" "S"
- [20] "T" "U" "V" "W" "X" "Y" "Z"
```

***

### Función ayuda

Existen tres formas de obtener ayuda:

1. Área miscelánea -> "Help"
2. Símbolo "?" antes de la función
3. Tecla Tabulador (Autocompleta el nombre)


```r
x <- c(1,2,3,4,5,6,7,8) # <- símbolo de asignación, permite agrupar los elementos dentro del objeto 
```


```r
x = c(1,2,3,4,5,6,7,8) # "<-" o "=" significa lo mismo
```


```r
mean(x)
- [1] 4.5
?sum
?rep
?sort
?order
```

Estructura de la función:

 + Función: "mean()"
 + Objeto: "x"
 + Argumento ('arg'): "na.rm=FALSE"

**Ejercicios:**
```
1. Explique brevemente la función "order". ¿Qué hace y que significan los argumentos? 
```

***

### Creando nuevas variables:

Para crear una nueva variable usted puede utilizar "<-" (símbolo de asignación) o "=". Es aconsejable el uso de "<-" ya que se refiere a la indexación dentro de un vector.

Cada variable necesita un nombre que puede estar compuesto de letras, números, "." o "_" y nunca por números. Ejemplo: "my_data".

R diferencia entre minúsculas y mayúsculas; "a" es diferente de "A". Las variables pueden ser reescritas. Una vez escrita una variable podemos llamar al objeto:


```r
x <- 3
x
- [1] 3
x <- 9
x
- [1] 9
resultado <- 3+9
resultado
- [1] 12
mode(resultado)
- [1] "numeric"
```

Además de las variables ('numeric'), R permite la definición de texto ('character') y de variables lógicas ('logic', ej: TRUE y FALSE). Los caracteres deben ser puestos entre comillas ("...") para que R los identifique como tal.

Estos tipos de vectores se definen como vectores atómicos:


```r
y <- "test"
y
- [1] "test"
mode(y)
- [1] "character"
a <- FALSE
a
- [1] FALSE
mode(a)
- [1] "logical"
mode(T) # T es igual a TRUE, y F es igual a FALSE
- [1] "logical"
```

¿Qué ocurre aquí?


```r
s <- as.numeric(c(T,F,F)) 
mode(s)
- [1] "numeric"
```

***

### El área de trabajo o memoria - ventana arriba a la derecha 'Environment'

Todos los objetos creados durante una sesión son guardados en el área de trabajo. Para ver el área de trabajo ejecute ls(), para remover algún objeto de esta ejecute rm().

También puede utilizar los botones en el área de trabajo


```r
ls()
- [1] "a"         "resultado" "s"         "x"         "y"
rm(s)
ls()
- [1] "a"         "resultado" "x"         "y"
```

***

## Vamos a practicar  

Puedes hacer cálculos simples con variables númericas


```r
a <- 5
b <- 7
a+b+3
- [1] 15
```

¿Qué ocurre a continuación? ¡Por favor explique!


```r
b = 2
b == 2
- [1] TRUE
b == 3
- [1] FALSE
c = 7
d = -3
?Syntax
```

**Ejercicios**
```
1. Compruebe las siguientes afirmaciones lógicas:

a. c mayor que d
b. c menor o igual que d
c. c igual a d

```
***

### R como calculadora - Operadores y funciones.
```
?Syntax

* <-               Asignar
* + - * / % ^      Aritméticas
* > >= < <= == !=  Relación (orden y comparación)
* ! & && | ||      lógicas
* $                lista indexada
* :                Crear una secuencia
```

Operadores lógicos para:
```
* !      NO
* &      Y
* |      O
* <     Menor que
* <=    Menor o igual que
* >     Mayor que
* >=    Mayor o igual que
* ==    IGUAL
* !=    NO IGUAL (diferente de)
* &&    AND with IF (y con si <condicional>)
* ||    OR with IF (o con si <condicional>)
```

***

## Tipos de Datos y Objetos

* **Logical** = (FALSO/VERDADERO) / (FALSE/TRUE)
* **Number** = (Entero, Decimal, Complejo (e.g. 3i))
* **Character** = Letras y palabras ("", o '')

Otros tipos de datos son "list", "expression", "name", "symbol" and "function"

Para operaciones más complejas necesitamos estructuras de datos más complejas. R ofrece más que solo objetos que contienen un elemento, como los vectores o las matrices.

***

### Vectores I: Vectores sencillos     

Para hacer un vector utilice la función concatenar "c()" . Los elementos sencillos de un vector están separados por ",".


```r
x <- c (2, 5, 10, 14, 3, 1, 18, 24, 17)
x
- [1]  2  5 10 14  3  1 18 24 17
mode(x)
- [1] "numeric"
```


```r
a <- c ("text", 2, 6, TRUE)
mode(a) ## ¿Qué ocurre aquí? Por qué "character"?
- [1] "character"
a <- c ( 2, 6, F)
mode(a) #y ahora?
- [1] "numeric"
```

Crear un vector vacío:


```r
b <- numeric(20)
b
-  [1] 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
```

**Ejercicio:**
```
1. Cree un vector con nombre "vec" que contenga los números de 1 a 10.
```

Un vector también puede contener diferentes tipos de variables. Usted puede realizar cálculos con vectores que contengan solo elementos "numeric"

Suma


```r
sort(x)
- [1]  1  2  3  5 10 14 17 18 24
sum(x)
- [1] 94
```

Promedio


```r
mean(x)
- [1] 10.44444
```

Cuartil


```r
quantile(x)
-   0%  25%  50%  75% 100% 
-    1    3   10   17   24
```

Longitud del vector


```r
length (x)
- [1] 9
length(letters)
- [1] 26
```

Ordenar


```r
x
- [1]  2  5 10 14  3  1 18 24 17
?sort(x)
sort(x, decreasing = F)
- [1]  1  2  3  5 10 14 17 18 24
sort(x, decreasing = FALSE)
- [1]  1  2  3  5 10 14 17 18 24
sort(x, decreasing = T)
- [1] 24 18 17 14 10  5  3  2  1
sort(x, decreasing = TRUE)
- [1] 24 18 17 14 10  5  3  2  1
```

¿Qué ocurre si colocamos "decreasing = TRUE"? Compruebe con "?sort"

"sort" y "order" realizan la misma función; sin embargo "order" puede ser aplicado a otro tipo de objetos diferentes a vectores, como los data frames.

Calculo con vectores: Por favor explique qué ocurre a continuación


```r
x
- [1]  2  5 10 14  3  1 18 24 17
length(x)
- [1] 9
#1
x + 10
- [1] 12 15 20 24 13 11 28 34 27
x
- [1]  2  5 10 14  3  1 18 24 17
#2
y <- c(1, 3, 5)
x + y
- [1]  3  8 15 15  6  6 19 27 22
x
- [1]  2  5 10 14  3  1 18 24 17
#3
y <- c (4, 2, 8, 5, 3, 9, 3, 10, 1)
xy <- x + y
xy
- [1]  6  7 18 19  6 10 21 34 18
x
- [1]  2  5 10 14  3  1 18 24 17
#4
y <- c(1, 3)
x + y
- Warning in x + y: longer object length is not a multiple of shorter object
- length
- [1]  3  8 11 17  4  4 19 27 18
x
- [1]  2  5 10 14  3  1 18 24 17
#5
y <- c (4, 2, 8, 5, 3, 9, 3, 10, 1)
sum(x)
- [1] 94
sum(x,y)
- [1] 139
sum(x + y)
- [1] 139
```

Etiquetar elementos de un vector con nombres. Función "names()"


```r
x <- c (2, 5, 10, 14, 3, 1, 18, 24, 17)
a <- c ("E1","E2","E3","E4","E5","E6","E7","E8","E9")
names (x) <- a
x
- E1 E2 E3 E4 E5 E6 E7 E8 E9 
-  2  5 10 14  3  1 18 24 17
names(x) # Vector de los nombres del vector numérico x 
- [1] "E1" "E2" "E3" "E4" "E5" "E6" "E7" "E8" "E9"
str (x) # sobre la estructura del vector x (muy útil!)
-  Named num [1:9] 2 5 10 14 3 1 18 24 17
-  - attr(*, "names")= chr [1:9] "E1" "E2" "E3" "E4" ...
summary (x) # indica los valores mínimos, máximos, etc.
-    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
-    1.00    3.00   10.00   10.44   17.00   24.00
head (x)
- E1 E2 E3 E4 E5 E6 
-  2  5 10 14  3  1
tail (x)
- E4 E5 E6 E7 E8 E9 
- 14  3  1 18 24 17
```

**Ejercicios:**
```
1. Sumar los números enteros de 1 hasta 5

2. Crear un variable v1 que contenga una letra

3. Copiar v1 a v2

4. Compare los valores de v1 y v2

5. Cree un vector de longitud 20 con el tipo de datos que usted quiera y muestre las primeras nueve entradas.

6. Cree un vector que contenga los seis primeras letras del abecedario.
```

***

### Vectores II: Vectores más complejos                       

Secuencias


```r
z <- 3:10
z
- [1]  3  4  5  6  7  8  9 10
```

?seq


```r
seq(from = 1, to = 6, by = 0.2) # El argumento "by" genera frecuencias #
-  [1] 1.0 1.2 1.4 1.6 1.8 2.0 2.2 2.4 2.6 2.8 3.0 3.2 3.4 3.6 3.8 4.0 4.2 4.4 4.6
- [20] 4.8 5.0 5.2 5.4 5.6 5.8 6.0
seq(from = 1, to = 6, length.out = 20)  # ¿Cuál es la diferencia con respecto al anterior? 
-  [1] 1.000000 1.263158 1.526316 1.789474 2.052632 2.315789 2.578947 2.842105
-  [9] 3.105263 3.368421 3.631579 3.894737 4.157895 4.421053 4.684211 4.947368
- [17] 5.210526 5.473684 5.736842 6.000000
```

Puede empezar desde cualquier punto


```r
seq(from = 530, to = 620, by = 30)
- [1] 530 560 590 620
```


```r
z <- c(1, 3, 9)
z
- [1] 1 3 9
?rep
rep (z, times = 10) # ¿Qué ocurre aqui?
-  [1] 1 3 9 1 3 9 1 3 9 1 3 9 1 3 9 1 3 9 1 3 9 1 3 9 1 3 9 1 3 9
```

La secuencia de elementos del vector z se repite 10 veces


```r
rep (z, each = 10)  			    # ¿Cuál es la diferencia con la linea anterior?
-  [1] 1 1 1 1 1 1 1 1 1 1 3 3 3 3 3 3 3 3 3 3 9 9 9 9 9 9 9 9 9 9
```

Aquí cada uno de los elementos del vector z se repite 10 veces.

***

### Indexar
Para extraer uno o varios elementos de un vector utilice "[]". Por favor observe y explique que ocurre en las siguientes líneas:


```r
x
- E1 E2 E3 E4 E5 E6 E7 E8 E9 
-  2  5 10 14  3  1 18 24 17
x[5]
- E5 
-  3
x[4]
- E4 
- 14
x[3:5]
- E3 E4 E5 
- 10 14  3
x[c(3,5)]
- E3 E5 
- 10  3
id<-c(1, 9, 2)
x[id]
- E1 E9 E2 
-  2 17  5
x[c (1, 9, 2)]
- E1 E9 E2 
-  2 17  5
x[-c (1, 9, 2)]
- E3 E4 E5 E6 E7 E8 
- 10 14  3  1 18 24
```

**Ejercicios:**
```
1. Cree un vector con los números de 1 a 100
x <- (1:100)

2. Extraiga del vector el elemento numero 87

3. Extraiga todos los elementos excepto el 87 para crear un nuevo vector "z"

4. Verifique la longitud del nuevo vector

PLUS: Extraiga cada segundo elemento del vector

5. Cree un vector vacío de longitud 10 y asigne a su tercer elemento el valor que tiene la suma de x

```

**Ejercicios:**
```
1. Cree un vector vacío de cuatro elementos

2. En el vector vacío indexe para cada posición la primera inicial de sus nombres y apellidos. (Si tiene un solo nombre indexe NA)
```

***

### NA         


```r
?NA
e <- c(122, 324, 34, NA, 234) 
mean(e) # porque sale este resultado? con NA no se puede calcular!
- [1] NA
?mean
mean(e, na.rm = T) # ahora sin tener en cuenta el NA
- [1] 178.5
is.na(e)        #¿Qué ocurre aquí? me indica cuales son NA
- [1] FALSE FALSE FALSE  TRUE FALSE
which(is.na(e)) #¿Qué ocurre aquí? me indica la posición del NA
- [1] 4
```

***

### Matrices                               

La matriz es un conjunto de elementos que son del mismo tipo, ya sea numéricos, de carácter o lógico, distribuidos en dos dimensiones, filas y columnas. 

 + [1,] indica la primera fila
 + [,1] indica la primera columna


```r
mat <- matrix(data = 1:12, nrow = 3, ncol = 4, byrow = T)
mat
-      [,1] [,2] [,3] [,4]
- [1,]    1    2    3    4
- [2,]    5    6    7    8
- [3,]    9   10   11   12
mat[,1]
- [1] 1 5 9
mat[2,2]
- [1] 6
mat[1:3,1:3]
-      [,1] [,2] [,3]
- [1,]    1    2    3
- [2,]    5    6    7
- [3,]    9   10   11
mat[,1]
- [1] 1 5 9
mat[1,]
- [1] 1 2 3 4
```

Transponer la matriz


```r
mat2 <- t(mat)
mat2
-      [,1] [,2] [,3]
- [1,]    1    5    9
- [2,]    2    6   10
- [3,]    3    7   11
- [4,]    4    8   12
mat
-      [,1] [,2] [,3] [,4]
- [1,]    1    2    3    4
- [2,]    5    6    7    8
- [3,]    9   10   11   12
colnames(mat2) <- c("A","B","C")
mat2
-      A B  C
- [1,] 1 5  9
- [2,] 2 6 10
- [3,] 3 7 11
- [4,] 4 8 12
rownames(mat2) <-c ("sp1","sp2","sp3","sp4")
mat2
-     A B  C
- sp1 1 5  9
- sp2 2 6 10
- sp3 3 7 11
- sp4 4 8 12
class(mat2[,1])
- [1] "integer"
class(mat2[2,1])
- [1] "integer"
```

**Ejercicios:**
```
1. Realice una matriz con 11 columnas y 11 filas.

2. Incluya en la matriz el número 8 en cada esquina y en la mitad de la matriz
```

cbind y rbind


```r
mat
-      [,1] [,2] [,3] [,4]
- [1,]    1    2    3    4
- [2,]    5    6    7    8
- [3,]    9   10   11   12
c5 <- c(5,5,5)
cbind(mat, c5)
-                 c5
- [1,] 1  2  3  4  5
- [2,] 5  6  7  8  5
- [3,] 9 10 11 12  5
r4 <- c(4,4,4,4)
rbind(mat, r4)
-    [,1] [,2] [,3] [,4]
-       1    2    3    4
-       5    6    7    8
-       9   10   11   12
- r4    4    4    4    4
```

rownames y colnames


```r
rownames(mat) <- c("a", "b", "c")
mat
-   [,1] [,2] [,3] [,4]
- a    1    2    3    4
- b    5    6    7    8
- c    9   10   11   12
colnames(mat) <- c("E1", "E2","E3","E4")
mat
-   E1 E2 E3 E4
- a  1  2  3  4
- b  5  6  7  8
- c  9 10 11 12
```

***

**!Felicitaciones, ahora has aprendido sobre el funcionamiento básico de R y Rstudio!**
