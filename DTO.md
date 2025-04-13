# DTO

Patron que permite la transferencia de informacion entre capaz, cuentan con las mismas cualidades que una **clase** donde se definen las propiedades que conformaran a la determinada entidad, la ventaja de trabajar con **DTOs** es que se pueden definir entidades complejas para retornar respuestas requeridas para determinados **endpoints** que conforman el **API**.  

## Integracion con lombok

Es posible definir por medio de la notacion **data**  de esta libreria la clase, para asi brindar la facilidad de la autoimplementacion de **getters** y **setters** para sus propiedades.  

~~~java
public class User {

    private String name;
    private String lastname;
    private String email;

    public User() {
    }

    public User(String name, String lastname, String email) {
        this(name, lastname);
        this.email = email;
    }

    public User(String name, String lastname) {
        this.name = name;
        this.lastname = lastname;
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public String getLastname() {
        return lastname;
    }
    public void setLastname(String lastname) {
        this.lastname = lastname;
    }
    public String getEmail() {
        return email;
    }
    public void setEmail(String email) {
        this.email = email;
    }
}
~~~

~~~java
importar lombok.Getter; 
importar lombok.Setter; 

@Getter 
@Setter 
public class UserDto {

    private String title;
    private User user;
}
~~~

~~~java
@RestController
@RequestMapping("/api")
public class UserRestController {

    @GetMapping("/details")
    public UserDto details() {

        UserDto userDto = new UserDto();

        String title = "Spring Boot REST API";
        User user = new User("Isanor", "Lopez", "isanor@isanor.com");

        userDto.setTitle(title);
        userDto.setUser(user);

        return userDto;
    }

}
~~~
