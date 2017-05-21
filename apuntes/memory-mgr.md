> @dannier --------------- 21 / 05 / 2017

# Descripción

El _memory manager_ o administrador de memoria es un módulo de la _GPU_ encargado de realizar la comunicación con la _CPU_, a través de la cual recibe los datos y la configuración para la _GPU_ para luego ser guardados en la memoria compartida. Para este proyecto, ésta memoria se refiere a la SRAM **MT48LC16M4A2-7E** embebida a la _Papilio Pro_.

Una vez terminado el almacemiento en la SRAM y recibida la indicación por parte de la _CPU_, cada uno de los datos se pone a disposición del _Graphics Pipeline_.

# Especificaciones

## Comunicación CPU-GPU

La comunicación entre ambas plataformas se hace a través del protocolo UART, el cual es compatible con la _Papilio Pro_. La velocidad de datos o el _baud rate_ es de **921600 bit/s**. Esta comunicación es bidireccional, ya que la GPU es capaz de reportar su estado y enviar confirmaciones hacia la CPU.

Es importante considerar para la implementación que los _bursts_ o ráfagas de datos del protocolo UART se dividen en bloques de 1 byte, pero la GPU trabaja con bloques de **16 bits**, es decir, tanto las direcciones de memoria, etiquetas y datos (parámetros de la cámara, rotaciones, escalamientos, translaciones, vértices, etc.) son de 16 bits.

## Funciones de la GPU

A través de la CPU se pueden realizar solicitudes a la GPU, y con las cuales configurar sus principales funciones. Para la programación de los APIs del _driver_ es importante dominar el conocimiento sobre el funcionamiento de la GPU, ya que facilita la exposición de estas funciones en alto nivel:

- **Inicializar la GPU:**
- **Configurar la cámara:**
- **Abrir y configurar un objeto:**
- **Agregar los vértices de un objeto:**
- **Cerrar un objeto:**
- **Modificar la configuración de un objeto:**
- **Refrescar la proyección:**
- **Eliminar uno o varios vértices:** (No implementado para esta versión).
- **Eliminar un objeto:** (No implementado para esta versión).
- **Modificar el color de un objeto:** (No implementado para esta versión).
- **Desinicializar la GPU:** (No implementado para esta versión).

Como se indicó anteriormente, para acceder a cada una de las funciones es necesario hacer la solicitud a través de CPU, esto conlleva el uso de _tags_ o etiquetas, además de utilizar el formato adecuado para enviar los datos necesarios hacia el administrador de memoria. Sobre ésto, se hablará más adelante.

## Tags o Etiquetas

Las etiquetas son constantes de 16 bits elegidas de manera arbitraria que sirven para relacionar cada una de las funciones de la GPU con un número. Esto ayuda al administrador de memoria a comprobar que las solicitudes de la CPU, el almacenamiento en memoria y la exposición de datos hacia el _Graphics Pipeline_ se estén realizando adecuadamente. En seguida se muestra la tabla con los _tags_ que pertenecen a la GPU.

| Tags | Nombre | Descripción |
| ---- | :----: | ----------: |
| **`0xAAAA`** | Inicializar GPU |  |
| **`0xCCCC`** | Habilitar GPU |  |
| **`0xBBBB`** | Configurar Cámara |  |
| **`0xEEEE`** | Crear y Configurar Objeto |  |
| **`0x9999`** | Agregar Vértices |  |
| **`0x8888`** | Cerrar Objeto |  |
| **`0xABCD`** | Modificar la Configuración del Objeto |  |
| **`0x1234`** | Refrescar la proyección |  |
| **`0x1414`** | Reporte de Error |  |
| **`0x4141`** | Reporte de Ocupado |  |

## Formato de almacenamiento

La SRAM MT48LC16M4A2-7E posee direcciones de 13 bits y entradas de 16 bits. A continuación, se explica el formato de como la información de la GPU es guardada en la memoria compartida durante el proceso de configuración, lo que quiere decir que la memoria debe de verse que tal forma antes del proceso de **refrescamiento de la proyección**, que es cuando todos los datos son pasados hacia el _Graphics Pipeline_.

