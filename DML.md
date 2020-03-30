# Apuntes
## A sublinguaxe DML
### Índice

- [Uso da sentencia INSERT](#Uso-da-sentencia-INSERT)
- [Uso da sentencia UPDATE](#Uso-da-sentencia-UPDATE)
- [Uso da sentencia DELETE](#Uso-da-sentencia-DELETE)


O DML é outra sublinguaxe de SQL, que ten a funcionalidade de **agregar**, **borrar** ou **modificar** tuplas de unha táboa da BD. Esta sublinguaxe a diferencia de DDl, ***actúa sobre os datos***, contando que a anterior actuaba sobre os obxectos.
O significado de DML e *Data Manipulation Languaje*, en galego: *Linguaxe de manipulación de datos*.

  ### Antes de empezar, aclarar o significado da simboloxía:

  [ ] Os corchetes significan que o que está entre eles é opcional
 
   |  A barra vertical significa OU (o que está antesd ou o que está despois)


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
#### Exemplos
```sql
INSERT INTO world
[(name, continent, area)]
VALUES
('Spain', 'Europe', 100),
('Portugal', 'Europe', 10);
```
Neste primeiro exemplo estamos engadindo 2 tuplas seguidas a táboa world. Como ben vemos podemos engadir todas as tuplas que queiramos de un tirón, separando sempre con , (coma) **E ao final acabando con ;**.
```sql
INSERT INTO world
[(name, continent, area)]

SELECT nome, continente, area
FROM mundo
WHERE continente='Europa';
```
Como tamén vemos neste outro exemplo, podemos conbinar o **INSERT INTO** con SELECT, FROM e WHERE.

### Uso da sentencia UPDATE
  A sentencia update, serve para modificar os datos xa existentes da táboa.
 ```sql
 UPDATE <nome_da_táboa>
 SET <atributo1> = <valor1>,
     <atributo2> = <valor2>,
 [WHERE <predicado>];
 ```
 Esta última liña ```[WHERE <predicado>] ``` é totalmente opcional
 
 #### Exemplos
 ```sql
 UPDATE world
 SET continent = 'Asia';
 WHERE name = 'Spain'
    OR name = 'Portugal'
 ```
 Neste exemplo añadiremos onde se encontre o nome Spain e Portugal o novo valor Asia.
 É moi importante puntualizar que se non establecemos o WHERE, aplicariao en toda a BD.
 
 ### Uso da sentencia DELETE
  A sentencia delete, serve para eliminar valores de algunhas tuplas, que lle digamos, unha táboa, ou ata poderiamos eliminar a BD enteira.
 ```sql
 DELETE FROM <nome_da_táboa>;
 [WHERE <predicados>]
 ```
 Como ben aparece na fórmula, o WHERE é opcional, aínda que non debería selo. Xa que se non espeficias o WHERE eliminarías a BD enteira. E ao mellor eso non é o que queremos, como un amigo do profesor, nun dos seus traballos, jejejejeje.
 
 #### Exemplos
 ```sql
 DELETE FROM world
 WHERE continent = 'Europe';
 ```
 Neste exemplo, eliminariamos todas as tuplas na que existise un valor de continent, que sexa iguala Europe.
