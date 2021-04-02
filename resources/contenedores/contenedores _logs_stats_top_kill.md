<div style="vertical-aligh: center;"> 

# Docker logs, stats, top, kill</h1> 

## Docker logs
<p>Arrancamos un contenedor basado en la imagen NGINX en modo background:</p>

```
  docker run -d --name nginx1 nginx
```
<p>Comprobamos que está funcionando:</p>

```
  docker ps
```
<p> Comprobamos si hay algún log. Debe salir vacio :</p>

```
  docker logs nginx1
```

<p>Nos conectamos al contenedor desde otro terminal: </p>

```
  docker exec -it nginx1 bash
```

<p>Instalamos el comando wget en el contenedor:</p>

```
  apt-get update    apt-get install wget
```

<p>Por supuesto, podemos entrar en una Shell si es necesario, indicando que es interactivo:</p>

```
  docker exec -it nginx1 bash
```

<p>Lanzamos un “wget” contra el servidor nginx del contenedor: </p>

```
  wget localhost
```

<p>Comprobamos con el comando Docker top los procesos que se están
   ejecutando en el contenedor  Podemos ver que está el nginx y además la bash con la que hemos
   entrado desde Docker exec ></p>
   
  
```
  docker top nginx1
```
   
<p>continua....</p>

## Docker stats
<p> Vemos ahora las estadísticas de uso del contenedor</p>
   
```
  dnocker stats nginx1(nombre o id del contenedor)
```
## Docker kill

<p>Por último, matamos el contenedor en vez de pararlo</p>

   
```
  docker kill nginx1
```

</div>