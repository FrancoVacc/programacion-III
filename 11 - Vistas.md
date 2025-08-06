# Vistas

## Cómo funcionan las vistas?

Las visatas son respuestas que se envían al cliente desde el controlador para ser renderizadas en el navegador del cliente.
Muchos sitios web Legacy, funcionan de esta manera, utilizando PHP tanto para el Frontend como para el Backend. Esto no es una práctica obsoleta ya que muchos frameworks actuales siguen funcionando de la misma manera. Un ejemplo de esto es Next.JS que emplea _Server Side Rendering_ o **Renderizado del lado del servidor**. en este caso lo que será enviado al cliente es un **HTML**.

Para esto es necesario construír la estructura html básica que contendrá la información. y dentro de la carpeta vistas los módulos de HTML con PHP embebido.

## Cómo hacer en el caso de una API

En este caso debemos enviar un JSON _JavaScript Object Notation_ directamente desde el controlador. En este caso no hace falta construír la estructura de vistas ya que el controlador se encargará de estructurar y enviar el JSON como respuesta.

### Estructura de un JSON

```json
{
  "nombre": "Ricardo",
  "apellido": "Ramírez",
  "direccion": "Carmen Gadea 20",
  "correo": "ricardoramirez123@mail.com",
  "telefono": "3444-444444"
}
```

Un **JSON** es un objeto, originalmente de JavaScript, pero adopatado como estandar gracias a su simplicidad y su fácil manipulación. Este cuenta con el esquema clave - valor y puede ser manipulado muy facilmente.

En el caso de una API, el Backend recibe datos a través de las peticiones en formato **JSON**, y las procesa, también responde a través de estos objetos.

### Obtener JSON con JavaScript

Para obtener un objeto con JavaScript, debemos enviar una petición al servidor utilizando _fetch_ o _AXIOS_
