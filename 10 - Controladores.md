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
