# Archivos de Entorno y Enrutador

Para hacer más segura nuestra API y para trabajarla de forma "profesional", nos hace falta tener algunos pequeños conceptos. Necesitamos valernos de estructuras que aseguren el correcto funcionamiento y la privacidad de los datos sensibles.

Es por esto que he optado por traerles dos librerías muy buenas para incluír en nuestra API rest.

## Manejo del Entorno

Las variables de entorno son un tipo de variable que permanecen ocultas. Estas se declaran en un tipo de archivo localizado en la raíz del proyecto con la denominación `.env`

```.env
DB_HOST = "localhost"
DB_USER = "root"
DB_PASSWORD =
DB_NAME = "nombre de la base de datos"
```

> Dentro de estas variables podremos tener cualquier tipo de información sensible. los nombres de las variables deben colocarse en Mayúsculas.

PHP no cuenta con soporte nativo para leer este tipo de archivos, aunque si soporta las variables en su código.

Para que PHP pueda leer estos archivos es necesario incluír una pequeña librería de terceros.

Aunque existen muchas de estas librerías recomiendo utilizar la de [vlucas/phpdotenv](https://github.com/vlucas/phpdotenv), ya que es muy fácil de implementar y está muy bien documentada.

para leer los archivos `.env`, unicamente necesitamos crear un pequeño archivo de PHP dentro de nuestra carpeta settings al que llamaremos `dotenv.php` dentro de este archivo colocaremos el siguiente código

```php
require_once __DIR__ . '/../vendor/autoload.php';

$dotenv = Dotenv\Dotenv::createImmutable(__DIR__ . '/../');
$dotenv->load();
```

> Ahora, cuando necesitemos leer las variables de entorno en un archivo, unicamente importamos este pequeño archivo.

Para leer una variable de entorno desde nuestro código utilizaremos una variable superglobal que nos permitirá acceder a un arreglo con todas las variables de entorno declaradas dentro de nuestro `.env`

```php
$variable = $_ENV['DB_HOST'];
```

En un ejemplo más concreto te mostraré un archivo de conexión de base de datos.

```php
require_once 'dotenv.php';

class Database {
    private static $host;
    private static $user;
    private static $pass;
    private static $db_name;

    public static function connect(){
        self::$host = $_ENV['DB_HOST'];
        self::$user = $_ENV['DB_USER'];
        self::$pass = $_ENV['DB_PASSWORD'];
        self::$db_name = $_ENV['DB_NAME'];

        $con = new mysqli(self::$host, self::$user, self::$pass, self::$db_name) or die('error en la conexión');
    }
}
```

> Cuando usamos métodos estáticos, también debemos declarar los atributos como estáticos. De esta manera, todo dentro de la clase es estático y no es necesario crear una instancia de la clase. Además, al ser estáticos los atributos, no necesitamos definir un constructor.

## Enrutador

Un enrutador o router, es utilizado para el manejo de las rutas dentro de nuestro proyecto. Esto es muy útil cuando construímos una API, ya que de esa forma podemos manejar los endpoints que nuestra API manejará.

Para ello necesitaremos una librería de terceros. Aunque hay muchas de estas librerías recomiendo utilizar la de [miladrahimi/phprouter](https://github.com/miladrahimi/phprouter) ya que es muy similar el manejo al que tienen muchos frameworks famosos de PHP como Laravel o Symphony.

este router utiliza nuestro archivo index para capturar las rutas a través de un archivo `.htaccess` este archivo se encarga de redirigur todo hacia el archivo especificado en su interior. Para crearlo debemos hacerlo en la raíz de nuestro proyecto con el siguiente contenido:

```htaccess
<IfModule mod_rewrite.c>
    <IfModule mod_negotiation.c>
        Options -MultiViews
    </IfModule>

    RewriteEngine On

    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteRule ^(.*)/$ /$1 [L,R=301]

    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteRule ^ index.php [L]
</IfModule>
```

> Esto apunta directamente al index

Ahora dentro del index debemos importar unicamente la librería y declarar una instancia para el enrutador y las rutas

```php
require_once 'vendor/autoload.php';
use MiladRahimi\PhpRouter\Router;
use Laminas\Diactoros\Response\JsonResponse;

$router = Router::create();

$router->get('/', function () {
    return new JsonResponse(['message' => 'ok']);
});

$router->dispatch();

```

> las nuevas rutas deben encontrarse declaradas despues de la instancia y antes del método dispatch

La estructura de la ruta es la siguiente

1. primero hacemos referencia al objeto a través de la instancia.
2. llamamos al método según corresponda con el verbo HTTP este puede ser get, post, put, patch, delete.
3. luego especificamos la ruta como primer parámetro.
4. Luego especificamos la acción que la ruta realizará utilizando un Callback. En este punto también podremos llamar a un método de un controlador.

Ejemplo:

```php
require_once 'vendor/autoload.php';
require_once 'controller/categoriaController.php';
use MiladRahimi\PhpRouter\Router;
use Laminas\Diactoros\Response\JsonResponse;

$router = Router::create();

$router->get('/', function () {
    return new JsonResponse(['message' => 'ok']);
});

$router->get('/categorias', [CategoriaController::class, 'obtenerCategorias']);

$router->dispatch();
```

> de esta manera podremos utilizar rutas para dirigirnos a nuestros controladores y devolver los JSON correspondiente.

Así legamos la estructura MVC que veníamos utilizando a un Router y a una API de tipo Rest.
