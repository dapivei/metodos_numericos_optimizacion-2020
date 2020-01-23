# Módulo 1: Cómputo Científico

Estas preguntas se responden a manera de preparación para los exámenes de teoría que se realizan en el curso **"Métodos Numéricos y Optimización 2020"**.

## 1.1 Análisis numérico y cómputo científico¶

###### 1) ¿Cuáles son las características del análisis numérico y cómputo científico?

El análisis numérico se enfoca al **diseño y análisis de algoritmos** para resolver problemas que surgen en la ciencia de la computación e ingeniería. Por esto, al análisis numérico se le ha llamado también cómputo científico y se distingue de otras áreas de la ciencia de la computación en que trabaja con cantidades continuas, cantidades como velocidad y temperatura presentes naturalmente.

###### 2) ¿Qué propiedades debe tener un buen algoritmo?

Algoritmos **iterativos** que **converjan "rápidamente"**, así como dar una **estimación de la exactitud** de las aproximaciones calculadas.

###### 3) ¿Cuáles fuentes de error principalmente son estudiadas por el análisis numérico y cómputo científico al resolver un problema?

El error computacional tiene dos componentes: a) **por truncamiento**: la diferencia entre el resultado veradero y el resultado que se obtiene con un algoritmo usando aritmética exacta; b) **por redondeo**: s la diferencia entre el resultado obtenido por un algoritmo utilizando aritmética exacta y el resultado producido por el mismo algoritmo usando aritmética de máquina.

###### 4) Menciona las diferencias entre los términos exactitud y precisión.

**La exactitud** se refiere a que tan cercano está el valor calculado o medido del valor verdadero; **la precisión** se refiere a qué tan cercanos se encuentran unos de otros diversos valores calculados o medidos.

## 1.2 Sistema de punto flotante

###### 1) ¿Cuáles componentes definen a un sistema de punto flotante?


En un sistema de punto flotante se define: **rango** de un exponente definido por un límite inferior y uno superior; **base del sistema**; y **precisión**.

Así, un número $x$ en el SPF, $x \in \mathcal{F}\mathcal{l}$, se representa de la forma:
$$\pm 0.d_1d_2 \dots d_k \times \beta^n .$$
donde:

$n$ es el exponente, $n \in [L,U] \cap \mathbb{Z}$ con $L, U$ fijos.
$k$ es la precisión.
$\beta$ es la base.
$d_i \in \{0,1,\dots,\beta-1\} \forall i=1,\dots,k$ son los dígitos.

*Obs: a la parte $\pm 0.d_1d_2 \dots d_k$ se le llama mantisa. A la porción $d_2 \dots d_k$ se le llama fracción $f$.*

###### 2) Si un número tiene una representación exacta en la máquina, ¿qué nombre recibe?

Los números reales que tienen una representación exacta en el $\mathcal{F}\mathcal{l}$ se les conoce como números de máquina.

###### 3) ¿Qué es un sistema de punto flotante normalizado?

Un Sistema de Punto Flotante Normalizado es aquel que cumple: $$d_1 \in \{1,2,\dots \beta -1\}.$$ para números distintos de cero.

*Obs: el número cero es el único que tiene dígitos de la mantisa y exponente iguales a cero.*

###### 4) Menciona algunas propiedades de un sistema de punto flotante normalizado.

###### 5) ¿Cuántos bits se utilizan en el hardware de una máquina para almacenar un número en un sistema de doble precisión?

Un sistema de punto flotante (SPF) de doble precisión utiliza **64 bits** para representar un número real. El primero es un indicador de signo denotado por $s$. Le siguen $11$ bits para construir al exponente $c$ llamado también característica y $52$ bits que construyen a la parte fraccionaria $f$ de la mantisa. La base es $\beta=2$.

*Nota 1: si es SPFN entonces aunque se tienen 52 bits, éstos se utilizan para almacenar un dígito más del número (ver Obs3 anterior). Así, en un SPF en general maneja 52 (o 53) dígitos binarios, que corresponden a aproximadamente 15 (o 16) dígitos decimales. Ver: Double-precision floating-point format.*
###### 6) ¿Qué nombre reciben los errores que se generan por utilizar un sistema de punto flotante?

