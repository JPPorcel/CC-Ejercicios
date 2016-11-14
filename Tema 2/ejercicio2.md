# Gestión de infraestructuras virtuales

## Ejercicio 2

### Crear una receta para instalar nginx, tu editor favorito y algún directorio y fichero que uses de forma habitual.

Primero hay que crear una receta de Chef, creamos un fichero *default.rb* en el directorio *chef/cookbooks/nginx/recipes/*:

	mkdir -p chef/cookbooks/nginx/recipes
	touch chef/cookbooks/nginx/recipes/default.rb

El nombre del fichero indica que se trata de la receta por omisión, pero el nombre de la receta viene determinado por el directorio en el que se meta. En *default.rb* es donde escribirimos la receta:

	package 'emacs'
	directory '/home/ubuntu/ejercicios'
	file "/home/ubuntu/ejercicios/LEEME" do
		owner "ubuntu"
		group "ubuntu"
		mode 00544
		action :create
		content "Directorio para ejercicios"
	end
    package 'nginx'

Con esta receta instalamos el nuestro editor favorito (emacs), creamos un directorio y un archivo dentro de él e instalamos nginx.

En el fichero *chef/node.json* se incluye la lista de recetas que se ejecutarán:

	{
		"run_list": [ "recipe[nginx]" ]
	}

Y en el fichero *chef/solo.rb* incluimos las rutas al recetario y a la lista de recetas:

    file_cache_path "/home/ubuntu/chef"
	cookbook_path "/home/ubuntu/chef/cookbooks"
	json_attribs "/home/ubuntu/chef/node.json"

Y ejecutamos:

	sudo chef-solo -c chef/solo.rb


![Resultado de ejecutar la receta](https://github.com/JPPorcel/CC-Ejercicios/blob/master/Tema%202/images/ej2.png?raw=true)