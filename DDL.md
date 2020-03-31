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

```sql
CREATE SCHEMA <nome_da_base_de_datos>
```

Logo desto temos que crear os dominios, para iso usaremos:

```sql
CREATE DOMAIN <nome_do_dominio> <tipo_de_datos>
```

Esta creación de dominios serve para declarar un elemento que vamos usar máis de unha vez. Esto aforrarános traballo xa que non teremos que escribir todo, (a sentenncia, o nome e o tipo (xunto co número da extensión)).

Dende que xza temos a BD creada, e todos os dominios declarados, comezaremos a crear táboas con:

```sql
CREATE TABLE <nome_da_táboa>
	<atributo1> <dominio1> [NOT NULL] [DEFAULT <x>]
````
	
**Un exemplo de creación de unha BD dende cero**

```sql
CREATE SCHEMA BaseDeDatosClase09032020

CREATE DOMAIN Nome_Válido CHAR(30);
CREATE DOMAIN Tipo_Código CHAR(5);
CREATE DOMAIN Tipo_DNI CHAR(9);

CREATE TABLE Sede (
    Nome_Sede Nome_Válido,
    Campus    Nome_Válido NOT NULL,
    CONSTRAINT PK_Sede
        PRIMARY KEY (Nome_Sede)
);

CREATE TABLE Departamento (
    Nome_Departamento Nome_Válido,
    Teléfono          CHAR(9) NOT NULL,
    Director          Tipo_DNI
        PRIMARY KEY (Nome_Sede)
);

CREATE TABLE Ubicación (
    Nome_Sede         Nome_Válido,
    Nome_Departamento Nome_Válido,
    CONSTRAINT PK_Ubicación
        PRIMARY KEY (Nome_Sede, Nome_Departamento),
    CONSTRAINT FK_Sede
        FOREIGN KEY (Nome_Sede)
        REFERENCES Sede (Nome_Sede)
        ON DELETE CASCADE
        ON UPDATE CASCADE,
    CONSTRAINT FK_Departamento
        FOREIGN KEY (Nome_Departamento)
        REFERENCES Departamento (Nome_Departamento)
        ON DELETE CASCADE
        ON UPDATE CASCADE,
);

CREATE TABLE Grupo (
    Nome_Grupo        Nome_Válido,
    Nome_Departamento Nome_Válido,
    Área              Nome_Válido NOT NULL,
    Lider             Tipo_DNI,
    PRIMARY KEY (Nome_Grupo, Nome_Departamento)
    FOREIGN KEY (Nome_Departamento) REFERENCES Departamento
        ON DELETE CASCADE
        ON UPDATE CASCADE

);

CREATE TABLE Profesor (
    DNI           Tipo_DNI    PRIMARY KEY,
    Nome_Profesor Nome_Válido NOT NULL,
    Titulación    VARCHAR(20) NOT NULL,
    Experiencia   Integer,
    N_Grupo         Nome_Válido,
    N_Departamento  Nome_Válido,
    CONSTRAINT FK_Grupo
        FOREIGN KEY        (N_Grupo, N_Departamento)
        REFERENCES N_Grupo (Nome_Grupo, Nome_Departamento)
        ON DELETE SET NULL
        ON UPDATE CASCADE
);

CREATE TABLE Proxecto(
    Código_Proxecto Tipo_Código,
    Nome_Proxecto   Nome_Válido NOT NULL,
    Orzamento       MONEY       NOT NULL,
    Data_Inicio     DATE        NOT NULL,
    Data_Fin        DATE,
    N_Gr            Nome_Válido,
    N_Dep           Nome_Válido,
    UNIQUE (Nome_Proxecto),
    CONSTRAINT Check_Dates
        CHECK (Data_Inicio < Data_Fin),
    CONSTRAINT FK_Grupo
        FOREIGN KEY        (N_Gr, N_Dep)
        REFERENCES N_Grupo (Nome_Grupo, Nome_Departamento)
        ON DELETE SET NULL
        ON UPDATE CASCADE
);

ALTER TABLE Departamento
    ADD CONSTRAINT FK_Departamento_Profesor
        FOREIGN KEY (Director) 
        REFERENCES Profesor (DNI) 
        ON DELETE SET NULL
        ON UPDATE CASCADE;
        
CREATE TABLE Participa (
    DNI             Tipo_DNI,
    Código_Proxecto Tipo_Código,
    Data_Inicio     DATE    NOT NULL,
    Data_Cese       DATE,
    Dedicación      INTEGER NOT NULL,
    PRIMARY KEY (DNI, Código_Proxecto)
    CHECK (Data_Inicio < Data_Cese)
    CONSTRAINT FK_Participa
        FOREIGN KEY (DNI)
            REFERENCES Profesor (DNI)
            ON DELETE NO ACTION
            ON UPDATE CASCADE
        FOREIGN KEY (Código_Proxecto)
            REFERENCES Profesor (Código_Proxecto)
            ON DELETE NO ACTION
            ON UPDATE CASCADE
        
);
```
Nesta BD, vemos como ao principio creamos a BD con ```sql CREATE SCHEMA ``` , logo definimos todos os dominios con ```sql CREATE DOMAIN ```.
Lodo disto comezamos a crear táboas con ```sql  CREATE TABLE ``` Creamos as táboas: **SEDE**, **DEPARTAMENTO**, **UBICACIÓN**, **GRUPO**, **PROFESOR**, **PROXECTO** e **PARTICIPA**
