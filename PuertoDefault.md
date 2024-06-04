# Puerto por default

El default para tomcat una vez que se ejecuta es el puerto **8080**, en caso de requerir que se levante el API en un puerto distinto hay que definir o bien modificar la propiedad de **server.port**.  

> ../src/main/resources/application.properties

~~~properties
.
.
.
server.port=8081
~~~

`*Nota: Por default no viene definida la propiedad.`
