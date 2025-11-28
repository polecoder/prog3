## Ejercicio 01 - Emparejamiento Estable

**Fecha:** 28-11-2025
**Estado:** 🟢 Resuelto solo

### Consigna

1.  **Kleinberg & Tardos, Ex. 1.2:**
Indique si la siguiente afirmación es verdadera o falsa. Si es verdadera, dé una breve explicación. Si es falsa, dé un contraejemplo.
Consideramos una instancia del problema de emparejamiento estable en la que existe un par $(m,w)$ tal que $m$ está primero en la lista de
preferencias de $w$ y $w$ está primero en la lista de preferencias de $m$.
Entonces, el par $(m,w)$ pertenece a toda solución $S$ para esta instancia
del problema.
2. Dé un instancia (mínima) del problema de emparejamiento estable para la cual hay más de un emparejamiento estable. Justifique cómo se
obtiene.

### Resolución

#### Parte 1

Probaremos que dicha afirmación es verdadera por absurdo, es decir asumiremos que existe una solución $S'$ tal que el par $(m,w)$ descrito no pertenece a ella.
Observemos que necesariamente $m$ se le propone a $w$ pues $w$ es la primera en la lista de preferencias de $m$, por lo tanto en algún momento de la ejecución del algoritmo de G-S el par $(m,w)$ existe en la lista de pares comprometidos.
Como el par $(m,w)$ no pertenece a la solución $S'$, en algún momento de la ejecución $w$ tuvo que haber rechazado a $m$ por un hombre $m'$ tal que $w$ prefiere a $m'$ antes que a $m$.

Pero esto último es absurdo, ya que no existe $m'$ tal que $w$ lo prefiere antes que a $m$, pues $m$ es el primero de la lista de preferencias de $w$ por hipótesis.
Concluimos entonces que $(m,w)$ tiene que pertencer a $S'$. $\blacksquare$

Por lo tanto la afirmación es **VERDADERA**.

#### Parte 2

Consideremos $M=\{m_1,m_2\}$ y $W=\{w_1,w_2\}$ y la siguiente tabla de preferencias:

|     |     |     |
| --- | --- | --- |
|$m_1$|$w_1$|$w_2$|
|$m_2$|$w_2$|$w_1$|

|     |     |     |
| --- | --- | --- |
|$w_1$|$m_2$|$m_1$|
|$w_2$|$m_1$|$m_2$|

Notemos que en este caso tenemos dos emparejamientos estables posibles:

- $(m_1,w_1), (m_2,w_2)$
- $(m_2,w_1), (m_1,w_2)$

Esto se obtiene haciendo que para cualquier hombre o mujer llamemosle $p$, se cumpla que $best(p)\neq worst(p)$. 
De este modo, como tenemos dos parejas válidas posibles para $p$, tendremos dos emparejamientos estables distintos, caraterizados por:

- Uno de ellos contiene al par $(p,best(p))$
- El otro contiene al par $(p,worst(p))$