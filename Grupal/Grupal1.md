# CASO PRÁCTICO 1:

1. (ORACLE, Postgres, MySQL) Crea un usuario llamado Empleado y, sin usar los roles de ORACLE, dale los siguientes privilegios: (1,5 puntos)

Conectarse a la base de datos.

Modificar la duración máxima de las sesiones de otros usuarios.

Modificar índices en cualquier esquema (este privilegio podrá pasarlo a quien quiera)

Insertar filas en scott.emp (este privilegio podrá pasarlo a quien quiera)

Insertar datos en tablas ubicadas en cualquier tablespace.

Gestión completa de usuarios, privilegios y roles.

#MYSQL

1.1 Conectarse a la base de datos.

```
CREATE USER 'Empleado'@'localhost' IDENTIFIED BY '1234';
```
![Ejercicio 1](1.png)
![Ejercicio 1](11.png)


2.2 Modificar la duración máxima de las sesiones de otros usuarios.

Para modificar el numero de intentos sobre una sesion para los usuarios, debemos ir a la siguiente ruta /etc/mysql/mariadb.conf.d/50-mysqld_safe.cnf y modificar el siguiente valor por el que consideramos.

![Ejercicio 2](2.png)

3.3 Modificar índices en cualquier esquema (este privilegio podrá pasarlo a quien quiera)


```
GRANT ALTER, INDEX ON *.* TO 'Empleado'@'localhost';

```
![Ejercicio 3](3.png)


Crear índice

```
create index indice on EMP(ename);
```

![Ejercicio 3](33.png)


```
show indexes from EMP;
```
![Ejercicio 3](333.png)


4.4 Insertar filas en scott.emp (este privilegio podrá pasarlo a quien quiera)

```
GRANT INSERT ON scott.Emp TO 'Empleado'@'localhost' WITH GRANT OPTION;
```

![Ejercicio 4](4.png)

```
INSERT INTO SCOTT.DEPT VALUES (80, 'INFORMATICA', 'ESPANA');

INSERT INTO EMP VALUES (7512, 'OSCAR', 'SAN', 7902, '1980-12-17', 300, NULL, 20);
```

![Ejercicio 4](44.png)

5.5 Gestión completa de usuarios, privilegios y roles.

```
GRANT ALL PRIVILEGES ON *.* TO 'Empleado'@'localhost' WITH GRANT OPTION;
```

![Ejercicio 5](5.png)

6.6 Insertar datos en tablas ubicadas en cualquier tablespace.


2. (ORACLE, Postgres, MySQL) Escribe una consulta que obtenga un script para quitar cualquier privilegio de consulta a alguna tabla de SCOTT a los usuarios que lo tengan.

# ORACLE
```
SELECT 'REVOKE SELECT ON SCOTT.' || table_name || ' FROM ' || grantee || ';' AS revoke_statement
FROM DBA_TAB_PRIVS
WHERE OWNER = 'SCOTT'
  AND PRIVILEGE = 'SELECT';
```

![Ejercicio 22](8.png)

```
grant Select on SCOTT.EMP to oscar;
grant Select on SCOTT.DEPT to oscar;
```

![Ejercicio 22](88.png)



# MYSQL

```
GRANT SELECT ON scott.EMP to 'Empleado'@'localhost' IDENTIFIED BY "1234" WITH GRANT OPTION;

select concat('Revoke Select on ',table_schema,'.',table_name,' from ',grantee,';') as script
from information_schema.table_privileges
where table_schema='scott'
and privilege_type='SELECT';
```

![Ejercicio 22](7.png)


(ORACLE) Crea un tablespace TS2 con tamaño de extensión de 256K. Realiza una consulta que genere un script que asigne ese tablespace como tablespace por defecto a los usuarios que no tienen privilegios para consultar ninguna tabla de SCOTT, excepto a SYSTEM.

(ORACLE, Postgres) Realiza un procedimiento que reciba un nombre de usuario y nos muestre cuántas sesiones tiene abiertas en este momento. Además, para cada una de dichas sesiones nos mostrará la hora de comienzo y el nombre de la máquina, sistema operativo y programa desde el que fue abierta.

(ORACLE) Realiza un procedimiento que muestre los usuarios que pueden conceder privilegios de sistema a otros usuarios y cuales son dichos privilegios.
