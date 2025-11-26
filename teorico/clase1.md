# Clase 01 - Objetivos del curso, Emparejamiento Estable y Gale Shapley

**Fecha:** 2025-11-25
**Estado:** 🟢 Estudiado

## Resumen en 3 líneas

El curso se enfoca en el **conocimiento, análisis, diseño, corrección y complejidad de algorítmos**.
Se busca solucionar el problema de emparejar dos conjuntos con preferencias entre si, con la analogía de hombres y mujeres mediante la reconstrucción paso a paso del algoritmo de Gale-Shapley.

## Preguntas Clave

1. Por qué son tan importantes la corrección y complejidad de algoritmos?
2. Qué es un emparejamiento? Qué es un emparejamiento perfecto? Y uno estable?
3. En la ideación del algoritmo de Gale-Shapley, que rol cumplen los compromisos entre hombres y mujeres?

## Contenido

### Objetivos del curso

1. Conocer **algoritmos clásicos** que constituyen una base para la resolución de problemas en computación, y aplicarlos para la resolución de problemas más concretos.
2. Dominar técnicas generales de **diseño de algorítmos** y aplicarlas.
3. Razonar con rigurosidad sobre cualidades como la **corrección y complejidad de algorítmos**.
4. Analizar rigurosamente **problemas algorítmicos** para identificar limitaciones de cómputo inherentes a cada problema, reconociendo diferentes clases de complejidad.

#### Escribir una demostración

- Anunciar el plan para la demostración, es decir que metodología o estrategia planeamos usar para demostrar la tesis.
- Mantener un flujo ordenado de pensamiento, no un rejunte de ideas desordenadas (para esto conviene trabajar con borradores).
- Escribir frases completas, no cadenas de ecuaciones libradas a interpretación por si solas. Para esto es importante no abusar de símbolos matemáticos, ya que sin ellos en general suelen ser más claras las explicaciones, y no por ello menos rigurosas. Otra nota importante sobre este punto, es que debemos definir toda la notación que se usa, como por ejemplo el significado de las variables: "Sea $n$ la cantidad de ...".
- Cuando nos referimos a un algoritmo, es conveniente numerar o etiquetar los pasos a los que nos vamos a referir en la demostración. Por ejemplo: "Si la condición del ciclo en el paso $X$ no se verifica, entonces debemos tener $n\leq m$ y por lo tanto...".
- Dividir demostraciones complejas en resultados auxiliares.
- Terminar diciendo claramente como se concluye la tesis a partir de lo que se ha desarrollado.

### Emparejamiento estable

El problema de Emparejamiento Estable, tiene sus orígenes, en parte, en 1962, cuando David Gale y Lloyd Shapley, dos matemáticos economistas estadounidenses, se hicieron la siguiente pregunta: "¿Puede uno diseñar un proceso de admisión para un colegio, o un proceso de reclutamiento para un emplejo, que sea autoevaluable?".

De otra forma, dado un conjunto de preferencias sobre empleados y postulantes, nos preguntamos si es posible asignar postulantes a empleadores de forma que cada empleador $E$, y cada postulante $P$, que no esté programado para trabajar para $E$, de alguna de las siguientes formas:

- $E$ prefiere a uno de sus postulantes aceptados antes que a $P$
- $P$ prefiere su situación actual antes que trabajar para $E$

Si esto se cumple, la salida es estable, es decir, los intereses personales prevendrán cualquier trato entre empresas detrás de escenas.

Si bien este es el origen del planteamiento de Gale y Shapley, notaron que es un caso particular de otro problema más general.

Este problema más general, es visto como el problema de idear un sistema para el cual cada uno de $n$ hombres y $n$ mujeres puedan terminar contrayendo matrimonio.
Consideraremos un conjunto $M=\{m_1,m_2,\ldots,m_n\}$ de $n$ hombres y otro conjunto $W=\{w_1,w_2,\ldots,w_n\}$ de $n$ mujeres. Denotamos $M\times W$ al conjunto de todos los posibles pares ordenados de la forma $(m,w)$, donde $m\in M$ y $w\in W$.

- Un emparejamiento $S$ es un conjunto ordenado de pares, cada uno perteneciente a $M\times W$, con la propiedad de que cada miembro $M$ y cada miembro de $W$ aparece como mucho en un par de $S$.
- Un emparejamiento perfecto $S'$ es un emparejamiento con la propiedad de que cada miembro de $M$ y $W$ aparece en **EXACTAMENTE** un par de $S'$.

