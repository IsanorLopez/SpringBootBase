# Constants

En aras de buscar una funcionalidad configurable dentro de los microservicios, es posible definir valores **constantes** que pueden ser reutilizados dentro del codigo, esto logra estandarizar mensajes, valores y propiedades.  

`*nota: Los valores definidos como constantes forman parte del compilado final a .jar, por lo que son inaccesibles para redefinirse una vez desplegado el servicio`  

> ../java/[proyecto]/constant

~~~java
public final class webApiConstant {

    public static final String MESSAGE = "Spring Boot Application REST";

}
~~~

~~~java
package com.isanor.webapi.controller;

import com.isanor.webapi.constant.webApiConstant;

import java.util.Map;
import java.util.HashMap;

@RestController
@RequestMapping("${basePath}") //Properties
public class UserRestController {

    @GetMapping("${endpoint}") //Properties
    public Map<String, Object> details() {

        Map<String, Object> response = new HashMap<>();

        response.put("Title", webApiConstant.MESSAGE); //Constant
        response.put("Name", "Isanor Lopez");

        return response;
    }

}
~~~
