# Conexión a bases de datos

En este texto vamos a ver como desde PHP podemos conectarnos a una base de datos MySQL y gestionar toda la información a través de consultas. Esto es fundamental ya que todos los sistemas por más pequeños que sean necesitan del guardado de la información.

## ¿Qué vamos a emplear?

Para trabajar con MySQL necesitamos tener instalado y funcionando **XAMPP**, o algún otro servidor local, contar con un administrador de bases de datos como **phpmyadmin** y lo más importante saber del lenguaje **SQL** para armar y realizar las consultas que corresponden.

## Conexión PHP - MySQL

PHP es un lenguaje que nació practicamente para gestionar bases de datos en servidores. Para ello tenemos varias opciones, dentro de las cuales las más utilizadas hoy en día son **mysqli** y **PDO**.
En este caso utilizaremos **mysqli** para gestionar nuestra conexión a la base de datos.

Recordemos un poco los conceptos de MVC y la modularización que esta arquitectura plantea.
Por un lado tenemos los **Modelos** que se encargan de interactuar con las bases de datos.
También tenemos los **Controladores** quienes se encargan de gestionar las entradas que recibe el servidor y las salidas que este envía al cliente.
Y las **Vistas** que son las respuestas que los controladores envían a través de una **API** en formato **XML** o **JSON** o simplemente un archivo **HTML** con todo el contenido.
Además de toda esta estructura, tenemos otros archivos importantes los cuales son muy útiles y que forman parte de la arquitectura MVC.
Entre estos se encuentran los archivos de **configuración** o **settings**, donde se pueden tener varios archivos importantes, entre ellos el de **conexión a la base de datos**.

## Archivo de Conexión a la base de datos - db.php

Este archivo es un simple script que pretende realizar la conexión a la base de datos para luego poder ser importado en otros archivos, como un módulo siempre que sea necesario.
La construcción de este archivo es sumamente importante ya que este será el nexo entre nuestro código y la base de datos.

```php
<?php

class db{
    protected $host;
    protected $user;
    protected $password;
    protected $dbName;

    public function _construct(){
        $this->host = "localhost"; //como trabajamos en local usamos ese nombre
        $this->user = "root"; // este es el usuario predeterminado
        $this->password = ""; // por lo general el usuario root no tiene contraseña
        $this->dbName = "prueba"; // el nombre de la base de datos no de la tabla
    }

    public function connect(){
        $con = new mysqli($this->host, $this->user, $this->password, $this->dbName) or die ("Error en la conexión");

        return $con;
    }

}

?>
```

> Tengamos en cuenta que estamos trabajando en un modo de prueba y en un entorno local, para evitar vulnerabilidades, la información de conexión como el HOST, USER, PASSWORD, DBNAME, debemos almacenarlo en un archivo .env o de entorno.

> Aclaremos también que la base de datos debe ser previamente creada en _phpmyadmin_ para evitar errores

## Ya me conecte, ahora qué hago?

Lo próximo será crear los modelos para trabajar con la base de datos. Lo más recomendable es tener un modelo por cada tabla, ya que estos se encargarán de gestionar la información de cada tabla.

Es sumamente necesario conocer la estructura de la base de datos con la que vamos a trabajar. Ya que muchas veces sucede que vamos a tener que almacenar información en varias tablas en una misma transacción. Aunque esto no es lo más adecuado, en ciertos casos no está mal. Pero en lo posible está bueno gestionar cada tabla en un modelo diferente.

# Modelo

## Operaciones Básicas de los modelos CRUD.

Las operaciones **CRUD** son las operaciones básicas que podemos realizar con las bases de datos y que más comunmente vamos a realizar a través de los modelos.

- **C - CREATE**: Se refiere a la creación de un nuevo registro dentro de una tabla en la base de datos. Esta operación se emplea para añadir información y guardarla.
- **R - READ**: Son operaciones de lecturas dentro de la base de datos, esto puede emplearse para traer muchos registros de tablas diferentes, de una misma tabla o un solo registro en concreto.
- **U - UPDATE**: Son operaciones utilizadas para actualizar información dentro de la base de datos.
- **D - DELETE**: Son operaciones que permiten eliminar de forma permanente registros dentro de la tabla.

Veamos el ejemplo en un modelo

```php
<?php

require_once './settings/db.php'; //inclusión del script de conexión

class Estudiante {
    protected $db;

    public function _construct(){
        //Dentro del constructor establecemos la instancia a la conexion y asignamos esto al atriburo db.
        $conection = new db;
        $this->db = connection->connect();
    }

    // Operaciones Read
    public function get(){
        //Función para obtener todos los elementos de la tabla.
        $query = "SELECT * FROM estudiantes"; //guardamos la consulta dentro de una variable
        $stmt = $this->db->prepare($query); //prepara la consulta
        $stmt->execute(); //ejecuta la consulta

        if($stmt->error){
            return ['message'=>'Error en la lectura']; //devolvemos si hay un error en la lectura
        }

        $res = $stmt->get_result(); //Obtenemos los resultados
        $data_arr = [];

        if ($res->num_rows > 0) {
            while ($data = $res->fetch_assoc()) { // obtenemos los resultados en forma de arreglo asociativo
                array_push($data_arr, $data); //guardamos los resultados dentro de un arreglo
            }
            return $data_arr; // devolvemos el arreglo con toda la información
        }
        return ['message'=>'sin datos'];
    }
}

?>
```

