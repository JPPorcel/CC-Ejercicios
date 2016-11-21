# Gestión de infraestructuras virtuales

## Ejercicio 5

### Desplegar los fuentes de una aplicación cualquiera, propia o libre, que se encuentre en un servidor git público en la máquina virtual Azure (o una máquina virtual local) usando ansible.

Después de instalar ansible en nuestra máquina y configurar el fichero inventario que contendrá la información de la máquina virtual a la que nos conectaremos:

	[server]
	35.164.175.173 ansible_ssh_private_key_file=~/key_ec2_aws.pem ansible_ssh_user=ubuntu

Ahora podemos comprobar si ansible funciona con:

	ansible server -m ping


![Resultado de ping con ansible](https://github.com/JPPorcel/CC-Ejercicios/blob/master/Tema%202/images/ej_5.png?raw=true)


Vamos a desplegar los fuentes de una aplicación subida a un repositorio público en GitHub ([MusicRecognitionCpp](https://github.com/JPPorcel/MusicRecognitionCpp)).

	ansible server -m git -a "repo=https://github.com/JPPorcel/MusicRecognitionCpp.git dest=/home/ubuntu/app version=HEAD"

Y obtenemos el siguiente resultado:

![Resultado de ping con ansible](https://github.com/JPPorcel/CC-Ejercicios/blob/master/Tema%202/images/ej_5_1.png?raw=true)

Y en la máquina virtual podemos encontrar los fuentes en el directorio especificado:

![Resultado de ping con ansible](https://github.com/JPPorcel/CC-Ejercicios/blob/master/Tema%202/images/ej_5_2.png?raw=true)