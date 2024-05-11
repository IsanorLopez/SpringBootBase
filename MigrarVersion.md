# Migrar version de springBoot

Para ralizar un cambio de version sobre springBoot es necesario modificar el **pom.xml** y cambiar el tag de **version**, ademas de establecer el **java.version** en funcion a la version que se este migrando.  

~~~xml
<parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>3.2.5</version>
        <relativePath/>
</parent>
.
.
.
<properties>
    <java.version>17</java.version>
</properties>
~~~
