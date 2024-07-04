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

## Metodos personalizados

Se debe definir el nombre del metodo y utilizar la notacion **@query** para definir la sentencia a ejecutar de lado de la **BD**, esta sentencia definida puede ser un procedimiento almacenado, una vista, una funcion, etc.  

Para el uso de parametros es necesario definirlos con nombre y anteponer el simbolo de **:**.  

`*Nota: Una vez definido el parametro es necesario que exista una referencia a el en el constructor del metodo`

~~~java
package com.paymentchain.customer.repository;

import org.springframework.data.jpa.repository.Query;
import org.springframework.data.jpa.repository.JpaRepository;

import com.paymentchain.customer.entity.Customer;

public interface CustomerRepository extends JpaRepository<Customer, Long> {

    @Query("SELECT c FROM Customer c WHERE c.code = :code")
    public Customer findByCode(String code);

    @Query("SELECT c FROM Customer c WHERE c.iban = :iban")
    public Customer findByAccount(String iban);

}

~~~
