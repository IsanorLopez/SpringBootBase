# Directiva IF

Nos permite el renderizado condicional de un determinado elemento en base la interaccion con el **controller**, esta acomplamiento entre vista y controlador es gracias a **thymeleaf**.  

~~~java
@GetMapping("/listar")
public String listado(Model model) {
    
    List<Usuario> usuarios = new ArrayList<>();

    model.addAttribute("titulo", "Listado de usuarios");

    model.addAttribute("usuarios", usuarios);
    
    return "listado";
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
    <span th:if="${usuarios.size() == 0 }" th:text="'no hay usuarios a mostrar'"/>
</body>

~~~
