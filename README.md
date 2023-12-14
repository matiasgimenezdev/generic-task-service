# Generic task executor

<img src="https://private-user-images.githubusercontent.com/117539520/290620333-79fa4b52-a62e-48c7-9516-4c628c70a30c.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTEiLCJleHAiOjE3MDI1NzkxMjYsIm5iZiI6MTcwMjU3ODgyNiwicGF0aCI6Ii8xMTc1Mzk1MjAvMjkwNjIwMzMzLTc5ZmE0YjUyLWE2MmUtNDhjNy05NTE2LTRjNjI4YzcwYTMwYy5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBSVdOSllBWDRDU1ZFSDUzQSUyRjIwMjMxMjE0JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDIzMTIxNFQxODMzNDZaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT0xN2EzMzgxMTE1N2VjOTAxMzBiMDQzZjEzZDU1ZTAxZjczZmU1YmJhOTIxMGI2MzhmNTIyODIwMjZlYWUzYTcyJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZhY3Rvcl9pZD0wJmtleV9pZD0wJnJlcG9faWQ9MCJ9.3Qn2rxoLJsDP4nDoqjDDrPKP8JyYc-wKfe7BVyM5b5o" alt="Arquitectura" width="550" height="300">

## Descripción
Para iniciar los proyectos con spring utilizamos el [Spring Initialzr](https://start.spring.io/). Luego, para la comunicación del servidor con el demonio de Docker hicimos uso de la liberia [docker-java](https://github.com/docker-java/docker-java), ya que Docker no provee una libreria oficial para Java pero si recomienda algunas y esta es una de ellas.

## Instrucciones de ejecución

La idea es levantar localmente el contenedor que contiene el servidor, por lo cual, debe tener Docker instalado. Luego, ejecutar el cliente para que se inicie la comunicacion entre procesos.

#### Descargar imagen del servidor
```
$ docker pull mgimenezdev/task-server:v1
```

#### Crear el contenedor
```
$ docker run --name=task-server --network=host -v /var/run/docker.sock:/var/run/docker.sock mgimenezdev/task-server:v1
```
- Puede agregar la opcion **-d o --detach** para ejecutar el servidor en segundo plano. Sin embargo, recomiendo no hacerlo la primera vez para ver el progreso de la ejecucion del servidor.
- La opcion **-v /var/run/docker.sock:/var/run/docker.sock** es para montar el socket de Docker del host en el contenedor, lo que permite que el contenedor pueda interactuar con el demonio de Docker que se está ejecutando en el host.
- La opcion **--network=host** es para que el contenedor se ejecute en la red del host y pueda interactuar con el contenedor del servicio que va a ejecutarse dentro del host, como contenedor hermano.

#### Ejecutar el cliente
Una vez que el contenedor del servidor se encuentra en ejecucion, en una nueva terminal o en la misma, dependiendo de si uso o no la **opcion -d o --detach** en el paso anterior, ubiquese en el directorio 'client' e inicie el cliente. <br>
```
$ cd client
$ java -jar target/client.jar
```
