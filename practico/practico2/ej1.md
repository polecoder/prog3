# Ejercicio 01 - Análisis de algoritmos

**Fecha:** 14-01-2026
**Estado:** 🟡 Con ayuda

## Consigna

Sean $f$ y $g$ dos funciones positivas tales que $f(n)$ es $O(g(n))$. Para cada una de las siguientes afirmaciones, indique si es verdadera, demostrándolo, o falso dando un contraejemplo.

1. $f(n)^2$ es $O(g(n)^2)$
2. $2^{f(n)}$ es $O(2^{g(n)})$

## Resolución

Empecemos por lo importante, expresemos que significa que $f(n)$ es $O(g(n))$:

- Existen $c$ y $n_0$ tales que $\forall n\geq n_0: f(n)\leq c\cdot g(n)$

## Afirmación #1

- $f(n)^2$ es $O(g(n)^2)$

Fácilmente se observa que esto se puede obtener desde la primera desigualdad, ya que operando tenemos que para todo $n\geq n_0$:

$$
\begin{aligned}
&f(n)\leq c\cdot g(n)\\
&\iff\scriptstyle{(\text{operatoria})}\\
&f(n)^2\leq c^2\cdot g(n)^2\\
\end{aligned}
$$

Esta es la definición de $O(-)$ para $c'=c^2$ y $n_0$, por lo que la afirmación es **VERDADERA**.

## Afirmación #2

- $2^{f(n)}$ es $O(2^{g(n)})$

A diferencia del caso anterior, al operar con la definición que planteamos en un principio no llegamos a nada. Sospechando que entonces la afirmación es falsa, busquemos algún contraejemplo.

Consideremos $f(n)=2n$ y $g(n)=n$, obviamente $f$ es $O(g(n))=O(n)$. 
Con esto entonces queremos probar que $2^{2n}$ es $O(2^n)$, es decir que:

- Existen $c$ y $n_0$ tales que $\forall n\geq n_0:2^{2n}\leq c\cdot 2^n$

Veamos que pasa operando en la desigualdad:

$$
\begin{aligned}
&2^{2n}\leq c\cdot 2^n\\
&\scriptstyle{(\text{operatoria})}\\
&(2^n)^2\leq c\cdot 2^n\\
&\scriptstyle{(\text{operatoria})}\\
&2^n\leq c\\
\end{aligned}
$$

Pero esto no puede pasar, ya que $2^n$ es una función creciente con $n$ y $c$ es una constante. Por lo tanto no existen $c$ y $n_0$ que cumplan con la desigualdad, es decir que:

- Para $f(n)=2n$ y $g(n)=n$ no se cumple que $2^{f(n)}$ es $O(2^{g(n)})$.

Concluimos entonces que la afirmación es **FALSA**.