# Apuntes
## A sublinguaxe DDL
### Índice

O DDL é unha sublinguaxe de SQL, xunto co DDL, DCL, TCL, SCL. O DDL ten a funcionalidade de **crear**, **borrar** e **modificar** tablas da BD. Este sublinguaxe actúa sobre os **obxectos**  significa Data Definition Languaje. Esto serve para crear, modificar e borrar tablas e bases de datos

  ### Antes de empezar, aclarar o significado da simboloxía:

  [ ] Os corchetes significan que o que está entre eles é opcional
 
   |  A barra vertical significa OU (o que está antesd ou o que está despois)

### Uso da sentencia CREATE
A sentencia CREATE, serve para crear tablas, BD, usuarios, esquemas (é o mismo que as BD, pero con menos restriccións).
```sql
CREATE (DATABASE | TABLE | SCHEMA | USER)
[IF NOT EXISTS] <nome_da_BD>
[CHARACTER SET <nome>]
(<atributo1> <dominio1> [NOT NULL] [DEFAULT <x>],
[restriction1],
...
[restriction2]
);
```
O ```IF NOT EXISTS``` serve para que comprobe se existe algunha táboa, bases de datos ou usuarios co nome proporcionado.

O ```CHARACTER``` Usase para asignar xogos de caracteres a BD, como o UTF.

O ```DEFAULT``` asigna un valor por defecto.
