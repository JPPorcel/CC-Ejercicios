# Arquitecturas software para la nube

## Ejercicio 1

### Buscar una aplicación de ejemplo, preferiblemente propia, y deducir qué patrón es el que usa. ¿Qué habría que hacer para evolucionar a un patrón tipo microservicios?

La aplicación seleccionada para identificar el patrón usado es una aplicación propia creada como proyecto externo a la universidad. Se trata de Cophrade, una red social cofrade para compartir información de horarios de cofradías y reconocimiento de marchas cofrades. El sistema fue creado como una aplicación monolítica corriendo en una única máquina virtual. En la misma máquina virtual se ejecutaba una aplicación web escrita en php que funcionaba como API, la base de datos de usuarios, cofradías, marchas, etc en MySQL y el servicio de reconocimiento de música escrito en C++ que funcionaba como un microservicio con el que los usuarios se comunicaban directamente tras conseguir su token de acceso relacionado con la petición realizada a la API mediante socket. 

Por lo tanto se trata de una arquitectura software monolítica. Para evolucionar este sistema a un patrón de tipo microservicios no sería muy complejo, personalmente optaría por dividir en dos la base de datos, una de ellas que contenga la información de usuarios, lista de maschas escuchadas, cofradías e información relativa a ellas, etc. y en la otra base de datos solo estaría el audio, etiquetado con tipo de marcha, autor, etc. Así habría dos microservicios de base de datos, uno con una base de datos SQL y la otra NoSQL.

Se pueden dividir más microservicios:
* Microservicio que ejecuta el reconocimiento de audio en C++
* Microservicio que se encarga de la información de cofradías
* Microservicio para la gestión de la red social, usuarios, amigos, compartir música

Todos estos microservicios no serían accesibles directamente al usuario, si no que habría un enlace entre ellos, una API, escrita en php, nodeJS, python o cualquier otro lenguaje de programación que nos facilite un framework sencillo de configurar.