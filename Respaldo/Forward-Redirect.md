# Forward y Redirect  

Ambas instrucciones permiten el servir una determinada ruta definida en alguno de los **controller** del proyecto, la diferencia radica en que **forward** mantiene la **URL** intacta desde donde se implemente, sin importar que ruta este renderizando, mientras que **Redirect** si modifica la **URL** desde donde renderiza y navega hasta ella de esa forma renderiza la ruta escogida.  

~~~java
@Controller
public class HomeController {

    @GetMapping("/")
    public String home() {
        return "forward:/app/index";
    } 

}

@Controller
public class HomeController {

    @GetMapping("/")
    public String home() {
        return "redirect:/app/index";
    } 

}
~~~

~~~java
package com.bolsadeideas.springboot.web.app.controller;

import org.springframework.ui.Model;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.ModelAttribute;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
@RequestMapping("/app")
public class IndexController {

    @Value("${texto.indexcontroller.index.titulo}")
    private String textoIndex;

    @GetMapping({"/index", "/home", "/", ""})
    public String index(Model model) {
        model.addAttribute("titulo", "Hola mundo!");
        model.addAttribute("textoIndex", textoIndex);
        
        return "index";
    }
}
~~~
