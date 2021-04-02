<div style="vertical-aligh: center;"> 

# Docker Compose 
<p>Docker Compose es una herramienta que permite simplificar el uso de Docker. A partir de archivos YAML es mas sencillo crear contendores, conectarlos, habilitar puertos, volumenes, etc. Aquí resumimos algunos tips.<p>
<p>Con Compose puedes crear diferentes contenedores y al mismo tiempo, en cada contenedor, diferentes servicios, unirlos a un volúmen común, iniciarlos y apagarlos, etc. Es un componente fundamental para poder construir aplicaciones y microservicios.</p>
<p>En vez de utilizar Docker via una serie inmemorizable de comandos bash y scripts, Docker Compose te permite mediante archivos YAML para poder instruir al Docker Engine a realizar tareas, programaticamente. Y esta es la clave, la facilidad para dar una serie de instrucciones, y luego repetirlas en diferentes ambientes.


 [documentacion] - oficial


<p>es un siguiente paso en la funcionalidad y característica dentro de docker:</p>
<p>una de las características de docker es el concepto de micro-servicios.</p>
<p>distintos contenedores que ofrecen distintas funcionalidades para micro-servicios</p>

- docker compose: producto que orquesta servicios o componete de contenedores.
- docker-compose.yml instrucciones para enlazar los servicios.
- MEAN-> un entorno de desarrollo angular expre.js node.js mongo

<p>docker compuse vamos a construir los contenedores necesarios para orquestar los servicios, cada uno forme parte de contenedor</p>

<p>Contenedor para agugular</p>
<p>Contenedor para exprese y nodejs</p>
<p>Contenedor mongodb</p>



## Instalar

<p>no viene instalador por defecto, pero en Windows suele venir instalado.</p>

 [instalar]
   
docker descarga desde github una version de docker compose.[descargar].
  
<p>lo que hace es descarga un fichero ejecutable, nos pide que hagamos un chmod para convertirlo en ejecutable</p>  
<p>docker-compose (salen las opciones, orientados a un conjunto de contenedores)</p>  
<p>lo que maneja por debajo son contenedores de docker.</p>

## Fichero docker-compose.yml

<p>Digamos que el equivalente al "dokerfiel de la imagen"</p>
  
```
cat docker-compose.yml
* version: 3 --> dependiendo de la version de docker tenemos distintos versiones compose esta orientado a micro servicios
* services -> servicios que vamos a tener cada servicio esta basado en una imagen seria un "contenedor" todo servicio debe tener build permite crear la imagen del contenedor . es el directorio -links: --> enlaces con los otros contenedores servicos
* image construye partir de una imagen existente
```


## Mi primer proyecto

<p>el nombre del directorio es importante usa el concepto del proyecto, es todo el entorno por defecto usa el nombre del directorio</p>


```
pr_nginx --> cat docker-compose.yml

version: '3'
services:
 ngix:
 imagee: nginx
 ports:
 -"80:80"
```

<p>(estando en la ruta de compose)
   se recomienda que utilizamos nuestra propia red para los enlazar los contenedores
   <strong>LO HACE POR DEFECTO</strong>
    </p>

```
docker-compose up
```
```
docker-compose ps (información de los contenedores de micro servicios)
```

<p>si el contenedor se hubiera creado -d mod background como no se puede hacer ctrl+z para detener se utilizaría el comando </p>

```
docker-compose stop
```
## Enlazar servicios. Puertos y variables

<p>Ejemplo:</p>
<p>docker-compose.yml</p>

```
version:'3' -> versión del docker
services:   -> a todos se le denomina servicies (ojo sintaxis yml)
   wordpress:->servicio1(nombre que quiera, descriptivo) ->
     images: wordpress (obvio la busca en dockerhub)
     enviroment:-> variables (seria el -e )
       WORDPRESS_DB_HOST: dbserver:3306 
       WORDPRESS_DB_PASSWORD: mysqlpw
      ports: -> se comportan como el -p al crear un contenedor (hots:contenedor)
      -80:80
      depends_on -> decimos que como debería docker arrancar los contenedores
      -dbserver
    dbserver: servicio2 ->
     image:mysql5.7
     enviroment:
      MYSQL_ROOT_PASSWORD: mysqlpw
     ports:
      -3306:3306
```

<p>cuando tenemos redes personalizas que se crean automáticamente con docker compose y no hace falta utilizar el --link</p>