Estos conceptos aparecerán a menudo en otros problemas que vamos a trabajar en el curso.
En el contexto actual, un emparejamiento perfecto corresponde a una manera de emparejar hombres y mujeres, de modo que todos terminen casados con alguien, y que nadie esté casado con más de una persona.

Llegados a este punto, podemos introducir la noción de preferencia a este problema.
Cada hombre clasifica a todas las mujeres de $W$ en orden de preferencia; diremos que $m$ prefiere a $w$ antes que a $w'$, si $m$ clasificó más alto a $w$ que a $w'$. De forma análoga, cada mujer clasifica a todos los hombres de $M$.

Si se da un emparejamiento perfecto, que podría salir mal?
Guiados por el problema que se plantearon Gale y Shapley inicialmente, que pasa si tenemos dos pares $(m,w),(m',w')\in S$ tales que:

- $m$ prefiere a $w'$ antes que a $w$
- $w'$ prefiere a $m$ antes que a $m'$

En este caso, nadie impide que $m$ y $w'$ abandonen a sus parejas y se junten, por tanto, el conjunto $S$ de emparejamientos no es autoevaluable. Diremos que el par $(m,w')$ es inestable respecto a $S:(m,w')$ no pertenece a $S$, pero tanto $m$ como $w'$ prefieren al otro como su compañero en $S$.

Es así, como nuestro objetivo es un conjunto de matrimonio que no tenga inestabilidades. Diremos que un emparejamiento $S$ es estable si: es perfecto y no hay inestabilidad con respecto a $S$. Así surgen dos preguntas:

- Existe algún emparejamiento para cada conjunto de listas de preferencia?
- Dado un conjunto de listas de preferencias, podemos construir eficientemente un emparejamiento estable, si es que es posible hacerlo?

#### Diseño del algoritmo

Veamos que existe un emparejamiento estable para cada conjunto de listas de preferencias entre hombres y mujeres. Además, daremos un algoritmo eficiente que tome las listas de preferencias y construya un emparejamiento estable.
Consideremos algunas ideas básicas que motivan el algoritmo:

- Cuando se inicia, todos están solteros. Supongamos que un hombre soltero $m$ elige a la mujer $w$, quién está en lo más alto de su lista de preferencias y se le propone. Con esto, no necesariamente podemos concluir que $(m,w)$ será uno de los pares de nuestro emparejamiento final, pues puede pasar que en el futuro un hombre $m'$ al cual $w$ prefiere se le proponga. Por otro lado, puede ser peligroso para $w$ rechazar a $m$, ya que tal vez nunca reciba una propuesta de alguien que esté más arriba de $m$ en la lista de sus preferencias. Entonces una idea natural, sería que el par $(m,w)$ entre en un estado intermedio de **compromiso**.

    ![Figura 1](../img/clase1fig1.png)

- Supongamos que ahora estamos en un estado en el cual tenemos algunos hombres y mujeres están solteros/as y algunos de ellos están **comprometidos**. El siguiente paso, podría ser el descrito a continuación. Un hombre soltero $m$ (cualquiera) elige a la mujer que más prefiere, a la cual todavía no se le ha propuesto, y se le propone, llamemos $w$ a esta mujer. Si la mujer $w$ también está soltera, entonces se **comprometen** . Si la mujer no está soltera, entonces está comprometida con otro hombre $m'$. Entonces en este caso, ella determina a quién de los dos hombres $m$ y $m'$ prefiere según su lista de preferencias; el elegido, se compromete con ella, y el otro se vuelve soltero.
- Finalmente, el algoritmo termina cuando no hay nadie que esté soltero, aquí todos los emparejamientos se declaran como definitivos y se devuelve el resultado como un emparejamiento perfecto.

A continuación podemos ver una descripción concreta del algoritmo Gale-Shapley:

```
Initially all m ∈ M and w ∈ W are free
While there is a man m who is free and hasn’t proposed to
every woman
    Choose such a man m
    Let w be the highest-ranked woman in m’s preference list
        to whom m has not yet proposed
    If w is free then
        (m, w) become engaged
    Else w is currently engaged to m
        If w prefers m to m then
            m remains free
        Else w prefers m to m
            (m, w) become engaged
            m becomes free
        Endif
    Endif
Endwhile
Return the set S of engaged pairs
```


Algo interesante del algoritmo es que, por más fácil de entender o escribir que sea el algorítmo, no es inmediatamente obvio que devuelve un emparejamiento estable. De hecho ni siquiera es fácil de ver que retorna un emparejamiento perfecto. Probaremos esto en la clase siguiente.
