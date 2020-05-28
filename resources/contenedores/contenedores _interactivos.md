<div style="vertical-aligh: center;"> 
<h1> Contenedores interactivos </h1> 

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