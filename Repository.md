# Repository

En estos archivos se definen las interacciones directas con la **BD**, es decir se ejecutan las instrucciones que manipuilan y/o obtienen informacion.  

Para que springboot carge los metadatos necesarios y asi otorgarle la funcionalidad necesaria se requiere la etiqueta **@Repository**.  

## Tipado

Es requerido definir el tipado dentro del repository considerando el **Entity** asociado y el tipo del campo **@Id** definido como segundo parametro.  

~~~java
package com.paymentchain.customer.repository;

import org.springframework.data.jpa.repository.JpaRepository;

import com.paymentchain.customer.entity.Customer;

public interface CustomerRepository extends JpaRepository<Customer, Long> {

    

}

~~~