> Aclaremos que **mysqli**, es un objeto y como todos los objetos tiene métodos que al ser instanciado podemos tener acceso. Para conocer más sobre estos métodos podes revisar el siguiente archivo [Manual MySQLi](https://www.php.net/manual/es/book.mysqli.php)

Así como esta operación, deberemos hacer las demás, siempre siguiendo el mismo esquema:

- primero guardamos la consulta en una variable
- preparamos el statement o declaración _variable $stmt_
- ejecutamos la consulta
- controlamos que no haya errores
- obtenemos el resultado de la consulta
- procesamos y guardamos el resultado y lo preparamos para enviarlo al controlador.

en el caso de una operación **_CREATE_**

```php
<?php
public function create($data)
{
    $query = "INSERT INTO estudiantes (nombre, apellido, direccion, correo, telefono) VALUES (?,?,?,?,?)"; //la query tiene signos de ? es aquí donde hacemos el bindeo
    $stmt = $this->con->prepare($query);
    $stmt->bind_param('sssss', $data['nombre'], $data['apellido'], $data['direccion'], $data['correo'], $data['telefono']); //realizamos el bindeo, esto se hace para inyección SQL.
    $stmt->execute();

    if (!$stmt) {
        return ['message'=>'Error en la ejecución de la consulta'];
    }

    return['message'=>'carga exitosa'];
}

?>
```

> En este caso y siempre que vayamos a instruducir datos en la base de datos, es importante realizar lo que se conoce como _bind_ con esto evitamos inyecciones de SQL y consultas maliciosas.

> En PHP, hacer "bind" es crucial para la seguridad y eficiencia al interactuar con bases de datos a través de consultas preparadas. Permite evitar ataques de inyección SQL y optimizar el rendimiento al reutilizar planes de ejecución de consultas.

# Controlador

## Cómo trabaja el Controlador?

Recordemos que el controlador es el nexo entre la entrada y la salida. Es el encargado de controlar los datos que ingresan, manipularlos para que estén correctos y asegurarse de que los datos que viajan al modelo para que estos sean procesados. También prepara las respuestas y retorna una vista al cliente.

un ejemplo del Contolador

```php
<?php
require_once './models/Estudiante.php';

class EstudianteController
{
    public function obtenerEstudiantes(){
        $estudiantes = new Estudiante; //Instanciamos la clase Estudiante del modelo
        return $estudiantes->get(); //ejecutamos el método get
    }
}
?>
```

> En el ejemplo anterior, vemos que es sensillo ya que no debemos procesar ningun dato, solo leer de la base de datos los estudiantes. El método get() que se utiliza allí es el método del modelo.

### Cómo procesamos una carga de datos?

Imaginemos que necesitamos procesar un formulario o que recibimos a nuestra api el pedido de carga de datos, por más de que en el frontend hayamos hecho todos los controles, siempre hay formas de inyectar código malicioso y debemos evitar que este código llegue a nuestras bases de datos. Para esto el controlador debe estar bien diseñado y estructurado.

Veamos el siguiente ejemplo:

```php
<?php
public function crearEstudiante($data)
{
    // Utilizamos Expresiones Regulares para evitar que pasen datos incorrectos.
    if (!preg_match('^[a-zA-Z-áéíóúÁÉÍÓÚñÑüÜ\s]+$^', $data['nombre'])) {
        header('Location: index.php?error=nombre');
    }
    if (!preg_match('^[a-zA-Z-áéíóúÁÉÍÓÚñÑüÜ\s]+$^', $data['apellido'])) {
        header('Location: index.php?error=apellido');
    }
    if (!preg_match('^[a-zA-Z0-9áéíóúÁÉÍÓÚñÑüÜ\s]+$^', $data['direccion'])) {
        header('Location: index.php?error=direccion');
    }
    if (!preg_match('^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$^', $data['correo'])) {
        header('Location: index.php?error=correo');
    }
    if (!preg_match('^[a-zA-Z0-9áéíóúÁÉÍÓÚñÑüÜ\s]+$^', $data['telefono'])) {
        header('Location: index.php?error=telefono');
    }

    $estudiante = new Estudiante;

    $estudiante->create($data);

    header('Location: ../index.php?ok=crate');
}
?>
```

### Función preg_match()

Esta función compara el valor de un dato con una expresión regular, en caso de que coincida devuelve un _true_ y si estos no coinciden devuelve _false_, de esta forma nos aseguramos de que los datos que viajen a la base de datos sean correctos.

En este caso, si da false, se envia a una vista exclusiva que maneja el error. Esto es muy común por ejemplo, en formularios de Login cuando ponemos mal el usuario o cuando ponemos mal la contraseña.

### Cómo crear una expresión regular

Para crear una expresión regular debemos tener en cuenta la estructura que ésta tiene, antes era muy común que el mismo programador arme la expresión regular a mano, hoy en día es una tarea para la IA.
