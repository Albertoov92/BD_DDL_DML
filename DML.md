# Apuntes
## A sublinguaxe DML
### Índice

O DML é outra sublinguaxe de SQL, que ten a funcionalidade de **agregar**, **borrar** ou **modificar** tuplas de unha táboa da BD. Esta sublinguaxe a diferencia de DDl, ***actúa sobre os datos***, contando que a anterior actuaba sobre os obxectos.
O significado de DML e *Data Manipulation Languaje*, en galego: *Linguaxe de manipulación de datos*.

### Uso da sentencia INSERT
  A sentencia insert, como ben dice en inglés, **inserta** datos da táboa.
```sql
INSERT INTO <nome_da_táboa>
[(atributo1, atributo2, ...)]
VALUES
(<valor1A>, <valor2A>, ...),
(<valor1B>, <valor2B>, ...),
| SELECT <atributo1> FROM <tabla1>
```

### Uso da sentencia UPDATE
  A sentencia update, serve para modificar os datos xa existentes da táboa.
 ```sql
 UPDATE <nome_da_táboa>
 SET <atributo1> = <valor1>
     <atributo2> = <valor2>
 [WHERE <predicado>]
 ```
 Esta última liña ```[WHERE <predicado>] ``` é totalmente opcional
