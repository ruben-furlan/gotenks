<div style="vertical-aligh: center;"> 

# Imagenes 
- FROM--> ubunto --> PADRE 
 - RUN --> apt-get update comando que quiero ejecutar 
 - RUN --> apt-get install -y python todos los comando tiene que ser automáticos (no interactivos) </li>


<p>cada vez que se crea o modifica una imagen se tiene que buildear</p>
<p>Comprobamos el estado: <strong>systemctl status docker</strong></p>
<p>construir imagen: <strong>docker build -t image_python</strong>.(contexto directorio donde me encuentro) , toma información de dockerfiel</p>
<p><strong>docker run  -t image_python python</strong></p>
<hr>

## comando, RUN: 

<p>ademas de poner un comando por linea podemos poner && 
   esto hace que se ejecuten varios comando en una sola capa. si hago varios RUN voy a tener N capaz:</p>
<p>cambios por lo que ha pasado esa imagen: <strong>docker image history imagen_python</strong></p>
<hr>

## comando, RUN: 
<p>es una directiva permite indicar comando por defecto del contenedor, una vez arrancado el contenedor se va a ejecutar los dockerfiel tiene un CMD (si llega a tener varios el que vale es el ultimo)</p>
<p><strong>CMD ["echo","welcome"]</strong>, ejecuta con exec (recomendado) formato json</p>

<hr>

## comando, ENTRYPOINT: 

<p>directiva que al igual que el CMD ejecuta algo cuando arrancamos el contenedor y solo puedes haber uno si hay varios solo toma el ultimo, diferencia --> cuando arranque el contedor se ejecute el comando siempre. te obliga a tener ese comando </p>
<p><strong>ENTRYPOINT["/bin/bash"]</strong>, (recomendaod modo exec)</p>
<p>si me creo un <strong>ENTRYPOINT["df"]</strong>, en un imagen cuando voy a crear un contenedor</p>
<p><strong>docker run -it --rm image_prueba:v2 -h </strong>en realida me esta lanzado un df -h</p>

<hr>

## comand, WORKDIR: 

<p>se tiene que tener en cuenta que el ultimo WD creado es donde esta el contexto. es decir donde esta apuntando al ruta</p>
<p>Determina el directorio de trabajo para directivas, ese comando se realiza bajo el ámbito de workdir</p>
<p>Ejemplo - imagen:</p>

```
 FROM ubunto<br>
 RUN apt-get update<br>
 RUN apt-install -y python<br>
 RUN echo 1.0 >> /etc/version && apt-get install -y git && apt-get install -y iputils-ping<br>
 RUN mkdir /datos<br>
 WORKDIR /datos<br>
 RUN touch f1.tx<br>
 RUN mkdir /datos1<br>
 WORKDIR /datos1<br>
 RUN touch f2.tx<br>
 ENTRYPOINT["/bin/bash"]<br>
```

<p>Se puede tener muchos WORKDIR  con ese podemos tener los comandos en base donde queramos 
   podemos ir construyendo en determinados directorios sin poner el path completo</p>


## comand, COPY-ADD

```
FROM ubunto
RUN apt-get update
RUN apt-install -y python
RUN echo 1.0 >> /etc/version && apt-get install -y git && apt-get install -y iputils-ping

##WORKDIR##
RUN mkdir /datos
WORKDIR /datos
RUN touch f1.tx
RUN mkdir /datos1
WORKDIR /datos1
RUN touch f2.tx

##COPY##
COPY index.html . (. hace referencia al directorio de trabajo /datos1 )
COPY app.log /datos (path completo teniendo en cuenta que nos estamos refirendo al contenedor donde tenemos el dockerfiel )

##ENTRYPOINT##
ENTRYPOINT["/bin/bash"]
```


## comand, ADD: 


```
FROM ubunto
RUN apt-get update
RUN apt-install -y python
RUN echo 1.0 >> /etc/version && apt-get install -y git && apt-get install -y iputils-ping

##WORKDIR##
RUN mkdir /datos
WORKDIR /datos
RUN touch f1.tx
RUN mkdir /datos1
WORKDIR /datos1
RUN touch f2.tx

##COPY##
COPY index.html . (. hace referencia al directorio de trabajo /datos1 )
COPY app.log /datos (path completo teniendo en cuenta que nos estamos refriendo al contenedor donde tenemos el dockerfiel )


##ADD##
ADD docks docks (copia todo un directorio)
ADD f* /datos/ (copiando todo lo que empieza por F al barra datos, copia también admite esto)
ADD f.tar .(se puede copiar ficheros .tar (descomprimir)con el COPY no se puede, podemos traernos datos de una url copy no se puede)

##ENTRYPOINT##
ENTRYPOINT["/bin/bash"]
```


## commad, ENV (variables)

-e o --env
donde puedo poner una variable:

docker run -it --rm -- x=10 image:v4
docker run -it --rm -- x=`hola` image:v4


