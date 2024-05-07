# Directiva Each

Permite generar iteraciones hasta recorrer un determinado arreglo o lista proveniente del controller.  Dentro e cada iteracion de puede generar un nuevo elemento **HTML**

~~~java
@GetMapping("/listar")
public String listado(Model model) {
    
    List<Usuario> usuarios = Arrays.asList(
        new Usuario("Jan", "Doe", "Jan@correo.com"), 
        new Usuario("Jhon", "Doe", "Jhon@correo.com"),
        new Usuario("Isanor", "Lopez", "isanor@correo.com"),
        new Usuario("tornado", "Lopez", "isanor@correo.com")
    );

    /*List<Usuario> usuarios = new ArrayList<>();

    usuarios.add(new Usuario("Jan", "Doe", "Jan@correo.com"));
    usuarios.add(new Usuario("Jhon", "Doe", "Jhon@correo.com"));
    usuarios.add(new Usuario("Isanor", "Lopez", "isanor@correo.com"));*/

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
