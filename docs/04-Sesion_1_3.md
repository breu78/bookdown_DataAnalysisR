# Leyendo y manejando datos en R

### Estableciendo el directorio de trabajo para poder leer datos desde un archivo {-}

Antes de empezar, debemos crear nuestro sitio de trabajo mediante la función setwd(), en el cual debemos poner entre comillas la dirección de la carpeta en la que tenemos guardado este script y el archivo con los datos del proyecto Santander BIO "Santander_BIO_data.csv"

```
setwd("~/r tic/sesion 2") # Note que empieza con ~ ya que esto nos dirige automáticamente a la carpeta mis documentos que R establece por defecto. Las carpetas se separan con /
```

En RStudio se recomienda utilizar: Session -> Set Working Directory

***

## Data frame                                

Al igual que una matriz, los data frames son un conjunto de elementos ordenados en dos dimensiones. Filas (observaciones) y columnas (variables). Sin embargo, en un data frame se pueden almacenar diferentes tipos de datos en diferentes columnas.

Una de las formas más comunes en la que vamos a encontrar datos, es en formato Excel o .csv. Estos son datos tabulados que constan de dos dimensiones, filas y columnas, que pueden almacenar datos numéricos y caracteres.

***

### Leer archivo desde carpeta de trabajo

Para leer con facilidad en R los archivos .csv, es posible convertirlos en formato .csv (coma seperated values por sus siglas en ingles) en Excel y importarlos de la siguiente forma:


```r
setwd("~/r tic/sesion 2")
dat <-read.csv("Santander_BIO_data.csv") # Note que los nombres de los documentos van entre comillas y con la extensión del documento
```

Ya hemos cargado nuestros datos en un data frame, el cual se trata de información sobre inventarios de la biodiversidad en el marco del proyecto Santander BIO. Nuestro data frame cuenta con información taxonómica (Nombre de la especie, familia, reino, etc.) e información sobre los sitios y la altura a la que se encuentran estas especies.

***

### Evaluar la estructura del data frame

Ahora vamos a explorar nuestro datos aprendiendo paso a paso algunas funciones importantes


```r
dim(dat) # Dimensiones de los datos: 1255 filas (observaciones) y 11 columnas (variables)
- [1] 1255   11
colnames(dat) #Nombre de las columnas
-  [1] "species"   "locality"  "municipio" "kingdom"   "phylum"    "class"    
-  [7] "order"     "family"    "genus"     "taxonRank" "elevation"
str(dat) #Estructura de los datos
- 'data.frame':	1255 obs. of  11 variables:
-  $ species  : chr  "Aciotis circaeifolia" "Adiantum obliquum" "Adiantum pulverulentum" "Adiantum wilsonii" ...
-  $ locality : chr  "Vereda El Aguila" "Vereda El Aguila" "Vereda El Aguila" "Vereda El Aguila" ...
-  $ municipio: chr  "Cimitarra" "Cimitarra" "Cimitarra" "Cimitarra" ...
-  $ kingdom  : chr  "Plantae" "Plantae" "Plantae" "Plantae" ...
-  $ phylum   : chr  "Tracheophyta" "Tracheophyta" "Tracheophyta" "Tracheophyta" ...
-  $ class    : chr  "Magnoliopsida" "Polypodiopsida" "Polypodiopsida" "Polypodiopsida" ...
-  $ order    : chr  "Myrtales" "Polypodiales" "Polypodiales" "Polypodiales" ...
-  $ family   : chr  "Melastomataceae" "Pteridaceae" "Pteridaceae" "Pteridaceae" ...
-  $ genus    : chr  "Aciotis" "Adiantum" "Adiantum" "Adiantum" ...
-  $ taxonRank: chr  "SPECIES" "SPECIES" "SPECIES" "SPECIES" ...
-  $ elevation: int  158 158 159 158 158 158 158 155 158 122 ...
```

Tambien es posible preguntar por otras condiciones en nuestro data frame que no sean necesariamente numéricas, o que su resultado no sea una posición. Por ejemplo, un resultado tipo lógico, mediante la función is.numeric/character()


```r
is.numeric(dat$species) 
- [1] FALSE
is.character(dat$species) 
- [1] TRUE
is.numeric(dat$elevation) 
- [1] TRUE
is.character(dat$elevation) 
- [1] FALSE
```

***

## Acceder variables del data frame           

Para seleccionar una variable o columna del data frame utilizaremos el caracter "$" seguido del nombre que asignamos al vector, después pondremos el nombre de la variable deseada o podremos desplegar todas las opciones con tabulador


```r
ele <- dat$elevation
head(ele)
- [1] 158 158 159 158 158 158
tail(ele)
- [1] 2575 2525 2402 2390 2525 2525
min(dat$elevation) #Valor mínimo de una variable deseada (en este caso altura de la observación)
- [1] 74
max(dat$elevation) #Valor máximo de una variable deseada (en este caso altura de la observación)
- [1] 3603
```

Explorar con las funciones mean() y sd().

