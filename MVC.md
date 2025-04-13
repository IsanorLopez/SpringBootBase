# MVC

Patron de arquitectura enfocado en generar una separacion de la logica entre capaz, misma que utiliza como ventaja la **Inyeccion de dependencias** y orientada al uso de **interfacez**.  

- Vista: Interfaz directa con la que tiene interaccion el usuario, es su herramienta para interactuar con el **sistema**.  
- Controlador: Encargado de manejar las solicitudes que hace llegar la **vista**, este administra las solicitudes y conecta con el modelo para obtener los datos requeridos.  
- Modelo: Logica de negcoio encargada de recibir las solicitudes del controlador y generar una conexin a la bd de ser necesario apra obtener la infromacion que se requiere.  
