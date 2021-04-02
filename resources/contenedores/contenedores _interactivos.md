<div style="vertical-aligh: center;"> 

# Contenedores interactivos 


<p>Vamos a crear un contenedor interactivo con una imagen de Fedora:</p>  

```
  docker run hello-world
```
<p>Podemos ver los datos del sistema operativo:</p>  

```
  uname -a
```

<p>Desde otro terminal, comprobamos si el contenedor está activo:</p>  

```
 docker ps
```

<p>Podemos ver las imágenes donde está la que acabamos de descargar:</p>  

```
  docker images
```

<p>Hacemos por ejemplo un upgrade del sistema:</p>  

```
yum upgrade
```

<p>Intentamos hacer un wget y vemos que no existea:</p>  

```
  wget
```
<p>Lo instalamos:</p>  

```
  yum install wget
```

<p>Ya podemos usarlo:</p>  

```
  wget www.oracle.com
```
<p>Hacemos un exit del contenedor</p>  
<p>Podemos comprobar que ya no está activo, que ese encuentra entre los parados:</p>  

```
  docker ps y docker ps -a
```


<p>Ahora lo volvemos a arrancar.</p>

```
   docker start -i c284
```
<p>Desde otro terminal lo vamos a parar y comprobamos.</p>

```
   docker stop c284 (id del contenedor)
```

</div>