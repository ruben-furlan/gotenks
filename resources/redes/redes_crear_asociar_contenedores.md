<div style="vertical-aligh: center;"> 

# Crear redes y asociarlas a contenedores  


<p>Creamos una nueva red de tipo bridge:</p>

```
  docker network create net1
``` 

<p>ver redes: <strong></strong></p>

```
  network ls
``` 

<p>La inspeccionamos:</p>

```
  docker network inspect net1
``` 
<p>Vemos que tiene el rango de direcciones “Subnet": "172.18.0.0/16",: <strong></strong></p>
<p>• A nivel físico del sistema operativo ha debido crear una nueva conexión para la red. La que tiene el nombre de docker0 es la que corresponde a
la red bridge predeterminada de Docker: </p>
<p>(NOTA. El comando “nmcli” es Red Hat-Fedora, en vuestro Linux puede variar. Podemos usar ifconfig por ejemplo para ver la información)></p>

```
  nmcli con
``` 

<p>El nombre de dispositivo que se ha puesto a la nueva conexión coincide  con el ID que Docker ha asignado a la red</p>

```
  docker network ls
```    
   
<p>Creamos un contenedor mongodb con esa red:</p>

```
  docker run -d -p 27017:27017 --network net1 --name mongo1 mongo
``` 

<p>Comprobamos que funciona y los puertos por los que escucha:</p>

```
  docker ps
``` 

<p>Comprobamos en la red que efectivamente se ha unido el contenedor a  la red y podemos comprobar también la IP que le ha facilitado
: <strong>Comprobamos en la red que efectivamente se ha unido el contenedor a la red y podemos comprobar también la IP que le ha facilitado </strong></p>
<p>Vamos a comprobar ahora que cuando creamos una red personalizada,   Docker genera un DNS interno que nos permite acceder a los
contenedores con el nombre que le pusimos con la opción –name al  crearlos </p>
   
<p>Si entramos dentro del contenedor “mongo1” (tu debes usar el nombre que has usado para crearlo)</p>

```
  docker exec -it mongo1 bash
``` 
<p>Instalamos ping:</p>

```
  apt-get update,apt-get install -y iputils-ping
``` 
<p>Si probamos a realizar un ping a “mongo1” (y recordemos que no hemos configurado nada en la red para poner ese nombre). Vemos que  funciona bien y localiza la IP: <strong>ping mongo1</strong></p>
<p>Desde otro terminal, vamos a crear un Segundo contenedor en esa red</p>

```
  docker run -d -p 27018:27017 --name mongo2 --network net1  mongo
``` 

<p>• Desde la bash en la que estamos dentro de mongo1 hacemos un ping a mongo2Debe funcionar perfectamente, ya que la red personalizada se encarga
de gestionar los nombre de los contenedores. Y como hemos visto, nosotros no hemos tenido que configurar nada.:<strong>ping mongo2</strong></p>
<p>• Ahora, vamos a crear una segunda red. Además le vamos a poner dos características::
o Que su subred sea la 172.30.0.0/16 o Que los contenedores se les asocie una IP que comience a partir  de la 172.30.10.0/24 :</p>

```
  docker network create net2 --subnet=172.30.0.0/16 --iprange=172.30.10.0/24
``` 
<p>Podemos comprobar haciendo un inspect a la red: </p>

```
  docker network inspect red2
``` 
<p>• Vamos a crear un contendor mongo asociado a esa red:</p>

```
  docker run -d --name mongo3 --network net2 mongo
``` 

<p>Comprobamos con inspect la red que tiene al contenedor. Mandamos la información a un fichero porque salen bastantes cosas :</p>

```
  docker inspect mongo3 > mongo3.json
``` 

<p>Editamos el fichero y buscamos la zona de la red. Podemos ver que está  asociado a la net2 y con la dirección IP adecuada, a partir de la 10: </p>
<p>Si intentamos acceder desde la bash que tenemos abierta en “mongo1”   a mongo3 no la encuentra porque no están en la misma subred: </p>
<p>Por último, vamos a asociar este contenedor a la red “net1”
<p>Desconectamos mongo3 de la red “net1”: </p>

```
  docker network connect net1 mongo3
  docker network disconnect net1 mongo3
``` 

 </div>


