# CORS Cross Origins Resource Sharing

Es un mecanismo de seguridad implementado en los navegadores que limita el acceso de una aplicación a un dominio que no es el propio.
Esto limita las peticiones a APIS, ya que no permite que los datos viajen de un punto a otro.

Si bien nuestra aplicación web puede acceder a un endpoint, de una api, la respuesta permanecerá bloqueada por normas de seguridad.

## Cómo funciona esto

Imaginemos un momento que tenemos una aplicación frontend, alojada en el servidor `X` bajo el dominio `https://mifrontend.com` y necesita la información que está en otro servidor `Y` que se encuentra bajo el dominio `https://mibackend.com`

En este caso quiro que mi aplicación frontend obtenga toda la información que necesita para funcionar desde la API alojada en el otro servidor. Por lo que tratandose de un Frontend web lo más probable es que empleemos JavaScript para realizar llamadas a esta api de forma asíncrona.

```Js
    const getData = async() => {
        const url = 'https://mibackend.com'

        try{
            const res = await fetch(`${url}/usuarios`);

            if(!res.ok){
                throw new Error
            }

            const json = await res.json();
            return json
        }catch(error){
            console.log(error)
        }
    }
```

> Con este código, lograremos hacer una petición a la API, utilizando la URL declarada en la variable. Como se trata de una petición asíncrona, debemos utilizar try-catch y el await para que espere una respuesta. Sí res.ok no se encuentra, enviará un error y se retornará por el catch finalizando el proceso. en caso de que si haya una respuesta, la guardamos dentro de la variable json luego de obtener su contenido y lo retornamos.

Cuando hagamos esto, lo primero que nos encontraremos es con el siguiente error

![CORS](https://lh3.googleusercontent.com/rd-d/ALs6j_EzyBuoCADBTtveoWJkKnWigENc0f5Ql0Z9vggue_TNImFrfFp-8L8waqcbQalYLa1kl0QgOE5xLUBC2yRuBi-t11nP5D4sl3OCH9ewbv_8mRClfc8R6pA0el_XnfcfbVP-BOj9ZVNUUWeobKv-r85_QWIlXxRJNIEP4ZFkHq8gLaIbwDCZT1mO1VAv_ljX0RD1-OnZvZ1HYtyys_3dWpfRrwmgLz1YOVdPu1WfrCkYHZsf_y4s5fhifaynlbadeY_lH7DDjv9FSuXFsrnTpmWFih9hD9CC9eP1UeFlWn6CslxVn83pRSRe5-rv7lN0AzLOp2MJH2Hlv-5V0JRKZGFRqeLHi2aK72pH0KgS3I90oN21yWkSTRllW5w_-m5k7LOyXW_84w4CjyZQGZ3tbkbrax0r28HHwHaFnlZdXRzWYbm8iJ3LJzP0vWbG9q5aCF4ris9Dk0W3WOGiV5_3xqU9RcIvi1gzFVFvmMRMYJ_PUMpRFQNs8y9RAmRTwOhX2y6sIJphPKJYIN-v8r_of7UFpBYdmP9ljz4dBU_oXqqmWjsCRmqfPfPFlcCr62WzTN1PqvI72I_DAijbhWaRYo4H4DfEckvK3jEq0biquYLwIVJJsrFHBQwhGDqYGLLaI0yH3vXzcGOCjV9HDrdfXm5DL83MMbGbb-icIFym3fBArdpAfPGbcQLle5Si_HZjNCYTIb6jqRDXyQ1iGZSYvF0E90i1Sz1ipGWwcPPHDnAXtZh8UEFEDfXj4BuDorUgQujz_GqJFGtEhkbvhlddhor0dOYqXelT0TjTLECOiEXiNZExdmBqvM8Rypimeif_zY97rBRNdnPmnvYNmt2QAcbNLBoS5uvlnDIB3S3N_rCZZ_tBlkazpuHhlALY-R2haxRivXNOKoA1xSvZzxjqVs0ajOCLB988WGkuEX1ZWynagu8IcParX29_-IYZC1tTXhmrHiOnxdDNzvvDN4qsiSB6jHEXBUNfqNlCOzc1QfWkghFzYLs11OGg6XfM9XTGze1dcnysIUzBrev8g4BKWzWpNdyk-XaObiB_eRFs93y1l7o=w1366-h613?auditContext=prefetch)

Este error quiere decir que se ha bloqueado el acceso a la información desde el Backend ya que no se encuentra en el mismo origen, o en el mismo servidor. Por ello por lo general siempre la api se aloja en el mismo dominio bajo un subdominio.

## La Solución

La solución a esto es sencilla, si nuestro servidor no nos bloquea igual estas peticiones, lo más seguro es que coloquemos en nuestro Backend las cabeceras correspondientes así cuando sea enviada la información las cabeceras habiliten el contenido y el error desaparezca. Para ello debemos agregar las siguientes líneas de Código

```php
header("Access-Control-Allow-Origin: *"); // Usar "*" permite cualquier origen y puede exponer datos sensibles; en producción, reemplaza "*" por la URL específica para mayor seguridad
header("Access-Control-Allow-Methods: GET, POST, PUT, DELETE, OPTIONS");
header("Access-Control-Allow-Headers: Content-Type, Authorization, X-Requested-With");


if ($_SERVER['REQUEST_METHOD'] === 'OPTIONS') {
    http_response_code(200);
    exit;
}
```

1. `header("Access-Control-Allow-Origin: *");` Esta línea de código es la que permite el acceso a las url declaradas, en este caso permite acceso a todas las url ya que colocamos un \*
2. `header("Access-Control-Allow-Methods: GET, POST, PUT, DELETE, OPTIONS");` Esta línea habilita las acciones que pueden ser recibidas por el backend desde el frontend. Por ejemplo, si queremos permitir solo lectura, debemos dejar únicamente el verbo `GET`. Restringir los métodos permitidos mejora la seguridad al limitar la superficie de la API expuesta a solicitudes cross-origin.
   El método `OPTIONS` es necesario porque los navegadores envían automáticamente una solicitud "preflight" (preliminar) usando `OPTIONS` antes de ciertas peticiones cross-origin para verificar los permisos CORS del servidor.
3. `header("Access-Control-Allow-Headers: Content-Type, Authorization, X-Requested-With");` Autoriza los contenidos que se reciben por el backend.
