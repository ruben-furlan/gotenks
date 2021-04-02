<div style="vertical-aligh: center;"> 

# Volumenes 

<p>Un volumen es un directorio o un fichero en el docker engine que se monta directamente en el contenedor. Podemos montar varios volúmenes en un contenedor y en varios contenedores podemos montar un mismo volumen.</p>

[documentacion] - oficial 

## Crear un volumen en el contenedor 

<p>volumnes:</p>
<p> Mientras exista un contendor apuntando al volumen está vivo "recuperable" si se borran todos los conteneros que apunta al volumen, quedan la información pero si quiero volverlo a montar tengo que </p>
<p> se puede crear volumnes read onli(ro)  </p>
   

```
  docker run it --name ubunto8 - v volt:data:ro ubunto
```

<p>Nos vamos a <strong>/var/docker/lib/volumes</strong> . Comprobamos los directorios que hay, si tenemos alguno Lanzamos un contenedor y le asociamos un volumen, por ejemplo con Fedora. El directorio del contenedor es <strong>/datos</strong> </p>

```
 docker run -it --name fedora1 -v /datos fedora bash
```
<p> Nos habrá creado un directorio y un volumen:</p>

```
  ls -l
```

<p>Si nos vamos al directorio _data del volumen debe aparecer: </p>


<p>Si ahora creamos un fichero en ese directorio debe aparecer en /datos   del contenedor Por último salimos del contenedor 
Si comprobamos los volúmenes, debe seguir existiendo, ya que n o se borra cuando el contenedor se par</p>
                                                    
```
  docker volume ls
```                                                  
                                                   


[//]: #
   [documentacion]: <https://docs.docker.com/storage/volumes/>
   
 </div>


