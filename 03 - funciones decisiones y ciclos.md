# Funciones, Estructuras condicionales y Ciclos

Como cualquier otro lenguaje de programación php no escapa de la utilización de las **funciones** para la reutilización de código, de **condicionales** para la bifurcación de código y de los **ciclos o bucles** para la repetición de código.

## Funciones

una función es un bloque de código reutilizable.

Este código es accedido a través de un nombre.

Una función cuenta con un **nombre**, **parámetros** y el **bloque en si**, el cual debe retornar un resultado.

En php podemos declarar una función colocando la palabra **function** y seguido el nombre de la función.

```php
<?php
function sumar($a, $b){
    return $a + $b;
}
?>
```

allí tenemos el claro ejemplo de una función de suma, si miramos detenidamente veremos que la función cuenta con un
**nombre**, sus **parámetros** y utilizando la palabra reservada **return** nos está devolviendo el resultado de la suma.

para que esta función sea ejecutada, debemos llamarla y pasarle los parámetros que necesita para funcionar.

```php
<?php
function sumar($a, $b){
    return $a + $b;
}

echo sumar(15,12); //de esta manera echo imprimirá el resultado de la función.

$resultado = suma(15,12); //De esta manera estaríamos guardando el resultado en una variable.

?>
```

Dentro de los parámetros de una función podremos tener también otras funciones, esto se conoce como callback y es un recurso bastante utilizado en programación.

Dentro del bloque de una función las variables declaradas en ella son exclusivas de la función. por lo que no existirán fuera de la función y dejan de existir una vez que la función termina de ejecutarse. Esto se conoce como **scope** o alcance de una variable.

## Estructuras Condicionales

Las estructuras condicionales son estructuras que nos permiten controlar el flujo de un programa, a través de ellas podremos tomar decisiones y por ejemplo restringir acceso, mostrar o no información, etc.

Las estructuras condicionales responden a una estructura donde:

- se establece una condición lógica
- luego se establece el valor si es verdadero (si la condición se cumple)
- luego el valor si es falso (si la condición no se cumple)

Estas estructuras están presentes en todos los lenguajes de programación y son sumamente útiles para determinar el flujo del programa.

En php existen varias formas de realizar estas estructuras, estas son:

- **If e if-else**: son las estructuras más clásicas, donde a través de la palabra reservada if podremos establecer una condición.
- **switch - case**: se trata de otro tipo de estructura condicional donde podremos optar por casos, estas son útiles cuando queremos establecer varios casos de aprobación.
- **Operadores ternarios**: es un tipo simplificado de condicional, que por lo general se aplica en una sola linea de código, esto ayuda a simplificar la lectura del código ya que no tiene la complejidad del if.

### Estructura condicional IF

Esta es una de las estructuras más conocidas, y más utilizadas a lo largo de los años y de la programación. Todos los lenguajes tienen una variante de esta estructura.

```php
<?php
if($password == "mipassword1234" ){
    echo "acceso consedido";
}else{
    echo "acceso denegado";
}
?>
```

En este ejemplo dentro de los paréntesis estamos comparando el valor de una variable con el valor de una cadena **string**, para comparar debemos utilizar los operadores de comparación que vimos en la clase anterior.

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

### elseif

Es una variante del If, donde en una esepción podremos volver a preguntar por una condición.

```php
<?php
    if($password == "miclave123"){
        echo "accede como administrador";
    }elseif($password == "mipassword123"){
        echo "accede como usuario";
    }else{
        echo "no accede";
    }
?>
```

También podremos incluír en estas condiciones los operadores lógicos

- and &&
- or ll
- not !

```php
<?php
//ejemplo con && and
if($edad >= 18 && $estatura > 1.60){
    echo "puede pasar";
}else{
    echo "lo lamentamos no puede pasar";
}

//ejemplo con || or

if($edad >= 18 || $estatura > 1.60){
    echo "puede pasar";
}else{
    echo "lo lamentamos no puede pasar";
}

//ejemplo con ! not

$paseVip = false;

if(!$paseVip){
    echo "lo lamentamos no puede pasar";
}
//al negar, es como si preguntamos si $paseVip es false
?>
```

### Estructura Switch-case

Son estructuras que simplifican y evitan que utilicemos muchos ifs uno detras del otro.

Estas estructuras evalúan un valor y en base a eso es que disponen de varios casos, importante es que uno de estos casos debe ser **default**, por lo general colocamos allí lo que debe suceder cuando ningun caso se cumpla.

```php
<?php
$dia = "martes";

switch($dia){
    case "lunes":
        echo "hoy es lunes, primer día de semana";
        break;
    case "martes"
        echo "un dia parecido al lunes, aburrido";
        break;
    case "miercoles"
        echo "mitad de semana!!!";
        break;
    case "jueves"
        echo "hoy es jueves, ya falta poquito para el viernes";
        break;
    case "viernes"
        echo "es viernes y tu cuerpo lo sabe";
        break;
    default
        echo "es fin de semana, no molestar!!!";
        break;
}

?>
```

### Operadores ternarios

Es un tipo de sentencia de comparación, muy parecido al if, pero con la diferencia de que su uso es mucho más sensillo y en una sola linea, este método es muy popular en javaScript ya que permite el renderizado dinámico de componentes.

ejemplo:

```php
<?php
$edad = 17;

$mensaje = ($edad >= 18)? "Puede pasar": "lamentamos informarle que es menos y no puede pasar";

//en los operadores ternarios la estructura responde a la siguiente forma prueba lógica ? valor si es verdadero : valor si es falso;

echo $mensaje;
?>
```

## Ciclos

Los ciclos o bucles nos permiten repetir un segmento de código hasta que se cumpla una condición previamente establecida. Estos son sumamente útiles cuando utilizamos arrays, ya que nos permiten recorrer los valores que se encuentran dentro y manipularlos.

Actuamente PHP cuenta con cuatro tipo de ciclos o bucles estos son:

- **For**
- **While**
- **Do While**
- **For each**

### Ciclo For

```php
<?php
    //Ciclo for
    $array = ["manzana", "pera", "banana", "uvas"];
    $stop = count($array); //nos brinda el largo del array

    for($i = 1; $i >= $stop; $i++){
        echo "item: " . $array[$i];
    }
?>
```

### Ciclo While

ejecutará el ciclo mientras una condición sea verdadera

```php
<?php
$array = ["manzanas", "peras", "bananas", "uvas"];
$i = 1;
$stop = count($array); //guardo el largo del array

while($i <= $stop){
    echo "item: ". $array[$i-1];
    $i++;
}

?>
```

### Ciclo Do while

es muy similar a while, pero en este caso el ciclo se ejecutará al menos una vez.

```php
<?php
$array = ["manzanas", "peras", "bananas", "uvas"];
$stop = count($array);
$i = 1;

do{
    echo "item: ". $array[$i-1];
    $i++;
}while($i <= $stop);

?>
```

### Foreach

es un tipo de ciclo especial para recorrer arreglos, si bien los podemos recorrer como en los ejemplos anteriores con los otros ciclos, **foreach** es un tipo de ciclo especial diseñado para este fin.

```php
<?php
$array = ["manzanas", "peras", "bananas", "uvas"];

foreach($array as $item){
    echo $items;
}
?>
```
