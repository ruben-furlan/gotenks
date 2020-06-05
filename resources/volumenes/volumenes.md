<div style="vertical-aligh: center;"> 
<h1> Volumenes </h1> 
<h4> Crear un volumen en el contenedor </h4>
<br> 


<p>volumnes:
   Mientras exista un contendor apuntando al volumen está vivo "recuperable" si se borran todos los conteneros que apunta al volumen, quedan la información pero si quiero volverlo a montar tengo que 
   se puede crear volumnes read onli(ro)
   docker run it --name ubunto8 - v volt:data:ro ubunto
</p>


<p>Nos vamos a /var/docker/lib/volumes . Comprobamos los directorios que hay, si tenemos alguno Lanzamos un contenedor y le asociamos un volumen, por ejemplo con Fedora. El directorio del contenedor es /datos 
:<strong>docker run -it --name fedora1 -v /datos fedora bash</strong></p>
<p> Nos habrá creado un directorio y un volumen: <strong>ls -l</strong></p>
<p>Si nos vamos al directorio _data del volumen debe aparecer: <strong></strong></p>
<p>Si ahora creamos un fichero en ese directorio debe aparecer en /datos
   del contenedor Por último salimos del contenedor Si comprobamos los volúmenes, debe seguir existiendo, ya que n o se
                                                    borra cuando el contenedor se par<strong>docker volume ls</strong></p>


 </div>


