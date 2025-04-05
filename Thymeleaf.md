# Thymeleaf

Motor de plantillas que permite definir vistas en formato **HTML** conectadas a un **controller**, generando asi el acoplamiento necesario para el patron **MVC**  

## Model

Intrerface de springboot que permite ser inyectada dentro de una **controller**, la cual permite definir atributos con **addAttribute** que seran renderizados dinamicamente sobre la vista **html** que devuelva la **request**.  

## th

De lado de la vista para acceder a los valores y renderizarlos sobre estrsucturas html, es necesario primero cargar **thymeleaf** en la etiqueta por defecto **html** de la vista, definiendo la url haca el sitio para cargar mediante **CDN** la funcionalidad.  

Una vez caragda, se hace uso de los valores por medio de la instruccion **th** y el tipo **text** como un atributo para las etiquetas html que lo renderizara, para terminar el renderizado se hace uso por medio de la notacion **${ [nombreDelAtributo] }**.  

~~~java
@Controller
public class UserController {

    @GetMapping("/details")
    public String details(Model model) {

        model.addAttribute("Title", "Spring Boot Application");
        model.addAttribute("Name", "Isanor Lopez");

        return "details";
    }

}
~~~

~~~html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title th:text="${ Title }"></title>
</head>
<body>
    <h1 th:text="${ Title }"> Hola mundo desde SpringBoot </h1>
    <h2 th:text="${ Name }"/>
</body>
</html>
~~~

`*Nota: No importa que definicion de valor pueda tener una etiqueta html,si esta utilizando un valor desde Model este sera el que termine renderizando, dado que la renderizacion es posterior al primer maquetdao en pantalla del DOM`  
