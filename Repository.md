# Repository

En estos archivos se definen las interacciones directas con la **BD**, es decir se ejecutan las instrucciones que manipuilan y/o obtienen informacion.  

Para que springboot carge los metadatos necesarios y asi otorgarle la funcionalidad necesaria se requiere la etiqueta **@Repository**.  

## Tipado

Es requerido definir el tipado dentro del repository considerando el **Entity** asociado y el tipo del campo **@Id** definido como segundo parametro.  

## Extends

Al extender de la clase **JpaRepository** cualquier objeto de la instancia del **repository** tiene acceso a un conjunto de metodos pre-definidos para manejar la data, estos metodos tienen implementada una funcionalidad basica para llevar a cabo un **CRUD**.  

- findAll: Obtiene todos los registros
- findById: Obtiene un registro especifico basado en el ID
- save: Genera un nuevo registro o bien actualiza uno preexistente
- deleteById: Eliminar un determinado registro filtrando por ID

`*Nota: En caso de requerir generar una funcionalidad en particular puede ser definida dentro de la clase repository`

~~~java
package com.paymentchain.customer.repository;

import org.springframework.data.jpa.repository.JpaRepository;

import com.paymentchain.customer.entity.Customer;

public interface CustomerRepository extends JpaRepository<Customer, Long> {

    

}

~~~