Al ver el diagrama anterior de la representación gráfica de un SPF se observa que existen huecos entre cada número de máquina. Lo anterior implica que al ingresar un número real $x$ en la computadora, ésta realiza una aproximación a $x$ que se encuentre en el SPF. Esta aproximación genera errores conocidos con el nombre de errores por redondeo.

###### 7) ¿Cuáles reglas utiliza la máquina para dar aproximaciones a un número?

Entre las reglas que una computadora realiza para dar las aproximaciones a un número $x \in \mathbb{R}$ están: la regla de corte y la de redondeo y se pueden representar con funciones matemáticas:

+ **Regla de corte**: sea $fl_c : \mathbb{R} \rightarrow \mathcal{F}\mathcal{l}$ una función cuya regla de correspondencia es: $x \in \mathbb{R}$ con $x$ en el rango de valores del SPF, entonces: $x = \pm 0.d_1d_2 \dots d_kd_{k+1}\dots \times \beta^n$ y la regla de corte a $k$ dígitos es: $fl_c(x) = \pm 0.d_1d_2 \dots d_k$.

+ **Regla de redondeo**: sean $\beta=10$ y $fl_r : \mathbb{R} \rightarrow \mathcal{F}\mathcal{l}$ una función cuya regla de correspondencia es: $x \in \mathbb{R}$ con $x$ en el rango de valores del SPF, entonces: $x = \pm 0.d_1d_2 \dots d_kd_{k+1}\dots \times \beta^n$ y la regla de redondeo es:
$$f_r(x) = \begin{cases}
\text{sumar uno a } d_k &amp; \text{si } d_{k+1} \geq 5,\\
f_c(x) &amp; \text{en otro caso}
\end{cases}$$

*Obs: también la regla $fl_r(\cdot)$ se define como antes pero se añade la restricción entre si es par o impar el último dígito en caso de empate, entonces se almacena el par.*

###### 8) Explica con palabras la diferencia entre el epsilon de la máquina y el nivel de underflow:


a. ¿Cuál de ellos depende únicamente del número de dígitos de la mantisa?
b. ¿Cuál de ellos depende únicamente del número de dígitos del exponente?
c. ¿Cuál de ellos no depende de la reglas usadas que se preguntaron en la pregunta 7?

###### 9) Si calculamos un error relativo para una aproximación y resulta ser del orden de $10^{-8}$ ¿alrededor de cuántos dígitos correctos tengo en mi aproximación?

###### 10) Menciona algunos problemas típicos de la aritmética de máquina y algunas formas de resolverlos.

Problemas típicos:

+ Problema de cancelación: pérdida de cifras significativas a partir de la resta de números similares.
+ Suma entre un número de magnitud grande y un número de magnitud pequeña.
+ Sumas con términos que involucren signos alternados.
+ Multiplicación por un número de magnitud grande.
+ División por un número de magnitud pequeña.

Posibles soluciones:

+ Usar mayor precisión.
+ Reordenar operaciones.
+ Reescribir expresiones matemáticas para obtener expresiones equivalentes.
+ Escalar las variables. También funciona estandarizarlas.


## 1.3 Condición, estabilidad y normas: condición de un problema y estabilidad del algoritmo

###### 1 )¿Qué factores influyen en la falta de exactitud de un cálculo?
###### 2) Menciona $5$ propiedades que un conjunto debe cumplir para que sea considerado un espacio vectorial.
###### 3) Menciona las propiedades que debe cumplir una función para que se considere una norma.
###### 4) ¿Qué es una norma matricial inducida?, ¿qué mide una norma matricial inducida?
###### 5)¿La norma de Frobenius, es una norma matricial inducida?
###### 6)¿A qué son iguales $\text{sup}(\emptyset)$, $\text{inf}(\emptyset)$ ? (el conjunto $\emptyset$ es el conjunto vacío)
###### 7) Si f es un problema mal condicionado, ¿a qué nos referimos? Da ejemplos de problemas bien y mal condicionados.
###### 8) Si f es un problema que resolvemos con un algoritmo g, ¿qué significa:
a. que g sea estable?

b. que g sea estable hacia atrás?

c. que g sea inestable?

###### 9) ¿Qué ventaja(s) se tiene(n) al calcular un error hacia atrás vs calcular un error hacia delante?



## 1.4 Polinomios de Taylor y diferenciación numérica

## 1.5 Integración Numérica

## 1.6 Perfilamento de código

## 1.7 OPciones para resolver bottlenecks:
