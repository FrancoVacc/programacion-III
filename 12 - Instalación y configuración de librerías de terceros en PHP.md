# Instalación y configuración de librerías de terceros en PHP

En PHP como en muchos otros lenguajes de programación, se busca la eficiencia del código. Para ello y para ahorrar tiempo a la hora de hacer nuestros programas, podemos reutilizar código de otras personas cuyas licencias son de libre acceso o de pago.

Muchas veces existen tareas que necesitamos hacer y que programarlas desde cero se torna difícil y engorroso. Para ello lo único que debemos hacer es instalar una dependencia en nuestro código, para luego importarlas y utilizarlas.

## Cómo intalamos una librería

Las librerías en PHP, como en cualquier otro lenguaje, se destinan a resolver un problema puntual dentro de nuestro código. Por ejemplo, si necesitamos recoger el pago de un cliente en una plataforma de e-commerce, sería engorroso tener que programar y realizar todas las estructuras necesarias para poder procesar y recibir pagos. Para ello utilizaremos una pasarela de pago de terceros como la pasarela de MercadoPago.
Puede que también necesitemos enviar E-Mails desde nuestro código, muchas veces esto es una técnica recurrente a la hora de registrar usuarios o de registrar cambios en sus contraseñas o simplemente para informar. También podremos recurrir a diferentes librerías de email como PHPMailer.
Estos son ejemplos de librerías de uso público en PHP.

Ahora para realizar la instalación de estas librerías no solo basta con encontrar un repositorio de github o encontrarlas en alguna página. Sino que debemos hacer algunas cosas extra.

### Manejador de Paquetes Composer

Para poder instalar librerías de terceros, debemos descargas e instalar un manejador de paquetes llamado **[Composer](https://getcomposer.org/)** el cual se encargará a través de instrucciones, de instalar y configurar las dependencias de nuestro proyecto.

Para instalar **Composer** debemos dirigirnos al [sitio oficial](https://getcomposer.org/) y descargar el instalador.

Allí nos encontraremos con su logo oficial

![Logo de composer](https://getcomposer.org/img/logo-composer-transparent5.png)

una vez allí podemos ir al apartado de descargas y veremos todas las opciones que tenemos para realizar la instalación.

En primer lugar nos encontraremos con la forma de instalación a través de su instalador oficial.

puedes descargarlo desde [aquí](https://getcomposer.org/Composer-Setup.exe)

una vez instalado en tu computadora deberás reiniciarla para asegurar que se haya instalado correctamente.

para asegurarte que se encuentra instalado, puedes abrir una terminal ya sea de CMD, de PowerShell o BASH y poner el siguiente comando

```cmd
composer --version
```

esto dará como resultado lo siguiente

```cmd
Composer version 2.8.4 2024-12-11 11:57:47
PHP version 8.2.12 (C:\xampp\php\php.exe)
Run the "diagnose" command to get more detailed diagnostics output.
```

Esto indicará la versión de composer con la que cuantas, la fecha y la hora de la instalación y la versión de php que estas manejando en este momento.

### Buscando librerías para tus proyectos

Para buscar librerías para tus proyectos, debes dirigirte al siguiente sitio [packagist](https://packagist.org/) este sitio es un sitio oficial donde encontrarás muchas de las librerías de usuarios certificados. También encontraras aquí la guía de implementación de las mismas.

Una vez que encontremos la librería que queremos utilizar debemos utilizar el siguiente comando para su instalación dentro de la raíz del proyecto donde estamos trabajando.

> Es recomendable que lo ejecutes con la terminal de tu visual Studio Code ya que esta siempre esta ubicada en la raíz del proyecto

```cmd
composer require <nombre de la librería>
```

> Por lo general esto se explica en cada documentación.

Una vez que se termina la instalación, veremos que dentro de nuestra raíz encontraremos nuevos archivos instalados.
estos son

- **_Carpeta Vendor_**: la cual contendrá todo el contenido de la librerías. Esta se crea de forma automática cuando instalamos la librería.
- **_Archivo composer.json y composer.lock_**: son archivos que describen las dependencias de nuestro proyecto. estos archivos son utilizados para instalar las librerías si en algún momento clonamos el repositorio.

Si seguiste todos estos pasos de forma correcta, ya deberías tener instalada tu librería y podrías comenzar a utilizarla en tu proyecto.
