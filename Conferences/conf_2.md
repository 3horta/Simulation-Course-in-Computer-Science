# Generación de Variables Aleatorias, Montecarlo

## Recap probabilidades

- **Variable Aleatoria (VA)**: Una variable aleatoria es una función que asigna un número real a cada resultado en el espacio muestral de un experimento aleatorio. Por ejemplo, si lanzamos un dado, la variable aleatoria $X$ podría ser el número que aparece en la cara superior del dado.

- **Función de probabilidad acumulada**: Esta función, denotada como $P(X \leq x)$, proporciona la probabilidad de que una variable aleatoria sea menor o igual a algún valor.
  
- **Función de densidad e histograma**: La función de densidad de probabilidad, denotada como $f(x)$, es utilizada para especificar la probabilidad de la variable aleatoria que cae dentro de un rango particular de valores, en lugar de tomar cualquier valor. El histograma es una representación gráfica de la distribución de un conjunto de datos. Por ejemplo, si tenemos una muestra de alturas de personas, podríamos usar un histograma para visualizar la distribución de las alturas.

## Números pseudo-aleatorios

 Los números pseudo-aleatorios son secuencias de números que parecen ser aleatorios, pero son generados por un proceso determinístico. Son esenciales en las simulaciones de Montecarlo porque permiten reproducir los resultados. Un ejemplo de generador de números pseudo-aleatorios es el generador lineal congruencial.

$$X_{n+1} = (aX_n + c) \mod m$$

Donde:

- $X_{n+1}$ es el próximo número en la secuencia.
- $X_n$ es el número actual en la secuencia.
- $a$, $c$ y $m$ son constantes que se eligen antes de comenzar a generar la secuencia.
- $a$ es el multiplicador.
- $c$ es el incremento.
- $m$ es el módulo.

El valor inicial $X_0$ (llamado semilla) también se elige antes de comenzar a generar la secuencia.

La elección de los valores de $a$, $c$, $m$ y $X_0$ puede afectar a las propiedades de la secuencia de números generada. En particular, para obtener una secuencia de números que parezca aleatoria y tenga un buen período (es decir, que tarde mucho en repetirse), estos valores deben elegirse cuidadosamente.

## Generación de variables aleatorias discretas

 **Finitas**: Para generar una variable aleatoria discreta con un número finito de resultados, podemos utilizar la transformada inversa. Por ejemplo, si queremos generar una variable aleatoria que toma los valores 1, 2, 3 con probabilidades 0.2, 0.3, 0.5 respectivamente, generamos un número pseudo-aleatorio $U$ y asignamos 1 si $U < 0.2$, 2 si $0.2 \leq U < 0.5$, y 3 si $U \geq 0.5$.

 **Infinitas**: Para generar una variable aleatoria discreta con un número infinito de resultados, podemos utilizar el método de la transformada inversa con una función de probabilidad acumulada que puede manejar un número infinito de resultados. Un ejemplo es la distribución geométrica.

  **Integrales con Número Pseudo Aleatorio (NPA)**: Podemos utilizar números pseudo-aleatorios para calcular integrales, que a su vez pueden ser utilizadas para generar variables aleatorias discretas. Por ejemplo, si queremos calcular la integral de una función $f(x)$ en el intervalo $[a, b]$, podemos generar $N$ números pseudo-aleatorios $U_i$ en el intervalo $[a, b]$, calcular $f(U_i)$ para cada $U_i$, y luego tomar el promedio. Este método se conoce como el método de Montecarlo para calcular integrales.

