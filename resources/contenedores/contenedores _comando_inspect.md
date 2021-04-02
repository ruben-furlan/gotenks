<div style="vertical-aligh: center;"> 

# Docker inspect

 <p>Docker inspect proporciona información detallada sobre las construcciones controladas por Docker. (imagenes, contenedores, etc)</p>
 
  [documentacion] - oficial

<p>Nos bajamos la imagen de MongoDB:</p>
     
```
  docker pull mongo
```
<p>Comprobamos que la tenemos:</p>     

```
  docker images
```
<p>Comprobamos las propiedades de la imagen. Debe salir bastante información</p>

```
  docker image inspect mongo
```
<p>Podemos usar GREP para encontrar información más concreta</p>

```
  docker image inspect mongo | grep MONGO_VERSION
```
<p>Lo mejor es mandar la salida a un fichero para inspeccionarlo después</p>

```
  docker image inspect mongo > mongo.json
```
<p>Creamos ahora un contenedor con esa imagen</p>

```
  docker run -d --name mongo1 mongo
```
<p>Lanzamos un inspect contra el contenedor. También debe aparecer mucha información</p>

```
  docker inspect mongo1
```
<p>Podemos usar de nuevo el <strong>GREP</strong>. Por ejemplo, hay un campo que nos  permite ver la dirección IP que ha asignado al contenedor</p>

```
  docker inspect mongo1 | grep IPAddress
```



[//]: #
   [documentacion]: <https://docs.docker.com/engine/reference/commandline/inspect/>
   

</div>