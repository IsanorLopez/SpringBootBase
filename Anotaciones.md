# Anotaciones

Las anotaciones son aquellas caracteristicas dentro de cada archivo que permiten incrustar informacion addicional dentro del mismo, lo que le permite definir por defecto un determinado comportamiento y/o funcionamiento.  

## @Controller

Determina el comportamiento de una determinada clase como controlador para ser utilizado en bajo el modelo **MVC** o **WebFlux.**  

## @RequestMapping

Permite a una determinada funcion de clase **controller**, manejar la solicitud que ingresa definida por la ruta establecida. Se puede utilizar tanto a nivel metodo como clase, de manera que a nivel clase se pueda establecer una determinada ruta y cada metodo tenga la opcion de concatenar algo a la ruta a nivel clase para un alcance mas especifico o bien, dejar el alcance a nivel general de clase.  

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

## @ModelAttribute

Permite establecer a cada uno de los **handlers** de un **controller** un determinado atributo(Lista, variable, valor, etc), de manera que cada uno disponga de este y pueda utilizarlo para renderizarlo en su vista.  Es una manera de centralizar cierta informacion que puede ser util entre **handlers**

~~~java
 @GetMapping("/listar")
public String listado(Model model) {
    
    /*List<Usuario> usuarios = new ArrayList<>();

    usuarios.add(new Usuario("Jan", "Doe", "Jan@correo.com"));
    usuarios.add(new Usuario("Jhon", "Doe", "Jhon@correo.com"));
    usuarios.add(new Usuario("Isanor", "Lopez", "isanor@correo.com"));*/

    model.addAttribute("titulo", "Listado de usuarios");
    
    return "listado";
}

@ModelAttribute("usuarios")
public List<Usuario> obtenerUsuarios(){
    List<Usuario> usuarios = Arrays.asList(
        new Usuario("Jan", "Doe", "Jan@correo.com"), 
        new Usuario("Jhon", "Doe", "Jhon@correo.com"),
        new Usuario("Isanor", "Lopez", "isanor@correo.com"),
        new Usuario("tornado", "Lopez", "isanor@correo.com")
    );

    return usuarios;
}
~~~

~~~html
<!DOCTYPE html>
<html lang="en" xmlns:th="http//www.thymeleaf.org">
<head>
    <meta charset="UTF-8"/>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title th:text="${titulo}" />
</head>
<body>
    <span th:text="${titulo}"/>
    <br/>
    <span th:if="${usuarios.isEmpty()}" th:text="'no hay usuarios a mostrar'"/>
    
    <table th:if="${!usuarios.isEmpty()}" >
        <thead>
            <tr>
                <th>Nombre</th>
                <th>Apellido</th>
                <th>Correo</th>
            </tr>
        </thead>
        <tbody>
            <tr th:each="usuario: ${usuarios}">
                <td th:text="${usuario.nombre}"></td>
                <td th:text="${usuario.apellido}"></td>
                <td th:text="${usuario.correo}"></td>
            </tr>
        </tbody>
    </table>  
</body>
~~~

## @RequestParam

Permite el leer parametros enviados por medio de la URL, donde **defaultValue** nos permite definir un valor por defecto en el consumo del **endpoint**, por otro lado **required** define si el parametro debe o no ser suministrado a la hora de consumir el endpoint.  

### ejecucion de ruta con parametro

Para este escenario se determina la ruta por medio de un **@**, armando el **path** y entre **()** especificando los parametros requerido para alcanzar la ejecucion del **controller**

### multiples parametros

La ejecucion con multiples parametros permite el envio de distintos tipos, mismos que deben estar declarados en el **controller** asociado a la ruta

### HttpServletRequest

Como alternativa al uso de **@RequestParam** esta **HttpServletRequest**, que como tal permite el recibir los parametros enviados al **controller** sin especificar, despues haciendo uso de los mismos considerando el tipo que son, sin embargo esta instruccion es anticuada y no fomenta el uso de buenas practicas ya que requiere por deficion, mas logica para manejar la conversion del tipo de los parametros.  

~~~java
package com.bolsadeideas.springboot.web.app.controller;

import org.springframework.ui.Model;
import jakarta.servlet.http.HttpServletRequest;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestParam;


@Controller
@RequestMapping("/params")
public class ParamsController {

    @GetMapping("/")
    public String param() {
        return "params/index";
    }

    @GetMapping("/string")
    public String param(Model model, @RequestParam(defaultValue = "", required = false) String texto) {
        model.addAttribute("parametro", "el mensaje es: " + texto);
        return "params/ver";
    }

    @GetMapping("/mix-params")
    public String param(Model model, @RequestParam String saludo, @RequestParam Integer numero) {
        model.addAttribute("parametro", "El saludo es: " + saludo + " El numero es: " + numero + "");
        return "params/ver";
    }

    @GetMapping("/mix-params-httpRequest")
    public String param(Model model, HttpServletRequest request) {

        String saludo = request.getParameter("saludo");
        Integer numero = null;

        try {
            numero = Integer.parseInt( request.getParameter("numero") );
        } catch () {
            numero = 0;
        }

        model.addAttribute("parametro", "El saludo es: " + saludo + " El numero es: " + numero + "");
        return "params/ver";
    }

}
~~~

~~~html
<!DOCTYPE html>
<html lang="en" xmlns:th="http//www.thymeleaf.org">
<head>
    <meta charset="UTF-8"/>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title th:text="ver" />
</head>
<body>
    <ul>
        
        <li>
            <a th:href="@{/params/string(texto='!Hola mundo!')}"> /params/string/'!Hola mundo!'</a>
        </li>

        <li>
            <a th:href="@{/params/string(texto='!Mundo hola!')}"> /params/string/'!Mundo hola!'</a>
        </li>

        <li>
            <a th:href="@{/params/mix-params( saludo = '!Hola mundo!', numero = 9)}"> /params/mix-params'!hola mundo!'&9</a>
        </li>

        <li>
            <a th:href="@{/params/mix-params( saludo = '!Hola mundo!', numero = 5)}"> /params/mix-params-httpRequest'!hola mundo!'&5</a>
        </li>

    </ul>
</body>
~~~

`*Nota: El nombrado similar entre funciones del controller solo se permite cuando los parametros a recibir varian, tecnica denominada como sobre carga`
