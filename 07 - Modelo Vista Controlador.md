# MVC - _Model View Controller_

Cuando hablamos de MVC, estamos hablando de un patrón de diseño o arquitectura de diseño de sistemas donde se modulariza el proyecto en tres grandes partes, con el fin de tener una mayor organización y hacer más fácil la programación. Esta arquitectura puede ser aplicada a cualquier modelo y en cualquier escala, y permite un crecimiento ordenado de las aplicaciones.

MVC pude ser aplicado o llevado a cualquier lenguaje de programación, esto nos permitirá trabajar de forma más cómoda una vez que aprendamos a trabajar con este modelo.

## ¿Cómo dividimos una aplicación en MVC?

Esta arquitectura plantea tres componentes bien definidos, a que se encargan de una tarea específica cada uno. estos son:

- **Modelo:** Es un componente que se dedica a realizar las transacciones con la base de datos, este debe recibir las instrucciones para hacer peticiones a la base de datos y devolver siempre un resultado. Imaginemos un proyecto pequeño que maneja productos, clientes y pedidos. Cada uno de estos tendrá un modelo.
- **Vista:** Las vistas por lo general están asociadas con el FrontEnd. En muchos proyectos es así pero en otros no, ya que las vistas pueden representar las respuestas generadas por el sistema en formatos como JSON, XML, etc.
- **Controlador:** Se trata de un componente nexo entre las peticiones, los modelos y las vistas, al igual que el modelo este corresponde a cada componente del sistema, dentro de los controladores se debe, validar, verificar y manejar errores que provengan del Frontend y de los modelos.

## Otros Componentes

Dentro de la estructura MVC, existen otros componentes extra, dependiendo del tipo de proyecto, lenguaje de programación y demás. En proyectos web, lo más común es el uso de un **Router** o componente enrutador, otro podría ser un **seeder** para rellenar bases de datos de forma rápida y con datos de prueba, también componentes de **configuración** como la conexión a la base de datos, archivos de **variables de ambiente**, **Middlewares**, encargados de controlar parámetros y restringir o autorizar accesos, etc.

### Router

El router es un componente muy importante, este se encarga de gestionar las peticiones que llegan al servidor desde el cliente. Recordemos que por lo general siempre se utiliza el protocolo **HTTP** y sus verbos **GET, POST, PUT, PATCH, DELETE**, este router se encarga de gestionar esto y de llamar al controlador correcto en el momento que se necesite.

### Middleware

Un middleware es un intermediario, imaginemos que tenemos funciones que solo las puede realizar el administrador, como por ejemplo cargar un nuevo producto. entonces el middleware debe encargarse de controlar que quien tenga acceso a esa funcion sea solo el administrador, por más que el usuario haya tenido acceso a un endpoint restringido. Estos son muy útiles ya que le agregan mucha seguridad a nuestros sistemas.

## MVC en PHP

PHP es un lenguaje que con los años se ha podido adaptar muy bien a los nuevos requerimientos de los programadores. Es super importante saber que PHP cuenta con la posibilidad de trabajar con MVC ya sea en forma pura o a través de un framework como Laravel.
En PHP puro es un poco más dificil ya que debemos crear desde cero la estructura de carpetas y organizar nuestros componentes. En cambio en Laravel esto ya está todo hecho.

## Ejemplo de MVC en PHP

Veamos un pequeño ejemplo y el flujo de información del MVC

### Estructura de carpetas

```
API
 └ config
 |   └ db.php
 └ model
 |   └ Products.php
 └ controller
 |   └ productsController.php
 └ view
 └ vendor //Carpeta de libreria
 └ .htaccess //Archivo de acceso
 └ index.php // punto de entrada
```

> En el caso anterior, se puede ver la distribución de carpetas, la carpeta Config, tiene los archivos necesarios para conectarse a la base de datos, la carpeta model, tendrá todos los modelos que interactuarán con la base de datos. la carpeta controller, tendrá todos los controladores y la carpeta view tendra todas las vistas.

### Gráfico de flujo de información.

