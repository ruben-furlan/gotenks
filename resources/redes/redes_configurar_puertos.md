<div style="vertical-aligh: center;"> 
<h1> Configurar Puertos </h1> 

<p>Vamos a averiguar los puertos por los que escucha. Podemos usar el comando inspect</p>
<p>Por supuesto, lo más rápido es comprobar la documentación de DockerHub para averiguarlo, donde además normalmente tenemos ejemplos: <strong>docker inspect --format='{{.Config.ExposedPorts}}' mongo</strong></p>
<p>Comprobamos que lo hace por el puerto 27017</p>
<p>Creamos un contenedor llamado mongo2 que escuche por el mismo  puerto en el host: <strong>docker run -d -p 27017:27017 --name mongo2 mongo
</strong></p>
<p>Comprobamos que funciona y los puertos por los que escucha: <strong>docker ps</strong></p>
<hr>
<p>Ahora vamos a comprobar las redes que tenemos: <strong>docker network ls</strong></p>
<p>Comprobamos los contenedores que tiene la red Bridge. Al final , mas o
   menos tenemos nuestro contenedor mongo2, con la IP que se le ha
   asignado: <strong>docker network inspect bridge</strong></p>
<p>Podemos probar que llegamos al contenedor con un ping: <strong>ping 172.17.0.2</strong></p>
<p>Si arrancamos otro contenedor Mongo, vamos a ver los datos que les
   indica. Recordemos que debemos poner otro puerto distinto para el host: <strong>docker run -d --name mongo3 -p 27018:27017 mongo</strong></p>
<p>Si inspeccionamos la red, debemos tener los dos contenedores, con sus
   direcciones IPs correspondientes </p>
<p>Vamos a probar que llegamos desde un contendor a otro
    Abrimos una bash contra mongo3: <strong>docker exec -it mongo3 bash</strong></p>
<p>Instalamos el ping: <strong> apt-get update, apt-get install iputils-ping</strong></p>
<p>Hacemos un ping contra mongo2. En mi caso es el 172.17.0.2, tal y como me ha indicado la red <strong></strong></p>
<p>Como prueba final, vamos a conectarnos como cliente, desde mongo3 a
   la base de datos MongoDB que tenemos en el contenedor mongo2. Es
   decir, vamos a comprobar que los contenedores de una red concreta se
   pueden conectar entre sí sin problemas.
   • Desde la Shell que hemos abierto en mongo3 ponemos el siguiente
   comando, que es la Shell de mongo: <strong>mongo --host 172.17.0.2 --port 27017
</strong></p>
<p>• Ya estamos conectados. Podemos probar por ejemplo viendo las Bases
   de datos de MongoDB: <strong>show dbs</strong></p>
<p>: <strong></strong></p>
 </div>


