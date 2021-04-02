<div style="vertical-aligh: center;"> 

# Contenedores 

<p> La idea detrás de Docker es crear contenedores ligeros y portables para las aplicaciones software que puedan ejecutarse en cualquier máquina con Docker instalado, independientemente del sistema operativo que la máquina tenga por debajo, facilitando así también los despliegues.</p>
  
  [documentacion] - oficial

## Arrancar y parar los servicios de Docker

<p>Arrancarlo ahora con SYSTEMCTL: </p>

```
  systemctl start Docker
```
<p>Comprobamos el estado:</p> 

```
  systemctl status docker
```

<p>Activamos el servicio para que funcione al arrancar el servidor: </p>

```
  systemctl enable docker
```

## Vamos a crear nuestro primer contenedor

```
  docker run hello-world
```

<p>Comprobar que el contenedor no está activo, ya que se cierra en cuanto sale el mensaje: </p>

```
  docker ps
```
<p>Comprobar que el contenedor se ha creado, pero que está parado: </p>

```
  docker ps -a
```

<p> Creamos un nuevo contenedor basado en otra imagen de Docker Hub  denominada busybox, que es un contenedor con un cierto número de   utilidades: </p>

```
  docker run busybox
 ```

<p>Comprobamos el nuevo contenedor:</p>

```
  docker ps -a
```

<p>Comprobar que existe la imagen: </p>

```
  docker images
 ```

<p>Visualizar solo las ids de los contenedores :></p>

```
  docker ps -aq
 ```
<p>Ver los dos últimos contenedores lanzados: </p>

```
  docker ps -a -n 2
```

<p>Comprobar el espacio utilizado por los contenedores creados:</p>

```
  docker ps -a -s
 ```
<p>También podemos usar la opción <strong>-f</strong> para filtrar por algún dato concreto,
   por ejemplo, por el nombre. Busca por el contenido dentro del texto. : </p>

```
  docker ps -a -f name=davinci
 ```


[//]: #
   [documentacion]: <https://docs.docker.com/engine/reference/commandline/container/>

</div>