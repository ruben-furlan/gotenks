<div style="vertical-aligh: center;"> 

# Redes en docker  
## Breve explicación de los puertos en Docker </h4>

- Un contenedor puede tener aplicaciones que necesiten ser accedidas desde fuera del contenedor, por ejemplo Apache o Tomcat
- Por defecto los puertos de un contenedor son privados y no pueden ser accedidos
- Debemos hacerlos públicos y mapearlos con un puerto del host


<p>nota:</p>  
<p>Si se crean redes se pueden ver los contenedores entre si, por defecto no lo hace. </p>
<p>el por defecto de <strong>name = bridge</strong> no lo hace se tiene que hacer </p>
<p>pasos para lograr que se vean entre si.(hacer ping)</p>


<p> para <strong>name = bridge --link</strong> (legacy "no está soportado, no se recomienda" crear nueva red)</p>
<p> busybox - verificar que todo nuestro entorno este bien</p>
<p> sirve para probar componentes(hacer ping para comprobar que este enlazado por ejemplo)</p>

<p> para enlanzar se recomienda cuando se enlazan es recomendable poner el nombre sino te ponen un uuid generico</p>

 </div>


