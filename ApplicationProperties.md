# Application Properties

Archivo donde se definen las configuraciones generales para el API, desde conexiones a BD como variables globales que interactuen con las dependencias o el codigo en si mismo.  

> ../resources/application.properties

## Acceso a las propiedades

Cada propiedad definida dentro de este archivo puede ser accesida para formar parte de la funcionalidad en nuestra **API**, de tal forma que los archivos **.properties** son concentradores de configuracion a nivel global.  

### value

Definiendo la notacion sobre una variable se puede definir como parametro el nombre de la propiedad definida en el archivo, de tal forma que la variable que en cuestion tiene asignada la notacion toma el valor mismo.  

~~~java
import org.springframework.beans.factory.annotation.Value;

@Value("${custom.activeprofileName}")
    private String profile;
~~~

`*Nota: Siempre se retornara el valor como String`

### env

Definiendo la notacion **Autowired** para la instancia de tipo **Enviroment** se genera un nexo con el archivo **.properties** lo que permite accerder por medio de la instancia a los valores definidos en dicho archivo.  

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
