## Ejercicio 02 - Emparejamiento estable

**Fecha:** 28-11-2025
**Estado:** 🟢 Resuelto solo

### Consigna

Considere una instancia del problema de emparejamiento estable entre los conjuntos:

- $M = \{m_1, m_2, m_3, m_4\}$  
- $W = \{w_1, w_2, w_3, w_4\}$  

con listas de preferencias dadas por las tablas mostradas a continuación. 
A modo de ejemplo, $m_1$ prefiere en primer lugar a $w_1$, mientras que para $w_1$ la mejor opción es $m_4$.

|     | 1° | 2° | 3° | 4° |
|-----|----|----|----|----|
| $m_1$ | $w_1$ | $w_2$ | $w_3$ | $w_4$ |
| $m_2$ | $w_1$ | $w_4$ | $w_3$ | $w_2$ |
| $m_3$ | $w_2$ | $w_1$ | $w_3$ | $w_4$ |
| $m_4$ | $w_4$ | $w_2$ | $w_3$ | $w_1$ |

|     | 1° | 2° | 3° | 4° |
|-----|----|----|----|----|
| $w_1$ | $m_4$ | $m_3$ | $m_1$ | $m_2$ |
| $w_2$ | $m_2$ | $m_4$ | $m_1$ | $m_3$ |
| $w_3$ | $m_4$ | $m_1$ | $m_2$ | $m_3$ |
| $w_4$ | $m_3$ | $m_2$ | $m_1$ | $m_4$ |

1. Presente una **sucesión de formaciones y separaciones de parejas** que se realizan a lo largo de una ejecución del algoritmo de **Gale–Shapley**.

2. Repita la parte 1 **invirtiendo los roles** de $M$ y $W$.

3. Note que el emparejamiento estable formado en las partes anteriores es el mismo (a menos del orden en que se listan las parejas).  
Muestre que, en esta instancia, para toda persona se verifica que:
    - su **mejor pareja válida** coincide con su **peor pareja válida**.

    ¿Qué resultados del libro está aplicando?

4. Concluya que para esta instancia del problema existe **una única solución**.

### Resolución

#### Parte 1

- Presente una **sucesión de formaciones y separaciones de parejas** que se realizan a lo largo de una ejecución del algoritmo de **Gale–Shapley**.

Veamos iteración por iteración el estado del conjunto $S$ que será devuelto como resultado.

##### Iteración 1

**Conjunto $S$:** $\{(m_1,w_1)\}$
**Pareja propuesta:** $(m_1,w_1)$
**Pareja formada:** $(m_1,w_1)$
**Pareja rechazada:** Ninguna

##### Iteración 2

**Conjunto $S$:** $\{(m_1,w_1)\}$
**Pareja propuesta:** $(m_2,w_1)$
**Pareja formada:** Ninguna
**Pareja rechazada:** $(m_2,w_1)$

##### Iteración 3

**Conjunto $S$:** $\{(m_1,w_1),(m_2,w_4)\}$
**Pareja propuesta:** $(m_2,w_4)$
**Pareja formada:** $(m_2,w_4)$
**Pareja rechazada:** Ninguna

##### Iteración 4

**Conjunto $S$:** $\{(m_1,w_1),(m_2,w_4),(m_3,w_2)\}$
**Pareja propuesta:** $(m_3,w_2)$
**Pareja formada:** $(m_3,w_2)$
**Pareja rechazada:** Ninguna

##### Iteración 5

**Conjunto $S$:** $\{(m_1,w_1),(m_2,w_4),(m_3,w_2)\}$
**Pareja propuesta:** $(m_4,w_4)$
**Pareja formada:** Ninguna
**Pareja rechazada:** $(m_4,w_4)$

##### Iteración 6

**Conjunto $S$:** $\{(m_1,w_1),(m_2,w_4),(m_4,w_2)\}$
**Pareja propuesta:** $(m_4,w_2)$
**Pareja formada:** $(m_4,w_2)$
**Pareja rechazada:** $(m_3,w_2)$

##### Iteración 7

**Conjunto $S$:** $\{(m_3,w_1),(m_2,w_4),(m_4,w_2)\}$
**Pareja propuesta:** $(m_3,w_1)$
**Pareja formada:** $(m_3,w_1)$
**Pareja rechazada:** $(m_1,w_1)$

##### Iteración 8

**Conjunto $S$:** $\{(m_3,w_1),(m_2,w_4),(m_4,w_2)\}$
**Pareja propuesta:** $(m_1,w_2)$
**Pareja formada:** Ninguna
**Pareja rechazada:** $(m_1,w_2)$

##### Iteración 9

**Conjunto $S$:** $\{(m_3,w_1),(m_2,w_4),(m_4,w_2), (m_1,w_3)\}$
**Pareja propuesta:** $(m_1,w_3)$
**Pareja formada:** $(m_1,w_3)$
**Pareja rechazada:** Ninguna

A este punto ya tenemos formado el emparejamiento estable que buscabamos.

#### Parte 2

- Repita la parte 1 **invirtiendo los roles** de $M$ y $W$.

Veamos iteración por iteración el estado del conjunto $S$ que será devuelto como resultado al proponer la mujer en vez del hombre.

