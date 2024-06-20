# JPA

API interna en springboot que permite implementar mecanismos para manejar la persistencia de la informacion y su correlacion con objetos definidos en el proyecto mismo a traves del concepto **Entity**.  

~~~xml
.
.
.
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
.
.
.
~~~

## OneToMany

Instruccion que permite definir una relacion de uno a muchos dentro de una propieda de un **entity**.  

## ManyToOne

Instruccion que permite definir una relacion muchos a uno dentro de una propieda de un **entity**.  

## OneToOne

Instruccion que permite definir una relacion uno a uno dentro de una propieda de un **entity**.  

## ManyToMany

Instruccion que permite definir una relacion muchos a muchos dentro de una propieda de un **entity**.  

## fetch

Opcion que define el comportamiento del **ORM** en tiempo de ejecucion entre entidades que estan relacionadas, es decir, permite definir el comportamiento que se tiene para obtener la informacion con la **BD**.  

Independientemente de que tipo de relacion tengan 2 entidades:

- La propiedad **EAGER** traera toda la informacion de un **Entity** y de los **Entitys** relacionados a el en memoria realizando los **JOIN** que tenga que hacer para consegir toda la informacion relacionada no haciendo del uso de memoria una prioridad.  

~~~java
Estudiante estudiante = entityManager.find(Estudiante.class, 2001L);
logger.info("Estudiante --> {}", estudiante);
~~~

~~~SQL
SELECT estudiante.id, estudiante.nombre, estudiante.materias
FROM estudiantes
LEFT JOIN materias
on estudiantes.materia.id = materias.id
WHERE estudiante = id
~~~

- La propiedad **LAZY** traera solo aquellas propiedades que sean solicitadas por medio de los **GET** a las propiedades mismas, realizando tantas consultas independientes como sea necesario generando un mejor manejo de memoria.  

~~~java
Estudiante estudiante = entityManager.find(Estudiante.class, 2001L);
logger.info("Estudiante --> {}", estudiante);
logger.info("Materia --> {}", estudiante.getMaterias());
~~~

~~~SQL
SELECT estudiante.id, estudiante.nombre
FROM estudiantes
WHERE estudiante = id

SELECT materia.id, materia.nombre
FROM materias
WHERE materia = id
~~~

## mappedBy

Define el nombre de la propiedad por el cual se esta generando una relacion bi-direccional entre dos **Entitys**.  

## Cascade

Define el tipo de relacion que tienen 2 **Entitys** con respecto a los cambios que sufren, es decir, dependiento si es **INSERT**, **UPDATE** o **DELETE** la operacion sobre un **entity** es a como se afectara el otro **entity** con el que esta realcionado.  

- ALL: el **entity** con la que se relaciona sufre tambien todos los cambios qe sufra el **entity** principal.  
- PERSIST: Al dar de alta al **entity** principal se da de alta tambien el **entity** con el que se relaciona, evitando enerar dos operaciones separadas.  
- MERGE: el **entity** principal se da de alta y actualiza/inserta segun sea el caso en **entity** con el que tiene relacion.  
- REMOVE: Especifica que si el **entity** principal es eliminado tambien se eliminara el **entity** con el que tiene relacion.  
- REFRESH: Poco utilizado pero define que independientemente del tipo de afectacion que sufra el **entity** principal el **entity** con el que tiene relacion realiza una consulta a la **BD** a fin de mantenerse actualizado.  

## orphanRemoval

Complemento a la eliminacion de **entitys** relacionados entre si, cuando se establece como **true**, se puede eliminar un **entity** principal y todos los **entitys** con los que tenga relacion.  

Ejemplo si se tiene un **entity** libro y una relacion **oneToMany** con el **entity** Capitulo, al eliminar un libro se eliminan tambien los capitulos.  

## Transient

Anotacion dentro de una propiedad de un **entity** que tiene la finalidad de ignorar el campo tanto para el grabado en **BD** como el manejo del objeto a travez de **JPA**

## targetEntity

Propiedad que se define en una relacion entre **entitys** para hacer referencia especifica a la clase de la cual se esta estableciendo la relacion.  

## JsonIgnore

Anotacion que se encarga de definir cuando una propiedad de un determinado **entity** no debe de ser serializado.  

~~~Java
@Data
@Entity
public class Customer {
    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private long id;
    private String code;
    private String iban;
    private String name;
    private String surname;
    private String phone;
    private String adress;

    @OneToMany(fetch = FetchType.LAZY, mappedBy = "customer", cascade = CascadeType.ALL, orphanRemoval = true)
    private List<CustomerProduct> products;

    @Transient
    private List<?> transactions;
}
~~~

~~~Java
public class CustomerProduct {

    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private long id;
    private long productId;
    @Transient
    private String productName;

    @JsonIgnore
    @ManyToOne( fetch = FetchType.LAZY, targetEntity = Customer.class)
    @JoinColumn( name = "customerId", nullable = true )
    private Customer customer;
}
~~~
