# Archivos de configuracion

## pom.xml

Archivo sobre el que se define las dependencias del proyecto asi como las principales configuraciones del mismo.  

## application.yml

Archivo que concentra las credenciales y configuracines de conexion hacia servidores.  

## controllers

Archivos que contienen la definicion y configuracion de los endpoints  

## dto

Archios que contienen la definicion de clases para la interaccion entre cliente y servidor  

## entities

## Relaciones bidireccionales

Dentro de el manejo de datos dentro de spring boot existe un evento llamado bidireccion, cuando dos entidades tiene una relacion bidireccional, por ejemplo un usuario puede tner muchos post y cada post tiene un usuario.  

Dado que la informacion que viaja por springboot son objetos JSON se requiere que exista una serizacion de la misma.  

La serializacion de la informacion implica convertir un objeto JSON en bytes para ser eviados a travez de el cnsumo del API y volverse a convertir en JSON una vez que se tome.  

Dada una situacion donde se tengan dos objetos relacionados entre si, es decir relacion bidireccional, puede generar un problema de infinita recursion, donde se serializa un objeto que apunta a otro y ese otro objeto apunta al objeto original.  
