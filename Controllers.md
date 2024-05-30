# Controllers

En estos archivos se definen las clases y metodos que contengan la interaccion del usuario con el **API** por medio de la definicion de los **enpoints** y de los **parametros** para operar los mismos.  

Para que springboot carge los metadatos necesarios y asi otorgarle la funcionalidad necesaria se requiere la etiqueta **@Controller**.  

Como complemento estas entidades se dedican tambien a consumir los **services** que retornan el resultado de una determinada operacion que llego hasta la **BD**  

## Inyeccion de repository

Se utiliza la notacion **@Autowired** para evitar crear la instancia del **repository** y tener acceso a un objeto que hace uso de todos sus metodos tanto predefinidos como personalizados.  

## ResponseEntity

Clase que centraliza multiples metodos para manejar las solicitudes **HTTP**.  

~~~java
package com.paymentchain.customer.controller;

import java.util.List;

import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PutMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.DeleteMapping;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.beans.factory.annotation.Autowired;

import com.paymentchain.customer.entity.Customer;
import com.paymentchain.customer.repository.CustomerRepository;

/**
 *
 * @author isanor.lopez
 */
@RestController
@RequestMapping("/customer")
public class CustomerRestController {

    @Autowired
    CustomerRepository customerRepository;

    @GetMapping()
    public List<Customer> findAll() {
        return customerRepository.findAll();
    }

    @GetMapping("/{id}")
    public Customer get(@PathVariable String id) {
        return null;
    }

    @PutMapping("/{id}")
    public ResponseEntity<?> put(@PathVariable String id, @RequestBody Customer input) {
        return null;
    }

    @PostMapping
    public ResponseEntity<?> post(@RequestBody Customer input) {
        Customer customer = customerRepository.save(input);
        return ResponseEntity.ok(customer);
    }

    @DeleteMapping("/{id}")
    public ResponseEntity<?> delete(@PathVariable String id) {
        return null;
    }

}
~~~
