# Programación Orientada a Objetos en PHP (POO)

La programación orientada a objetos es un paradigma de la programación, donde todo el software se intenta volver menos abstracto utilizando "objetos" que actuan como los objetos de la vida real. El objetivo de esta programación es intentar acercar la lógica de la programación al mundo real.

Este paradigma es muy importante y cobró mucha relevancia en los lenguajes de programación modernos, haciendo que la mayoría de los lenguajes adoptaran este paradigma como base. Esto no quiere decir que todos los lenguajes si o si deben trabajar con este paradigma sono que se adaptaron para ofrecerlo como alternativa.

Un ejemplo de esto es el lenguaje PHP que en un principio no contaba con POO pero que a partir de la versión 5 comenzó a soportar este tipo de programación.

Este tipo de programación en lugar de centrarse en la lógica del programa, se enfoca en la interacción entre objetos para modelar la realidad o el problema que se quiere resolver.

## Conceptos que debemos tener en cuenta para trabajaro con POO

Hay conceptos que debemos conocer para poder trabajar con este tipo de programación. estos son:

- **Objetos**: Son las entidades que tienen estados (los atributos) y que pueden realizar acciones con ellos (métodos). Un ejemplo podría ser un auto, cuyos atributos podrían ser el color, la patente, el modelo, el tipo de motor, etc. y los métodos podrían ser por ejemplo que pueda arrancar el motor, que pueda marchar, que frene, etc.
- **Calses**: estos son como moldes para poder fabricar los objetos, sin las clases no tendríamos objetos. Las clases son una plantilla, es decir definimos en ellas aspectos generales del objeto que vamos a crear luego. dentro de la clase tendremos los atributos del objeto y sus métodos. una clase podría ser por ejemplo la clase auto (en general). Sabemos que todos los autos tienen un color, una patente, un motor, etc y que a su vez tienen los métodos.
- **Atributos**: Son las variables que almacenan información dentro de los objetos.
- **Métodos**: Son las funciones que determinan el comportamiento del objeto. Literalmente son funciones que estarán detntro del objeto.
- **Herencia**: muchas veces no es necesario contruir una clase de cero, sino que lo más común es construír una clase a partir de una clase ya existente y que esta herede los razgos de la clase superior. Explicado mejor, imaginemos que tenemos una clase Animal, con sus atributos y métodos. Si nos ponemos a pensar, un perro es un animal por lo tanto muchos de los atributos y los métodos de los perros pueden ser repetidos dentro de la clase Perro. Para aprovechar esto podemos hacer que la clase Perro se extienda de la clase animal y que herede todos los atributos y todos los métodos.
- **Encapsulamiento**: al trabajar con POO, podremos proteger algunos atributos o métodos de las clases, de esta menera podremos restringir el acceso desde fuera.
- **Plimorfismo**: Permite que un objeto pueda tener diferentes comportamientos dependiendo del contexto, lo que facilita la reutilización del código.
- **Abstracción**: Esta facultad oculta todo el funcionamiento interno del objeto y nosotros solo podremos interactuar con el a través de sus atributos y métodos, sin conocer como estos funcionan. Muchos lenguajes de programación funcionan así, por ejemplo en el lenguaje JavaScript todo es un objeto y estos objetos tienen métodos. ejemplo si creamos un arreglo, para obtener el largo debemos llamar al metodo length, el cual nos devuelve el largo del arreglo. Al llamar al método, nosotros no conocemos como este opera, ni que hace sino que solo conocemos el resultado de su proceso.

## Ventajas de la POO

Existen varias ventajas a la hora de trabajar con POO, estas son:

- Reutilización de código
- Mantenimiento y estabilidad
- Modelado en torno a lo real
- Mayor eficacia
- Trabajo en equipo
- Aplicación en nuevas tecnologías
- Desarrollo de cara al futuro

## POO en PHP

Para aplicar **POO** en **PHP**, debemos tener en cuenta la forma en la que vamos a estructurar el proyecto. Muchas veces la mejor forma es utilizar la arquitectura **MVC** O **Modelo Vista Controlador**, la cual está preparada para trabajar con proyectos enfocados a la Programación Orientada a Objetos.

Para comenzar a trabajar, debemos recordar los conceptos de POO

### Clases en PHP

Recordemos que una clase es un molde o plantilla, que contiene los **atributos** y los **métodos** que luego definiremos a la hora de crear nuestros objetos.

Para definir una clase debemos usar el siguiente código:

```php
<?php
//Creación de la Clase persona
class Persona {
    public $nombre; //Atributo
    public $apellido; //Atributo

    public function saludar(){  //Método
        return "hola mi nombre completo es ". $this->nombre . " " . $this->apellido;
    }
}

$persona = new Persona; // Instanciación de la clase
$persona->nombre = "Franco"; // Definición de atributos
$persona->apellido = "Vaccari";

echo $persona->saludar(); //Llamado al método
?>
```

> si miramos en el código anterior veremos cómo establecemos una clase, sus atributos y métodos.

### Encapsulamiento

El encapsulamiento es una forma que tenemos de darle protección a los atributos y los métodos de una clase. Esto es útil para resguardar la integridad de un objeto.

