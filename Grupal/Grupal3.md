# EJERCICIO GRUPAL 3:

Elaboración de un vídeo grupal resumiendo las diferencias de concepto y en la gestión de usuarios, permisos de sistema y permisos sobre objetos, roles y perfiles entre los cuatro SGBDs estudiados. Cada miembro del grupo hablará de uno de los siguientes temas:


a) Usuarios y permisos sobre objetos. Óscar


b) Permisos de sistema. Ándres 

## Oracle:

Oracle permite asignar los privilegios -> Usuarios o a roles

- CONNECT -> conectarse a la bbdd

- RESOURCE -> acceso a todos los recursos (tablas etc)

- DBA -> administración y manejo de las bbdd

- SYSDBA -> administración pero pudiendo incluso detener o arrancar la base de datos, recuperación de datos, copias de seguridad, etc

- SYSOPER -> mantiene un monitoreo de la bbdd

## Postgre:

Permite asignar los privilegios -> Usuarios o a roles con la diferencia con Oracle de que los usuarios son realmemte roles, es como un alias de rol.

- SUPERUSER -> superusuario

- CREATEUSER -> crea usuarios o roles

- CREATEDB -> puede crear bbdd

- LOGIN -> puede iniciar sesión en las bbdd

- USAGE -> para poder usar una bd concreta

## Mariadb:

permite asignar los privilegios -> Usuarios o a roles, pero en este caso hay que especificar en que bbdd se esta trabajando ya que tiene las bbdd separadas

- SUPER -> modo superusuario, cocntrol total

- PROCESS -> puede comprobar procesos de la bbdd

- RELOAD -> puede recargar permisos y configuraciones 

- REPLICATION CLIENT -> para ver el estado de la replicación de la bbdd

- REPLICATION SLAVE -> para configurar y administrar la replicación

- SHUTDOWN -> apagar la base de datos

## Mongodb:

En Mongo la gran diferencia es que los privilegios / roles no se pueden asignar a usuarios, sino que primero creo un rol con los privilegios que quiero y luego se lo doy a un usuario, especificando tambien en que bbdd estamos trabajando

Roles (cambia):

- ROOT -> acceso total como superusuario

- SYSTEM -> modificar documentos

- DBA_ADMIN -> tareas administrativas

- CLUSTERMONITOR -> monitoreo a nivel de cluster

- BACKUP -> para copias de seguridad


