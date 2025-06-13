# Introducción a SQL

Existen dos tipos de bases de Datos, las Relacionales y las No relacionales, las de tipo relacionales son las conocidas como **SQL** y las no relacionales **NOsql**, ambas tienen el mismo propósito que es el almacenamiento de la información, pero su principal diferencia es que las SQL guardan información mediante tablas y manejan el modelo **Entidad-Relación** y las NoSql en cambio, manejan el modelo de **colecciones de documentos**.

## SQL

_Structured Query Language_ es un lenguaje para manejar bases de datos, que es muy similar al ingles en su sintaxis y permite a través de su sintaxis obtener datos de tablas. Además de la obtención de datos también podremos crear, eliminar tablas y datos.

## Motor de bases de datos

SQL es un lenguaje estandarizado, pero a pesar de ser un estandar, existen diferentes motores de bases de datos con sutiles diferencias, estos motores pueden ser PosgresSQL, MySQL, SQLite, etc. que si bien utilizan SQL para gestionar las bases de datos, tienen sutiles diferencias unas con otras.

## Bases de datos

Una base de datos SQL es una colección de tablas que hacen referencias a **entidades**, una **entidad** es una extracción de algo real por ejemplo una tabla puede ser autos, la cual contendrá **atributos** generales de los autos por ejemplo todos los autos tienen una patente, un color, una marca y un modelo. Estos atributos hacen referencia a los todos los autos.  
**Bases de datos relacionales:** son bases de datos relacionales ya que vamos a poder hacer relación entre un atributo de una tabla y un registro de otra tabla, para evitar que se repitan los datos que estamos almacenando.

### Para practicar

