# Apuntes
## A sublinguaxe DDL
### Índice

O DDL é unha sublinguaxe de SQL, xunto co DDL, DCL, TCL, SCL. O DDL ten a funcionalidade de **crear**, **borrar** e **modificar** tablas da BD. Este sublinguaxe actúa sobre os **obxectos**  significa Data Definition Languaje. Esto serve para crear, modificar e borrar tablas e bases de datos

  ### Antes de empezar, aclarar o significado da simboloxía:

  [ ] Os corchetes significan que o que está entre eles é opcional.
 
   |  A barra vertical significa OU (o que está antes ou o que está despois).

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

As restriccións que aparecen ao final en realidade chámanse *constraints*, que é o nome da sentencia que usamos para definilas.

Existen 4 *contriants* ou restriccións, que son as seguintes:

**De clave primaria**

```sql
[[CONSTRAINT <nome_da_restricción>] 
	 PRIMARY KEY (<atributos>)]
```

**De clave foránea**
```sql
[[CONSTRAINT <nome_da_restricción>]
         FOREIGN KEY (<atributos>)
         REFERENCES <nome_da_táboa_de_referencia> (<atributo_referenciado>)]
 ```
 
**De unicidade**
```sql
[CONSTRAINT <nome_da_restricción>]
             UNIQUE (<atributos>)]
```

**De comprobación** (non entra en exame)
```sql
[CONSTRAINT <nome_da_restricción]
	CHECK (atributoA IN (valor1, ... , valorN))
	[[NOT] DEFERABLE]
	[INITIALLY INMEDIATED | DEFERRD]]
```

#### Creación dunha base de datos
Para crear unha base de datos, temos que levar a cabo diferentes CREATE.

O primeiro que temos que usar é:

´´´sql
CREATE SHEMA <nome_da_base_de_datos>
´´´

Logo desto temos que crear os dominios, para iso usaremos:

´´´sql
CREATE DOMAIN <nome_do_dominio> <tipo_de_datos>
´´´

Esta creación de dominios serve para declarar un elemento que vamos usar máis de unha vez. Esto aforrarános traballo xa que non teremos que escribir todo, (a sentenncia, o nome e o tipo (xunto co número da extensión)).

Dende que xza temos a BD creada, e todos os dominios declarados, comezaremos a crear táboas con:

´´´sql
CREATE TABLE <nome_da_táboa>
	<atributo1> <dominio1> [NOT NULL] [DEFAULT <x>]
´´´
	
** Un exemplo de creación de unha BD dende 0 **
