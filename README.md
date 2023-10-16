# SpringBoot

Framework dedicado a la creacion de microservicios **Backend**, se centra en la simplicidad, permitiendo dejar de lado muchas configuraciones manuales y centrarse por completo en el desarrollo mismo. Tiene como principio el desarrollo de piezas pequeñas **modulos**, que al integrarse generan una funcionaliad mas completa.  

[Pagina oficial](https://spring.io/projects/spring-boot)

## Java

Se utiliza el lenguaje de Java como base para la codificacion en el framework.  

## JDK 8

Este framework requiere como minimo el kit de desarrollo version 8 como minimo.  

## Inyeccion de dependencias  

Maneja de manera centralizada toda aquella clase definida con la anotacion **@Component** dentro de un mismo contexto, para facilitar el acoplamiento(**Inyeccion**) dentro de otra clase que la necesite, a estas clases se les conoce como **beans**.  

A este proceso se le conoce como **inversion of control(IOC)**  

## MVC

Patron implementado dentro del framework, permite la modularidad entre las entidades separando en distintas capas la logica que conforma la funcionalidad del aplicativo.  

## Modelo de programacion reactiva (webflux)

Paradigma de programacion que se centra en generar logica **asincrona** y **No bloqueante**, es decir permitir el flujo dela funcionalidad independientemente de que se este esperando la respuesta de un recurso en particular.  

Esto se logra en parte gracias a una entidad conocida como **event loop** el cual se encarga de coordinar el orden de las peticiones, sin bloquear la funcionalidad.  

El determinado orden de las peticiones queda controlado en **registro callback**, que no es otra cosa que una lista de las peticiones echas.  

## ORM

Mapeo relacional con objetos que permite la persistencia de la informacion desde un aplicativo a la base de datos, esto sin la necesidad de ejecutar procedimientos almacenados dentro de la base de datos misma, el framework permite el acceso a esta funcionalidad guiada por el estandar **JPA**, este ultimo dicta la manera en como se realiza al codificacion y uso de las herramientas que da ORM.  

## Programacion orientada a aspectos(AOP)

Paradigma que se centra en la modularidad de la funcionalidad generada sobre un aplicativo, la idea es anadir nueva funcionaliad sin modificar lo previamente generado.  
