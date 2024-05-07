# Acciones SpringBoot

## cambiar nombre de group

Al inicializar un nuevo proyecto dentro de springboot se define la propiedad **group** en la interfaz inicial, etse valor es el configurado para organizar todos los **packages** y **namepaces** del proyecto. A manera opcional se puede definir uno personalizado.  

~~~Interfaz
Group: com.example
Package: com.example
~~~

## Cambio version de java

Para cambiar la version especifica de java a ejcutar desde el aplicativo basta con modificar la version del siguiente tag, esto para cuando desde asistente de creaciond e proyectos la version de java que se busque no este dentro de las opciones

~~~xml
.
.
.
<java.version>17</java.version>
.
.
.
~~~

## Errores de inicio

De manera predefinida cuando el asistente genera un nuevo proyecto marca un par de errores **cvc-elt.1.a: Cannot find the declaration of element 'project'** y **No grammar constraints (DTD or XML Schema)**

El primero se resuelve cambiando el protocolo **http** por **https** de los links iniciales.  

El segundo que detona una vez corregido el primero se resuelve por medio del agregado **DOCTYPE** debajo de la etiqueta **xml**

~~~xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE xml>
.
.
.
<project xmlns="https://maven.apache.org/POM/4.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
.
.
.
~~~
