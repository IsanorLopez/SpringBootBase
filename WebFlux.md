# WebFlux

Framework reactivo de **SpringBoot** destinado a proveer de los metodos necesarios para el consumo de recursos externos a un **MicroServicio**.  

## WebClient.Builder

Interface que representa el punto de entrada principal para el consumo de determinadas peticiones dentro de un **MicroServicio**, permitiendo ejecutar estos consumos con una funcionalidad **sincrona** o bien **asincrona** en caso de ser necesario.  

## HttpClient

Cliente para realizar peticiones **HTTP**, en el se configuran diferentes aspectos como el **TimeOut** en los escenarios relacionados al consumo y conexion del recurso externo.  

## WebClient.clientConnector

Permite definir un cliente para consumir peticiones **HTTP** provenientes de un **API** de 3ros, en lo que respecta a la creacion del cliente se pueden definir las configuraciones bajo las que operaran los consumos **HTTP**.  

## WebClient.baseUrl

Propiedad sobre la que define la base url a consumir.  

## WebClient.defaultHeader

Propiedad que permite definir el header para las peticiones que se realizaran.  

## WebClient.defaultUriVariables

Propiedad que define el parametro de **url**.  

## WebClient.method

Se debe definir el tipo de consumo que se estara realizando hacia el **endpoint**

## WebClient.uri

Propiedad donde se especifica el **endpoint** especifico.  

## WebClient.retrieve

Propiedad que permite definir como tratar la respuesta una vez realizado el consumo.  

### bodyToMono

Se Obtiene solo el **body** correspondiente a la respuesta por lo que puede ser asignada de manera directa a un **entity**

### toEntity

Se obtiene por completo la respuesta, por lo que es necesario utilizar un **ResponseEntity** y el **entity**.  

## block

Propiedad que permite definir el comportamiento del consumo a esperar la respuesta y detener la ejecucion hasta que se obtenga una respuesta.  

## JsonNode.class

Clase base para representar un **JSON**, asignada como la clase sobre la cual cae el **body** de la respuesta comvierte esta ultima en un **JSON**.  

## JsonNode.get

Metodo basico para acceder a una propiedad de **JSON**, se debe definir el nombre del campo como parametro principal o bien el indice que representa dentro de un determinado arreglo de objetos.  

~~~Java
import org.springframework.web.reactive.function.client.WebClient;

import com.paymentchain.customer.entity.Customer;
import com.paymentchain.customer.repository.CustomerRepository;

import io.netty.channel.ChannelOption;
import reactor.netty.http.client.HttpClient;
import io.netty.channel.epoll.EpollChannelOption;
import io.netty.handler.timeout.ReadTimeoutHandler;
import io.netty.handler.timeout.WriteTimeoutHandler;

/**
 *
 * @author isanor.lopez
 */
@RestController
@RequestMapping("/customer")
public class CustomerRestController {

    @Autowired
    CustomerRepository customerRepository;

    private final WebClient.Builder webClientBuilder;

    public CustomerRestController( WebClient.Builder webClientBuilder ) {
        this.webClientBuilder = webClientBuilder;
    }

    HttpClient httpClient = HttpClient.create()
        .option(ChannelOption.CONNECT_TIMEOUT_MILLIS, 5000) //Timeout para generar conexion
        .option(ChannelOption.SO_KEEPALIVE, true)
        .option(EpollChannelOption.TCP_KEEPIDLE, 300)
        .option(EpollChannelOption.TCP_KEEPINTVL, 60)
        .responseTimeout(Duration.ofSeconds(1)) //TimeOut en espera de respuesta
        .doOnConnected(connection -> {
            connection.addHandlerLast(new ReadTimeoutHandler(5000, TimeUnit.MILLISECONDS)); //TimeOut para lectura
            connection.addHandlerLast(new WriteTimeoutHandler(5000, TimeUnit.MILLISECONDS)); //Timeout para escritura
        })
    ;
    .
    .
    .
    private String getProductName(long id) {
        
        WebClient build = webClientBuilder.clientConnector(new ReactorClientHttpConnector(httpClient))
            .baseUrl("http://localhost:8083/product")
            .defaultHeader(HttpHeaders.CONTENT_TYPE, MediaType.APPLICATION_JSON_VALUE)
            .defaultUriVariables(Collections.singletonMap("url", "http://localhost:8083/product"))
            .build();

        JsonNode block = build.method(HttpMethod.GET)
                            .uri("/" + id).retrieve()
                            .bodyToMono( JsonNode.class )
                            .block();

        String name = block.get("name").asText();

        return name;

    }
}
~~~