##### Iteración 1

**Conjunto $S$:** $\{(w_1,m_4)\}$
**Pareja propuesta:** $(w_1,m_4)$
**Pareja formada:** $(w_1,m_4)$
**Pareja rechazada:** Ninguna

##### Iteración 2

**Conjunto $S$:** $\{(w_1,m_4),(w_2,m_2)\}$
**Pareja propuesta:** $(w_2,m_2)$
**Pareja formada:** $(w_2,m_2)$
**Pareja rechazada:** Ninguna

##### Iteración 3

**Conjunto $S$:** $\{(w_2,m_2),(w_3,m_4)\}$
**Pareja propuesta:** $(w_3,m_4)$
**Pareja formada:** $(w_3,m_4)$
**Pareja rechazada:** $(w_1,m_4)$

##### Iteración 4

**Conjunto $S$:** $\{(w_2,m_2),(w_3,m_4),(w_1,m_3)\}$
**Pareja propuesta:** $(w_1,m_3)$
**Pareja formada:** $(w_1,m_3)$
**Pareja rechazada:** Ninguna

##### Iteración 5

**Conjunto $S$:** $\{(w_2,m_2),(w_3,m_4),(w_1,m_3)\}$
**Pareja propuesta:** $(w_4,m_3)$
**Pareja formada:** Ninguna
**Pareja rechazada:** $(w_4,m_3)$

##### Iteración 6

**Conjunto $S$:** $\{(w_3,m_4),(w_1,m_3),(w_4,m_2)\}$
**Pareja propuesta:** $(w_4,m_2)$
**Pareja formada:** $(w_4,m_2)$
**Pareja rechazada:** $(w_2,m_2)$

##### Iteración 7

**Conjunto $S$:** $\{(w_1,m_3),(w_4,m_2),(w_2,m_4)\}$
**Pareja propuesta:** $(w_2,m_4)$
**Pareja formada:** $(w_2,m_4)$
**Pareja rechazada:** $(w_3,m_4)$

##### Iteración 8

**Conjunto $S$:** $\{(w_1,m_3),(w_4,m_2),(w_2,m_4),(w_3,m_1)\}$
**Pareja propuesta:** $(w_3,m_1)$
**Pareja formada:** $(w_3,m_1)$
**Pareja rechazada:** Ninguna

A este punto ya tenemos formado el emparejamiento estable que buscabamos.

#### Parte 3

- Note que el emparejamiento estable formado en las partes anteriores es el mismo (a menos del orden en que se listan las parejas).  
Muestre que, en esta instancia, para toda persona se verifica que:
    - su **mejor pareja válida** coincide con su **peor pareja válida**.

    ¿Qué resultados del libro está aplicando?

Para esta parte usamos ambos los resultados:

- **(1.7) Cada ejecución del algoritmo G-S da como resultado el conjunto $S^*=\{(m,best(m)):m\in M\}$.**
- **(1.8) En el emparejamiento estable $S^*$, cada mujer es emparejada con su peor pareja posible.**

Estos resultados hablan de hombres y mujeres, pero en realidad es el rol lo que importa para inferir el resultado.
El hombre (por lo menos en lo que estudiamos en el libro) es quién propone, por lo tanto lo que quieren decir los resultados es que:

- Quién propone siempre termina emparejado con su mejor pareja posible.
- A quién se le proponen, siempre termina emparejado con su peor pareja posible.

Bajo este concepto, la parte uno nos devuelve:

- $S^*=\{(m,best(m)):m\in M\}$, o alternativamente:
- $S^*=\{(w,worst(w)):w\in W\}$

Por otra parte, la parte dos nos devuelve:

- $S^*=\{(w,best(w)):w\in W\}$, o alternativamente:
- $S^*=\{(m,worst(m)):m\in M\}$

Entonces todos los conjuntos que vimos en los puntos, son iguales entre si, ya que ambas las partes uno y dos nos devuelven el mismo conjunto. 

Por lo tanto, tenemos que:

- $S^*=\{(m,best(m)):m\in M\}=\{(m,worst(m)):m\in M\}$,
- $S^*=\{(w,best(w)):w\in W\}=\{(w,worst(w)):w\in W\}$,

Es decir, para toda persona, se verifica que **su mejor pareja válida** coincide con su **peor pareja válida**. $\blacksquare$

#### Parte 4

- Concluya que para esta instancia del problema existe **una única solución**.

Recordemos que $best(m)$ y $worst(m)$ representan parejas válidas para $m$, lo cual significa que existe un emparejamiento estable $S$ que contiene a estos pares $(m,best(m))$ y $(m,worst(m))$.

Ahora, consideremos una persona cualquiera $p$ (hombre o mujer). Por la parte anterior, sabemos que para esta persona se cumple que $best(p)=worst(p)$, lo cual significa que para esta persona $p$ existe una única pareja válida (pues la peor y la mejor son la misma pareja).
Esto vale para cualquier persona $p$, ya que no hicimos suposiciones adicional sobre ésta, entonces todas las personas tienen una sola pareja válida posible, lo que implica que existe un solo emparejamiento estable para las personas y tabla de preferencias indicada. $\blacksquare$