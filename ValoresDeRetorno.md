# Valores de retorno

Dentro del contexto de un **Api REST**, siempre sera necesario retornar una determinada respuesta para una solicitud hacia el micro servicio, esta respuesta por estandar debe de mantenerse como un **Json**.  

## Map<String, Object>

Este tipo de retorno es el mas simple, se define un mapa con clave tipo string para mantener un nombrado para cada propiedad y como valor se puede definir el tipo de dato que sea necesario, puede ser un string, int, object etc.  

Cuando desde un **controller** se realize el return para el cliente que solicito el consumo de un **endpoint**, **springboot** se encargara de convertir el mapa a tipo **Json** de forma automatica.  

~~~java
@RestController
@RequestMapping("/desarrollo/detalles-management/api/v1")
public class UserRestController {
    @GetMapping("/details")
    public Map<String, Object> details() {

        Map<String, Object> usuario = new HashMap<>();

        usuario.put("Name", "Isanor"); 
        usuario.put("Password", "123456");
        usuario.put("Age", 18);
        
        return usuario;
    }
}
~~~

`*Nota: Este tipo de retorno es recomendado para operaciones que no requieren mucha logica, sin embargo, debe evitarse tanto como sea posible, dado que su definicion en si misma puede considerarse mala practica`  

## Object Mapper

Tipo de retorno que se vale de la clase **ObjectMapper** para transformar una entidad tipo **DTO** hacia el formato **Json** pero de tipo **String**, este camino es mas apropiado para el manejo de logica completa enfocada en la separacion de capaz para implementar la logica necesaria de un consumo hacia un determinado **endpoint**.  

~~~java
import lombok.Data;

@Data
public class UsuarioDTO {

    private String name;
    private String password;
    private Integer age;

}
~~~

~~~java
@Service
public class UsuarioServiceImpl implements IUsuarioService {

    private final ObjectMapper objectMapper;

    public UsuarioServiceImpl(ObjectMapper objectMapper) {this.objectMapper = objectMapper;}
    public static final Logger LOGGER = LoggerFactory.getLogger(UsuarioServiceImpl.class);

    @Override
    public String obtenerUsuario() {
        try {
            UsuarioDTO usuarioDTO = new UsuarioDTO();

            usuarioDTO.setName("Isanor");
            usuarioDTO.setPassword("123456");
            usuarioDTO.setAge(18);

            return objectMapper.writeValueAsString(usuarioDTO);

        } catch (JsonProcessingException e) {
            e.printStackTrace();
            LOGGER.error("Error obtenerUsuario", e.getMessage());

            return e.getMessage();
        }
    }
}
~~~

~~~java
@RestController
@RequestMapping("/desarrollo/detalles-management/api/v1")
public class UserRestController {

    private final IUsuarioService usuarioService;

    public UserRestController( IUsuarioService usuarioService) { this.usuarioService = usuarioService;  }

    @GetMapping("/userDetails")
    public String userDetails() {
        return usuarioService.obtenerUsuario();
    }

}
~~~
