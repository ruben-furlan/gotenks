<div style="vertical-aligh: center;"> 

# Docker exec
<p>El comando exec se usa para interactuar con contenedores que ya se están ejecutando en el host de Docker. Le permite iniciar una sesión dentro del directorio predeterminado del contenedor. Las sesiones creadas con el comando exec no se reinician cuando se reinicia el contenedor. </p>

  [documentacion] - oficial
  
<p>Arrancamos un contenedor basado en la imagen NGINX en modo background:</p>  
     
```
  docker run -d --name nginx1 nginx
```

<p>Comprobamos que está funcionando:</p>  
     
```
  docker ps
```

<p>Lanzamos algún comando contra el contenedor con “EXEC”. Visualizar los ficheros de /:</p>  
     
```
  docker exec nginx1 ls /
```

<p>Podemos lanzar varios comandos al mismo tiempo. Por ejemplo la fecha  y nombre del sistema:</p>  

     
```
  docker exec nginx1 date ; uname -n
```
<p>Por supuesto, podemos entrar en una Shell si es necesario, indicando que es interactivo:</p>  
     
```
  ddocker exec -it nginx1 bash
```
<p>una vez dentro del ubunto lanzar un ls y da el mismo resultado</p>

<p>Salimos y paramos el contenedor:</p>  
     
```
 docker stop nginx1
```

<p>Comprobamos que existe:</p>  
     
```
 docker ps -a
```

## Borrados

<p>Borramos el contenedor. Comprobamos que no está:</p>  

```
 docker rm nginx1(o id del contenedor)
```


<p>Borramos imagenes. si esa imagen esta siendo usada por un contenedor no se podra eliminar :</p> 

```
 docker rm nginx1(o id del contenedor)
```

<p>ejemplo del error :</p>

```
Error response from daemon: conflict: unable to remove
repository reference "fedora" (must force) - container
28b5e0c7b73c is using its referenced image 9110ae7f579f
```

<p>Si se aplica al eliminar la imagen un <strong>-f (force)</strong> , Los contenedores de fedora aparecen con un id de imagen “fantasma”</p> 

```
 docker rm nginx1(o id del contenedor)
```

<p>Podíamos borrarlo de la siguiente manera, pasando esa “id”(contenedor)</p>

```
 docker rm `docker ps -aq | grep 9110ae7f579f`
```


[//]: #
   [documentacion]: <https://docs.docker.com/engine/reference/commandline/exec/>
   

</div>
