# Variables en PHP

Las variables en php funcionan como en cualquier lenguaje de programación, estas son:
**Espacios en memoria donde se almacena información mientras el script está en ejecución**

Las variables siempre se definen utiliando un **$** delante, estas son **case sensitive**, es decir que son sensible a las mayusculas.

**Ejemplo**

```php
<?php
    $nombre = "Franco";
    $Apellido = "Vaccari";
?>
```

Si en este caso queremos revisar el valor de la variable nombre deberíamos hacer lo siguiente:

```php
<?php
    echo $nombre;
?>
```

De esta manera veríamos reflejado el contenido de la variable. pero si hacemos lo siguiente

```php
<?php
    echo $apellido;
?>
```

PHP nos enviará un error ya que la variable no existe, porque utilizamos $apellido en vez de $Apellido.

**Por convención las variables siempre se declaran en minusculas**

## Tipos de datos que pueden almacenar las Variables

En php no es neceario que declaremos el tipo de variable, ya que es de tipado dinámico, pero, esto no quiere decir que podamos guardar cualquier cosa, sino que vamos a poder almacenar **ocho** tipos de datos. Estos son:

### Datos de tipo escalares o simples

- Boolean o Boleano (true o false)
- Integer o entero (números sin la coma)
- float o flotantes (números con coma decimal)
- String o cadenas (cadenas alfanuméricas)

Ejemplos

```php
<?php
    $boolean = true;
    $int = 5;
    $float = 35.2;
    $string = "Hola mundo";
?>

```

### Datos de tipo compuestos

Estos son dos y son muy útiles a la hora de programar:

- Array o arreglo (estos pueden almacenar varios datos)
- Object o objetos

```php
<?php
    $array = ["manzana", "pera", 36, 4.5];
    $array2 = array("manzana", "pera", 36, 4.5);

    //podremos acceder a sus valores a través de sus índices

    echo $array[0]; //muestra el primer valor -> manzana
?>

```

para los objetos es un tanto más complejo ya que deberemos trabajar con clases que pueden tener métodos

```php
<?php
    class Personas{
        public $nombre;
        public $edad;

        public function saludar()
        {
            return "Hola mi nombre es ". this->nombre . " y tengo ". this->edad;
        }

    }

// para instanciar debemos declararlo de esta manera

    $persona = new Personas();
    $persona->nombre = "Franco";
    $persona->edad = "33";

// ahora mostramos

    echo $persona->saludar();

?>

```

### Tipos de datos especiales

- resourse o recursos
- NULL o nulo

el tipo de datos resourse se utiliza en el caso de obtener y guardar un recurso, por ejemplo a la hora de conectarnos a la base de datos

y el nulo se utiliza para declarar un dato de tipo null o nulo, al cual luego podremos asignar un valor.

## Funciones para utilizar con variables

- **_var_dump():_** Permite saber el contenido y el tipo de la variable
- **_is_int()_**
- **_is_string()_**
- **_is_array()_**
- **_is_object()_**
- **_is_bool():_** Permite saber el tipo de variable
- **_isset():_** Nos permite saber si la variable contiene o no algo dentro.

## Variables del sistema

Se trata de variables globales, ya definidas que permiten guardar momentaneamente valores, estas son globales es decir que tienen alcance en todos los ambitos del script.

las más comunes son:

- $\_SESSION: controla la sesion y permiten guardar los datos del usuario.
- $\_GET: obtiene datos provenientes de un formulario.
- $\_POST: proporciona datos a través del verbo post de http
- $\_GLOBALS: contiene todas las variables globales

todas estas variables funcionan como objetos es decir utilizan clave valor para la definición.

Hay otras más que no vale la pena mencionar.

## Operadores

### Operadores de asignación

permiten asignar valores a las variables estos son

| **Operador** | **Función**                                |
| ------------ | ------------------------------------------ |
| =            | Asigna un valor a una variable             |
| +=           | suma un valor a una variable               |
| -=           | resta un valor a una variable              |
| \*=          | multiplica un valor a una variable         |
| /=           | divide un valor a una variable             |
| %=           | divide un vlaor por otro y asigna el resto |
| .=           | contatena una cadena a la variable         |

### Operadores Aritméticos

Permiten trabajar y realizar operaciones matemáticas
estos son:

| **Operador** | **Función**                     |
| ------------ | ------------------------------- |
| +            | suma                            |
| -            | resta                           |
| \*           | multiplicación                  |
| /            | división                        |
| %            | resto                           |
| ()           | Agrupa valores                  |
| ++           | suma una unidad a una variable  |
| --           | Resta una unidad a una variable |

### Operadores de comparación

| **Operador** | **Función**                        |
| ------------ | ---------------------------------- |
| ==           | compara si son iguales             |
| ===          | compara si son exactamente iguales |
| !=           | distinto                           |
| !==          | Exactamente distintos              |
| <            | Menor que                          |
| >            | Mayor que                          |
| <=           | Menor o igual                      |
| >=           | Mayor o igual                      |

### Operadores Lógicos

| **Operador** | **Función** |
| ------------ | ----------- |
| &&           | $a y $b     |
| ll           | $a o $b     |
| !            | Not o no    |