Para practicar SQL debemos acceder a [SQLBOLT](https://sqlbolt.com/ "ejercicios prácticos"), donde podremos realizar ejercicios prácticos.

## Sintaxis SQL

SQL es un lenguaje que es fácil de entender a la hora de realizar consultas.
Debemos tener en cuenta a la hora de ralaizar consultas que este no es key sensitive osea que no requiere de mayusculas y minusculas en algunas palabrar específicas sino que eso no importa, lo que si importa y hay que tener mucho cuidado es en el **;** al final de cada sentencia.

### La primer sentencia

la primer sentencia que seguramente nos vamos a cruzar y con la cual podremos recuperar toda la información de una tabla es la siguiente: `SELECT * FROM tabla;`, en la cual seleccionamos toda la información de una tabla.

Debemos recordar que una tabla está formada por **Columnas, Filas y Celdas**. las tablas hacen referencia a una Entidad y sus columnas hacen referencia a un atributo de la entidad. Ejemplo:

| id_autos | marca     | modelo | año  |
| -------- | --------- | ------ | ---- |
| 1        | Vokswagen | GOL    | 2011 |
| 2        | Renault   | CLIO   | 2015 |
| 3        | Peugeot   | 408    | 2011 |
| 4        | Vokswagen | Voyage | 2008 |
| 5        | Renualt   | Suran  | 2007 |

Con la sentencia SQL `SELECT * FROM autos;`, estaríamos recuperando toda la información contenida en la tabla.

Para recuperar por ejemplo solo las marcas de los autos deberíamos hacer lo siguiente: `SELECT marca FROM autos;`

## Clase 2

[SQLBolt - Clase 2](https://sqlbolt.com/lesson/select_queries_with_constraints)

### Filtrar registros

Para filtrar registros de una tabla, debemos aplicar la clausura **WHERE** la cual nos traerá los registros que coincidan con el filtro. Ejemplo si solo queremos los autos de marca Volkwagen lo que debemos hacer es `SELECT * FROM autos WHERE marca = 'Volkswagen';`, deberíamos utilizar aquí operadores de comparación por ejemplo si queremos traer autos fabricados antes del 2010 `SELECT * FROM autos WHERE año < 2010;`

### Operadores de ADICIÓN:

Son operadores que permiten concatenar varias clausulas en una sola sentencia:
Ejemplo:
Sí queremos recuperar todos los autos de marca renault que fueron fabricados antes del 2010 `SELECT * FROM autos WHERE marca = 'Renault' AND año < 2010;`

### Operadores de COMPARACIÓN NUMÉRICOS:

| Operador | Acción        |
| -------- | ------------- |
| >        | Mayor         |
| <        | Menor         |
| =        | Igual         |
| !=       | Distinto      |
| >=       | Mayor o igual |
| <=       | Menor o igual |
| IN()     | en una lista  |
| NOT IN() | no inclido    |

## Clase 3

[SQLBolt - Clase 3](https://sqlbolt.com/lesson/select_queries_with_constraints_pt_2)

### Operadores de COMPARACIÓN ALFABÉTICOS:

| Operador | Acción                                            |
| -------- | ------------------------------------------------- |
| =        | exactamente Igual                                 |
| != o <>  | exactamente Distinto                              |
| LIKE     | Igual                                             |
| NOT LIKE | Distinto                                          |
| %        | se usa para buscar una cadena dentro de otra      |
| \_       | se usa para buscar una letra dentro de una cadena |
| IN()     | si la cadena existe en una lista                  |
| NOT IN() | si una cadena no esta en una lista                |

## Clase 4

[SQLBolt - Clase 4](https://sqlbolt.com/lesson/filtering_sorting_query_results)

### DISTINCT

Hace una distinción, esto queire decir que, si filtramos y tenemos varios resultados con el mismo dato supongamos el mismo nombre, lo que hace es mostrar solo uno.

```sql
SELECT DISTINCT nombre, año, …
FROM tabla
WHERE año > 2010;
```

> Sí hay más de un dato que coincida se mostrará solo uno.

### ORDER BY

nos permite una vez hecho el filtro, tomar una columna como referencia y ordenar de manera ASC (ascendente) o DESC (descendente) la información

```sql
SELECT nombres, años
FROM personas
WHERE año < 2000
ORDER BY año ASC
```

> la información se mostrará de menor a mayor, esto también funciona para las letras.

### LIMIT y OFFSET

- Limit se usa para limitar el resultado es decir por ejemplo limitar los 5 primeros.

```sql
SELECT nombres, años
FROM personas
WHERE año < 2000
ORDER BY año ASC
LIMIT 5 OFFSET 0
```

- Ahora si necesitamos que me muestre los 5 siguientes usamos offset para que los 5 anteriores no aparezcan

```sql
SELECT nombres, años
FROM personas
WHERE año < 2000
ORDER BY año ASC
LIMIT 5 OFFSET 5
```

> Clase 5 fue repaso [SQLBolt - Clse 5](https://sqlbolt.com/lesson/select_queries_with_joins)

## Clase 6

[SQLBolt - Clase 6](https://sqlbolt.com/lesson/select_queries_with_joins)

# JOINS

Se trata de relaciones entre tablas, en las cuales podremos extraer datos de varias tablas y mostrarlos todos juntos. Existen muchos tipos de joins.

![joins](https://miro.medium.com/v2/resize:fit:1400/0*rFMChX4SAmQ9RzF9.png)

- **Inner Join:** Es, si se quiere, el más importante de los joins, permite traer datos de dos tablas diferentes donde ambos coinciden.
- **Full Outer Join:** En este se traen todos los datos sin importar si algunos no tienen coincidencias.
- **Full Outer Join excludding inner:** Trae todos los tados que no tienen coincidencias.
- **Left y Right Join:** Trae la información solo de la tabla izquierda o de la derecha, sin importar que tenga coincidencias en la otra tabla, pero si las tiene las trae.
- **Left and Right Join Excludding inner:** Trae solo los datos de las tablas izquierdas o derechas que no tengan coincidencias.

#### Ejemplo:

Tabla Autos:
| id | marca | modelo | año |
| -------- | --------- | ------ | ---- |
| 1 | Vokswagen | GOL | 2011 |
| 2 | Renault | CLIO | 2015 |
| 3 | Peugeot | 408 | 2011 |
| 4 | Vokswagen | Voyage | 2008 |
| 5 | Renualt | Suran | 2007 |

Tabla Propietario:
| id |Nombre| id_auto |
|-------|-------------------|-----------|
| 1 | Gonzalo García | 2 |
| 2 | Mariana Rodríguez | 4 |
| 3| Roberto Almada | 1|

```sql
SELECT nombre, marca, modelo
FROM propietario
INNER JOIN autos on id_auto = id
```

## Clase 7

[SQLBolt - Clase 7](https://sqlbolt.com/lesson/select_queries_with_outer_joins)

# OUTER JOINS

Los OUTER JOINS nos permitirán traer datos incompletos de las tablas, estos pueden ser:

- LEFT JOIN: muestra todos los datos de la tabla de la izquierda, sin importar que en la otra tabla no haya datos, en el ejemplo anterior podría tener clientes que no tengan autos y me mostraría todos los clientes y sus autos y en el caso de no tener auto me los mostraría igual con el campo vacío.
- RIGHT JOIN: es lo inverso del anterior, mostraría todos los autos con y sin propietario.
- FULL JOIN: muestra todo propietarios con autos, propietarios sin auto y autos sin propietarios.

## Clase 8

[SQLBolt - Clase 8](https://sqlbolt.com/lesson/select_queries_with_nulls)

# NULLS

En lo posible es apropiado evitar los valores nulos en las bases de datos ya que son dificiles de trabajar.
Lo apropiado como alternativa a este tipo de datos nulos es tener un dato que lo represente según el tipo de datos que haya en el campo. Ejemplo: si el campo tiene un tipo de dato String, guardamos una string vacía, o si el dato es de tipo número, guardamos un 0.
Existen casos donde no pueden ser evitados los nulls, por lo tanto podríamos chequearlos dentro de las clausulas `WHERE`, con el comparador `IS NULL` o `IS NOT NULL`.

## Clase 9

[SQLBolt - Clase 9](https://sqlbolt.com/lesson/select_queries_with_expressions)

# Consultas con Expresiones

Con el fin de obtener resultados más concretos en las tablas, podriamos realizar consultas incluyendo opéraciones matemáticas, lo que nos ayudaría a conseguir resultados inmediatos.  
Estas columnas podrían utilizar métodos tanto para números como así tambien para String o Date.

> Cada motor de bases de datos tiene su propio formato para esto así que sería apropiado consultarlo en la documentación.

Cabe destacar que estas consultas con datos fabricados a través de expresiones matemáticas, son complejos de leer cuando se presentan en una tabla, por lo tanto es apropiado renombrar la nueva columna con la clausula `AS`.  
A su vez las expresiones matemáticas no solo permiten fabricar nuevas columnas sino también permiten ralizar filtros dentro del `WHERE`.

Ejemplos

TABLA: alumnos  
|apellido_nombre| trimestre_1 | trimestre_2 | trimestre_3|
|-----------------|-------------|-------------|------------|
| Ramírez, José | 5.5 | 6.8 | 4.5 |

```sql
SELECT apellido_nombre, (trimestre_1 + trimestre_2 + trimestre_3) / 3 AS Promedio FROM alumnos;
```

Esta consulta arrojará el siguiente resultado

| apellido_nombre | promedio |
| --------------- | -------- |
| Ramírez, José   | 5.6      |

## Clase 10

[SQLBolt - Clase 10](https://sqlbolt.com/lesson/select_queries_with_aggregates)

# Consultas con Agregados

Estas consultas permiten obtener diferentes resultados como podrían ser totales, promedios, mínimos o máximos de una columna determinada.
Para ello contamos con diferentes funciones que podemos utilizar en la consulta.
La estructura de estas consultas son de la siguiente manera:

```sql
SELECT sum(cantidad) AS total_stock
FROM productos
WHERE cantidad > 0;
```

### Funciones de Agregación

| Nombre de la Función       | Descripción                                                                                                                                                                                                                  |
| -------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| COUNT(\*) y COUNT(columna) | Una función común que se utiliza para contar el número de filas del grupo si no se especifica ningún nombre de columna. De lo contrario, cuente el número de filas del grupo con valores no NULL en la columna especificada. |
| MIN(columna)               | Encuentra el valor mínimo en la columna especificada                                                                                                                                                                         |
| MAX(columna)               | Encuentra el valor máximo en la columna especificada                                                                                                                                                                         |
| AVG(columna)               | Encuentra el valor promedio en la columna especificada                                                                                                                                                                       |
| SUM(columna)               | Encuentra el valor total de la columna especificada                                                                                                                                                                          |

## Clase 11

[SQLBolt - Clase 11](https://sqlbolt.com/lesson/select_queries_with_aggregates_pt_2)

# Consultas con Agregados pt 2

Cuando ejecutamos una consulta y utilizamos el `GROUP BY` con la intención de agrupar los resultados, nos encontramos que no podremos filtrar más, ya que el `GROUP BY` se ejecuta si o si luego del `WHERE`, por suerte SQL nos permite utilizar la clausula `HAVING` luego del `GROUP BY` para realizar este filtro.
Las clasulas `HAVING` son escritas de la misma forma que las `WHERE`.

## Clase 12

[SQLBolt - Clase 12](https://sqlbolt.com/lesson/select_queries_order_of_execution)

# Órden de Ejecución de una Consulta

El órden de ejecución de las consultas son muy importantes ya que es lo que le da coherencia a la consulta y que permite que SQL pueda funcionar correctamente.  
En este contexto, podremos decir que el orden es el siguiente:

1. `SELECT`: es el que nos permitirá seleccionar la columa que necesitamos operar.
2. `DISTINCT`: Permite hacer distinciones entre los datos y limitar los resultados repetidos.
3. `FROM`: Indica de que tabla viene dicha columna.
4. `JOIN`: indica si vamos a unir la tabla con otra este puede ser `INNER JOIN`,`OUTER JOIN`, `RHIGT/LEFT JOIN`, `FULL JOIN`, etc.
5. `ON`: Este simpre viene enganchado al `JOIN`, y determina una condición de la forma en que las tablas van a vincularse.
6. `WHERE`: Plantea una condición para poder filtrar la tabla.
7. `GROUP BY`: utilizada para determinar cómo se agruparán los datos en la tabla generada.
8. `HAVING`: Funciona como un `WHERE`, pero una vez utilizado el `GROUP BY`.
9. `ORDER BY`: Permite ordenar los datos, es decir permite mostrarlos de forma ascendente o descendente, etc.
10. `LIMIT` y `OFFSET`: permiten limitar los datos de desplegados en las tablas, y a su vez, permite determinar desde que dato comenzar a mostrar.

## Clase 13

[SQLBolt - Clase 13](https://sqlbolt.com/lesson/inserting_rows)

# Insertar Registros en las Tablas

A la hora de insertar nueva información en una tabla debemos tener en cuenta que una tabla es una entidad y esta tiene atributos que deben ser respetados.  
Para ello debemos respetar un _esquema_, el cual describe la estructura de una tabla, esto quiere decir que determina, el orden y los tipos de datos admitidos en cada campo de la tabla.  
Esta estructura es lo que le permite a las bases de datos gozar de eficiencia.
Una vez claro esto pasemos al siguiente ejemplo:

**Tabla: autos**
|id|marca|modelo|año_fabricacion|
|--|-----|------|---------------|
|1 |VW | GOL | 2011|

Si queremos insertar nueva información en esta tabla debemos reconocer el esquema, donde id es un numero autoincremental, marca es _String_, modelo es _String_ y año de fabricación es un _Integer_.

## Insert

esta clausula, nos permite insertar información en una tabla, de la cual previamente conocemos el esquema. Para ello debemos utilizar la siguiente sintaxis:

```sql
INSERT INTO nombre_de_la_tabla
VALUES (valorA1, valorA2, valorA3),
       (valorB1, valorB2, valorB3);
```

> En este ejemplo, se muestra que no solo podemos ingresar un solo registro, sino que podríamos cargar varios registros siempre y cuando estos estén entre parentesis y separados por comas.
> Siguiendo el ejemplo anterior:

```sql
INSERT INTO autos
VALUES ('Toyota', 'Hillux', 2020),
       ('Peugeot', '308', 2018);
```

¿Qué hacemos si tenemos información incompleta y necesitamos igual guardarla en la tabla?

Para ello debemos declarar cuales serán las columnas a rellenar.

```sql
INSERT INTO nombre_de_la_tabla
(columna2, columna3)
VALUES (valorA,valorB),
       (valorA2, valorB2);
```

Siguiendo el ejemplo anterior:

```sql
INSERT INTO autos
(marca, modelo)
VALUES ('Toyota', 'Hillux'),
       ('Peugeot', '308');
```

> Es preciso siempre declarar cuales son las columnas aunque sean todas ya que nos permitirán un mejor manejo de la tabla.

Cabe aclarar además que no solo valores pueden ser insertados, sino tambien operaciones matemáticas.

## Clase 14

[SQLBolt - Clase 14](https://sqlbolt.com/lesson/updating_rows)

# Actualizar registros

Así como insertar nueva información en una tabla, actualizarla o modificarla también es una acción que podemos realizar dentro de una tabla. Esta acción la debemos realizar a través de consultas.  
Para ello debemos usar la instancia `UPDATE` y especificar los datos a actualizar nombrando la columna que vamos a actualizar y el valor que esta va a tener dentro de la instancia `SET`. Además es sumamente importante que pongamos una condición y para ello usaremos un `WHERE`.

```sql
UPDATE tabla
SET columna1 = dato1,
    columna2 = dato2,
    columna3 = dato3
WHERE condición
```

Por ejemplo si queremos modificar un auto en la tabla autos debemos hacer lo siguiente:

```sql
UPDATE autos
SET marca = 'Chevrolet',
    modelo = 'Corsa',
    año_fabricacion = 2016
WHERE id = 1
```

> De esta manera modificaremos la información del primer registro ya que el id conincide con el primer auto.

> Debemos destacar que si no nombramos una columna esta no se verá modificada.

## Clase 15

[SQLBolt - Clase 15](https://sqlbolt.com/lesson/deleting_rows)

# Eliminar Registros

En el caso de la eliminación de registros, es mucho mas sensillo que la actualización o la inserción de nueva información.  
Solo con `DELETE` y una condición en `WHERE`, lograremos este propósito.

```sql
DELETE tabla
WHERE condición;
```

> **EXTREMADAMENTE IMPORTANTE**  
> En el caso de no colocar un `WHERE` y ejecutar la consulta, toda la información de nuestra tabla será eliminada completamente.

