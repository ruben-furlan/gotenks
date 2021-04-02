<div style="vertical-aligh: center;"> 

# Docker swarm 

<p>Como se utiliza docker a nivel de cluster</p>
<p>docker swarm permite crea un cluster de uno o mas nodos docker, esto permite dispone "servicios" que se despliegan de forma replicada a o largo de los nodos.</p>
<p><strong>Managers:</strong> 
<br>gestores del cluster repartir tareas gestionar 1 o N manager que es lo normal para poder aumentar la disponibilidad se comunican entry si y saben el estado de los cluster los nodos que los contienen etc etc</p>

<p><strong>(nodos)Worker:</strong><br>desplegar el contenedor a partir de una imagen y donde se van a ejecutar los servicios
                                      cada worker se comunica con cada mánager todo el cluster funciona de una manera compartida
</p>

## servicios en swarm

<p>Cuando desplegamos una imagen en el docker Engine se crea un servicio, un servicio identifica tareas en el contexto de una aplicación, por ejemplo un servidor web, una Base de datos, etc.. siempre debemos indicar la imagen a usar para crear los contenedores y que comandos lanzar dentro</p>
<p>cada micro servicio va ser un servio.</p>
<p>Mánager definimos un servicia apache se desplegá en dos nodos de cluster cada nodo tiene una tarea y de desplegar un contenedores para cada tarea</p>

## Crear un cluster

<p> cada maquina fisica o virtual</p>

```
 docker swarm 
 docker services (crear micro servicios dentro del cluster)
```

<p> identifica la maquina donde estoy tirando el comando como nodo maestro, manager</p>


- inicializa un nuevo cluster
-  identifica la maquina como managers 
- y asignar un token para usar en los Worker para unirlos a mánager


<p> es importante que los nodos de los cluster de docker tengan ip fija statica porque si cambia de ip puede complicarse, para que los workes sepan donde ir</p>
<p>  se tiene que agregar la ip si la maquina tiene varias tarjetas de red (varias ip)</p>

 ```
 docker swarm init --advertise-addr 192.168.28.149 
 ```
 <p> de la respuesta a este comando es importante guardar la linea:</p>
 
 ```
  docker swarm join --token asdoiasjdo2j34n32i9e0dqjsndqbfuipwfbi 

-  (si se pierde se me puede preguntar de nuevo al nodos que token tiene 
-  docker swarm join-token worker
-  docker info en swarm active(solo info))
 ```
<p>  esto es importante porque nos dice como puede asociar los Worker a este mánager(nodo master cluster etc como lo queramos llamar) que cree </p>

## Agregar nodos

<p>Es básicamente pegar lo que nos arrojo el cluster</p>

 ```
 - docker swarm join --token asdoiasjdo2j34n32i9e0dqjsndqbfuipwfbi

y debe de decirnos un mensaje similar a "this node joined a swarm as a workwe"

En el cluster lanzar el 
 
 - docker info -> en swarm 
 ```

## Trabajar con nodos del cluster

<p><strong>ESTAS OPERACIONES SE TIENEN QUE LANZAR EN LOS NODOS MANAGERS</strong></p>

<p>nos permite realizar las operaciones de docker</p>
 
 ```
  docker node ls -> vemos los nodos
  docker node inspect --pretty nodo2 -> información del nodo dos
 ```
<p>Si quiero tener mas de un managers, esperando si se cae el primero tomar el control.
   como convertir en leader(managers) un nodo</p>

 ```
  docker node  promote nodo3 -> promover a managers
  docker node ls
 ```
<p>vamos que el nodo3 queda Reachable y no queda como Leader que quiere decir aunque sea mánager no esta gestionado el cluster pero el tres estas esperando por si un dia se cae o le quito de mánager tome el control</p>
<p> nodo1 deja de ser mánager y se convierte en Worker</p>
 
 ```
   docker node demote nodo1 -> leader mánager cluster
 ```
<p>para bajar un nodo del cluster -> desde el nodo(worker) LAZAR</p>

 ```
 docke swarm leave -> para el nodo - lo deja "down". se puede hacer nuevamente el join con el token 
 docker rm node1 -> lo elimina
 ```

## Crear y trabajar con servicios

<p><strong>SOLO SE EJECUTA EL COMANDO EN EL MANAGERS</strong></p>


 ```
 replicas: cuantas veces el proceso se va a lanzar en los distintos nodos alpine es la imagen
- docker services create --replicas 1 --name ser1 alpine ping docker.com
- docker services ls -> ver los servicios mas información
- docker services ps ser1 
- docker services logs servicio1 --> lo ultimo que ejecuto
- docker services inspect -->pretty servico1  
 ```
## Escalar un servicio(mas replicas)
<p>puedo replicarlo muchas veces y esa replica puede replicarse en el mismo nodo, cuantas quieras depende de la maquina</p>
<p>indicar en un servicio cuantas tareas va a ejecutar</p>

 ```
 docker service scale servio1=2
 docker service ps
 ```

<p>docker services scale servicio=5
siempre y cuando estemos en espacio suficiente y memoria podemos tener las replicas que queramos
intenta siempre de manera homogenia las replicas en la cantidad ed nodos que tengamos
</p>

## Borrar un servicio (borra replicas)

 ```
bajar cantidad de replicas:
- docker service scale servicio1=3
- docker service ls ->tarda un rato, es posible que veas aquí las anteriores en realidad ya las ha eliminado

borrar un servicio:
- docker service servicio=1
- docker service ls-> lo mismo puede ver cosas viejas mientras procesa
esto es re escalar y borrar servicios.
 ```

</div>



