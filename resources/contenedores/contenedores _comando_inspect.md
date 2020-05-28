<div style="vertical-aligh: center;"> 
<h1> docker inspect</h1> 
<p>Nos bajamos la imagen de MongoDB: <strong>docker pull mongo</strong></p>     
<p>Comprobamos que la tenemos: <strong>docker images</strong></p>     
<p>Comprobamos las propiedades de la imagen. Debe salir bastante información <strong>docker image inspect mongo</strong></p>
<p>Podemos usar GREP para encontrar información más concreta<strong>docker image inspect mongo | grep MONGO_VERSION</strong></p>
<p>Lo mejor es mandar la salida a un fichero para inspeccionarlo después<strong>docker image inspect mongo > mongo.json</strong></p>
<p>Creamos ahora un contenedor con esa imagen<strong>docker run -d --name mongo1 mongo</strong></p>
<p>Lanzamos un inspect contra el contenedor. También debe aparecer   mucha información<strong>docker inspect mongo1</strong></p>
<p>Podemos usar de nuevo el GREP. Por ejemplo, hay un campo que nos
   permite ver la dirección IP que ha asignado al contenedor<strong> docker inspect mongo1 | grep IPAddress</strong></p>
</div>