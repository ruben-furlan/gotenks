<div style="vertical-aligh: center;"> 

# Docker registry
<p>sino queremos guardar en dockerhub y necesitamos tener en un entorno privado. </p>
<p>Queremos utilizar las imágenes en un repositorio en nuestra organización (red privada), tenemos que crear registros privados, podemos tener varios registros como queramos y ademas las imágenes que corresponda, esto ayuda para una buena gestión.</p>


## Crear un registro de imagen
<p>dockerhub  busqueda --> registry(oficial)</p>
<p>Descargamos la imagen y creamos un contenedor para poder gestionar esto, quedan en volúmenes.</p>

```
    docker pull registry
    crear un contedor
    docker run -d (background) -p 5000:5000(recomendado) --name registro1 registry
    docker ps -> para verificar el contenedor
```
<p>podemos crear un segundo registro, no lo puedo tener el mismo puerto si esta en la misma maquina tiene que ser puerto distintos</p>

```
  docker run -d (background) -p 5001:5001(recomendado) --name registro2 registry
```
<p>yo puedo tener dos registro para gestionar las imágenes</p>

## Subir y bajar imágenes del registro

-  SUBIR:

<p>tener en cuenta comprobamos si tenemos arrancado nuestro contenedor.</p>
<p>ejemplo con ubunto</p>

```
docker images ubuntu 
```


<p>antes de poder subir un imagen a repositorio ahí que etiquetarla al 
repositorio para que docker sepa donde tiene que buscar la imagen</p>

```
                     (nombre de la maquina:puerto)   
  docker tag ubunto localhost:50000/mi-ubunto
  docker images localhost:50000/mi-ubunto
```

<p> etiquetamos nuestra imagen con el nombre de la maquina del puerto</p>
<p>subir la imagen:</p>

```
  docker push localhost:5000/mi-ubunto
```
<p>al nombra la imagen con nombre de la maquina y puerto ya sabe a 
cual subir por eso no pide confirmacion.</p>

```
 docker images ls
```
<p>en la columna repositorio te sale localhost:5000/mi-ubunto</p>

- BAJAR:

<p>  para ver todas las imágenes locales dentro de mi registro</p>

```
    - docker images localhost:5000/*   
      es importante saber que cuando borramos la imagen que esta subida a un 
      registro se tiene que tener en cuenta que el comando siguiente lo borra local. digamos que es un branch (xD)
    - docker rmi localhost:5000/mi-ubunto
```
<p>   para descargar la imagen</p>

```
    docker pull localhost:5000/mi-ubunto
```

## Cambiar almacenamiento del repository

```
    docker inspect registro1
```
<p> tenemos que buscar el sitio donde deja el almacenamiento ver volúmenes. lo deja donde siempre cuando crea un volumen por <strong>defecto -> var/lib/docker/volumenes</strong></p>
<p> para modificar el sitio de almacenamiento</p>

```
     mkdir /reg_docker
     docker run -d --name repo1 -p 5000:5000 -v /reg_docker:/var/lib/registry registry
     docker tag ubunto localhost:5000/ubunto-prueba
     docker push localhost;ubuntu-prueba
```
<p> debería de quedar dentro de reg_docker</p>

</div>



