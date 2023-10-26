# Controller

Clase que permite definir dentro de ella todas las funciones que estaran habilitadas a ser consumidas, sea por una vista o bien un recurso externo que se conecte al aplicatio para ser consumido.  

`*Nota: Por funcionalidad todo controller debe ser publico del mismo modo que sus funciones, adema de deffinirse con la anotacion @Controller`

## Pasar datos de un controller a la vista

Dentro de la funcionalidad del aplicativo y sobre todo si se esta utilizando el patron **MVC**, los controladores deberan suministrar informacion a las vistas y por tanto se utilizan las siguientes tecnicas.  

### Model

Es por mucho la mas popular

~~~java
package com.bolsadeideas.springboot.web.app.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.ui.Model;

@Controller
public class IndexController {

    @GetMapping({"/index", "/home", "/"})
    public String index(Model model) {
        model.addAttribute("titulo", "Hola mundo cruel!!!");
        return "index";
    }

}
~~~

~~~java
package com.bolsadeideas.springboot.web.app.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.ui.ModelMap;

@Controller
public class IndexController {

    @GetMapping({"/index", "/home", "/"})
    public String index(ModelMap model) {
        model.addAttribute("titulo", "Hola mundo !!");
        return "index";
    }

}
~~~

~~~java
package com.bolsadeideas.springboot.web.app.controller;

import java.util.Map;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;

@Controller
public class IndexController {

    @GetMapping({"/index", "/home", "/"})
    public String index(Map<String, String> map) {
        map.put("titulo", "Hola mundo map !!");
        return "index";
    }

}
~~~

~~~java
package com.bolsadeideas.springboot.web.app.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.servlet.ModelAndView;
import org.springframework.web.bind.annotation.GetMapping;

@Controller
public class IndexController {

    @GetMapping({"/index", "/home", "/"})
    public ModelAndView index(ModelAndView mv) {
        mv.addObject("titulo", "Hola mundo cruel!!!");
        mv.setViewName("index");
        return mv;
    }

}
~~~

### configuracion de la vista

Se cual sea el metodo de envio de informacion a la vista esta debe configurarse para recibir la informacion enviada por el controlador , donde **xmlns:th** especifica la ruta relacionada a thymeleaf y par hcer uso de los valores se utiliza la instruccion **th**.  

~~~html
<!DOCTYPE html>
<html lang="en" xmlns:th="http//www.thymeleaf.org">
<head>
    <meta charset="UTF-8"/>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title th:text="${titulo}" />
</head>
<body>
    <h1 th:text="${titulo}"/>
</body>
~~~
