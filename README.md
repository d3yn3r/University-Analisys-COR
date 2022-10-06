# College Scorecard Data analysis
#### Andrés Camilo García Moreno - Ingeniería de sistemas e informatica 
#### Deyner Elías López Pineda - Ingeniería de sistemas e informatica 

## Tabla de contenido
* [Introducción](#introduccion)
* [Pre-Procesamiento de datos](#pre-procesamiento-de-datos)
* [Variables](#variables)
    * [PREDDEG](#preddeg)
    * [DISTANCEONLY](#distanceonly)
    * [TUITFTE](#tuitfte)
    * [ADM_RATE_ALL](#admrateall)
    * [NPT4_PUB](#npt4pub)
    * [NPT4_PRIV](#npt4pub)
* [Matriz de correlación](#matriz-de-correlacion)
* [Análisis de nulos](#analisis-de-nulos)
* [Análisis de un caso](#análisis-de-un-caso)
    * [Curva del codo](#curva-del-codo)
    * [Dendrograma](#dendrograma)
    * [Grupos](#grupos)
        * [Grupo 0](#grupo-0)
        * [Grupo 1](#grupo-1)
        * [Grupo 2](#grupo-2)
* [Conclusión](#conclusion)
* [Video promocional](#video-promocional)
* [Aplicación](#aplicacion)
* [Referencias Bibliográficas](#referencias-bibliograficas)


<a name=introduccion></a>

## Introducción

Tomando el dataset de College Scoreboard el cual cuenta amplia información de instituciones de educación superior, usaremos técnicas de clustering para separar en grupos distintos a las instituciones.

Esto con el fin de crear una aplicación donde una persona pueda escoger entre 3 variables, y que de estas se genere un clustering, como los grupos en clustering tienen sus características particulares, una persona podrá mirar la base de datos de cada grupo además de una descripción de cada grupo, para cual pueda mirar si encuentra una institución de educación superior, que se acomode a sus necesidades en base a las variables que escogió.


<a name=pre-procesamiento-de-datos></a>

## Pre-procesamiento de datos
Para que una persona pueda elegir una institución está lógicamente debe encontrarse activa, por ende, filtramos inicialmente la base de datos usando la variable CURROPER, para que esta solo contenga las universidades que aún están operando.

Las variables que serán escogidas que sean numéricas serán normalizadas para lo siguiente será escoger variables de interés para una persona que quiera escoger una universidad, para esto escogemos las siguientes variables:

<a name=variables></a>

## Variables

<a name=preddeg></a>

#### PREDDEG
Esta variable nos indica el grado de certificación que predomina en la institución, a esta variable en particular se le aplicara la técnica de One-Hot encoding, ya que los números dan una información categórica, sin embargo no existe una institución en el que predomina el grado más alto de certificación, por eso al preprocesar los datos al normalizar los datos, la categoría más alta, muestran datos nulos, por ende cuando se hace el one-hot encoding la columna resultante a esta categoría es eliminada ya que el método k-means no admite nulos.

- 0, Non-degree-granting
- 1, Certificate degree
- 2, Associate degree
- 3, Bachelor's degree
- 4, Graduate degree

<a name=distanceonly></a>

#### DISTANCEONLY
Esta variable indica si la institución ofrece únicamente o no, educación remota.

- 0, Not distance education
- 1, Distance education only

<a name=tuitfte></a>

#### TUITFTE

Esta variable numérica podemos encontrar los ingresos netos por matrícula por estudiante equivalente a tiempo completo (TUITFTE, por sus siglas en inglés) utilizan los ingresos por matrícula menos los descuentos y asignaciones, y los dividen por el número de estudiantes FTE de pregrado y posgrado.

<a name=admrateall></a>

#### ADM_RATE_ALL

Representa la tasa de admisión en todos los campus, definida como el número total de estudiantes universitarios admitidos en todas las sucursales dividido por el número total de estudiantes universitarios que presentaron solicitudes en todas las sucursales.

<a name=npt4pub></a>

#### NPT4_PUB

Esta variable indica el precio promedio neto para garantizar la asistencia normal de los estudiantes menos la ayuda federal, estatal e institucional, esta métrica se limita a los estudiantes universitarios que pagan matrícula estatal.

<a name=npt4priv></a>

#### NPT4_PRIV

Esta variable indica el precio neto promedio para garantizar la asistencia normal de los estudiantes para las instituciones privadas, esta métrica incluye un promedio ponderado de todos los estudiantes universitarios que reciben Título IV.

<a name= Matriz-de-correlación></a>

## Matriz de correlación

Luego de revisar la documentación de la base de datos y escoger las variables de importancia para nuestro análisis, realizamos la matriz de correlación entre estas, y en la cual encontramos que no presentan una correlación alta, por lo cual son excelentes variables para realizar el análisis, ademas como podemos ver ,NPT4_PRIV y NT4_PUB no muestra ningún valor , esto se debe a que estas variables tienen comportamiento cercano a mutuametente excluyente entre ellas , por lo tanto para las tecnicas de clustering , estas 2 variables nunca estaran juntas , ademas por el carácter de estas variables podemos separar a las intstituciones entre publicas y privadas.

![Matriz de correlacion de las variables](https://github.com/d3yn3r/University-Analisys-COR/blob/main/Nuevas%20Imagenes/Matriz%20de%20correlacion%20de%20las%20variables.PNG)

<a name=analisis-de-nulos></a>

## Análisis de Nulos 

Como para la aplicación se usarán opciones para los usuarios, las variables tienen diferente cantidad de nulos por columna, en especial ADM_RATE_ALL, ya que esta no cuenta con muchas observaciones, por lo tanto, al no tener información concluyente acerca de los datos nulos, procedemos a eliminarlos de la base de datos, obteniendo como resultado diferentes cantidades de observaciones según cada variable.

<a name=analisis-de-un-caso></a>

## Análisis de un caso 

Dado que en la aplicación podemos escoger varias opciones, esto nos da como resultado varios casos, y por practicidad solo interpretaremos los resultados de uno de los casos posibles, y analizaremos diferentes métodos de obtención del k optimo.

Para este caso usamos las variables: [NPT4_PUB](#npt4pub), [PREDDEG](#preddeg), [DISTANCEONLY](#distanceonly)

<a name=curva-del-codo></a>

### Curva del codo

El primer análisis para la obtención del k optimó que realizamos, fue el de la curva del codo, este nos dio como resultado un k=3.

![Curva del codo caso 1](https://github.com/d3yn3r/University-Analisys-COR/blob/main/Nuevas%20Imagenes/Curva%20del%20codo%20Caso1.png)

Posteriormente realizamos un dendrograma 

<a name=dendrograma></a>

### Dendrograma

![Dendrograma caso 1 ](https://github.com/d3yn3r/University-Analisys-COR/blob/main/Nuevas%20Imagenes/Dendrograma%20Caso1.png)

<a name=grupos></a>

### Grupos

Luego de los cálculos realizados, procedemos a realizar los análisis de los grupos obtenidos mediante las técnicas ejecutadas.

<a name=grupo-0></a>

#### Grupo 0

En el grupo cero, nos encontramos con 566 instituciones de carácter público, con una media neta de pago de matrícula estatal de 13,315.85 las cuales cerca de un 98% cuentan con un grado de certificación 3, Bachelor's degree.


|index|DISTANCEONLY|NPT4\_PUB|PREDDEG\_ Associate degree|PREDDEG\_ Bachelor&\#39;s degree|PREDDEG\_ Certificate degree|PREDDEG\_ Non-degree-granting|Labels\_3Clusters|
|---|---|---|---|---|---|---|---|
|count|566\.0|566\.0|566\.0|566\.0|566\.0|566\.0|566\.0|
|mean|0\.0017667844522968198|13315\.851590106007|0\.0|0\.9876325088339223|0\.0|0\.012367491166077738|0\.0|
|std|0\.042033135170919854|3958\.619634615561|0\.0|0\.11061715498377031|0\.0|0\.11061715498377031|0\.0|
|min|0\.0|2035\.0|0\.0|0\.0|0\.0|0\.0|0\.0|
|25%|0\.0|10780\.25|0\.0|1\.0|0\.0|0\.0|0\.0|
|50%|0\.0|13529\.5|0\.0|1\.0|0\.0|0\.0|0\.0|
|75%|0\.0|15883\.5|0\.0|1\.0|0\.0|0\.0|0\.0|
|max|1\.0|27032\.0|0\.0|1\.0|0\.0|1\.0|0\.0|

<a name=grupo-1></a>

#### Grupo 1

Para el grupo uno, se agruparon 777 instituciones de carácter público, con una media neta de pago de matrícula estatal de 7,536.90, de las cuales cuentan con un grado de certificación 2, Associate degree.

|index|DISTANCEONLY|NPT4\_PUB|PREDDEG\_ Associate degree|PREDDEG\_ Bachelor&\#39;s degree|PREDDEG\_ Certificate degree|PREDDEG\_ Non-degree-granting|Labels\_3Clusters|
|---|---|---|---|---|---|---|---|
|count|777\.0|777\.0|777\.0|777\.0|777\.0|777\.0|777\.0|
|mean|0\.0|7536\.906048906048|1\.0|0\.0|0\.0|0\.0|1\.0|
|std|0\.0|3074\.8167463083573|0\.0|0\.0|0\.0|0\.0|0\.0|
|min|0\.0|-445\.0|1\.0|0\.0|0\.0|0\.0|1\.0|
|25%|0\.0|5476\.0|1\.0|0\.0|0\.0|0\.0|1\.0|
|50%|0\.0|7258\.0|1\.0|0\.0|0\.0|0\.0|1\.0|
|75%|0\.0|9140\.0|1\.0|0\.0|0\.0|0\.0|1\.0|
|max|0\.0|22774\.0|1\.0|0\.0|0\.0|0\.0|1\.0|

<a name=grupo-2></a>

#### Grupo 2

Para el grupo uno, se agruparon 567 instituciones de carácter público, con una media neta de pago de matrícula estatal de 8,646.82, de las cuales cuentan con un grado de certificación 1, Certificate degree.

|index|DISTANCEONLY|NPT4\_PUB|PREDDEG\_ Associate degree|PREDDEG\_ Bachelor&\#39;s degree|PREDDEG\_ Certificate degree|PREDDEG\_ Non-degree-granting|Labels\_3Clusters|
|---|---|---|---|---|---|---|---|
|count|567\.0|567\.0|567\.0|567\.0|567\.0|567\.0|567\.0|
|mean|0\.0|8646\.828924162257|0\.0|0\.0|1\.0|0\.0|2\.0|
|std|0\.0|4700\.063112576339|0\.0|0\.0|0\.0|0\.0|0\.0|
|min|0\.0|-1643\.0|0\.0|0\.0|1\.0|0\.0|2\.0|
|25%|0\.0|5647\.5|0\.0|0\.0|1\.0|0\.0|2\.0|
|50%|0\.0|7834\.0|0\.0|0\.0|1\.0|0\.0|2\.0|
|75%|0\.0|10688\.0|0\.0|0\.0|1\.0|0\.0|2\.0|
|max|0\.0|27199\.0|0\.0|0\.0|1\.0|0\.0|2\.0|

<a name=conclusion></a>

## Conclusión 

Gracias al anterior análisis, las personas interesadas en ingresar a una institución universitaria pueden tener una base más clara acerca de a que institución desean presentarse, y mediante el [aplicativo](https://ancgarciamo.shinyapps.io/Uni-Score/) presentado pueden generar casos en los que se evidencien los resultados más óptimos para las variables de preferencia de cada usuario.


<a name=video-promocional></a>

## Video promocional

<a name=aplicacion></a>

## Aplicación

[Link del aplicativo web](https://ancgarciamo.shinyapps.io/Uni-Score/)

<a name=referencias-bibliograficas></a>

### Referencias

[[1] K-Means Clustering in Python: A Practical Guide](https://realpython.com/k-means-clustering-python/#:~:text=The%20k%2Dmeans%20clustering%20method,the%20oldest%20and%20most%20approachable.)<br>

[[2] U.S. DEPARTMENT OF EDUCATION College Scorecard](https://collegescorecard.ed.gov/data/)<br>

[[3] Cluster Analysis Exercise 2](https://data.world/exercises/cluster-analysis-exercise-2)<br>

[[4] Stack overflow](https://stackoverflow.com/)<br>

[[5] Shiny](https://shiny.rstudio.com/)<br>
