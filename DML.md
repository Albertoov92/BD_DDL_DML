# Apuntes
## A sublinguaxe DML
### Índice

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
Neste primeiro exemplo estamos engadindo 2 tuplas seguidas a táboa world. Como ben vemos podemos engadir todas as tuplas que queiramos de un tirón, separando sempre con , (coma) **E ao final acabando con ;**
```sql
INSERT INTO world
[(name, continent, area)]

SELECT nome, continente, area
FROM mundo
WHERE continente='Europa';
```

### Uso da sentencia UPDATE
  A sentencia update, serve para modificar os datos xa existentes da táboa.
 ```sql
 UPDATE <nome_da_táboa>
 SET <atributo1> = <valor1>,
     <atributo2> = <valor2>,
 [WHERE <predicado>];
 ```
 Esta última liña ```[WHERE <predicado>] ``` é totalmente opcional
