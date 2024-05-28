# Entities

Son clases comunes donde se definen los objetos a manejar con la **BD** con la finalidad de ser interpretados por **JPA** para generar persistencia.  

Para que springboot carge los metadatos necesarios y asi otorgarle la funcionalidad necesaria se requiere la etiqueta **@Entity**.  

## Data

Anotacion de libreria de **lombok** que permite la generacion de **getters y setters** para las propiedades que conforman el **entity**.  

## Id

Notacion necesaria para definir **entitys** dentro de springboot en versiones recientes.  

~~~java
package com.paymentchain.customer.entity;

import jakarta.persistence.Entity;
import jakarta.persistence.GeneratedValue;
import jakarta.persistence.GenerationType;
import jakarta.persistence.Id;
import lombok.Data;

@Data
@Entity
public class Customer {
    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private long id;
    private String name;
    private String phone;
}

~~~
