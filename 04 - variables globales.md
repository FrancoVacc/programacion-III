# PHP como Backend

Php trabaja como un lenguaje de backend ya que permite procesar información dentro de un servidor, almacenar en las bases de datos y a su vez enviar una respuesta. Para esto debemos utilizar un protocolo de transferencia como lo es el protocolo HTTP.

Un ejemplo claro de esto es cuando rellenamos un formulario de inscripción en internet y damos click en el botón enviar. Estamos enviando información a través del protocolo HTTP.

Este protocolo es fundamental para el **Backend** ya que a través de sus verbos la información llega desde el **Frontend** y puede ser gestionada apropiadamente.

Veamos un poco sobre este protocolo

## Protocolo HTTP

Este protocolo significa _HyperText Transfer Protocol_ y es un protocolo de transferencia de hipertextos. Con este protocolo podremos conectarnos a través de **endpoints** a un servidor y exigirle una respuesta.

Este protocolo cuenta con algunos verbos para poder trabajar, que deberemos manejar para que la información viaje de forma segura.

los verbos son:

- Get (para obtener información)
- Post (para crear información)
- put/patch (para actualizar información)
- delete (para borrar información)

Estos verbos son manejados desde las cabeceras de las consultas que realizamos a través del navegador y son recibidos por el backend para que este ejecute una acción y devuelva un resultado.

## Resultados a través de una APIRest

Lo más común hoy en día es que en el servidor tengamos montado un backend que gestione la información y que brinde un servicio, donde cualquier aplicación Frontend sea del dispositivo que sea pueda conectarse y obtener información. Para ello se utiliza lo que conocemos como **Rest API**, una interfaz que utiliza un tipo de dato **JSON** (JavaScript Object Notation) para enviar y recibir datos.

Las ventajas de trabajar de esta manera es que podremos crear un Backend en cualquier lenguaje de programación que pueda correr en un servidor (php, java, c#, python, node.JS, Ruby, Go, etc.) y que sin importar el lenguaje de programación, la respuesta sea estandarizada. Para que cualquier Frontend ya sea Desktop, Web o Mobile, pueda conectarse y consumir sus datos.

## Cómo hacemos Backend con php?

Para hacer backend en php hay muchas maneras, lo más apropiado es usar el Stack php, MySQL o usar un Framework como es Laravel que ya cuenta con todas estas funcionalidades.

### Lo básico

Para comenzar a trabajar con backend es esencial poder probarlo sin contruir un frontend, para ello vamos a trabajar con una extensión de Visual Studio Code llamada [ThunderClient](https://marketplace.visualstudio.com/items?itemName=rangav.vscode-thunder-client)

Este te permitirá realizar llamadas a endpoints manejando los verbos de HTTP, crear cabeceras y crear los bodys.

### Variables Globales en php

Estas son variables con alcance en todo el proyecto, podemos declararlas tanto dentro del Script como por fuera a través de distintos métodos HTTP.

Estas variables son útiles para pasar información de un archivo php a otro o simplemente para captar información proveniente del lado del cliente, Permitiendo de esta manera una interacción directa.

### Principales Variables Globales en PHP

PHP ofrece un conjunto de superglobales que están disponibles en todo momento sin necesidad de declararlas como global.

| **Variable** | **Descripción**                                             |
| ------------ | ----------------------------------------------------------- |
| $\_GET       | Datos enviados por URL (método GET).                        |
| $\_POST      | Datos enviados por formulario (método POST).                |
| $\_REQUEST   | Combina $\_GET, $\_POST y $\_COOKIE.                        |
| $\_SERVER    | Información del servidor y del entorno de ejecución.        |
| $\_SESSION   | Datos de sesión.                                            |
| $\_COOKIE    | Cookies enviadas por el navegador.                          |
| $\_FILES     | Archivos subidos.                                           |
| $\_ENV       | Variables de entorno.                                       |
| $\_GLOBALS   | Acceso global a todas las variables definidas en el script. |

Nos vamos a centrar unicamente en las variables **$\_GET** y **$\_POST** por ahora.

### Variable $\_GET

Esta variable nos permite obtener información que viaja en la URL de la consulta, por ejemplo

Imaginemos que tenemos un sitio web que se llama www.tienda.com el cual es un ecommerce, y en el tenemos varios productos. Estos productos están almacenados en una base de datos. esta base de datos debe ser leía de alguna manera. De esto se encargará el backend.

Queremos consultar el producto que tiene el id 1 para ello es apropiado que en la URL pasemos un **parámetro Query** o de consulta. Nos va a quedar algo así:

www.tienda.com/productos?id=1

todo lo que está luego del signo de pregunta es una variable y su valor. y de esta forma podemos enviar esto al servidor. La unica desventaja de esto es que los parámetros quedan visibles y se guardan en el navegador lo que lo hace inseguro para datos sensibles.

El Backend debería recibir este parámetro y manejarlo para ello debemos acceder a la variable $\_GET y obtener el valor

```php
<?php
$id = $_GET['id']; //la variable $_GET, funciona como un arreglo Clave valor que contiene los parámetros enviados por la url.

echo $id; //mostraríamos el id;

```

Esto nos abre muchisimas posibilidades ya que ahora podríamos solicitar información al backend a través de un endpoint.

### Variable $\_POST

Es una variable global igual a la variable $\_GET, un arreglo clave-valor. Con la diferencia que en vez de manejar los parámetros a través de las URL, lo hace a través de formularios o JSON. Siempre teniendo encabezados.

```html
<form action="clientes.php" method="POST">
  <input type="text" name="nombre" placeholder="nombre" />
  <input type="text" name="apellido" placeholder="apellido" />
  <input type="email" name="email" placeholder="email" />
  <input type="submit" value="enviar" />
</form>
```

Este formulario envía al archivo clientes.php la información y será recibida de la siguiente forma

$\_POST['nombre'=>'Alejandro', 'apellido'=>'González', 'correo'=>'ale@mail.com'];

nosotros tendremos la posibilidad de manejar esta variable extrayendo los parámetros que necesitamos.

```php
//archivo clientes.php
<?php
$nombre = $_POST['nombre'];
$apellido = $_POST['apellido'];
$correo = $_POST['email'];

//guardar en la db
```

Este ejemplo de arriba, es todo lo que **no** hay que hacer ya que debemos hacer muchisimos controles a la hora de manejar datos, para evitar cualquier intento de **hakeo** en nuestro backend.