Sabemos que hay distintos lugares en donde se colecto la información de las especies, y que cada lugar puede aparecer más de una vez porque es probable que cuente con más de una especie colectada. Vamos a averiguar el número de especies que existen sin que se repitan:


```r
head(dat$species)
- [1] "Aciotis circaeifolia"   "Adiantum obliquum"      "Adiantum pulverulentum"
- [4] "Adiantum wilsonii"      "Aechmea longicuspis"    "Aegiphila cordata"
length(dat$species)
- [1] 1255
species <- unique(dat$species) #Con la función "unique" obtendremos los nombres de las especies sin que se repitan

length(species) #Hay 1000 especies en total
- [1] 1000
```

Ahora averiguaremos cuantas especie únicas puede haber en un municipio aleatorio. Para esto, vamos a crear un vector que contenga solo los datos del municipio deseado, aunque esto no es obligatorio, puede ser una forma ordenada de escribir nuestro código.


```r
unique(dat$municipio) #Averiguamos los municipios de colecta
- [1] "Cimitarra"            "El Carmen de Chucuri" "Santa Barbara"
m_Cimitarra <- dat[dat$municipio=="Cimitarra",] #Usamos los corchetes [] para seleccionar las filas que contengan datos únicamente del municipio de Cimitarra. Después de la "," se deja vacía para que extraiga todas las columnas asociadas a las filas que seleccionamos

sp_unicas_cimitarra <- unique(m_Cimitarra$species)

length(sp_unicas_cimitarra) #En el municipio de Cimitarra existen 397 especies
- [1] 397
```

***Ejercicios:***
```
1. Averigue la elevacion máxima y mínima de los registros realizados

2. Por favor extrae la altura máxima y mínima de la que se tiene registro en cada reino (Plantae, Animalia ) por localidad (Vereda El Aguila, Vereda Guineales, Vereda Locacion, Vereda Riveras de San Juan)

3. ¿Cuál es el promedio de altura de todo los registros por municipio?
```

***

## Acceder observaciones mas complejos           

Podemos especificar más de una condición para crear un set de datos más pequeño


```r
or_operador <- dat[dat$municipio=="Cimitarra" | dat$municipio=="Santa Barbara",] # Utilizamos el simbolo "|" o "or" para extraer una condición u otra. Si ambas condiciones son verdaderas en nuestro set de datos, se extraeran las dos

or_operador <- dat[dat$municipio=="Cimitarra" | dat$municipio=="Santa",] # En este caso solo extraera observaciones de Cimitarra ya que no hay un municipio llamado "Santa"

#Si queremos elegir todas las observaciones menos una en particular, usamos el operador lógico !

plantas_no <- dat[!dat$kingdom=="Plantae",] # Seleccionamos solo observaciones con registros del reino Animalia
```

Para seleccionar varias condiciones usamos &


```r
alt_0_100 <- dat[dat$elevation > 0 & dat$elevation < 100,] # seleccionar alturas entre 0 y 100 metros

length(alt_0_100[,1]) # Existen 16 observaciones registradas en el rango de altura de 0 a 100 metros, todos en Cimitarra
- [1] 16
```

¿Cómo podemos verificar que obtuvimos los datos deseados?


```r
min(alt_0_100$elevation)
- [1] 74
max(alt_0_100$elevation)
- [1] 97
```

¿Cómo podemos averiguar el número de registros de anfibios registrados en cada municipio?


```r
amphi_cimitarra <- dat[dat$municipio=="Cimitarra" & dat$class=="Amphibia",]
length(amphi_cimitarra[,1])
- [1] 33
amphi_el_carmen <- dat[dat$municipio=="El Carmen de Chucuri" & dat$class=="Amphibia",]
length(amphi_el_carmen[,1]) 
- [1] 6
amphi_st_barbara <- dat[dat$municipio=="Santa Barbara" & dat$class=="Amphibia",]
length(amphi_st_barbara[,1]) 
- [1] 7
```

***Pregunta:*** Como podemos averiguar el número de especies de anfibios registrados en cada municipio?

***

## Agregar columnas al data frame para apoyar el análisis  

En el ejercicio anterior observamos una diferencia en el número de registros de anfibios en cada municipio. Vamos a ver el número de registros totales en cada municipio


```r
dat$conteo <- 1 #Podemos añadir una nueva columna que tenga el número 1 en cada observación y así hacer una suma de filas 

sum(dat[dat$municipio=="Cimitarra", 13]) #En Cimitarra existen 551 registros
- [1] 0
sum(dat[dat$municipio=="El Carmen de Chucuri", 13]) #En el Carmen de Chucuri existen 372 registros totales
- [1] 0
sum(dat[dat$municipio=="Santa Barbara", 13]) #En Santa Barbara existen 332 registros
- [1] 0
```

Finalmente, podemos eliminar la columna de conteo


```r
dat <- dat[,-13]
```

***

### crear rangos en una variable continua:

¿Cuál es el rango de altura en la que registraron los anfibios del ejercicio anterior? 

Para esto usaremos la función cut()

?cut


```r
dat$cut <- cut(dat$elevation, 4)

dat$cut <- cut(dat$elevation, 4, labels = c("a", "b", "c", "d"))
```

