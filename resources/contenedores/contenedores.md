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
<h4>Contenedores interactivos</h4> 

<p>Vamos a crear un contenedor interactivo con una imagen de Fedora: <strong>docker run hello-world</strong></p>  
<p>Podemos ver los datos del sistema operativo: <strong>uname -a</strong></p>  
<p>Desde otro terminal, comprobamos si el contenedor está activo: <strong>docker ps</strong></p>  
<p>Podemos ver las imágenes donde está la que acabamos de descargar: <strong>docker images</strong></p>  
<p>Hacemos por ejemplo un upgrade del sistema: <strong>yum upgrade</strong></p>  
<p>Intentamos hacer un wget y vemos que no existea: <strong>wget</strong></p>  
<p>Lo instalamos: <strong>yum install wget</strong></p>  
<p>Ya podemos usarlo: <strong>wget www.oracle.com</strong></p>  
<p>Hacemos un exit del contenedor</p>  
<p>Podemos comprobar que ya no está activo, que ese encuentra entre los parados: <strong>docker ps y docker ps -a</strong></p>  
<p>Ahora lo volvemos a arrancar. <strong>docker start -i c284</strong> (id del contenedor)</p>
<p>Desde otro terminal lo vamos a parar y comprobamos. <strong>docker stop c284</strong> (id del contenedor)</p>
      
</div>
