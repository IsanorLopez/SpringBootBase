# Comandos Springboot

## Generar compilado

> [CarpetaDelProyecto]\

~~~cmd
    .\mvnw.cmd package
~~~

## Levantar aplicacion compilada  

~~~cmd
    java -jar .\target\[proyecto]-0.0.1.jar
~~~

### Alternativa con VsCode

~~~CMD
    & 'C:\Program Files\Java\jdk-17\bin\java.exe' '[ obtener de vsCode ]' 'com.paymentchain.customer.CustomerApplication'
~~~

### Definir ambiente de ejecucion

Cuando se tienen multiples archivos de configuracion dirigidos hacia ambientes diferentes, basta con agregar un flag mas en el comando de ejecucion del **jar**, definiendo cual es el archivo que tomara para ejecutarse.  

- **application.properties**
- **application-dev.properties**

~~~CMD
    java -jar .\target\[proyecto]-0.0.1.jar --spring.profiles.active=dev

    & 'C:\Program Files\Java\jdk-17\bin\java.exe' '[ obtener de vsCode ]' 'com.paymentchain.customer.CustomerApplication' '--spring.profiles.active=dev'
~~~

`*Nota: Es necesario solo definir la parte del nombre distintiva entre un archivo y otro, ignorando los dos guiones --`

## Obtener dependencias de Maven forzado

~~~cmd
    mvn clean package -U
~~~