![Grafico MVC](https://lh3.googleusercontent.com/fife/ALs6j_ESm32cifSKXcNApukQjCNK3M0bkspJbreWBCMRB2mmC4FbGmbh-TCLB1hdwpKBeQFS38XsoETttCz3BNE_lduuIyLdlur05_iOFmtdPLvL6OrRnl6JpUNaG6QjWHWe7VHipVM8WAaRB9k52mGJFYPTa_Xm89sx8GT2H8sQOdFtMnsDUWoA4GbVOHYv6jO3uPozqTjIA4K1gxE16Mxh-yKgC4F8G9B66P6xrZmNkmLus0wX9bxdfBjWYv7em-aj2l-yTLDjRLSS1PQQ6oVTRKrjtTnswUaxTD9ijBHgpnW9mKzuy13UHpgHqeyyYeTzvnPYR3c-rZ6lotq3oA05VwpWV7Ww7zVBMIumYQIoWy_VLLyQ7RFISSSd8bacQ8H3A8CTmArSPo1M7mVFWGJZ8nq5E5P6d-7CpXlRAs7zt2ks2_qkF3pGGr-akpv1JhOwc7s6dMeWczyYs8rpfPxoUbLJNHmtGs2noruMETMhn8nE23QIxz-JEf1HVzde0jzFVmpkyNwfpDSdUc9MXJqmw61r5PCyU4l0Ttod32KGvNVPJAMH4h3Yp925YqN-CCH2yu4bJcbqbX8E2vIDD6zkVqA0Jzx5aXbZy-qNjYjEzV4QFY4IRWr9w1DEBA8zdssYhtAG8IybEGb31eyGdteJqJf1CQsbRBr0pG1ckvxSRP9gRFvSMnRmIpMQ05cGxD9VEdDzY9wVzOVdglipgbf8XqzmxrlNAFkgDc_G-NdOM_dFYogDHgAy_5BK_161EwlTyt8ZYpvottRrBWIwuk-ZQrMTdP2j8Z2a9XbqNK_4mqj6mBCDoSonRgAW1k-MQSPFFtKMl49EoykMvGSUgvT3XCVRnk5wNROZhcNFyRHoX3zIBTaYI3kPIRxxj8TpQXMXveP2tyYVQQh0BzO142IiZXTKUbpC4KSbCx7FVuZYAXB-K7R8uCSMLILdMj5TVVNJ5qLPvS36WfssjkSajQAtsBuikjEIJTGXuH-zOKKonuCU8jZHfkxS5dkVbZEFOIqDVFLygbS9BhK8VYo2Pb7R9efPqRW2pocVx5sOPZ4dqE396nt6sd4pHG1oMjc9FULjiigiphuGHDnLgcXUdFW8Fk-F0MupxRPc3DRdqu54zG1y0pUikyftN7Di86dXdJQU4VpYr1wFviWZuD7YjFXgc1bqTCCrDKNnJnYXylaVBVGwUrxbK2yO-e21wnqnkkCm8nLPrzw7k4pzBzNCMTHdALZDvzMWCSBg1SCZJp1aZOkoR1mcrpvqElbk-tm6l0cuol3w8fpUXnG7m3DZpJ19pu8nEs-WZyg_aH4jU4_VreMaqKVhhRJSC-fLMhaXNTy65MEzbePi3OMlUnY0ZJu8aed0dZMrvY2rhGwzzvuiKaaL7zkY9c5D1ywolCdiuTudhqu4uPTxL8HEnG99JVa--w1v9WwsAi5V1spXD2xFKq3i6DEznOIIsDqaL85GRJ1QO1Opy6qqFXTpHjG8OtMWmGghDdvCcEQGxn493S-I9Te50rL5Y9hxrEk85zqMBx3Jj8ciWDYgMQWcALmnjLfN_S6xgqzWy0vMJtcIvVh5IXO57QbiF5DktpFG1mNVvyeNEG-dceJQFzeB5qbCeXI5ISk06IpWDQs6HTjPlfjjTVD8K7S4tqFlItMDw5oo6Xcp4niVCdwZSQ=w1366-h613?auditContext=forDisplay)
