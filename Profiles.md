# Profiles

Tecnica que permite definir configuraciones globales en funcion de un ambiente sobre el que correra nuestra **API**, con la finalidad de switchear entre ambientes desde el momento en que se levanta al **.jar**  

[Spring Config](https://docs.spring.io/spring-cloud-config/docs/current/reference/html/#_spring_cloud_config_server)

## properties

Por default un proyecto tomara siempre como base su **application.properties** como archivo principal y se ejecutara e base a el.

Para definir archivos de configuracion para distintos ambientes basta con definirse un archivo **.properties** o **.yaml** con el sufijo **application** pero agregando un guion seguido del nombre del ambiente:  

- Local: **application.properties**
- Desarrollo: **application-dev.properties**
- Produccion: **application-prod.yaml**

## Configuracion con repo en GIT

Las configuraciones que se deben definir son principalmente la ruta del repositorio, seguido de la configuracion en **true** para hacer un clonado la primera vez que se ejecute el **API** y por ultimo la rama de la cual se estaria haciendo el clonado.  

~~~properties
    spring.cloud.config.server.git.uri=file:///C:/PROYECTOS-ISA/S_Configuraciones/
    spring.cloud.config.server.git.clone-on-start=true
    spring.cloud.config.server.git.default-label=main
~~~

### Comprobacion de carga de profile

~~~URL
    http://localhost:8888/[Nombre de archivo de propiedades sin extension]/profile
~~~
