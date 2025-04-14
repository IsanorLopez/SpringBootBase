# DTO

Data transfer object por su traduccion, son clases de java con la finalidad de brindar un modelo de datos enfocado en al transferencia de informacion entre capaz.  

Estas entidades pueden contener tantos campos como sea necesario, sin embargo deben de contener como estandar solo propiedades accesibles de lectura y utilizar unicamente tipos de datos **seriablizables**, entiendase serializable como objetos que puedan ser convertidos a un determinado formato de exposision como lo es **JSON**, un ejemplo de datos NO serializables son los **Date** o **Calendar**  

## Caso de uso

Cuando se tienen 2 clases cuyos campos son necesarios para un determinada respuesta de un **endpoint**, un DTO permite definir un modelo de punto medio, una fusion entre los campos de ambos **modelos** con los campos unicamente necesarios para dar respuesta a la funcionalidad buscada.  

De no contar con la estructura de **DTO** como intermediario se pondria muy complejo el resolver la necesidad del objeto **JSON**, ademas que esta estructura intermedia nos permite el ocultar por razones de seguridad campos no necesariamente utiles al expotar como el caso del **password**.  

~~~mermaid
graph TB
    A["Class Usuario
    userName String
    password String
    name String
    lastName String
    birthDate Date
    direction Direction"];

    B["Class Sport
    id Integer
    name String
    "];

    C["Class UsuarioDTO
        fullName String (name + lastname)
        birthDate String (Serializable type)
        List[Sport] userSports
    "];

    A -->C
    B -->C

~~~
