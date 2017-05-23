> @dannier
> ------------------------------------
> 22 / 03 / 2017

**Actividad:**
- Propuesta del Anteproyecto.

**Observaciones:**
- Título del proyecto: _"Creación de instructivo para el diseño y síntesis de GPU sobre GPU sobre FPGA e implementación de módulos de Graphics Pipeline en Verilog"_.

**Pendientes:**
- [x] Realizar el capítulo 1 para la aprobación de Diego Valverde.
> ------------------------------------


> @esteban
> ------------------------------------
> 08 / 04 / 2017

**Actividad:**
- Inicio y finalización del capítulo 1 del trabajo escrito: Introducción.

**Observaciones:**
- Se envía para aprobación del profesor tutor y lectores.

**Pendientes:**
- [x] Aprobación del capítulo 1.

> ------------------------------------

> @dannier
> ------------------------------------
> 11 / 04 / 2017

**Actividad:**
- Instalación y documentación de Papilio Loader.
- Descarga de ISE Desing Suite de Xilinx.
- Investigar acerca de comunicaciones PC-FPGA.

**Observaciones:**
- Papilio Loader es el programa utilizado para _flashear_ la plataforma Papilio Pro.
- Es necesario habilitar la instalación de paquetes para la arquitectura i386 ya que el Papilio Loader utiliza las librerías de libftdi-dev:i356.
- UART y RS232 parecen ser los protocolos más comunes para comunicación PC-FPGA.

**Pendientes:**
- [x] Instalar la licencia del ISE Design Suite.
- [ ] Implentar los protocolos de comunicación.
- [x] Crear el repositorio para la implementación de la GPU.
> ------------------------------------


> @dannier
> ------------------------------------
> 12 / 04 / 2017

**Actividad:**
- Instalación y documentación de ISE Design Suite WebPack.
- Instalación y documentación de los driver de los cable.

**Observaciones:**
- Las herramientas como el Papilio Loader, el FTDI y los _drivers_ de los cables han sido compilados para la arquitectura i386.

**Pendientes:**
- [x] Sintetizar algún ejemplo con el ISE Design Suite WebPack y _flashearlo_ con el Papilio Pro.

> ------------------------------------


> @dannier
> ------------------------------------
> 16 / 04 / 2017

**Actividad:**
- Instalación de la licencia para ISE Design Suite.
- Sintetización de un ejemplo en HDL _(Pong)_ utilizando el ISE Design Suite.
- _Flasheo_ del archivo sintetizado .bit sobre la Papilio Pro utilizando el Papilio Loader.
- Reunión en casa de Esteban para coordinar el uso de los datos en la SRAM de la Papilio Pro.

**Observaciones:**
- Las herramientas utilizadas funcionan correctamente: conexión con el VGA y utilización del MegaWing.

**Pendientes:**
- [ ] Escribir y leer desde la SRAM.

> ------------------------------------


> @esteban
> ------------------------------------
> 23 / 04 / 2017

**Actividad:**
- Se inicia la implementación de IEEE-754 en Verilog y las primeras pruebas.

**Observaciones:**
- Se descubrieron algunos problemas en cuanto al uso de este estándar y los números decimales en Verilog.
- Se plantea algoritmo que preliminarmente pareciera funcionar para operar números con decimales utilizando lenguaje de descripción de hardware.


> ------------------------------------


> @dannier
> ------------------------------------
> 26 / 04 / 2017

**Actividad:**
- Implementación de una librería para IEEE-754 _half-precision_ (16 bits).

**Observaciones:**
- Cuando se pasa de _uint16_t_ a _string_ utilizando la función de _memcpy()_, los bytes están intercambiados.

**Pendientes:**
- [x] Reparar los bytes intercambiados de cuando se pasa de _uint16_t_ a _string_.
- [x] Establecer las funciones del _driver_ para la CPU.
- [x] Proponer una forma para almacenar los datos en la memoria de la GPU.

> ------------------------------------


> @dannier
> ------------------------------------
> 28 / 04 / 2017

**Actividad:**
- Declaración de las funciones del _driver_ para la papiGPU.

**Observaciones:**
- No se sabe si la cámara también necesita matrices de transformación como la de los objetos.

**Pendientes:**
- [ ] Aplicar las revisiones de Diego Valverde sobre el capítulo 1.
- [ ] Realizar el capítulo 2 para la aprobación de Diego Valverde.
- [ ] Implementar las funciones de _driver_.

