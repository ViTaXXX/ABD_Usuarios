# Alumno 2 (Postgres y ORACLE):

## Postgres:

## 1. Averigua que privilegios de sistema hay en Postgres y como se asignan a un usuario.

La verdad que PostgreSQL funciona un poco diferente a Oracle, ya que los  privilegios y permisos se administran utilizando roles. Estos roles son básicamente grupos de usuarios que comparten los mismos privilegios y permisos en la base de datos, algo parecido a los "privilegios de los grupos" como tal, pero haciendo incapié que evidente no es lo mismo, pero sirve un poco para poder comprenderlo de mejor manera.

| Privilegio   | Descripción                                               |
|--------------|-----------------------------------------------------------|
| SELECT       | Permite al usuario recuperar datos de una tabla o vista.   |
| INSERT       | Permite al usuario agregar nuevos registros a una tabla.   |
| UPDATE       | Permite al usuario modificar los registros existentes.     |
| DELETE       | Permite al usuario eliminar registros de una tabla.        |
| TRUNCATE     | Permite al usuario truncar una tabla, es decir, eliminar todos los registros. |
| REFERENCES   | Permite al usuario crear una clave foránea que haga referencia a otra tabla. |
| TRIGGER      | Permite al usuario crear y ejecutar disparadores (triggers).|
| CREATE       | Permite al usuario crear nuevos objetos en la base de datos, como tablas, vistas, índices, etc. |
| CONNECT      | Permite al usuario conectarse a una base de datos específica. |
| TEMPORARY    | Permite al usuario crear tablas temporales.                 |
| EXECUTE      | Permite al usuario ejecutar una función.                    |
| USAGE        | Permite al usuario utilizar un esquema, secuencia o función. |


### Roles:

Los roles se asignan por ejemplo tanto a usuarios como también a grupos de usuarios, aunque también pueden ser asignados a otros roles, permitiendo la creación de jerarquías y estructuras más complejas. La asignación de roles puede realizarse en diferentes niveles, como bases de datos, esquemas y tablas. Por ejemplo, como vimos en clase si tenemos varios roles A B y C, C puede contener también sus privilegios y también los de A o B.

### Roles a Objetos de Bases de Datos:

Además de asignar roles a usuarios, se pueden asignar a objetos específicos de la base de datos, como vistas, secuencias y funciones. También es posible asignar roles a otros objetos de la base de datos, como índices y secuencias.

Por ejemplo la asignación de permisos a un rol puede llevarse a cabo de dos maneras, durante la creación del rol mediante la instrucción CREATE ROLE rol WITH opción y por otra parte después de la creación del rol mediante la instrucción ALTER ROLE rol WITH opción.

### Opciones de Roles:

Algunas de las opciones de uso para los roles son:

- SUPERUSER/NOSUPERUSER: Para otorgar privilegios de super usuario.
- ADMIN: Establece qué rol o roles tienen el derecho de agregar otros roles.
- CREATEDB/NOCREATEDB: Para permitir o no que un usuario pueda crear nuevas bases de datos
- REPLICATION/NOREPLICATION: Permite o niega al usuario replicar la base de datos.
- CREATEROLE/NOCREATEROLE: Para permitir o no que un usuario pueda crear nuevos roles.
- INHERIT/NOINHERIT: Para que un usuario herede  privilegios de los roles o no.
- LOGIN/NOLOGIN: Para conceder o no que un usuario pueda iniciar sesión.
- CONNECTION LIMIT: Para establecer un límite de las conexiones simultáneas.
- VALID UNTIL: Para establecer una fecha de caducidad de un usuario.
- PASSWORD: Para asignar contraseñas.
- ENCRYPTED: Para establecer si la contraseña debe estar encriptada (si fuera necesario).
- IN ROLE: Define los roles a los que pertenece el usuario.

Ejemplo:

Para crear un rol que de privilegios que permita crear bases de datos o crear neuvos roles:

`CREATE ROLE rol WITH CREATEDB, CREATEROLE;`

Para asignarme el nuevo rol:

`ALTER USER andres WITH ROLE rol;`



Averigua cual es la forma de asignar y revocar privilegios sobre una tabla concreta en Postgres.

Averigua si existe el concepto de rol en Postgres y señala las diferencias con los roles de ORACLE.

Averigua si existe el concepto de perfil como conjunto de límites sobre el uso de recursos o sobre la contraseña en 
Postgres y señala las diferencias con los perfiles de ORACLE. En cualquier caso, intenta averiguar la forma de implementar en Postgres cada uno de los límites que se pueden definir en ORACLE.

Crea un rol valido hasta final de 2024 en Postgres y añádelo a otro rol existente.

Realiza consultas al diccionario de datos de Postgres para averiguar todos los privilegios que tiene un usuario concreto.

Realiza consultas al diccionario de datos en Postgres para averiguar qué usuarios pueden consultar una tabla concreta.

Realiza una consulta al diccionario de datos de Postgres para mostrar qué usuarios tienen privilegios sobre algún objeto de otro usuario.

## ORACLE:

Realiza una función de verificación de contraseñas que compruebe que la contraseña tiene el mismo formato que una dirección IPv4 y que la longitud de la misma es diferente de la longitud de la anterior. Asígnala al perfil CONTRASEÑARARA. Comprueba que funciona correctamente.

Realiza un procedimiento llamado MostrarPrivilegiosdelRol que reciba el nombre de un rol y muestre los privilegios de sistema y los privilegios sobre objetos que lo componen, incluyendo los pertenecientes a otros roles concedidos a dicho rol. Debes utilizar la técnica de la recursividad contemplando la posibilidad de que existan infinitos niveles de roles anidados.