## Generación de variables aleatorias continuas

 **Algoritmo de la transformada inversa**: Este algoritmo se basa en la idea de que si $U$ es una variable aleatoria uniforme en el intervalo $[0, 1]$, entonces la variable aleatoria $X = F^{-1}(U)$ tiene una función de distribución acumulada $F$. Por ejemplo, si $F$ es la función de distribución acumulada de la distribución exponencial, entonces $F^{-1}(u) = -\ln(1-u)/\lambda$, y podemos generar una variable aleatoria exponencial generando un número pseudo-aleatorio $U$ y calculando $-\ln(1-U)/\lambda$.

 **Inversa generalizada**: La función inversa generalizada se utiliza cuando la función de distribución acumulada $F$ no es estrictamente creciente y, por lo tanto, no tiene una inversa única. En este caso, definimos $F^{-1}(u)$ como el ínfimo de los $x$ tales que $F(x) \geq u$.
  $$F^{-1}(u) = \inf\{x: F(x) \geq u\}$$
  demostracion: ROSS p69

 **Casos ad-hoc**: Algunas distribuciones tienen métodos específicos para generar variables aleatorias. Por ejemplo, para generar una variable aleatoria gamma, podemos utilizar la suma de exponenciales.

 **Aceptación y rechazo**: Este método se utiliza para generar variables aleatorias cuando la inversa de la función de distribución no se puede calcular fácilmente. Supongamos que queremos generar una variable aleatoria con una función de densidad de probabilidad (PDF) objetivo f(x). Sin embargo, no podemos generar directamente esta variable aleatoria porque la función de distribución acumulada (CDF) de f(x) no tiene una inversa fácilmente calculable.

  1. En lugar de eso, comenzamos con una variable aleatoria que podemos generar fácilmente, digamos con PDF g(x), y su CDF tiene una inversa fácilmente calculable. Esta distribución se llama distribución de propuesta
  2. Luego encontramos una constante c tal que c⋅g(x)≥f(x) para todos los x. En otras palabras, c⋅g(x) es una envolvente de f(x). Esto se hace generalmente dibujando las gráficas de f(x) y g(x) y eligiendo un c apropiado.
  3. Ahora generamos dos números aleatorios. El primero, X, se genera de la distribución de propuesta, y el segundo, U, se genera de una distribución uniforme en el intervalo [0, 1].
  4. Aceptamos X como nuestra variable aleatoria generada si U≤c⋅g(X)f(X)​. Si no, volvemos al paso 3.

Este método funciona porque la probabilidad de aceptar X es proporcional a f(x), por lo que las variables aleatorias aceptadas siguen la distribución objetivo.

 **Método de composición**: Este método se utiliza para generar variables aleatorias cuando la función de densidad puede ser expresada como una mezcla de otras funciones de densidad. El método consiste en generar una variable aleatoria para seleccionar la función de densidad y luego generar la variable aleatoria utilizando la función de densidad seleccionada.

## Monte Carlo

 El método de Montecarlo es un método numérico que utiliza números pseudo-aleatorios para simular fenómenos aleatorios y calcular cantidades que serían difíciles o imposibles de calcular de otra manera. Por ejemplo, el método de Montecarlo se puede utilizar para calcular integrales, resolver ecuaciones diferenciales estocásticas, simular sistemas físicos, etc.

Supongamos que queremos calcular una integral definida de una función $f(x)$ en el intervalo $[a, b]$. La integral de $f(x)$ de $a$ a $b$ se puede aproximar como el promedio de los valores de $f(x)$ en puntos aleatorios dentro del intervalo, multiplicado por el ancho del intervalo. En otras palabras, si generamos $N$ números pseudo-aleatorios $X_i$ en el intervalo $[a, b]$, entonces la integral se puede aproximar como:

$$\int_a^b f(x) dx \approx \frac{b - a}{N} \sum_{i=1}^{N} f(X_i)$$

Este método se basa en la ley de los grandes números, que dice que el promedio de una muestra de observaciones aleatorias converge al valor esperado a medida que el tamaño de la muestra aumenta.

El método de Montecarlo es una técnica poderosa que puede ser utilizada para calcular integrales, incluso cuando las variables aleatorias involucradas no siguen una distribución uniforme. Aquí te dejo una explicación detallada:

Supongamos que queremos calcular una integral definida de una función $f(x)$ en el intervalo $[a, b]$. La integral de $f(x)$ de $a$ a $b$ se puede aproximar como el promedio de los valores de $f(x)$ en puntos aleatorios dentro del intervalo, multiplicado por el ancho del intervalo. En otras palabras, si generamos $N$ números pseudo-aleatorios $X_i$ en el intervalo $[a, b]$, entonces la integral se puede aproximar como:

$$\int_a^b f(x) dx \approx \frac{b - a}{N} \sum_{i=1}^{N} f(X_i)$$

