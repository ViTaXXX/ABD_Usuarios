# Alumno 4 (MongoDB y ORACLE):

## MongoDB:

### Averigua si existe la posibilidad en MongoDB de limitar el acceso de un usuario a los datos de una colección determinada.
Se puede realizar mediante el uso de roles.

Ejemplo:

Creamos un nuevo rol con permisos de lectura solo para la “**colección1**” en la base de datos “**dbprueba**”

```bash
db.createRole({
        role: "rol1",
        privileges: [
            { resource: { db: "dbprueba", collection: "coleccion1" }, actions: [ "find" ] }
        ],
        roles: []
    })
```

Asignamos el rol a un usuario y de esta forma estamos restringiendo el acceso al resto de colecciones:

### Averigua si en MongoDB existe el concepto de privilegio del sistema y muestra las diferencias más importantes con ORACLE.
Oracle tiene dos tipos de privilegios para el usuario:

**System:**

```
Permite al usuario realizar tareas administrativas.
```

**Object**:

```
En este caso le permite al usuario crear algunos objetos en la base de datos, como tablas, vistas, funciones…
```

En el caso de **MongoDB** no tenemos estos permisos sino **roles.**

Un rol es un conjunto de privilegios.

Un privilegio define una accion o acciones que se pueden realizar sobre un recurso.

Los recursos:

```
Base de datos
Colecciones
Conjunto de colecciones
Nivel de cluster: representa operaciones sobre el conjunto de réplica o el cluster de shards
```

Un rol puede heredar privilegios de otros roles

Tipo de roles:
```
Roles predefinidos por el sistema: son los que vienen por defecto en el sistema, no es necesario crearlos.
Roles definidos por el usuario: solo creados por el administrador de la base de datos.
```

### Explica los roles por defecto que incorpora MongoDB y como se asignan a los usuarios.
- read: permite leer datos de todas las colecciones.
- readWrite: permite leer y escribir datos de todas las colecciones.
- dbAdmin: permite realizar tareas administrativas.
- userAdmin: permite crear y modificar usuarios y roles en la base de datos actual.
- dbOwner: puede efectuar cualquier operaación administrativa en la base de datos. Por lo tanto junta los privilegios de readWrite, dbAdmin y userAdmin.
- clusterMonitor: permite acceso de solo lectura a las herramientas de supervisión.
- clusterManager: permite realizar acciones de administración y monitorización en el cluster.
- hostManager: permite monitorizar y administrar servidores.
- clusterAdmin: combina los tres roles anteriores añadiendo ademas el rol de dropDatabase.
- backup: permite realizar copias de seguridad de los datos.
- restore: permite restaurar los datos de las copias de seguridad.
- roles de superusuarios:
    
    ```
    -userAdmin
    -dbOwner
    -userAdminAnyDatabase
    -root: asigna privilegios completos sobre todos los recursos del sistema.
    ```
    
- Roles de todas las base de datos:
    
    ```
    -readAnyDatabase: es el mismo rol que read pero se aplica a todas las bases de datos.
    -readWriteAnyDatabase: es el mismo rol que readWrite pero se aplica a todas las bases de datos.
    -userAdminAnyDatabase: es el mismo rol que userAdmin pero se aplica a todas las bases de datos.
    -dbAdminAnyDatabase: es el mismo rol que dbAdmin pero se aplica a todas las bases de datos.
    ```
    

Para aplicar a los usuarios:

Mientras creamos el usuario:

```
db.createUser( {user: "USUARIO", pwd: "PASS", roles: [ { role: "NOMBRE DEL ROL", db: "DB" } ] })
```

Cuando el usuario ya esta creado:
```
db.grantRolesToUser( "USUARIO", [ { role : "NOMBRE DEL ROL", db : "DB" }, "NOMBRE DEL ROL", … ])
```

### Explica como puede consultarse el diccionario de datos de MongoDB para saber que roles han sido concedidos a un usuario y qué privilegios incluyen.
Para poder ver los roles que tiene un usuario sobre una base de datos primero debemos entrara a la base de datos:

```
use dbprueba
```

Para colsultar los roles usamos la siguiente instruccion:

```
db.getUser("usuario1")
```

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/61185465-41d8-48ee-82b8-66b31bf699da/659dca70-fb73-4421-ad80-151cd02f9add/Untitled.png)

