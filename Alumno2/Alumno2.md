# Alumno 2 (Postgres y ORACLE):

## Postgres:

Averigua que privilegios de sistema hay en Postgres y como se asignan a un usuario.

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
