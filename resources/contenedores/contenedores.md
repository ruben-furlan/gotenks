<div style="vertical-aligh: center;"> 
<h1> Contenedores </h1> 

<h4> Arrancar y parar los servicios de Docker </h4>
<br> 
<p>Arrancarlo ahora con SYSTEMCTL: <strong>systemctl start Docker</strong></p>
<p>Comprobamos el estado: <strong>systemctl status docker</strong></p>
<p>Activamos el servicio para que funcione al arrancar el servidor: <strong>systemctl enable docker</strong></p>
<hr>

<h4> Vamos a crear nuestro primer contenedor </h4>

<p><strong>docker run hello-world</strong></p>
<p>Comprobar que el contenedor no está activo, ya que se cierra en cuanto sale el mensaje: <strong>docker ps</strong></p>
<p>Comprobar que el contenedor se ha creado, pero que está parado: <strong>docker ps -a</strong></p>
<p>Comprobar que existe la imagen: <strong>docker ps -a</strong></p>
<p> Creamos un nuevo contenedor basado en otra imagen de Docker Hub  denominada busybox, que es un contenedor con un cierto número de
   utilidades: <strong>docker run busybox</strong></p>
<p>Comprobamos el nuevo contenedor: <strong>docker ps -a</strong></p>
<p>Comprobar que existe la imagen: <strong>docker images</strong></p>
<p>Visualizar solo las ids de los contenedores : <strong>docker ps -aq</strong></p>
<p>Ver los dos últimos contenedores lanzados: <strong>docker ps -a -n 2</strong></p>
<p>Comprobar el espacio utilizado por los contenedores creados: <strong>docker ps -a -s</strong></p>
<p>También podemos usar la opción -f para filtrar por algún dato concreto,
   por ejemplo, por el nombre. Busca por el contenido dentro del texto. : <strong>docker ps -a -f name=davinci</strong></p>

<hr>
<h4>Notas:</h4> 



      
</div>