Para ver los privilegios que tiene un rol usamos el siguiente comando:
```
db.getRole("rol1")
```
![getRole](https://www.notion.so/Individual-Usuarios-3e43b70059b44668a9000c71ad190013?pvs=4#a969a45ce7e2424e94733d3c9e02a62f)

### Averigua si es posible limitar el acceso a un documento concreto de una colección.
La unica forma que he encontrado de limitar el acceso a un documento en concreto es crear una vista en la que no aparezcan los documentos que queremos restringir y mediante los roles dar acceso a la vista en vez de a la coleccion entera.

Por ejemplo tengo la coleccion coches, que contiene marcas de coches y ahora crearemos una vista para limitar el acceso a ciertas marcas:

```sql
db.createCollection("coches")

##Insertamos datos:
db.coches.insertMany([
   { nombre: "Toyota", pais: "Japón" },
   { nombre: "Ford", pais: "Estados Unidos" },
   { nombre: "Volkswagen", pais: "Alemania" },
   { nombre: "Honda", pais: "Japón" },
])
```

Ahora mostramos todos los datos de la coleccion:

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/61185465-41d8-48ee-82b8-66b31bf699da/26187f73-4fb7-409a-8a6d-b61b821af7ff/Untitled.png)

Ahora crearemos una vista para restringir y no mostraremos la marca Honda:

```sql
db.createView("marcas_restringidas", "coches", [
   {
      $match: {
         nombre: { $ne: "Honda" } 
      }
   },
]);
```

Por ultimo asignamos un rol al usuario para que pueda ver la lista:

```sql
db.createRole({
    role: "Rmarcas_restringidas",
    privileges: [
        {
            resource: { db: "prueba", collection: "coches" },
            actions: ["find"]
        }
    ],
    roles: []
});

**db.grantRolesToUser("restringido", ["Rmarcas_restringidas"]);**
```

Consultamos la vista:

### Averigua si se puede conseguir que un usuario solo tenga permiso para ver ciertos atributos de los documentos.

### Averigua si en MongoDB existe alguna posibilidad de limitar la cantidad de recursos utilizados por un usuario.

### Averigua si en MongoDB existe alguna posibilidad de definir las características de la contraseña de un usuario.
		
## ORACLE:

### 1. Realiza un procedimiento llamado MostrarObjetosAccesibles que reciba un nombre de usuario y muestre todos los objetos a los que tiene acceso, bien porque sean suyos o porque algún privilegio de sistema o sobre objetos se lo haya concedido.
```
create or replace procedure MostrarObjetosAccesibles (p_usuario varchar2)
IS
  Cursor c_objeto is
  select table_name, privilege, owner from dba_tab_privs where grantee = p_usuario;
  v_nombretabla varchar2(50);
  v_nombretabla_old varchar2(50):=' ';
BEGIN
  dbms_output.put_line('objetos accesibles:');
  for v_objeto in c_objeto loop
    v_nombretabla:=v_objeto.table_name;
    if v_nombretabla_old != v_nombretabla then
      dbms_output.put_line('Tabla: ' || v_objeto.table_name);
      dbms_output.put_line(CHR(9)|| 'Propietario: '|| v_objeto.owner);
      dbms_output.put_line(CHR(9)|| 'privilegios:');
    end if;
    dbms_output.put_line(CHR(9)||CHR(9)|| '- '|| v_objeto.privilege);
    v_nombretabla_old:=v_nombretabla;
end loop;
END;
/

exec MostrarObjetosAccesibles('JOSEMA');
```

### 2. Realiza un procedimiento que reciba un nombre de usuario, un privilegio y un objeto y nos muestre el mensaje 'SI, DIRECTO' si el usuario tiene ese privilegio sobre objeto concedido directamente, 'SI, POR ROL' si el usuario lo tiene en alguno de los roles que tiene concedidos y un 'NO' si el usuario no tiene dicho privilegio.  Debes realizar el procedimiento empleando la técnica de la recursividad para contemplar infinitos niveles de roles anidados.
```
create or replace procedure mostrarobjetoprivilegio (p_usuario varchar2, p_privilegio varchar2, p_objeto varchar2)
IS
v_contador number:=0;
BEGIN
COMPROBARUSUARIO (p_usuario);
SELECT COUNT(*) INTO v_contador FROM DBA_TAB_PRIVS WHERE GRANTEE = p_usuario AND PRIVILEGE = p_privilegio AND TABLE_NAME = p_objeto;
if v_contador = 1 then
    SELECT COUNT(*) INTO v_contador FROM DBA_ROLE_PRIVS WHERE grantee = p_usuario;
    if v_contador = 1 then
        dbms_output.put_line('SI, POR ROL');
    else
        dbms_output.put_line('SI, DIRECTO');
    end if;
else
    dbms_output.put_line('NO');
end if;
END;
/


create or replace procedure COMPROBARUSUARIO (p_usuario varchar2)
IS
v_existe number:=0;
BEGIN
select count(*) into v_existe from DBA_USERS where USERNAME = p_usuario;
if v_existe = 0 then
    raise_application_error(-20112,'No existe el usuario');
end if;
END;
/

exec mostrarobjetoprivilegio('JOSEMA', 'RESOURCE', 'EMP');
exec mostrarobjetoprivilegio('SYSTEM', 'EXECUTE', 'DBMS_ALERT');
```