Explique que sucede en las líneas de código anterior, luego defina 4 rangos de altura que empiece desde 0 y termine en 4000 metros y colóqueles una etiqueta. Finalmente responda la pregunta anterior


```r
dat$cut <- cut(dat$elevation, breaks = c(0,1000,2000,3000,4000), labels = c("Cero a mil", "Mil a dos mil", "Dos mil a tres mil", "Tres mil a cuatro mil"))

levels(dat$cut)
- [1] "Cero a mil"            "Mil a dos mil"         "Dos mil a tres mil"   
- [4] "Tres mil a cuatro mil"
```

***Ejercicios:***

```
1. Calcula el numero de registros por cada rango de alturas

2. Calcula el numero de especies por cada rango de alturas

3. Calcula el numero de especies de plantas por cada rango de alturasil a cua
```

***

## Indexar  y reemplazar                  

En R podemos preguntar por una condición en específico y el resultado será la posición de este en el data frame. Esto se hace mediante la función which().

?which

Podemos preguntar por ejemplo por los registros que se encuentren a una altura menor de 80 metros


```r
which(dat$elevation<80) #Existen 6 registros que se encuentran a una altura menor de 80 metros
- [1] 1144 1147 1165 1173 1179 1180
dat[1144,] #El resultado de la fila 1144 corresponde la especie Curimata mivartii registrada a 74 metros de altura
-                species                   locality municipio  kingdom   phylum
- 1144 Curimata mivartii Vereda Riveras de San Juan Cimitarra Animalia Chordata
-               class         order      family    genus taxonRank elevation
- 1144 Actinopterygii Characiformes Curimatidae Curimata   SPECIES        74
-      conteo        cut
- 1144      1 Cero a mil
```

Si guardamos las posiciones del resultado anterior, podemos obtener todos los resultados en un nuevo data frame de manera rápida:


```r
posiciones <- which(dat$elevation<80)

nuevo_dat <- dat[posiciones,] #Podemos escribir el nombre del vector que contiene los valores de las posiciones para no escribirlas una por una
nuevo_dat
-                             species                   locality municipio
- 1144              Curimata mivartii Vereda Riveras de San Juan Cimitarra
- 1147      Dasyloricaria filamentosa Vereda Riveras de San Juan Cimitarra
- 1165        Megaleporinus muyscorum Vereda Riveras de San Juan Cimitarra
- 1173 Pimelodella floridablancaensis Vereda Riveras de San Juan Cimitarra
- 1179      Rhinoclemmys melanosterna Vereda Riveras de San Juan Cimitarra
- 1180       Rineloricaria magdalenae Vereda Riveras de San Juan Cimitarra
-       kingdom   phylum          class         order        family         genus
- 1144 Animalia Chordata Actinopterygii Characiformes   Curimatidae      Curimata
- 1147 Animalia Chordata Actinopterygii  Siluriformes  Loricariidae Dasyloricaria
- 1165 Animalia Chordata Actinopterygii Characiformes   Anostomidae Megaleporinus
- 1173 Animalia Chordata Actinopterygii  Siluriformes Heptapteridae   Pimelodella
- 1179 Animalia Chordata       Reptilia    Testudines   Geoemydidae  Rhinoclemmys
- 1180 Animalia Chordata Actinopterygii  Siluriformes  Loricariidae Rineloricaria
-      taxonRank elevation conteo        cut
- 1144   SPECIES        74      1 Cero a mil
- 1147   SPECIES        74      1 Cero a mil
- 1165   SPECIES        74      1 Cero a mil
- 1173   SPECIES        74      1 Cero a mil
- 1179   SPECIES        74      1 Cero a mil
- 1180   SPECIES        74      1 Cero a mil
```

Ademas de extraer información de un data frame, podemos editarlo de forma sencilla. Supongamos que encontramos un error asociado a un dato en específico, como el nombre de una familia. En nuestro caso hipotético, supongamos que nuestros datos tienen un error de digitación, y el nombre de la familia Acanthaceae está mal escrito, por lo que necesitamos cambiarlo.


```r
dat2 <- dat #Copiamos el data frame en un nuevo vector

nombre_incorrecto <- which(dat2$family=="Acanthaceae") #Guardamos la posición de las filas en las que esta el nombre de la familia mal escrito

dat2[nombre_incorrecto, 8] <- "Nombre correcto" #Cambiamos el nombre por el que deseamos
```

Otra alternativa: Utilice la siguiente función para cambiar el nombre de la familia Viperidae a "Notviperidae" y verifique que el cambio se hizo correctamente

?replace


```r
dat2$family <- replace(dat2$family ,c(dat2$family=="Viperidae"), "Notviperidae")
verificacion <- dat2[dat2$family=="Nombre correcto",] #Y finalmente verificamos que el cambio fue realizado
```

***Ejercicios:***
```
1. Realice en una gráfica de barras el número de registros totales por cada municipio

2. Realice una gráfica del número de registros de insectos en cada localidad

3. Realice un boxplot de la elevacion por las distintas clases

4. Realice un histograma de la elevación
```
