<div style="vertical-aligh: center;"> 
<h1> Docker exec </h1> 
<p>
docker exec: https://docs.docker.com/engine/reference/commandline/exec/
</p>
<p>Arrancamos un contenedor basado en la imagen NGINX en modo background: <strong>docker run -d --name nginx1 nginx</strong></p>  
<p>Comprobamos que está funcionando: <strong>docker ps</strong></p>  
<p>Lanzamos algún comando contra el contenedor con “EXEC”. Visualizar los ficheros de /: <strong>docker exec nginx1 ls /</strong></p>  
<p>Podemos lanzar varios comandos al mismo tiempo. Por ejemplo la fecha  y nombre del sistema: <strong>docker exec nginx1 date ; uname -n</strong></p>  
<p>Por supuesto, podemos entrar en una Shell si es necesario, indicando que es interactivo: <strong>docker exec -it nginx1 bash
</strong> una vez dentro del ubunto lanzar un ls y da el mismo resultado</p>  
<p>Salimos y paramos el contenedor: <strong>docker stop nginx1</strong></p>  
<p>Comprobamos que existe: <strong>docker ps -a</strong></p>  


<h1> Borrados</h1> 
<p>Borramos el contenedor. Comprobamos que no está: <strong>docker rm nginx1(o id del contenedor)</strong></p>  
<p>Borramos imagenes. si esa imagen esta siendo usada por un contenedor no se podra eliminar : <strong>docker rm nginx1(o id del contenedor)</strong></p> 
<p>ejemplo del error :
Error response from daemon: conflict: unable to remove
repository reference "fedora" (must force) - container
28b5e0c7b73c is using its referenced image 9110ae7f579f
</p> 
<p>Si se aplica al eliminar la imagen un -f (force) , Los contenedores de fedora aparecen con un id de imagen “fantasma”
: <strong>docker rm nginx1(o id del contenedor)</strong></p> 

<p>Podíamos borrarlo de la siguiente manera, pasando esa “id”(contenedor) <strong>docker rm `docker ps -aq | grep 9110ae7f579f`</strong> </p>

</div>
