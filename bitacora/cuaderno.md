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


> @dannier
> ------------------------------------
> 26 / 04 / 2017

**Actividad:**
- Implementación de una librería para IEEE-754 _half-precision_ (16 bits).

**Observaciones:**
- Cuando se pasa de _uint16_t_ a _string_ utilizando la función de _memcpy()_, los bytes están intercambiados.

**Pendientes:**
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
