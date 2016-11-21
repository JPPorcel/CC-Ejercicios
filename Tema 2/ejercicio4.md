# Gestión de infraestructuras virtuales

## Ejercicio 4

### Provisionar una máquina virtual en algún entorno con los que trabajemos habitualmente usando Salt.

Vamos a provisionar una máquina virtual con el compilador g++ y las librerías de OpenGL para poder trabajar con C++ y OpenGL en la máquina objetivo usando Salt.

Para ello vamos a usar salt-ssh, antes debemos de segurarnos de instalar antes Python, ya que Salt está basado en Python y requiere este lenguaje para funcionar.

Instalamos salt-ssh en la máquina anfitriona desde la que vamos a provisionar:

	sudo apt install salt-ssh

Para ejecutar salt-ssh sin necesidad de ser superusuario tenemos que configurar varias cosas. Seguiremos los pasos descritos [aquí](https://github.com/JJ/BoBot/tree/master/provision) (by JJ) para ello.

Debemos de configurar el archivo roster de salt-ssh con la información de nuestra máquina virtual:

	app:
  		host: IP-MÁQUINA-VIRTUAL
  		user: usuario
  		sudo: True

Aquí se declara la dirección a la que vamos a conectar, el usuario de la máquina y si hace falta ser sudo o no. Con esto podemos probar nuestra conexión con:

	salt-ssh 'app' --priv ~/key_ec2_aws.pem --roster-file ~/lib/salt/roster -c ~/lib/salt --force-color  test.ping

Con la opción --priv le indicamos la ubicación de nuestra clave privada para conectar por ssh. Y obtenemos:

![Resultado de test.ping](https://github.com/JPPorcel/CC-Ejercicios/blob/master/Tema%202/images/ej_4.png?raw=true)


Nuestro fichero salt-stack (gOGL.sls) para provisionar con g++ y las librerías de OpenGL es:

	g++:
     pkg.installed

    freeglut3:
     pkg.installed
    freeglut3-dev:
     pkg.installed
    libglew1.5:
     pkg.installed
    libglew1.5-dev:
     pkg.installed
    libglu1-mesa:
     pkg.installed
    libglu1-mesa-dev:
     pkg.installed
    libgl1-mesa-glx:
     pkg.installed
    libgl1-mesa-dev:
     pkg.installed

Este fichero debe de estar en nuestra carpeta *~/lib/satl/states/*. La ruta al directorio de estados se especifica en nuestro fichero master con:

	file_roots:
  		base:
    		- ~/lib/salt/states

Y ejecutamos este estado con:

	salt-ssh app state.apply gOGL --priv ~/key_ec2_aws.pem --roster-file ~/lib/salt/roster -c ~/lib/salt --force-color

![Resultado del provisionamiento](https://github.com/JPPorcel/CC-Ejercicios/blob/master/Tema%202/images/ej_4_1.png?raw=true)