# Clase 02 - Emparejamiento estable

**Fecha:** 2025-11-26
**Estado:** 🟢 Completado

## Resumen en 3 líneas



## Preguntas Clave



## Contenido

### Emparejamiento estable

#### Analizando el algoritmo

A continuación, intentaremos responder a algunas de las preguntas que nos hicimos en la clase anterior, y otras posibles preguntas que podrían habernos surgido analizando el algoritmo.

Consideremos inicialmente el punto de vista de una mejor, durante la ejecución del algoritmo. En un principio, nadie se le ha propuesto, por lo que está soltera. Entonces un hombre puede proponerle matrimonio, resultando en que ella quede comprometida. A medida que pasa el tiempo, ella puede recibir propuestas adicionales, aceptando aquellas que vienen de un hombre con mayor preferencia que el actual. De esto obtenemos que:

- **(1.1) $w$ permanece comprometida desde el momento en que recibe su primera propuesta; y la secuencia de parejas irá mejorando en términos de sus preferencias.**

Por otra parte, el punto de vista de un hombre durante la ejecución es bastante diferente. Él está soltero hasta que se le propone a la mujer mejor clasificada en su lista de preferencias; en este punto, puede comprometerse o no. A medida que pasa el tiempo su estado oscila entre soltero y comprometido. Sin embargo se sostiene lo siguiente:

- **(1.2) La secuencia de mujeres a las que $m$ se les propone irá empeorando en términos de preferencia.**

Ahora demostraremos que el algoritmo termina, dando un límite del número máximo de iteraciones necesarias para que finalice.

- **(1.3) El algoritmo de G-S finaliza después de un máximo de $n^2$ de iteraciones en el ciclo de While.**

**Demostración:**

Buscaremos una forma precisa de mostrar que cada paso del algoritmo lo lleva más cerca de su finalización como método para determinar el máximo límite de tiempo de ejecución del mismo.
Notemos que en el algoritmo, cada iteración consiste en que un hombre se le propone, una única vez, a una mujer que nunca se le ha propuesto. Entonces si llamamos $P(t)$ al par $(m,w)$ tal que $m$ se le propone a $w$ en la iteración $t$, tendremos que para todo $t$ se cumplirá que el tamaño de $P(t+1)$ es estrictamente mayor que el de $P(t)$ (esto porque en toda iteración se hace exactamente una propuesta), esto nos permite concluir que el algoritmo se acerca hacia la condición de fin en cada iteración.
Por otra parte, la máxima cantidad posible de pares de hombres y mujeres es $n\times n$, por lo tanto el tamaño de $P(\cdot)$ puede aumentar como mucho hasta $n^2$.
Por lo tanto podemos concluir que el algoritmo finaliza con un máximo de $n^2$ iteraciones. $\blacksquare$

Ahora querremos verificar que el emparejamiento devuelto por el algoritmo es efectivamente un emparejamiento estable. Para esto necesitamos varios pasos previos, siendo el primero probar que un hombre no puede salir del final de su lista de preferencias (pues quedaría soltero y el algoritmo no terminaría).

- **(1.4) Si $m$ está soltero en algún punto de la ejecución del algoritmo, entonces hay una mujer a la que aún no se le ha propuesto.**

**Demostración:**

Supongamos que se llega al punto en que $m$ está soltero, pero ya se le propuso a todas las mujeres. Entonces por el punto (1.1), cada una de las $n$ mujeres está comprometida en este momento. Dado que el conjunto de los pares comprometidos forma un emparejamiento, también debe haber $n$ hombres comprometidos. Pero el total de hombres es $n$, por lo tanto no puede pasar que $m$ no esté comprometido.
Como llegamos a una contradicción, la suposición que hicimos inicialmente fue absurda. $\blacksquare$

- **(1.5) Al finalizar la ejecución, el emparejamiento obtenido es perfecto.**

**Demostración:**

El conjunto de pares comprometidos siempre devuelve un emparejamiento. Supongamos que el algoritmo termina con $m$ soltero, entonces $m$ se le propuso a todas las mujeres, de lo contrario el ciclo while no hubiera terminado.
Pero esto no puede pasar, pues por el punto (1.4) si el hombre $m$ está soltero entonces existe alguna mujer $w$ a la que todavía no se le ha propuesto.
Como esto contradice nuestras hipótesis, tenemos que concluir que lo que supisimos es absurdo. $\blacksquare$

Ahora si, podemos probar que el algoritmo produce un emparejamiento estable.

- **(1.6) Al finalizar la ejecución, el emparejamiento obtenido $S$ es estable.**

**Demostración:**

Ya vimos en (1.5) que el algoritmo produce un emparejamiento perfecto.
Ahora para probar que el emparejamiento también es estable, supondremos que no lo es, es decir que existe una instabilidad con respecto a $S$ y obtener una contradicción.
Como definimos en la clase anterior, esta inestabilidad consiste de dos pares $(m_1,w_1),(m_2,w_2)$ en $S$ tales que:

- $m_1$ prefiere a $w_2$ antes que a $w_1$
- $w_2$ prefiere a $m_1$ antes que a $m_2$

Por el orden de ejecución del algoritmo, necesariamente la última propuesta que hizo $m_1$ fue a $w_1$. Con esto podemos distinguir dos casos:

