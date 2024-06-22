# WebFlux

Framework reactivo de **SpringBoot** destinado a proveer de los metodos necesarios para el consumo de recursos externos a un **MicroServicio**.  

## WebClient.Builder

Interface que representa el punto de entrada principal para el consumo de determinadas peticiones dentro de un **MicroServicio**, permitiendo ejecutar estos consumos con una funcionalidad **sincrona** o bien **asincrona** en caso de ser necesario.  

## HttpClient

Cliente para realizar peticiones **HTTP**, en el se configuran diferentes aspectos como el **TimeOut** en los escenarios relacionados al consumo y conexion del recurso externo.  

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
~~~
