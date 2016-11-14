# Gestión de infraestructuras virtuales

## Ejercicio 1

### Instalar chef en la máquina virtual que vayamos a usar.

Para este ejercicio y los siguientes dentro de este tema se usará una máquina virtual en AWS EC2. La imagen provista para la máquina virtual es ***ubuntu-xenial-16.04-amd64-server-20161020 (ami-a9d276c9)***.

Lo primero es instalar Ruby y Ruby Gems, el gestor de librerías:

	sudo apt-get install ruby1.9.1 ruby1.9.1-dev rubygems

Y posteriormente instalar Chef con gem:

	sudo gem install ohai chef

![Resultado de instalar Chef](https://github.com/JPPorcel/CC-Ejercicios/blob/master/Tema%202/images/ej1.png?raw=true)