```
consola:

entrar a la carpeta donde tenemos el docker-compose.yml
 - docker-compose up (utiliza las imágenes que ya tiene sino se la descarga)
 - docker network ls (debe mostrar las redes creadas pro defecto)

   [documentacion]: <https://docs.docker.com/compose/install/>
   [descargar]:<https://github.com/docker/compose/releases>

```

## Comandos utiles
```
docker-compose -> ayuda sobre el comando

docker-compose up --> crear y arranca los contenedores
docker-compose stop --> para los contenedores
docker-compose ps -> contenedores corriendo
docker-compose image --> vemos las imágenes de contenedores

(dentro de la carpeta docker-compose.yml)
docker-compose config -> muestra si el yml esta correcto
docker-compose start -> arranca el contenedor desde el directorio o si es afuera pasar el nombre (nombre del servicio)
docker-compose logs dbserver(nombre del servio configurado en el yml) -> veo los los de servicios(contenedores)
docker-compose top wordpress (nombre del servio configurado en el yml) -> ver los procesos mas pesados

docker-compose pause -> parar temporalmente los contedores
docker-compose unpause -> ejecuta los contenedores

docker-compose-restart -> restarte los contenedores

docker-compose rm -> elimina los servios (se puede pasar nombre del servio)
docker-compse up -> crea todo de nuevo
```

## Volumenes
```
version: "3.2"
services:
  web:
    image: nginx:alpine
    volumes: (ejemplo 1 o manera 1)
      - type: volume
        source: mydata 
        target: /data
        volume:
          nocopy: true
      - type: bind
        source: ./static
        target: /opt/app/static
    ports:
      - 80:80
  db:
    image: postgres:latest
    volumes:(ejemplo 2 o manera 2)
      - "/var/run/postgres/postgres.sock:/var/run/postgres/postgres.sock"(bind)
      - "dbdata:/var/lib/postgresql/data"(volumen)
```


<p>(importante,se declara los volumenes creados en la etapa superior, para confirmar )</p>

```
volumes:
     mydata:
     dbdata:
```
<p>Diferencias</p>

- volume -> crea el volumen dentro del directorio de docker bar/lib/docker/volume
- bind:asocia un determinado de la maquina principal (host) a un contenedores


<p>  siempre nuestro docker-compose.yml debe estar dentro de un directorio donde voy a ejecutar</p>

```
  docker volume ls -> para ver volúmenes
  docker volume prune-> elimina volúmenes que no estén asociados a algún contenedor
```
```
  docker-compose confg --services
  contenedores en de la orquestacion

  docker-compose exec web sh
  
  dcoker-compose down (OJO borra todo)
```

## Redes 
```
version: '3.3'

services:
  app:(servicio 1, este es creando nosotros la imagen)
    image: client 
    container_name: client (nombre del contenedores)
    build: . (construya la imagen en base al dockerfield el . es la ruta tiene que estar en esa misma ruta)
    ports: 
      - 80:3000
    environment:
      - MONGO_URI=mongodb://mongo_db/sample (apunta a la base)
    depends_on: 
      - db (servio app depende de db)
    networks: 
      - net3(en vez de una red personalizada de manera automática, esto es una red propia)
  db:
    image: mongo:3.0.15
    container_name: mongo_db
    volumes:
      - ./db:/data/db
    networks:
      net3:
        aliases:
          - "mongo_db"-> un nombre alternativo que podemos utilizar dentro de esta red, se puden poner varios
        ipv4_address: 172.16.238.10 --->ip fijas (por ejemplo)
        ipv6_address: 2001:3984:3989::10
(clausa networks. si ponemos solos net3: funciona pero para ver mas propiedades)
networks:
  net3:
    driver: bridge 
    ipam: (configurar sub redes )
      driver: default
      config:
      -
        subnet: 172.16.238.0/24
      -
        subnet: 2001:3984:3989::/64
```


## Opciones interesantes:
```
docker-compose -f -> permite que el fichero donde vamos a tomar la confuracion yml no se llame docker-compose

docker-compose -p nombre  que le vamos a dar a la orquestacion


se tiene que tener en cuenta si se cambia el nombre de la orquestacion se tiene que aplicar la mayoría de comandos con -p ejemplo:

docker-compose -p nombrenuevo ps
```


[//]: #
   [documentacion]: <https://docs.docker.com/compose/>
   [instalar]: <https://docs.docker.com/compose/install/>
   [descargar]:<https://github.com/docker/compose/releases>
</div>



