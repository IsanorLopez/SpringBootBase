# Logger

Una de las practicas mas adecuadas para el manejo de microservicios es el uso de un **logger**, ya que al tratarse de programacion de lado del **backend**, no se cuenta con una visualizacion de los posibles errores o circunstancias que rodean la ejecucion de los flujos definidos en programacion.  

## slf4j Logger

Permite definir una instancia tipo **static** en las diferentes clases de un microservicio, inicializando la clase misma mediante el metodo **LoggerFactory.getLogger**, el cual requiere como parametro necesario el definir el tipo **.class** de la clase misma del micro servicio donde se esta implementando.  

### Info y error

Como los principales metodos utilizados en el logeo, se tienen **info** y **error**, los cuales cuentan con una lista de metodos sobre cargados que permiten definir una x cantidad de escenarios para mostrar informacion en consola, por el concepto en si mismo **info** se utiliza para mensajes de trazabilidad y **error** para escenarios de manejo de excepciones.  

~~~java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

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
            LOGGER.error("Error en funcion obtenerUsuario", e.getMessage());

            return e.getMessage();
        }
    }
}

~~~
