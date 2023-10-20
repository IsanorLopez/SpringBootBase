# Anotaciones

Las anotaciones son aquellas caracteristicas dentro de cada archivo que permiten incrustar informacion addicional dentro del mismo, lo que le permite definir por defecto un determinado comportamiento y/o funcionamiento.  

## @Controller

Determina el comportamiento de una determinada clase como controlador para ser utilizado en bajo el modelo **MVC** o **WebFlux.**  

## @RequestMapping

Permite a una determinada funcion de clase **controlador**, manejar la solicitud que ingresa definida por la ruta establecida. Se puede utilizar tanto a nivel metodo como clase, de manera que a nivel clase se pueda establecer una determinada ruta y cada metodo tenga la opcion de concatenar algo a la ruta a nivel clase para un alcance mas especifico o bien, dejar el alcance a nivel general de clase.  

- value: Determina la ruta de la clase o el metodo para ser consumido
`*Nota: Value viene a ser un alias de path`

- method: requiere una especificacion del tipo de metodo por el que sea consumido **GET,PUT,POST,DELETE** utilizando la clase estatica **RequestMethod**
`*Nota: En caso de no definir esta propiedad especificamente por defult seria de tipo GET`

~~~java
package com.bolsadeideas.springboot.web.app.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;

@Controller
@RequestMapping(value = "/index",method = RequestMethod.GET)
public class IndexController {

    @RequestMapping(value = "/msg")
    public String index() {
        return "index";
    }

}

~~~

## Abreviaciones de @RequestMapping

Para definir un codigo mas limpio se han definido abreviaciones de la anotacion **RequestMapping**, mismas que por su declaracion establecen el metodo por el que seran comsumidas.  

Como defecto su primer parametro es la propiedad **value/path**, por lo que no es necesario especificarlo.  

En caso de que una determinada funcion sea alcanzable por mas de un ruta se define a manera de objeto y separado por comas las multiples rutas.  

### @GetMapping

Establece al metodo de un determinado controlador la ruta para manejar la solicitud que implicitamente, sin necesidad de mas codigo, seria de tipo **GET**

~~~java
package com.bolsadeideas.springboot.web.app.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;

@Controller
@RequestMapping(value = "/index")
public class IndexController {

    @GetMapping({"/index", "/home", "/"})
    public String index() {
        return "index";
    }

}
 
~~~
