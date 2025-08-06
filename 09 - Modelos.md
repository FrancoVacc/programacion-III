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
