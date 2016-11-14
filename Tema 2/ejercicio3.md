# Gestión de infraestructuras virtuales

## Ejercicio 3

### Escribir en YAML la siguiente estructura de datos en JSON

	{ uno: "dos", tres: [ 4, 5, "Seis", { siete: 8, nueve: [ 10, 11 ] } ] }

En YAML quedaría:

	uno: "dos"
	tres:
    	- 4
    	- 5
    	- "Seis"
    	-
        	siete : 8
        	nueve : [10, 11]