```
FROM ubunto
RUN apt-get update
RUN apt-install -y python
RUN echo 1.0 >> /etc/version && apt-get install -y git && apt-get install -y iputils-ping

##WORKDIR##
RUN mkdir /datos
WORKDIR /datos
RUN touch f1.tx
RUN mkdir /datos1
WORKDIR /datos1
RUN touch f2.tx

##COPY##
COPY index.html . 
COPY app.log /datos 
##ADD##
ADD docks docks 
ADD f* /datos/ 
ADD f.tar .

##ENV##
ENV dir=/data dir1=/data1
RUN mkdir $dir && mkdir dir1 (puedo tener dos comando run separados con &&)

##ENTRYPOINT##
ENTRYPOINT["/bin/bash"]

```

## command. ARG (variables)
<p>(ARG permite pasar variables al momento de construir la IMAGEN)</p>
<p>donde puedo poner una variable:</p>


```

FROM ubunto
RUN apt-get update
RUN apt-install -y python
RUN echo 1.0 >> /etc/version && apt-get install -y git && apt-get install -y iputils-ping

##WORKDIR##
RUN mkdir /datos
WORKDIR /datos
RUN touch f1.tx
RUN mkdir /datos1
WORKDIR /datos1
RUN touch f2.tx

##COPY##
COPY index.html . 
COPY app.log /datos 
##ADD##
ADD docks docks 
ADD f* /datos/ 
ADD f.tar .

##ENV##
ENV dir=/data dir1=/data1
RUN mkdir $dir && mkdir dir1 (puedo tener dos comando run separados con &&)

##ARG##
ARG dir2 
RUN mkdir $dir2 

(ARG permite pasar variables al momento de construir la IMAGEN)

##ENTRYPOINT##
ENTRYPOINT["/bin/bash"]
```
<p>(construccion de la imagen)</p>
<p><strong>docker build -t image:v6 --build-arg dir2=/data </strong>crea y elimina el contenedor docker run -it --rm image:v6</p>

## command, EXPOSE
<p>permite exponer puertos, indicar que la imagen va un puerto que puede usar públicamente, no se hacen públicos por defaul, ayuda a la persona que va a construir el contenedor que puerto necesita usar, esta imagen esta utilizando el puerto para alguno de los productos que estamos usando</p>

```
FROM ubunto
RUN apt-get update
RUN apt-install -y python
RUN echo 1.0 >> /etc/version && apt-get install -y git && apt-get install -y iputils-ping

##WORKDIR##
RUN mkdir /datos
WORKDIR /datos
RUN touch f1.tx
RUN mkdir /datos1
WORKDIR /datos1
RUN touch f2.tx

##COPY##
COPY index.html . 
COPY app.log /datos 
##ADD##
ADD docks docks 
ADD f* /datos/ 
ADD f.tar .

##ENV##
ENV dir=/data dir1=/data1
RUN mkdir $dir && mkdir dir1 (puedo tener dos comando run separados con &&)

##ARG##
#ARG dir2 
#RUN mkdir $dir2 
#ARG user
#ENV user_docker $user
#ADD add_user.sh /datos1
#RUN /datos1/add_user.sh


##EXPOSE##
RUN apt-get install -y apache2
EXPOSE 80
ADD entrypoint.sh /datos1



##CMD
#script que arranca el apache y ejecuta una bash
CMD /datos1/entrypoint.sh


##ENTRYPOINT##
#ENTRYPOINT["/bin/bash"]

```

## COMMAND, volume
<p>para creear volumenes de manera automaticas</p>

```

FROM ubunto
RUN apt-get update
RUN apt-install -y python
RUN echo 1.0 >> /etc/version && apt-get install -y git && apt-get install -y iputils-ping

##WORKDIR##
RUN mkdir /datos
WORKDIR /datos
RUN touch f1.tx
RUN mkdir /datos1
WORKDIR /datos1
RUN touch f2.tx

##COPY##
COPY index.html . 
COPY app.log /datos 
##ADD##
ADD docks docks 
ADD f* /datos/ 
ADD f.tar .

##ENV##
ENV dir=/data dir1=/data1
RUN mkdir $dir && mkdir dir1 (puedo tener dos comando run separados con &&)

##ARG##
#ARG dir2 
#RUN mkdir $dir2 
#ARG user
#ENV user_docker $user
#ADD add_user.sh /datos1
#RUN /datos1/add_user.sh


##EXPOSE##
RUN apt-get install -y apache2
EXPOSE 80
ADD entrypoint.sh /datos1

##VOLUME##
(pagina es un directorio en la maquina fisica (host mi maquina), se añade el paquete se añade y se sustituyte el directorio pagina a esa ruta)
ADD paginas /var/www/html
VOLUME["var/www/html"]


##CMD
#script que arranca el apache y ejecuta una bash
CMD /datos1/entrypoint.sh


##ENTRYPOINT##
#ENTRYPOINT["/bin/bash"]

```

</div>



