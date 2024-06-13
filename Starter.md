# Starter

Permite un manejo de dependencias mas eficiente, ya que por medio de un **starter** se pueden definir las dependencias necesarias pero no su version, de tal forma que dos proyecto pueden cargar el mismo **starter** y **SpringBoot** se encargara de asignarle la version adecuada de las dependencias a cada uno.  

[Documentacion](https://docs.spring.io/spring-boot/reference/using/build-systems.html#using.build-systems.starters)

## Propertie de version

Se debe definir a manera configurable en una propertie la version que se esta implementando en el API.  

## Manejador de dependencias

Permite a los **starters** tomar la version que se defina dentro de su propiedad **version**, tanto en codigo duro como en la utilizacion de variables definidas en **properties**

~~~yaml
.
.
.
<properties>
    <spring-boot.version>3.2.2</spring-boot.version>
</properties>
.
.
.
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-dependencies</artifactId>
            <version>${spring-boot.version}</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>  
.
.
.
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-test</artifactId>
        <scope>test</scope>
        <!--If want exclude junit4 and use only junit5-->
        <exclusions>
            <exclusion>
                <groupId>org.junit.vintage</groupId>
                <artifactId>junit-vintage-engine</artifactId>
            </exclusion>
        </exclusions>
    </dependency>  
~~~
