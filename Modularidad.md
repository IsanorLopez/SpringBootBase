# Modularidad

Permite definir una estructura jerarquica entre los micro servicios lo que permite implementar una especie de **herencia** entre dependencias y un agrupado par la **compilacion**, las dependecias que se definan a un determinado nivel aplican para todos los microservicios de nivel inferior asi como dependiendo de que nivel se detone la compilacion seran los microservicios que se compilen.  

De este modo se prevee la redundancia de carga para las dependencias estableciendo un archivo **pom** de nivel superior.  

Se permite tambien la organizaacion de un determinado negocio a un nive tecnico.  

Se puede especificar una version especifica de una dependencia para un determinado microservicio si es necesario.  

`*Nota: Este tipo de organizacion es viable solo en escenarios donde el negocio es el mismo`

## Crear modulo padre

> File > new project > Java with maven > POM project

## Crear modulo hijo

Es necesario definir dentro de un modulo hijo sea microservicio o un nodo POM mas, su relacion directa con el padre haciendo uso de la etiqueta **parent** y definiendo los atributos correspondientes al padre.  

> [Proyecto padre] > Modules > [create/add existing module]

~~~yaml
<parent>
    <groupId>com.paymentchain.businessdomain</groupId>
    <artifactId>bussinesdomain</artifactId>
    <version>1.0-SNAPSHOT</version>
</parent>
~~~

## Redundancias

De trabajar de esta forma se debe cuidar el tema de las importanciones de dependencias redundantes ya que se pueden importar tanto a nivel de padre como a nivel de hijos.  
