# API Rest y sus conceptos

Ultimamente en la programación, la tendencia es separar la parte visual de la lógica.

De esta manera nacen los conceptos de **Backend** y **Frontend** los cuales tienen funciones y ambientes sumamente específicos.

Por un lado el **Backend** habita en el **Servidor** este convive muchas veces con la base de datos y con servicios de la nube para facilitar el almacenamiento.

Por otro lado el **Frontend** es la parte del sistema que habita en el **Cliente** y se refiere a toda la parte visual y la lógica que se da dentro del dispositivo del cliente. Estas pueden ser aplicaciones de tipo web, aplicaciones de escritorio, aplicaciones móviles, etc.

Con esta división logramos conectar nuestra aplicación Backend a cualquier tipo de aplicación Frontend sin necesidad de programar y adaptar nuestro backend a todos los tipos de dispositivos sino que nos permite programar la lógica de negocio solo una vez y adaptar unicamente el frontend a las necesidades del cliente.

## Cómo comunicamos el Backend con el Frontend?

Para establecer una conexión entre estas dos partes, necesitamos tender un puente entre el cliente y el servidor. Sí bien hay muchas formas de hacerlo, lo más común es utilizar consultas a través del protocolo **HTTP** _(HyperText Transfer Protocol)_, y sus verbos **GET, POST, PUT, PATCH y DELETE**.

La aplicación del cliente debe estar preparada para enviar peticiones y esperar respuestas. En tanto a la aplicación Backend debe estar preparada para recibir las peticiones, procesarlas y devolver una respuesta.

## Cómo se contruye este puente?

Para la construcción de este "puente" entre el frontend y el backend, debemos construír lo que se conoce como **API** _(Aplication Programming Interface)_ o Interfaz de Programación de Aplicaciones.

Sí prestamos atención al significado de API y recordamos los conceptos de Clases, veremos que una **interfaz** es la forma que tiene la clase de ocultar el funcionamiento y ofrecer un punto de acceso a estas funciones. Es, en pocas palabras, lo que el control remoto es para el televisor.

Teniendo esto claro, vamos a trabajar en esto desde el backend ya que será quién deberá procesar todas las peticiones provenientes del cliente.

Estas interfaces serán creadas empleando lo que se conoce como **Endpoints** o puntos de acceso a nuestra interfaz.

## Construcción de un Endpoint

Un endpoint no es más que una **URL** a la cual se puede acceder. Esto lo podemos hacer desde varias aplicaciones clientes.

Estos Endpoints cuentan con partes muy concretas:

- **Verbo**: se debe establecer el verbo HTTP que se va a utilizar ya que la api debe ser capaz de detectarlo y redirigir la consulta según el caso.
- **Header**: se refiere a los encabezados que viajan a través de la solicitud, estos sirven para muchas cosas, entre ellas, para establecer el tipo de consulta, el tipo de archivo que viaja, si hay o no un token de autorización disponible, etc.
- **Body**: El cuerpo de la consulta es empleado más que nada en solicitudes de tipo **POST, PUT, PATCH y DELETE** donde el cliente debe enviar información hacia la aplicación Backend.

De esta manera establecemos comunicación entre el Frontend y el Backend.

Por lo general el tipo de archivo que se transferirá es el formato **JSON** _(JavaScript Object Notation)_, tipo de archivo que nació en JS y que luego fué adoptado por la mayoría de los lenguajes de programación.

```JS
// Objeto en JavaScript
{
    nombre : "Franco",
    apellido: "Vaccari",
    edad: 33
}

// Objeto JSON
{
    "nombre":"Franco",
    "apellido":"Vaccari",
    "edad": 33
}
```

## Peticiones en el Frontend

Por lo general el frontend será contruído con tres tecnologías, HTML, CSS y JavaScript, aunque también puede ser construído con otros lenguajes de programación.

En el caso de una aplicación web, emplearemos JavaScript para realizar estas peticiones.

```JS
const getData = async () => {
    try{
        //usamos la api fetch integrada en JS de forma asíncrona ya que no sabemos cuanto tiempo tardará en llegar la respuesta.
        const res = await fetch('http://localhost/productos');

        // en caso de que la respuesta no llegue
        if(!res.ok){
            throw new Exception('Error en la conexión con el servidor');
        }

        // procesamos el JSON  y lo retornamos para que pueda ser manipulado.
        const json = await res.json();
        return json;
    }catch(e){
        //devolvemos el error
        throw e;
    }
}
```
