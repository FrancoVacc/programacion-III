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
