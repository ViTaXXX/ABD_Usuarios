# Alumno 4 (MongoDB y ORACLE):

## MongoDB:

Averigua si existe la posibilidad en MongoDB de limitar el acceso de un usuario a los datos de una colección determinada.

Averigua si en MongoDB existe el concepto de privilegio del sistema y muestra las diferencias más importantes con ORACLE.

Explica los roles por defecto que incorpora MongoDB y como se asignan a los usuarios.

Explica como puede consultarse el diccionario de datos de MongoDB para saber que roles han sido concedidos a un usuario y qué privilegios incluyen.

Averigua si es posible limitar el acceso a un documento concreto de una colección.

Averigua si se puede conseguir que un usuario solo tenga permiso para ver ciertos atributos de los documentos.

Averigua si en MongoDB existe alguna posibilidad de limitar la cantidad de recursos utilizados por un usuario.

Averigua si en MongoDB existe alguna posibilidad de definir las características de la contraseña de un usuario.
		
## ORACLE:

1. Realiza un procedimiento llamado MostrarObjetosAccesibles que reciba un nombre de usuario y muestre todos los objetos a los que tiene acceso, bien porque sean suyos o porque algún privilegio de sistema o sobre objetos se lo haya concedido.

2. Realiza un procedimiento que reciba un nombre de usuario, un privilegio y un objeto y nos muestre el mensaje 'SI, DIRECTO' si el usuario tiene ese privilegio sobre objeto concedido directamente, 'SI, POR ROL' si el usuario lo tiene en alguno de los roles que tiene concedidos y un 'NO' si el usuario no tiene dicho privilegio.  Debes realizar el procedimiento empleando la técnica de la recursividad para contemplar infinitos niveles de roles anidados.
