> @esteban --------------- 25 / 06 / 2017

# Descripción

El _graphics pipeline_ es el módulo encargado de procesar datos que contienen características deseadas a aplicar en un objeto que será representado como un conjunto de puntos. Este conjunto de características son aplicadas a cada punto que entra en el graphics pipeline, entregando como resultado un par ordenado _(x,y)_ que serán los puntos _(pixeles)_ que estarán dados en coordenadas cartesianas tomando como origen el centro de una pantalla.

El conjunto de transformaciones que se aplican a un objeto no son más que operaciones matemáticas que son representadas comúnmente de manera matricial, por lo cual concluimos que será necesario construir bloques sencillos y realizar el _graphics pipeline_ con base en estos.


# Especificaciones 

## Multiplicador

El bloque multiplicador recibe dos entradas de 16 bits que representan un número real mediante el uso del estándar IEEE-754. Dentro de este bloque son realizadas las operaciones necesarias para obtener una salida de 16 bits que representan la multiplicación de los valores de entrada. Además existe una señal de salida de un bit llamada "excepción" para alertar en caso de presentarse un _overflow_ o _underflow_ al realizar la multiplicación de los valores de entrada.

## Divisor

El bloque divisor recibe dos entradas de 16 bits que representan un número real mediante el uso del estándar IEEE-754. Dentro de este bloque son realizadas las operaciones necesarias para obtener una salida de 16 bits que representan la división de los valores de entrada. Además existe una señal de salida de un bit llamada "excepción" para alertar en caso de presentarse un _overflow_ o _underflow_ al realizar la división de los valores de entrada, o bien un intento de división entre cero.

## Sumador

El bloque sumador recibe dos entradas de 16 bits que representan un número real mediante el uso del estándar IEEE-754. Dentro de este bloque son realizadas las operaciones necesarias para obtener una salida de 16 bits que representan la suma de los valores de entrada.
