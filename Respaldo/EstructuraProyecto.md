# Estructura de proyecto

## Dependencias de Maven

- [Proyecto] > Maven Dependencies  

Paquetes necesarios para que esta herramienta gestione el proyecto e inclusive la compilacion del mismo.  

## properties

- [Proyecto] > src/main/resources > application.properties

Archivo destinado a contener las configuraciones especificas para el proyecto, como el puerto a utilizar, las configuraciones a BD, URL centralizada, etc.  

`*Nota: No utilizar espacios en blanco una vez que se defina el valor de una propiedad`

## static

- [Proyecto] > src/main/resources > static

Carpeta destinada a conetnber toda entidad estatica dentro del proyecto, scripts js, imagenes, etc

## Templates

- [Proyecto] > src/main/resources > templates

Contiene las vistas asignadas a los controladores

## application.java

- [Proyecto] > src/main/java > [Proyecto] > [nombreDelProyecto]Application.java

Main del aplicativo, siendo el punto de entrada principal del proyecto

## target

- [Proyecto] > target

Directorio que contiene el aplicativo una vez generado.  
