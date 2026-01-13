# Clase 04 - Análisis de algoritmos

**Fecha:** 13-01-2026
**Estado:** 🟢 Completado

## Resumen en 3 líneas



## Preguntas Clave



## Contenido

### Algoritmo de G-S usando arrays y listas

En esta sección veremos como implementar el algoritmo de G-S para el problema de emparejamiento estable. Buscaremos las estructuras necesarias para que el algoritmo efectivamente sea $O(n^2)$.

#### Arrays y listas

Para resolver este problema, necesitamos varias estructuras, empezando por ejemplo con la lista de preferencias de mujeres para cada hombre. Esto se puede representar sin mucha dificultad en cualquier lenguaje de programación con un arreglo $A$ de tamaño $n$, donde $A[i]$ es el $i$-ésimo elemento del arreglo.

1. En un arreglo podemos obtener el $i$-ésimo elemento en tiempo $O(1)$ accediendo a través del índice $i$.
2. Si queremos determinar si un elemento $e$ pertenece o no a la lista, tenemos que recorrerla toda, por lo que esta tarea tiene un tiempo $O(n)$.
3. Si los elementos del arreglo están ordenados de alguna manera clara, entonces la tarea anterior se puede hacer en tiempo $O(n\log n)$ utilizando búsqueda binaria.

En general, un arreglo no es una buena estructura para mantener una lista que cambia su tamaño dinámicamente con el tiempo, como en el caso de la lista de hombres libros en el algoritmo de Emparejamiento Estable.

Una buena alternativa para mantener un conjunto dinámico, es mediante una lista encadenada.
Por lo general se representa mediante punteros, con dos de ellos especiales llamados "first" y "null" que representan el primer y último puntero respectivamente, marcando el inicio y final de la lista. Para cada elemento también asignamos un registro $e$ que contenga el valor del elemento que queremos agregar a la lista.

No entraremos mucho más al detalle de la implementación de una lista encadenada, pues ya lo hemos hecho en algún momento, pero lo importante para esta parte es notar que las listas encadenadas son buenas cuando el tamaño cambia dinámicamente, pero tenemos una desventaja con respecto a los arreglos, que es que el $i$-ésimo elemento no se puede hallar en tiempo $O(1)$, ya que necesariamente tenemos que recorrer la lista y buscarlo, que nos deja con un tiempo $O(n)$.

Dadas las ventajas y desventajas de las listas y arreglos, a menudo es importante poder trabajar con una representación u otra según la necesidad. Esto se puede hacer fácilmente en tiempo $O(n)$.

#### Implementación del algoritmo de Emparejamiento Estable

Empezaremos con las listas de preferencias para cada hombre y cada mujer, tendremos dos arreglos respectivamente:

- $\operatorname{ManPref}[m,i]$ denotando a la $i$-ésima mujer preferida por $m$.
- $\operatorname{WomanPref}[w,i]$ denotando al $i$-ésimo hombre preferido por $w$.

Notemos que la cantidad de espacio necesario es $O(n^2)$, pues cada persona tiene una lista de largo $n$.
Continuamos considerando que necesitamos poder implementar de forma eficiente cada una de las siguientes cuatro cosas:

1. Necesitamos poder identificar un hombre libre.
2. Necesitamos, para un hombre $m$, ser capaces de identificar la mujer con mayor prioridad a la que aún no se le ha propuesto.
3. Para una mujer $w$, necesitamos poder decir si está actualmente en pareja, y si lo está determinar quién es su pareja.
4. Para una mujer $w$ y dos hombres $m$ y $m'$, determinar si $m$ o $m'$ es preferido por $w$.

Primero consideremos el problema de identificar un hombre libre. Esto se resuelve fácilmente manteniendo el conjunto de hombres libres como una lista enlazada. Cuando necesitamos seleccionar a un hombre libre, seleccionamos al primero $(O(1))$, si se compromete lo eliminamos $(O(1))$ y posiblemente insertamos a otro hombre $m'$ al frente de la lista $(O(1))$.

Ahora consideremos a un hombre $m$. Necesitamos poder identificar la mujer más preferida a la que aún no se le ha propuesto. Para esto usamos un arreglo extra "$\operatorname{Next}$" que indique para cada hombre $m$ la posición de la siguiente mujer a la que se le propondrá.
Inicializamos $\operatorname{Next}[m]=1$ para todo $m$. Si un hombre $m$ necesita proponerle a una mujer entonces, se le propondrá a $w=\operatorname{ManPref}[m,Next[m]]$, y una vez que $m$ se le propone a $w$ incrementamos $\operatorname{Next}[m]$ en uno.

Por otra parte, dado un hombre $m$ que se le propone a una mujer $w$, debemos poder identificar el hombre $m'$ con el que $w$ está comprometida, si es que existe tal hombre.
Para esto creamos un arreglo "$\operatorname{Current}$" de tamaño $n$, donde $\operatorname{Current}[w]$ es el actual compañero de la mujer $w$, es decir $m'$. Inicializamos $\operatorname{Current}[w]$ en un símbolo especial nulo, para representar cuando $w$ no está comprometida.

Por último, dada una mujer $w$ y dos hombres $m$ y $m'$ queremos determinar el preferido por $w$. Para esto nos podríamos ver tentados de usar $\operatorname{WomanPref}[m,i]$, pero deberíamos recorrer todo este arreglo para usarlo, lo que nos dejaría con tiempo $O(n)$, que se puede mejorar.
Creando una estructura auxiliar, un arreglo $n\times n$, "$\operatorname{Ranking}$", donde $\operatorname{Ranking}[w,m]$ contiene la posición de $m$ en la tabla de preferencias de $w$, por lo que esta tarea sea puede hacer en tiempo $O(1)$, requiriendo una inversión inicial de un tiempo proporcional a $n^2$.
Con esto decidimos entre los hombres simplemente comparando $\operatorname{Ranking}[w,m]$ y $\operatorname{Ranking}[w,m']$ quedandonos con el mayor de ellos.

- **(2.10) Las estructuras de datos descriptas en esta sección nos permiten implementar el algoritmo de G-S en tiempo $O(n^2)$.**