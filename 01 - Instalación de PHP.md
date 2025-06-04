## Instalación de PHP

### Instalar un servidor apache

Para este paso puedes utilizar XAMPP, WAMPP o laragon.

En lo personal recomiendo xampp ya que es gratuito y de código abierto.

Descargamos xampp desde el siguiente link:

https://www.apachefriends.org/es/index.html

realizamos la instalación como cualquier aplicación.

Debemos instalar xampp en la raíz de nuestro dispositivo en **C:**

debemos dirigirnos a **C:\xampp\php\php.exe\***
y copiamos la dirección ya que esta la debemos declarar dentro de las variables de entorno

para ello entramos a la barra de búsqueda de la barra de inicio y escribimos **editor de variables de entorno**

vamos a:

1. variables de entorno,
2. variables del sistema,
3. buscamos path,
4. nuevo y pegamos ahí la dirección.

una vez intalado esto, debemos abrir nuestro **Visual Studio Code**

allí buscaremos las siguientes Extensiones

- PHP Intelephense
- PHP Server

ahora probamos si funciona.

abrimos CMD, BASH o PowerShell y colocamos el siguiente comando:

```cmd
php -v
```

de esta manera veremos la versión de php que tenemos disponible en nuestra pc.

## Crear un proyecto en php

lo primero es abrir el gestor de xampp, si no está todo iniciado, lo iniciamos

luego buscamos en la opción **_explorer_** y hacemos clic.

buscamos la carpeta htdocs y la abrimos.

Creamos una carpeta llamada PrimerProyecto y la abrimos con VS Code.

Creamos un archivo llamado index.php y colocamos el siguiente códogo.

```php
<?php
    echo "Hola mundo"
?>
```

ahora vamos a la siguiente dirección en nuestro navegador:

http:localhost/PrimerProyecto
