<div style="vertical-aligh: center;"> 
<h1> Docker logs, stats, top, kill</h1> 

<h5>Docker logs</h5>
<p>Arrancamos un contenedor basado en la imagen NGINX en modo background: <strong>docker run -d --name nginx1 nginx
</strong></p>
<p>Comprobamos que está funcionando: <strong>docker ps</strong></p>
<p> Comprobamos si hay algún log. Debe salir vacio : <strong>docker logs nginx1</strong></p>
<p>Nos conectamos al contenedor desde otro terminal: <strong>docker exec -it nginx1 bash</strong></p>
<p>Instalamos el comando wget en el contenedor: <strong>apt-get update    apt-get install wget</strong></p>
<p>Por supuesto, podemos entrar en una Shell si es necesario, indicando que es interactivo: <strong>docker exec -it nginx1 bash</strong></p>
<p>Lanzamos un “wget” contra el servidor nginx del contenedor: <strong>wget localhost</strong></p>
<p>Comprobamos con el comando Docker top los procesos que se están
   ejecutando en el contenedor  Podemos ver que está el nginx y además la bash con la que hemos
   entrado desde Docker exec <strong>docker top nginx1</strong></p>
   
<p>continua....</p>
<h5>Docker stats</h5>
<p> Vemos ahora las estadísticas de uso del contenedor<strong>dnocker stats nginx1(nombre o id del contenedor)</strong></p>
<h5>Docker kill</h5>
<p>Por último, matamos el contenedor en vez de pararlo
<strong>docker kill nginx1</strong></p>
</div>