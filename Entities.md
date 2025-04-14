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


software.amazon.awssdk.services.dynamodb.model.DynamoDbException: ExpressionAttributeValues can only be specified when using expressions: UpdateExpression and ConditionExpression are null (Service: DynamoDb, Status Code: 400, Request ID: ITCDIQ6SN253CRJ50F6GR71RHJVV4KQNSO5AEMVJF66Q9ASUAAJG) (SDK Attempt Count: 1)

software.amazon.awssdk.services.dynamodb.model.DynamoDbException: ExpressionAttributeValues contains invalid key: Syntax error; key: "reintentos" (Service: DynamoDb, Status Code: 400, Request ID: BGCG0C0UCK249N7PKGSLQM5SLNVV4KQNSO5AEMVJF66Q9ASUAAJG) (SDK Attempt Count: 1)

software.amazon.awssdk.services.dynamodb.model.DynamoDbException: ExpressionAttributeValues contains invalid key: Syntax error; key: "fechaModificacion" (Service: DynamoDb, Status Code: 400, Request ID: 7C3Q9L9SDH6G2NMB1J7P6764VNVV4KQNSO5AEMVJF66Q9ASUAAJG) (SDK Attempt Count: 1)


software.amazon.awssdk.services.dynamodb.model.DynamoDbException: Value provided in ExpressionAttributeValues unused in expressions: keys: {:fechaCreacion, :fechaModificacion} (Service: DynamoDb, Status Code: 400, Request ID: CSBDU75HBH62FGVAHTPCL4H79BVV4KQNSO5AEMVJF66Q9ASUAAJG) (SDK Attempt Count: 1)


/*if (updateExpression.toString().endsWith(", ")) {
                updateExpression.delete(updateExpression.length() - 2, updateExpression.length());
            }*/