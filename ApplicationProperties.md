# Application Properties

Archivo donde se definen las configuraciones generales para el API, desde conexiones a BD como variables globales que intervengan en la configuracion del microservicio.  

> ../resources/application.properties

## Acceso a las propiedades

Cada propiedad definida dentro de este archivo puede ser accedida para formar parte de la funcionalidad en nuestra **API**, de tal forma que los archivos **.properties** son concentradores de configuracion a nivel global.  

### value

Definiendo la notacion sobre una variable se puede definir como parametro el nombre de la propiedad definida en el archivo, de tal forma que la variable que en cuestion tiene asignada la notacion toma el valor mismo.  

~~~java
import org.springframework.beans.factory.annotation.Value;

@Value("${custom.activeprofileName}")
    private String profile;
~~~

`*Nota: Siempre se retornara el valor como String`

### env

Definiendo la notacion **Autowired** para la instancia de tipo **Enviroment** se genera un nexo con el archivo **.properties** lo que permite acceder por medio de la instancia a los valores definidos en dicho archivo.  

~~~java
import org.springframework.core.env.Environment;

@Autowired
private Environment env;

@GetMapping("/check")
    public String check() {
        return "Hi, your property value is :" + env.getProperty("custom.activeprofileName");
    }
~~~

`*Nota: Siempre se retornara el valor como String`

## Implementacion endpoints

Se puede definir una propiedad global para ser utilizada de manera configurable en un determinado **endpoint**, mismo que tendra la habilidad de ser dinamico una vez en **produccion**, la implementacion se puede hacer desde un punto global en el **RequestMapping** que plicaria para todos los **endpoints** o bien a nivel de **endpoint individual**.  

~~~properties
basePath=/desarrollo/detalles-management/api/v1
endpoint=/details
~~~

~~~java
@RestController
@RequestMapping("${basePath}") //Global
public class UserRestController {

    @GetMapping("${endpoint}") //Especifico
    public Map<String, Object> details() {

        Map<String, Object> response = new HashMap<>();

        response.put("Title", "Spring Boot Application REST");
        response.put("Name", "Isanor Lopez");

        return response;
    }

}
~~~