1. Si $m_1$ **NO** propuso anteriormente a $w_2$, entonces $m_1$ prefiere a $w_1$ antes que a $w_1$, lo cual contradice nuestras hipótesis.
2. Si $m_1$ **SI** le propuso anteriormente a $w_2$, entonces tiene que existir un tercer hombre $m_3$ tal que $w_2$ prefiere a $m_3$ antes que a $m_1$. Como la última pareja de $w_2$ es $m_2$, tenemos dos posibilidades; o bien $m_3=m_2$, o bien $w_2$ prefiere a $m_2$ antes que a $m_3$ (por (1.1)). Ambas las dos posibilidades contradicen nuestra suposición inicial de que $w_2$ prefiere a $m_1$ antes que a $m_2$

Como los dos casos contradicen alguna de las hipótesis, concluimos que $S$ es un emparejamiento estable. $\blacksquare$

#### Extensiones del análisis

Hay algunas cuestiones más que vamos a investigar más profundamente.
Una de ellas, es que dado el diseño actual del algoritmo, termina siendo "injusto" hacia el conjunto al que se le proponen (en nuestro caso las mujeres). Consideremos el caso donde ninguna de las preferencias de los hombre se solapan en el primer lugar, entonces para este caso todos los hombres terminarían en pareja con la mujer que más prefieren, mientras que las preferencias de las mujeres no serían tomadas en cuenta.

Aparte de esta cuestión de injusticia, la cosa se pone peor para el conjunto al que se le proponen, pues vamos a demostrar que todas las ejecuciones del algoritmo devuelven siempre el mismo emparejamiento.
Esto es clave para la consistencia del resultado, y para probarlo lo que haremos es caracterizar el resultado de forma única, mediante el concepto fundamental de "mejor pareja posible".

Consideramos que una mujer $w$ es una "pareja válida" para un hombre $m$ si existe un emparejamiento estable que incluya el par $(m,w)$. Además, la mujer $w$ es considerada la "mejor pareja posible" para el hombre $m$ si es una pareja válida para él, y además no hay ninguna otra mujer que él prefiera más, que también sea una pareja válida para él.
Denotaremos a la mejor pareja posible para un hombre $m$ como $best(m)$.
Llamaremos $S^*$ al conjunto de pares $(m,best(m))$ con $m\in M$. Probaremos lo siguiente:

- **(1.7) Cada ejecución del algoritmo G-S da como resultado el conjunto $S^*$**

**Demostración:**

Supongamos, a modo de contradicción, que alguna ejecución $E$ del algoritmo de G-S resulta en un emparejamiento $S$ tal que un hombre se empareja con una mujer que no es su mejor pareja posible. Como los hombres proponen en orden de preferencia, significa que si un hombre no se empareja con su mejor pareja posible, entonces fue rechazada por ella. De esta forma, consideramos el primer momento de la ejecución $E$ en el que un hombre $m$ es rechazado por una pareja válida $w$.

Como los hombres proponen en orden decreciente de preferencia, y dado que es la primera vez que se produce un rechazo de una pareja válida, debe ser que $w$ es la mejor pareja posible para $m$.
El rechazo de $m$ por $w$ puede haber ocurrido porque $m$ propuso, y fue rechazado a favor del compromiso existente de $w$, o porque $w$ rompió su compromiso a favor de una mejor propuesta. En cualquier caso, en este punto **$w$ se compromete o continúa comprometida con un hombre $m'$, a quién prefiere por sobre $m$ $(*_1)$**.

Como $w$ es una pareja válida para $m$, existe un emparejamiento estable $S'$ que contiene el par $(m,w)$. Luego nos preguntamos: ¿con quién está emparejado $m'$ en este emparejamiento? Supongamos que es una mujer $w'\neq w$.
Como el rechazo de $m$ por $w$ fue el primer rechazo de un hombre por una pareja válida en la ejecución $E$, debe de ser que $m'$ no había sido rechazado por ninguna pareja válida en $E$ al momento de comprometerse con $w$. Sumando a esto, que $m'$ se propone en orden decreciente de preferencia y dado que $w'$ es una pareja válida de $m'$, tiene que ser entonces que $m'$ prefiere a $w$ antes que a $w'$. Vimos en $*_1$ que $w$ prefiere a $m'$ antes que a $m$, y como $(m, w')$ no está en $S'$, tenemos que este par es una inestabilidad en $S'$.

Esto último contradice nuestra suposición de que $S'$ es estable, luego se genera un absurdo con nuestra suposición inicial. $\blacksquare$

De lo anterior, concluimos que el algoritmo G-S es ideal para los hombres, desafortunadamente no se puede decir lo mismo para las mujeres. Decimos que $m$ es la peor pareja posible para una mujer $w$ si $m$ es una pareja válida de $w$ y ningún hombre que $w$ califica por debajo de $m$ es una pareja válida de ella.

- **(1.8) En el emparejamiento estable $S^*$, cada mujer es emparejada con su peor pareja posible.**

**Demostración:**

Supongamos que hay un par $(m,w)\in S^*$ tal que $m$ no es la peor pareja válida de $w$. Luego, hay un emparejamiento estable $S'$ en que se corresponde a $w$ con un hombre $m'$ a quién ella prefiere menos que a $m$. En $S'$, $m$ es emparejado con una mujer $w'\neq w$; como $w$ es la mejor pareja válida para $m$ y $w'$ es una pareja válida de $m$, podemos ver que $m$ prefiere a $w$ antes que a $w'$.

Entonces el par $(m,w)$ es una inestabilidad de $S'$, contradiciendo la suposición que $S'$ es estable y, por tanto contradiciendo nuestra suposición inicial.
