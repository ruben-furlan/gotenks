<div style="vertical-aligh: center;"> 
<h1> Redes en docker </h1> 
<h4> Breve explicación de los puertos en Docker </h4>
<br> 
<ul>
<li type="circle">Un contenedor puede tener aplicaciones que necesiten ser accedidas desde fuera del contenedor, por ejemplo Apache o Tomcat</li>
<li type="circle"> Por defecto los puertos de un contenedor son privados y no pueden ser accedidos</li>
<li ttype="circle">Debemos hacerlos públicos y mapearlos con un puerto del host</li>
</ul>

<p>nota:  
- Si se crean redes se pueden ver los contenedores entre si, por defecto no lo hace. el por defecto de name = bridge no lo hace se tiene que hacer pasos para lograr que se vean entre si.(hacer ping)

para name = bridge --link (legacy "no está soportado, no se recomienda" crear nueva red)
busybox - verificar que todo nuestro entorno este bien
sirve para probar componentes(hacer ping para comprobar que este enlazado por ejemplo)

para enlanzar se recomienda cuando se enlazan es recomendable poner el nombre sino te ponen un uuid generico
</p>
 </div>


