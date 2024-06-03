# Controllers

En estos archivos se definen las clases y metodos que contengan la interaccion del usuario con el **API** por medio de la definicion de los **enpoints** y de los **parametros** para operar los mismos.  

Para que springboot carge los metadatos necesarios y asi otorgarle la funcionalidad necesaria se requiere la etiqueta **@Controller**.  

Como complemento estas entidades se dedican tambien a consumir los **services** que retornan el resultado de una determinada operacion que llego hasta la **BD**  

## Inyeccion de repository

Se utiliza la notacion **@Autowired** para evitar crear la instancia del **repository** y tener acceso a un objeto que hace uso de todos sus metodos tanto predefinidos como personalizados.  

## ResponseEntity

Clase que centraliza multiples metodos para manejar las solicitudes **HTTP**.  

## @PathVariable

Notacion que permite acceder a las variables definidas como parte de la **URL** en la notacion **@GetMapping** estableciendo un parametro como parte del metodo que atiende determinada peticion.  

`*Nota: Se requiere definir un tipado para el mismo.`  

## @RequestBody

Notacion que permite acceder al **Body** de la peticion estableciendo un parametro como parte del metodo que atiende determinada peticion, permitiendo asi hacer uso de el.

`*Nota: Se requiere definir un tipado para el mismo.`  

## @Autowired

Notacion que permite inyectar dependencias dentro del contexto de un proyecto, estableciendo el nexo necesario entre archivos para permitir que la funcionaldiad sea fluida.  

~~~java
package com.paymentchain.customer.controller;

import java.util.List;
import java.util.Optional;

import org.springframework.http.HttpStatus;
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
    public ResponseEntity<Customer> post(@RequestBody Customer input) {
        Customer customer = customerRepository.save(input);
        return new ResponseEntity<>(customer,HttpStatus.OK);
    }

    @DeleteMapping("/{id}")
    public ResponseEntity<Customer> delete(@PathVariable long id) {
        customerRepository.deleteById(id);
        return new ResponseEntity<>(HttpStatus.OK);
    }

}
~~~