1. Bloque inicial:

| ADDR | `0x0000` | `0x0001` | ... |
| :----: | :----: | :----: | :----: |
| **DATA** | `0xCCCC` / `~0xCCCC` | `0x(Número de Objetos)` | ... |

La GPU espera el valor de `0xCCCC` o su complemento para saber si la GPU se encuentra habilitada o deshabilitada, respectivamente. En caso de encontrar otro valor, se retorna un error hacia la CPU.

2. Bloque de la camara:

| ADDR | `0x0002` | `0x0003` | `0x0004` | `0x0005` | `0x0006` | ... |
| :----: | :----: | :----: | :----: | :----:| :----: | :----: |
| **DATA** | `0xBBBB` | `0x(Vx)` | `0x(Vy)` | `0x(Vz)` | `0x(Dc)` | ... |

En caso de no encontrar el valor de `0xBBBB` la GPU retorna un error hacia la CPU.

3. Bloque de objetos:

La configuración de cada objeto en la memoria se muestra a continuación. La GPU espera el _tag_ `0xEEEE` o su complemento para indicar si el objeto se encuentra habilitado o no. Al final de los vértices del último objeto se coloca el _tag_ `0xFFFF` para hacer esta indicación. En caso de hallar otro valor, la GPU retorna un error hacia la CPU.

| ADDR | `0x0007` | `0x0008` | ... |
| :----: | :----: | :----: | :----: |
| **DATA** | `0xEEEE` / `~0xEEEE`<sub>1</sub> | `0x(Dirección al Siguiente Objeto)` | ... |

| ADDR | `0x0009` | `0x000A` | `0x000B` | `0x000C` | 0x000D | 0x000E | ... |
| :----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: |
| **DATA** | `0x(Cos(yaw))`<sub>1</sub> | `0x(Cos(pitch))`<sub>1</sub> | `0x(Cos(roll))`<sub>1</sub> | `0x(Sen(yaw))`<sub>1</sub> | `0x(Sen(pitch))`<sub>1</sub> | `0x(Sen(roll))`<sub>1</sub> | ... |

| ADDR | `0x000F` | `0x0010` | `0x0012` | `0x0013` | `0x0014` | `0x0015` | ... |
| :----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: |
| **DATA** | `0x(ScaleX)`<sub>1</sub> | `0x(ScaleY)`<sub>1</sub> | `0x(ScaleZ)`<sub>1</sub> | `0x(TranslX)`<sub>1</sub> | `0x(TranslY)`<sub>1</sub> | `0x(TranslZ)`<sub>1</sub> | ... |

| ADDR | `0x0015` | `0x0016` | `0x0017` | `0x0018` | ... |`0x0016` + `3n` | `0x0017` + `3n` | `0x0018` + `3n` | `0x0019` + `3n` | ... |
| :----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: |
| **DATA** | `0x9999`<sub>1</sub> | `0x(X)`<sub>11</sub> | `0x(Y)`<sub>11</sub> | `0x(Z)`<sub>11</sub> | ... | `0x(X)`<sub>1n</sub> | `0x(Y)`<sub>1n</sub> | `0x(Z)`<sub>1n</sub> | `0xEEEE` / `~0xEEEE`<sub>2</sub> | ... |

La GPU espera el _tag_ `0x9999` indicando el inicio de los vértices del objeto. La GPU retorna un valor de error en caso de que el valor sea diferente. Como se indicó anteriormente, al final del último objeto se coloca el _tag_ `0xFFFF`:

| ADDR | `0x0015` | `0x0016` | `0x0017` | `0x0018` | ... |`0x0016` + `3n` | `0x0017` + `3n` | `0x0018` + `3n` | `0x0019` + `3n` | ... |
| :----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: |
| **DATA** | `0x9999`<sub>m</sub> | `0x(X)`<sub>m1</sub> | `0x(Y)`<sub>m1</sub> | `0x(Z)`<sub>m1</sub> | ... | `0x(X)`<sub>mk</sub> | `0x(Y)`<sub>mk</sub> | `0x(Z)`<sub>mk</sub> | `0xFFFF` | ... |

> @name --------------- DD / MM / AAAA
