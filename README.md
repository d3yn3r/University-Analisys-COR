# University-Analisys-COR

Tomando el dataset de College Scoreboard el cual cuenta amplia información de instituciones de educación superior , usaremos técnicas de clustering para separar en grupos distintos a las instituciones.

Esto con el fin de crear una aplicación donde una persona pueda escoger entre 3 variables, y que de estas se genere un clustering, como los grupos en clustering tienen sus características particulares , una persona podrá mirar la base de datos de cada grupo además de una descripción de cada grupo , para cual pueda mirar si encuentra una institución de educación superior, que se acomode a sus necesidades en base a las variables que escogió.

## Pre-procesamiento de datos
Para que una persona pueda elegir una institución está lógicamente debe encontrarse activa , por ende filtramos inicialmente la base de datos usando la variable CURROPER , para que esta solo contenga las universidades que aún están operando.

Las variables que serán escogidas que sean numericas seran normalizadas para 

Lo siguiente son escoger variables de interés para una persona que quiera escoger una universidad , para esto escogemos las siguientes variables :
### Variables

#### PREDDEG
Esta variable nos indica el grado de certificación que predomina en la institución, a esta variable en particular se le aplicara la técnica de One-Hot encoding , ya que los números dan una información categórica, sin embargo no existe una institución en el que predomina el grado más alto de certificación, por eso al pre-procesar los datos al normalizar los datos, la categoría más alta , muestran datos nulos , por ende cuando se hace el one-hot encoding la columna resultante a esta categoria es eliminada ya que el metodo k-means no admite nulos.

- 0, Non-degree-granting
- 1, Certificate degree
- 2, Associate degree
- 3, Bachelor's degree
- 4, Graduate degree

#### DISTANCEONLY
Esta variable indica si la institución ofrece unicamente o no , educacion remota.

- 0, Not distance education
- 1, Distance education only

#### TUITFTE

Esta variable numerica significan los ingresos netos por matrícula por estudiante equivalente a tiempo completo (TUITFTE, por sus siglas en inglés) utilizan los ingresos por matrícula menos los descuentos y asignaciones, y los dividen por el número de estudiantes FTE de pregrado y posgrado.

#### ADM_RATE_ALL

#### NPT4_PUB

#### NPT4_PRIV

### Análisis de Nulos 
Como para la aplicación se usarán opciones para los usuarios , las variables tienen diferente cantidad de nulos por columna , en especial ADM_RATE_ALL, ya que esta no cuenta con muchas observaciones ya que es una variable que toma.


## Análisis de un caso 
La aplicación al ser opciones

### Curva del codo

### Dendrograma

### Grupos

#### Grupo 0

#### Grupo 1

#### Grupo 2
