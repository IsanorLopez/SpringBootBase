# Services

En estos archivos se definen las clases y los metodos que contengan toda la logica de negocio necesaria para llevar a cabo un consumo por parte del **controller**, haciendo uso de tantos metodos como sean necesarios de las clases **repository** y **retornar** el resultado de tales operaciones de vuelta al **controller** a fin de retroalimentar el resultado del cosumo sobre el **API**.  

Para que springboot carge los metadatos necesarios y asi otorgarle la funcionalidad necesaria se requiere la etiqueta **@Service**.  
