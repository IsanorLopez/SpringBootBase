# Estilos Arquitectura

## Monolithic

Arquitectura basada en generar un producto de software completo que atiende a todo un negocio.  

Por ejemplo una pagina de e-commerce que tiene un frontend y un backend en el que se definen todos los servicios necesarios para hacer funcionar la plataforma.  

El backend implementa:

- El servicio CRUD a productos
- El servicio de compra
- El servicio de timbrado con el SAT
- El servicio de manejo de stock

Desventajas:  

- Escalabilidad
- Desarrollo lento
- Falta de flexibilidad

## Orientada a servicios  

Arquitectura basada en des-centralizar los servicios que atienden a un negocio y definir un **sistema intermedio** para proveer acceso a los multiples clientes que necesitan hacer uso de estos, servicios.  

Es un punto medio donde en una pagina de e-commerce que tiene un frontend web, una app y una x cantidad de servicios hacen funcionar la plataforma.  

El sistema intermedio implementa:

- Todos los servicios que atienden al negocio.  
- Brinda un acceso para cualquier cliente que requiera hacer uso de los servicios.  

Desventajas.  

- Alto coste de mantenimiento
- Equipos especializados

## Microservicios

Arquitectura enfocada en generar servicios des-centralizados que atiendan a un negocio completo en particular sin la necesidad de interconetar estos servicios ya que se comunicacon bajo el contexto de un **API**.  

Son un monton de servicios expuestos esperando ser consumidos por una x cantidad de clientes a fin de hacer uso de la funcionalidad de cada servicio particular y dar funcionalidad completa a una plataforma.  

Desventajas:  

- Complejidad en la gestion en proyectos grandes
- Monitoreo y depuracion dados los multiples lenguajes y/o tecnologias interactuando  
