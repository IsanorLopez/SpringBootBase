# WebFlux

Framework reactivo de **SpringBoot** destinado a proveer de los metodos necesarios para el consumo de recursos externos a un **MicroServicio**.  

[List-map](https://www.bezkoder.com/reactor-flux-list-map/)

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

`*Nota: Regresa solo de 0 a 1 elemento`

### bodyToFlux

Se Obtiene solo el **body** correspondiente a la respuesta por lo que puede ser asignada de manera directa a un **List<entity>**

`*Nota: Regresa solo de 0 a n elementos`

### collectList

Obtiene el **body** correspondiente a la respuesta de forma que los elementos que se obtengan seran contenidos en una lista.  

### collectSortedList

Obtiene el **body** correspondiente a la respuesta de forma que los elementos que se obtengan seran contenidos en una lista **ordenada**.  

### collectMap

Obtiene el **body** correspondiente a la respuesta de forma que los elementos pueden se mapeados bajo cierta logica que permita generar un objeto de tipo **Map**

~~~java
Map<String, String> map1 = flux
            .collectMap(
                item -> item.split(":")[0], 
                item -> item.split(":")[1]
            )
        .block();

map1.forEach((key, value>) -> System.out.println(key + " -> " + value))
~~~

### collectMultimap

Obtiene el **body** correspondiente a la respuesta de forma que los elementos pueden se mapeados bajo cierta logica que permita generar un objeto de tipo **Map** con multiples valores para cada **key**

~~~java
Map<String, Collection<String>> map2 = flux
        .collectMultimap(
                item -> item.split("_[0-9]+:")[0], 
                item -> item.split(":")[1])
        .block();
        
map2.forEach((key, value) -> System.out.println(key + " -> " + value));
~~~

### toEntity

Se obtiene por completo la respuesta, por lo que es necesario utilizar un **ResponseEntity** y el **entity**.  

## block

Propiedad que permite definir el comportamiento del consumo a esperar la respuesta, deteniendo la ejecucion hasta que se obtenga.  

## JsonNode.class

Clase base para representar un **JSON**, asignada como la clase sobre la cual cae el **body** de la respuesta comvierte esta ultima en un **JSON**.  

## JsonNode.get

Metodo basico para acceder a una propiedad de **JSON**, se debe definir el nombre del campo como parametro principal o bien el indice que representa dentro de un determinado arreglo de objetos.  

~~~Java
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

    @GetMapping()
    public List<Customer> findAll() {
        return customerRepository.findAll();
    }

    @GetMapping("/{id}")
    public ResponseEntity<Customer> get(@PathVariable long id) {
        Optional<Customer> customer = customerRepository.findById(id);
        
        if (customer.isPresent()) {
            return new ResponseEntity<>(customer.get(),HttpStatus.OK);
        } else {
            return new ResponseEntity<>(HttpStatus.NOT_FOUND);
        }

    }

    @PutMapping("/{id}")
    public ResponseEntity<Customer> put(@PathVariable long id, @RequestBody Customer input) {
        Optional<Customer> currentCustomer = customerRepository.findById(id);
        
        if (currentCustomer.isPresent()) {
            Customer updatedCustomer = currentCustomer.get();
            
            updatedCustomer.setName(input.getName());
            updatedCustomer.setPhone(input.getPhone());

            customerRepository.save(updatedCustomer);

            return new ResponseEntity<>(updatedCustomer,HttpStatus.OK);
        
        } else {
            return new ResponseEntity<>(HttpStatus.NOT_FOUND);
        }

    }

    @PostMapping
    public ResponseEntity<Customer> post(@RequestBody Customer customer) {
        
        customer.getProducts().forEach( x -> x.setCustomer(customer));
        customer.getTransactions().forEach( x -> x.setCustomer(customer));
        
        Customer newCustomer = customerRepository.save(customer);

        return new ResponseEntity<>(newCustomer,HttpStatus.OK);
    }

    @DeleteMapping("/{id}")
    public ResponseEntity<Customer> delete(@PathVariable long id) {
        customerRepository.deleteById(id);
        return new ResponseEntity<>(HttpStatus.OK);
    }

    @GetMapping("/full")
    public ResponseEntity<Customer> getByCode(@RequestParam String code) {
        Customer customer = customerRepository.findByCode(code);

        List<CustomerProduct> products = customer.getProducts();
        products.forEach(product -> {
            String productName = this.getProductName(product.getProductId());
            product.setProductName(productName);
        });
        
        List<CustomerTransaction> transactions = getTransactions(customer.getIban());
        customer.setTransactions(transactions);

        return new ResponseEntity<>(customer, HttpStatus.OK);
    }
    
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

        return block.get("name").asText();
    }

    private List<CustomerTransaction> getTransactions(String accountIban) {
        
        WebClient build = webClientBuilder.clientConnector(new ReactorClientHttpConnector(httpClient))
            .baseUrl("http://localhost:8082/transactions/")
            .defaultHeader(HttpHeaders.CONTENT_TYPE, MediaType.APPLICATION_JSON_VALUE)
            .build();

        return build.method(HttpMethod.GET)
                    .uri("accountIban/" + accountIban)
                    .retrieve()
                    .bodyToFlux(CustomerTransaction.class)
                    .collectList()
                    .block();

    }

}
~~~
