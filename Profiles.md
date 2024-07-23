# Profiles

Tecnica que permite definir configuraciones globales en funcion de un ambiente sobre el que correra nuestra **API**, con la finalidad de switchear entre ambientes desde el momento en que se levanta al **.jar**  

## properties

Por default un proyecto tomara siempre como base su **application.properties** como archivo principal y se ejecutara e base a el.

Para definir archivos de configuracion para distintos ambientes basta con definirse un archivo **.properties** o **.yaml** con el sufijo **application** pero agregando un guion seguido del nombre del ambiente:  

- Produccion: **application.properties**
- Desarrollo: **application-dev.properties**
- Desarrollo: **application-prod.yaml**
