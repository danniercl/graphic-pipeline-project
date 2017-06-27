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

## Entradas al graphics pipeline

A continuación se presentan las entradas que recibe el bloque completo.

- **Posición X de la cámara en el mundo**
- **Posición Y de la cámara en el mundo**
- **Posición Z de la cámara en el mundo**
- **Distancia focal**
- **Coseno del ángulo de rotación en X**
- **Coseno del ángulo de rotación en Y**
- **Coseno del ángulo de rotación en Z**
- **Seno del ángulo de rotación en X**
- **Seno del ángulo de rotación en Y**
- **Seno del ángulo de rotación en Z**
- **Escalamiento en X**
- **Escalamiento en Y**
- **Escalamiento en Z**
- **Traslación en X**
- **Traslación en Y**
- **Traslación en Z**
- **Posición X del punto a procesar**
- **Posición Y del punto a procesar**
- **Posición Z del punto a procesar**

## Salidas del graphics pipeline

A continuación se presentan las salidas que entrega el bloque completo.

- **Posición en X (pixeles) desde el centro de la pantalla**
- **Posición en Y (pixeles) desde el centro de la pantalla**
- **Señal de excepción para alertar la presencia de algún caso especial no soportado**

