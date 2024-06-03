# Swagger

Conjunto de herramientas enfocado en disenar y documentar el contrato de interfaz que puede llegar a tener una determinada **API**.  

- [Swagger y SpringBoot](https://springdoc.org/#getting-started)

## Dependencia

Dentro del contexto de **Springboot** se puede definir como una herramienta que apoya en tiempo de desarrollo a ir dando forma visual a todas las entiedades que convergen en una determinada **API**, **Entity**, **Enpoints** definidos en el **controller**, etc.  

~~~xml
    <dependency>
        <groupId>org.springdoc</groupId>
        <artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
        <version>2.5.0</version>
    </dependency>
~~~

~~~URL
    http://server:port/context-path/swagger-ui.html
~~~

## Desactivar

Es recomendable desactivar cuando se despligue a produccion, esto relacionado a la funcionalidad que implementa de consumir el **API** ya que no se cuenta con seguridad.  

> ../resources/application.properties

~~~properties
    springdoc.api-docs.enabled=false
~~~