Este método se basa en la ley de los grandes números, que dice que el promedio de una muestra de observaciones aleatorias converge al valor esperado a medida que el tamaño de la muestra aumenta.

Ahora, si los $X_i$ no son uniformemente distribuidos, sino que siguen alguna otra distribución $g(x)$, podemos ajustar la fórmula de la siguiente manera:

$$\int_a^b f(x) dx \approx \frac{1}{N} \sum_{i=1}^{N} \frac{f(X_i)}{g(X_i)}$$

Aquí, los $X_i$ son generados de acuerdo con la distribución $g(x)$, y la función $f(x)$ se pondera por $1/g(X_i)$ para compensar el hecho de que los $X_i$ no están uniformemente distribuidos.

Este método se conoce como **Montecarlo con muestreo de importancia**. Es especialmente útil cuando la función $f(x)$ es difícil de integrar directamente, pero podemos generar fácilmente muestras de una distribución $g(x)$ que es similar a $f(x)$.

La convergencia del método de Montecarlo es una propiedad importante que garantiza que las estimaciones del método se acercan al valor real a medida que el número de muestras aumenta. El Teorema del Límite Central proporciona información sobre la velocidad de convergencia del método de Montecarlo. Según este teorema, el error absoluto de la estimación decrece como $1/\sqrt{N}$, donde $N$ es el número de muestras. Esto significa que para reducir a la mitad el error de la estimación, necesitamos cuadruplicar el número de muestras.

Es importante tener en cuenta que aunque la convergencia del método de Montecarlo está garantizada en teoría, en la práctica puede ser difícil determinar cuándo se ha alcanzado la convergencia. Esto se debe a que la velocidad de convergencia puede depender de la función específica que se está integrando y de la distribución de las variables aleatorias utilizadas

El método de Montecarlo también se puede utilizar para resolver problemas de optimización, ecuaciones diferenciales estocásticas, y simular sistemas físicos, entre otras aplicaciones. En todos estos casos, el método se basa en la generación de números pseudo-aleatorios y la estimación de cantidades a través de promedios o conteos.

## Tests de bondad de ajuste

 Es importante probar y validar los métodos de generación de variables aleatorias para asegurarse de que están funcionando correctamente. Esto puede implicar comparar las distribuciones de las variables aleatorias generadas con las distribuciones teóricas, realizar pruebas de bondad de ajuste, y utilizar otras técnicas de diagnóstico estadístico.

Un test de bondad de ajuste se utiliza para determinar si una muestra de datos sigue una distribución específica. Las hipótesis para esta prueba son:

- $H_0$: La variable sigue una distribución hipotética.
- $H_1$: La variable no sigue una distribución hipotética.

## Test de bondad de ajuste chi-cuadrado

El test de bondad de ajuste chi-cuadrado se utiliza para determinar si una variable categórica o discreta sigue o no una distribución hipotética.

El estadístico de prueba para una prueba de bondad de ajuste chi-cuadrado es:

$$X^2 = \sum \frac{(O - E)^2}{E}$$

Donde:

- $O$ son los valores observados.
- $E$ son los valores esperados.

Si el valor p que corresponde al estadístico de prueba $X^2$ con $n-1$ grados de libertad (donde $n$ es el número de categorías) es menor que el nivel de significancia elegido, entonces puedes rechazar la hipótesis nula.

## Test de bondad de ajuste Kolmogorov-Smirnov

El test de Kolmogorov-Smirnov es una prueba no paramétrica que se utiliza para determinar si una muestra de datos se ajusta a una distribución específica. El test compara la función de distribución acumulada empírica de la muestra con la función de distribución acumulada teórica.

El estadístico de contraste es:

$$D = \sup |F(x) - F_n(x)|$$

Donde:

- $F(x)$ es la función de distribución acumulada teórica.
- $F_n(x)$ es la función de distribución acumulada empírica.

Si los valores observados son similares a los esperados, el valor de $D$ será pequeño. Cuanto mayor sea la discrepancia entre la distribución empírica $F_n(x)$ y la distribución teórica $F(x)$, mayor será el valor de $D$.
