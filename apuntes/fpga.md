> @dannier --------------- 12 / 04 / 2017

# FPGA: Papilio Pro LX9

La plataforma a utilzar para el diseño de la FPGA es la Papilio Pro LX9 de Gadget Factory la cual posee una FPGA Spartan 6 de Xilinx, además del _shell_ LogicStart Megawing V1.2 para proporcionar el puerto de VGA. La Papilio Pro utiliza el ISE Design Suite para sintetizar el código escrito en Verilog y generar un archivo en formato .bit, el cual luego es _flasheado_ a la plataforma utilizando el programa Papilio Loader.

## Instalación de Papilio Loader en Linux (distribuciones de Debian)

Es necesario que el paquete `git` se encuentre instalado, así que en caso de que no sea así, ingrese el siguiente comando en la terminal:

	$ sudo apt-get install git

Instale las dependencias de Papilio Loader, este programa utiliza la biblioteca de FTDI para la detección y comunicación con la Papilio Pro, además de utilizar el JDK de Java para el GUI (Graphic User Interface).

Los ejecutables de Papilio Loader fueron compilados para la arquitectura i386, así que es posible que sea necesario habilitar la instalación de paquetes para i386 en caso de que su computadora tenga una arquitectua amd64, para esto ejecute los siguientes comandos en la terminal:

	$ sudo dpkg --add-architecture i386

	$ sudo apt-get update

Ingrese el siguiente comando en la terminal para instalar las dependencias de Papilio Loader:

	$ sudo apt-get install libftdi-dev:i386 default-jdk

Clone el repositorio de Papilio Loader en el Github de Gadget Factory:

	$ git clone git@github.com:GadgetFactory/Papilio-Loader.git

Ingrese a la carpeta de Papilio Loader y corra el instalador usando los siguientes comandos:

	$ cd Papilio-Loader

	$ chmod +x linux-installer.sh

	$ ./linux-installer.sh

Abra el programa Papilio Loader con el siguiente comando:

	$ papilio-loader-gui

## Instalación de ISE Design Suite WebPack de Xilinx

El ISE es un programa utilizado para sintetizar el HDL, en este caso Verilog, para ser _flasheado_ sobre la FPGA Spartan 6 en el Papilio Pro.

Descargue el ISE Design Suite para Linux directamente de la página oficial de Xilinx, en el siguiente enlace:
[https://www.xilinx.com](https://www.xilinx.com/member/forms/download/xef.html?filename=Xilinx_ISE_DS_Lin_14.7_1015_1.tar&akdm=1)

Acceda al directorio en donde se encuentra la descarga y descomprímala:

	$ cd hacia/el/directorio/de/descarga/

	$ tar -zxvf Xilinx_ISE_DS_Lin_14.7_1015_1.tar

Acceda al directorio del ISE Design Suite, corra el instalador con los siguientes comandos:

	$ cd Xilinx_ISE_DS_Lin_14.7_1015_1

	$ chmod +x xsetup

	$ ./xsetup

Configure el ISE Design Suite con los siguientes comandos, según la arquitectura de la computadora:

- i386:

		$ source /opt/Xilinx/14.7/ISE_DS/settings32.sh

- amd64:

		$ source /opt/Xilinx/14.7/ISE_DS/settings64.sh

Durante la instalación, selecciones las opciones de `WebPack` e `Install Cable Drivers`. Los _drivers_ de los cables deben instalarse manualmente. Primero, instale las dependencias de los _drivers_:

	$ sudo apt-get install libusb-dev fxload gcc-4.7-multilib

Descargue los _drivers_ de los cables usando el siguiente enlace:
[http://git.zerfleddert.de](http://git.zerfleddert.de/cgi-bin/gitweb.cgi/usb-driver?a=snapshot;h=HEAD;sf=tgz)

Acceda al directorio en donde se encuentra la descarga y descomprímala:

	$ cd hacia/el/directorio/de/descarga/

	$ tar -zxvf usb-driver-HEAD-2d19c7c.tar.gz

Acceda al directorio de los _drivers_ y compílelos para la arquitectura i386 usando los siguientes comandos:

	$ cd usb-driver-HEAD-2d19c7c/

- i386:

		$ make

- amd64:

		$ make lib32

Asigne los _drivers_ a la biblioteca de USB utilizando los siguientes comandos:

	$ sudo mkdir /usr/local/libusb-driver

	$ sudo cp libusb-driver.so /usr/local/libusb-driver/

	$ export LD_PRELOAD=/usr/local/libusb-driver/libusb-driver.so

	$ export XIL_IMPACT_USE_LIBUSB=1

	$ ./setup_pcusb /opt/Xilinx/14.7/ISE_DS/ISE/

	$ sudo /etc/init.d/udev restart


> @name --------------- DD / MM / AAAA
