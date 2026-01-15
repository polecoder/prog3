# Ejercicio 02 - Análisis de algoritmos

**Fecha:** 14-01-2026
**Estado:** 🟡 Con ayuda

## Consigna

En el libro de referencia para el curso se describe una implementación del algoritmo de Gale-Shapley cuyo tiempo de ejecución es $O(n^2)$.

1. Muestre, a través de un ejemplo, que este tiempo de ejecución es también $\Omega(n^2)$ en el peor caso.
2. El hecho que acaba de demostrar en la parte uno, depende de la implementación específica del algoritmo de Gale-Shapley? Justifique.

## Resolución

### Parte 1

- Muestre, a través de un ejemplo, que este tiempo de ejecución es también $\Omega(n^2)$ en el peor caso.

Recordemos el algoritmo de Gale-Shapley:

```
Initially all m ∈ M and w ∈ W are free
While there is a man m who is free and hasn’t proposed to
every woman
    Choose such a man m
    Let w be the highest-ranked woman in m’s preference list
        to whom m has not yet proposed
    If w is free then
        (m, w) become engaged
    Else w is currently engaged to m'
        If w prefers m' to m then
            m remains free
        Else w prefers m to m'
            (m, w) become engaged
            m' becomes free
        Endif
    Endif
Endwhile
Return the set S of engaged pairs
```

La intuición clave para este ejercicio, es entender que el tiempo de ejecución de algoritmos va a estar dado según la cantidad de propuestas que se hagan, si se hacen menos propuestas, entonces la cota inferior será más pequeña que $n^2$.
Por la consigna del ejercicio, nosotros queremos evaluar el peor caso, y éste es cuando se hacen la mayor cantidad de propuestas posibles.

Consideremos las siguientes tablas de preferencia para ambos hombres y mujeres:

- $m_i:w_1>w_2>\ldots>w_n$
- $w_i:m_n>m_{n-1}>\ldots>m_1$

Con esto, observemos que:

- En el primer paso, quedan $n$ hombres libres, todos los cuales se proponen a $w_1$, quedándose con $m_n$.
- En el segundo paso, quedan $n-1$ hombres libres, todos los cuales se proponen a $w_2$, y ella termina quedándose con $m_{n-1}$.
- Y así sucesivamente...

Con esto tenemos que el total de propuestas es:

- $n+(n-1)+\ldots+1=\frac{n(n+1)}{2}=\Omega(n^2)$

**Idea:** Entendamos que este es el máximo número de propuestas posibles, la razón de esto es que estamos "demorando" la mayor cantidad de iteraciones posibles para establecer una pareja "definitiva".

### Parte 2

- El hecho que acaba de demostrar en la parte uno, depende de la implementación específica del algoritmo de Gale-Shapley? Justifique.

Lo primero que tenemos que identificar es que lo principal que cambia entre diferentes implementaciones son las estructuras de datos que se utilizan.

Empecemos recordando (resultados del libro) que:

- $(*_1)$ **Cualquier ejecución del algoritmo de G-S, siempre devuelve el conjunto $S^*$, conformado por las parejas $(m,best(m))$.**

Y además:

- $(*_2)$ **Dado un hombre $m$, este propone en el orden establecido por su tabla de preferencias, hasta proponerle a $best(m)$ con quién se queda hasta finalizar el algoritmo.**

Juntando las dos afirmaciones $(*_1)$ y $(*_2)$, éstas nos dicen que el número de propuestas que se tienen que procesar es totalmente **INDEPENDIENTE** de la implementación particular del algoritmo.

Como lo que probamos en la parte anterior es una observación inherente a la cantidad de propuestas que se tienen que procesar, podemos concluir que lo que demostramos en la parte uno es **INDEPENDIENTE** de la implementación