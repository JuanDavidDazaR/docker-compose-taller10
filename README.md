# **Sistema de Gestión de Tienda en Microservicios**

Este proyecto implementa un sistema de gestión de tienda basado en una arquitectura de microservicios. Utiliza Docker y Docker Swarm para la orquestación, HAProxy para el balanceo de carga y PySpark para análisis de datos, con el objetivo de facilitar la administración de usuarios, productos y carritos de compra. Los resultados de los análisis se presentan en un dashboard para los administradores.


# Ambiente de trabajo

El ambiente de trabajo consta de las siguientes herramientas: Vagrant + VirtualBox + Ubuntu. Veremos cómo manejar cada una de ellas.

OJO: Para no tener problemas con este ambiente de trabajo se recomienda desactivar las actualizaciones automáticas de Windows.

#### Instalación de VirtualBox.

Descargar e instalar la última versión de VirtualBox. La descarga la puede hacer desde el siguiente enlace: https://www.virtualbox.org/wiki/Downloads. La instalación no requiere ninguna configuración especial así que se puede hacer con todos los valores por defecto.

#### Instalación de Vagrant

Descargar e instalar la última versión de Vagrant, la descarga la puede hacer desde el siguiente enlace: https://releases.hashicorp.com/vagrant/

En la consola de Windows se puede verificar la versión de Vagrant que se instaló:

 ```vagrant version```
 
Instalar el plugin vbguest para vagrant, con el fin de mantener las adiciones de los guest de VirtualBox actualizados. Estas adiciones (Guest Additions) son un paquete de software que forma parte de VirtualBox y añade funcionalidades a la instalación básica de VirtualBox que mejoran su rendimiento y consiguen un mejor nivel de integración entre la máquina huésped y la máquina anfitriona

```plugin install vagrant-vbguest```

#### Configuración y creación de las máquina virtuales

Muchos de los servicios que trabajaremos en este módulo requieren un servidor y un cliente, por tanto configuraremos 2 máquinas virtuales. El proceso de configuración es el siguiente: 

1. Cree un directorio y le da un nombre, en este ejemplo se llamará prueba.

 2. Ingrese al directorio y desde la consola de Windows ejecute el siguiente comando vagrant init con lo cual se crea un archivo de configuración llamado Vagrantfile

```vagrant init```

El archivo Vagrantfile contiene la información básica para la creación de las dos máquinas virtuales. El contenido de Vagrantfile debe ser el siguiente:

```
# -*- mode: ruby -*-

# vi: set ft=ruby :

  

Vagrant.configure("2") do |config|

  

if  Vagrant.has_plugin? "vagrant-vdguest"

config.vbguest.no_install =  true

config.vdguest.auto_update =  false

config.vdguest.no_remote =  true

  

end

config.vm.define :clienteUbuntu  do |clienteUbuntu|

clienteUbuntu.vm.box =  "bento/ubuntu-22.04"

clienteUbuntu.vm.network :private_network, ip:  "192.168.100.2"

clienteUbuntu.vm.hostname =  "clienteUbuntu"

end

  

config.vm.define :servidorUbuntu  do |servidorUbuntu|

servidorUbuntu.vm.box =  "bento/ubuntu-22.04"

servidorUbuntu.vm.network :private_network, ip:  "192.168.100.3"

servidorUbuntu.vm.hostname =  "servidorUbuntu"

servidorUbuntu.vm.provider "virtualbox"  do |v|

v.cpus =  3

v.memory =  2048

end

end

end
```