```php
<?php

class Persona{
    private $nombre;

    public function setNombre($nombre){
        $this->nombre = $nombre;
    }
    public function saludar(){
        return "Mi nombre es: ". $this->nombre;
    }
}

$persona = new Persona;
// $persona->nombre = "Franco" //esta acción no está permitida
$persona->setNombre("Franco");
echo $persona->saludar;
?>
```

> si miramos el código anterior veremos que el atriburo nombre solo es modificable desde dentro de la clase, no desde fuera. Para modificarlo debemos llamar al método.

En el caso de los **atributos** y **métodos** de tipo protected, estos solo serán accesibles desde **clases extendidas**.

**Para Recordar:**

- **Public**: Las propiedades y métodos declarados como public son accesibles desde cualquier parte del código, incluso fuera de la clase. Este es el modificador de acceso predeterminado si no se especifica ninguno.
- **Protected**:Las propiedades y métodos declarados como protected son accesibles dentro de la clase donde se definen y desde las clases que heredan de ella. No son accesibles desde fuera de la jerarquía de clases.
- **Private**: Las propiedades y métodos declarados como private son accesibles únicamente dentro de la clase donde se definen. No son accesibles desde ninguna otra clase, ni siquiera desde las clases derivadas.

### Constructor

El constructor de una clase es un método especial que nos obliga a definir los atributos fundamentales que deberá tener el objeto a la hora de ser instanciado.

```php
<?php
class Persona{
    public $nombre;
    public $edad;

    public function __construct($nombre, $edad){
        $this->nombre = $nombre;
        $this->edad = $edad;
    }

    public function saludar(){
        return "Hola mi nombre es ". $this->nombre;
    }

    public function decirEdad(){
        return "mi edad es ". $this->edad;
    }
}

//Al instanciar la clase si o si debemos colocar el nombre y la edad
$persona = new Persona("Carlos", 22);
echo $persona->saludar();
echo $persona->decirEdad();
?>
```

### Herencia y Polimorfismo

la herencia es la característica de una clase de heredar rasgos de la clase de la cual se extiende ejemplo

```php
<?php
//clase padre
class Animal {
    public $nombre;

    public function hacerSonido(){
        echo "sonido genérico de animal";
    }
}

class Perro extends Animal {
    public function __construct($nombre){
        $this->nombre = $nombre;
    }
}

$miPerro = new Perro("Firulais");
$miPerro->hacerSonido(); //sonido genérico
?>
```

> si nos fijamos, no es necesario declarar el atributo nombre en la clase perro ya que este lo hereda de la clase animal, lo mismo con el método hacerSonido()

Herencia de constructor, para que una clase herede el contructor de la clase padre, debemos declararlo para ello hacemos lo siguiente

```php
<?php

abstract class Personas {
    protected $nombre;
    protected $apellido;

    public function __construct($nombre, $apellido){
        $this->nombre = $nombre;
        $this->apellido = $apellido;
    }

    public function saludar(){
        echo "hola soy ".$this->nombre." y mi apellido es" . $this->apellido;
    }
}

class Pacientes extends Personas{
    protected $dni;
    protected $direccion;
    protected $telefono;

    public function __construct($nombre, $apellido, $dni,$direccion, $telefono){
        parent::__construct($nombre, $apellido); //a través de esta clausula, la clase hereda el constructor de su clase padre.
        $this->dni = $dni;
        $this->direccion = $direccion;
        $this->telefono = $telefono;
    }
}

```

En el caso de necesitar alterar algunas de las caracteríticas que la clase adquiere por herencia, esto lo podremos hacer redefiniendo el atributo o el método.

```php
<?php
//clase padre
class Animal {
    public $nombre;

    public function hacerSonido(){
        echo "sonido genérico de animal";
    }
}

class Perro extends Animal {
    public function __construct($nombre){
        $this->nombre = $nombre;
    }
    public function hacerSonido(){
        echo "Ladrar Guau! Guau!"
    }
}

class Pollito extends Animal {
    public function hacerSonido(){
        echo "pio pio";
    }
}

$miPerro = new Perro("Firulais");
$miPerro->hacerSonido(); //Ladrar Guau Guau
$miPillito = new Pollito;
$miPollito->hacerSonido(); //pio pio
?>
```

> En este caso redefinimos el método hacerSonido() para que cambie, ahora en vez de hacer un sonido genérico, este va a ladrar, en el caso del perro y va a hacer pio pio en el caso del pollito. El método adquiere diferentes formas según como lo extendamos.

### Abstracciones

se trata de clases abstractas, esto quiere decir que no pueden ser instanciadas, solo pueden ser extendidas, es decir que sirven como plantillas para otras clases. Los métodos y clases deben ser implementadas si o si por las clases instanciadas.

```php
<?php
abstract class Figura{
    abstract public function calcularArea()
}

class Circulo extends Figura{
    private $radio;

    public function __construct($radio){
        $this->radio = $radio;
    }

    public function calcularArea(){
        return pi() *  pow($this->radio,2);
    }
}

$miCirculo = new Circulo(22);
echo $miCirculo->calcularArea(); // 1.519,76
?>
```

### Interfaces

Es similar a las clases abstrctas, pero solo detalla los métodos que deben ser implementados al instanciar la clase.

```php
<?php
interface Autenticable{
    public function ($user, $pass);
}

class Admin implements Autenticable {
    public function login($user, $pass) {
        // lógica de login
        echo "Admin $user logueado";
    }
?>
```