> ------------------------------------


> @dannier
> ------------------------------------
> 29 / 04 / 2017

**Actividad:**
- Creación del Makefile para el _driver_ de la GPU. En proceso.
- Implementación de la función `papiGPU_initialize()`.
- Creación del API test. En proceso.

**Observaciones:**
- Fue necesario incorporar una variable global en `i_cpu_driver.c` la cual es utilizada por las funciones de UART.
- Al parecer, el _driver_ realiza correctamente la comunicación con la FPGA.

**Pendientes:**
- [x] Probar si el input/output de UART se está realizando correctamente.

> ------------------------------------


> @dannier
> ------------------------------------
> 30 / 04 / 2017

**Actividad:**
- Implementación de la transmisión/recepción de datos con la FGPA utilizando el protocolo UART.
- Propuesta del manejo de la memoria de la papiGPU

**Observaciones:**
- Las funciones de UART recaudaron exitosamente los datos que envía el _demo_ de la Papilio Pro.

> ------------------------------------


> @esteban
> ------------------------------------
> 01 / 05 / 2017

**Actividad:**
- Se inicia del capítulo de marco teórico y antecedentes del trabajo escrito.

**Observaciones:**
- Se cae en la duda si para el caso de la cámara es posible que tenga sus tres ejes de libertad siempre, o es posible definirlos desde un inicio.

**Pendientes:**
- [ ] Hacer en Inkscape las imágenes necesarias para las demostraciones de las rotaciones.
> ------------------------------------


> @esteban
> ------------------------------------
> 02 / 05 / 2017

**Actividad:**
- Se agrega la sección de manejo de punto flotante a nivel de hardware en el marco teórico del proyecto.

**Observaciones:**
- Se utiliza un bias de 15 de acuerdo al estándar IEEE-754.
> ------------------------------------


> @esteban
> ------------------------------------
> 07 / 05 / 2017

**Actividad:**
- Se finaliza la primer versión el marco teórico del proyecto.

**Pendientes:**
- [ ] Hacer, usando inskcape, las imágenes utilizadas. Por ahora hay capturas de pantalla.


> ------------------------------------
> @dannier
> ------------------------------------
> 07 / 05 / 2017

**Actividad:**
- Función _papiGPU_initialize()_ completa.
- Comienzo de los bloques del manejador de memoria en Verilog.

**Observaciones:**
- La implementación de los controladores de UART y de SRAM es bastante complicada, por el momento se decide utilizar alguno hecho por alguien más.

**Pendientes:**
- [ ] Implementar el bloque de memoria para probar el UART y la función del _driver_.

> ------------------------------------


> ------------------------------------
> @dannier
> ------------------------------------
> 14 / 05 / 2017

**Actividad:**
- Inicio de la implementación del Controlador de Memoria.

**Observaciones:**
- El modulo de UART solamente se puede pasar _frames_ de 1 byte a la vez.

**Pendientes:**
- [x] Estudiar y probar los módulos de SRAM y UART tomados de otros repositorios.
> ------------------------------------


> ------------------------------------
> @dannier
> ------------------------------------
> 18 / 05 / 2017

**Actividad:**
- Modificar el módulo de UART para indicar con un _flag_ cuando la escritura por _Tx_ fue finalizada. Esta bandera es necesaria para la implementación de _hardware_ capaz de enviar bloques de datos de 16-bits a través de UART.

**Observaciones:**
- Al parecer el bloque de _Refresh_ en el Controlador de Memoria conlleva una implementación más complicada que los demás estados.

**Pendientes**
- [ ] Implentar el bloque de _Refresh_ para el Controlador de Memoria.

> ------------------------------------


> ------------------------------------
> @dannier
> ------------------------------------
> 21 / 05 / 2017

**Actividad:**
- Realización de la especificación para el Administrador de Memoria.

**Observaciones:**
- Las indicaciones de la especificación deben ser clara tanto para la implementación en _hardware_ como para el ambiente de verificación.

**Pendientes:**
- [ ] Terminar completamente la especificación.


> ------------------------------------
> @nombre
> ------------------------------------
> DD / MM / AAAA

**Actividad:**
- abc

**Observaciones:**
- def

**Pendientes:**
- [ ] hij

> ------------------------------------
