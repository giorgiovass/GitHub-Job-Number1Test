---
nav\_title: Postman y otras solicitudes article\_title: Cartero y otras peticiones page\_order: 3 Descripción: "Este artículo de referencia cubre la colección Braze Postman, lo que hace, cómo configurar y usar la colección, así como cómo editar y enviar todas las solicitudes." page\_type: reference

---

# Cartero y otras solicitudes de la muestra

> Braze le permite generar solicitudes de API de prueba para nuestros endpoints a través de nuestra colección de carteros. Este artículo de referencia cubre la colección Braze Postman, qué es, cómo configurar y usar la colección, así como cómo editar y enviar solicitudes.

## ¿Qué es Postman?

Postman es definitivamente una herramienta de edición visual gratuita para crear solicitudes de API. A diferencia de otros métodos para interactuar con API (por ejemplo, usando cURL), Postman le permite editar fácilmente solicitudes de API, ver información de encabezados y mucho más. Postman le permite guardar colecciones o bibliotecas de solicitudes de API prefabricadas de muestra. Para facilitar a nuestros clientes la puesta en marcha de nuestra API REST, hemos creado una colección con ejemplos prefabricados para todos nuestros endpoints API.

Vea o descargue nuestra Colección Postman haciendo clic en **Ejecutar en Postman** en los [documentos Postman](https://documenter.getpostman.com/view/4689407/SVYrsdsG?version=latest#intro) para comenzar.

## Usando la colección Braze Postman

Si tienes una cuenta de Postman (y puedes descargar las respectivas versiones de macOS, Windows y Linux desde el [sitio web Postman][1]), puedes abrir nuestra documentación de Postman en tu propia aplicación Postman haciendo clic en el botón naranja **Ejecutar en Postman**. A continuación, puede [crear un entorno](#setting-up-your-postman-environment), o utilizar nuestro entorno de API Braze REST como plantilla, y editar las solicitudes `POST` y `GET` disponibles para satisfacer sus necesidades.

### Configuración de su entorno de cartero

{% raw %} La colección Braze Postman utiliza una variable de plantilla, `{{instance_url}}`, para sustituir la URL REST API de su instancia Braze en las solicitudes preconstruidas, y la variable `{{api_key}}` para su API Key. En lugar de tener que editar manualmente todas las solicitudes de la colección, puede configurar esta variable en su entorno de cartero. Puede seleccionar nuestro entorno con plantilla (Plantilla de entorno API Braze REST) en el menú desplegable y reemplazar los valores de las variables por los suyos propios, o puede configurar su propio entorno.

Para configurar su propio entorno, realice los siguientes pasos:

1. En la pestaña **Áreas de trabajo**, seleccione **Entornos**.
2. Haga clic en el botón **+** plus para crear un nuevo entorno.
3. Asigne un nombre a este entorno (por ejemplo, "Solicitudes de API de Brazo") y agregue claves para `url_instancia` y `clave_api` con valores correspondientes a su \[instancia de Brazo]\[7] y \[clave API REST de Brazo]\[8].
4. Haga clic en **Guardar**.

{% alert note %} En los organismos de solicitud `POST`, la `clave_api` debe encapsularse entre comillas: `"MY-API-KEY-EXAMPLE"`. En `GET` URLs, no debería ser. Ya hemos proporcionado este formato para usted en los cuerpos de solicitud `POST` de esta documentación, `OBTENER` URL y plantilla de entorno para `SU-API-CLAVE-AQUÍ`.

\![Agregando variables para la clave API y URL de instancia al entorno de la API Braze REST en Postman.]\[3]

### Usando las solicitudes preconstruidas de la colección

Después de configurar su entorno, puede usar cualquiera de las solicitudes precompiladas de la colección como plantilla para crear nuevas solicitudes de API. Para empezar a utilizar una de las solicitudes preconstruidas, haga clic en ella en el menú **Colecciones** de Postman. Esto abrirá la solicitud como una nueva pestaña en la ventana principal de la aplicación Postman.

En general, hay dos tipos de solicitudes que aceptan los endpoints de Braze API: `GET` y `POST`. Dependiendo del método `HTTP` que utilice el punto final, deberá editar la solicitud precompilada de manera diferente.

#### Editar una solicitud POST

Al editar una solicitud `POST`, abra la solicitud y vaya a la sección **Cuerpo** en el editor de solicitudes. Para facilitar la lectura, seleccione el botón de radio **en bruto** para formatear el cuerpo de solicitud `JSON`.

\![Ficha Cuerpo al editar una solicitud POST User Track en Postman]\[4]

#### Editar una solicitud GET

Al editar una solicitud `GET`, edite los parámetros pasados en la URL de la solicitud. Para hacerlo, seleccione la pestaña **Parámetros** y edite los pares clave-valor en los campos que aparecen para que funcione.

\![Ficha Parámetros al editar una solicitud GET Query List of Unsubscribed Email Addresss en Postman.]\[5]

### Envíe su solicitud

Después de que su solicitud de API esté lista, haga clic en **Enviar**. La solicitud envía y los datos de respuesta se rellenan en una sección debajo del editor de solicitudes. Desde aquí, puede ver los datos sin procesar devueltos desde la API de Braze, ver el código de respuesta HTTP, ver cuánto tiempo tardó en procesarse la solicitud y ver la información de encabezado.

\![Ejemplo de datos de respuesta corporal de una solicitud POST con un estado de 201 Creado y tiempo de respuesta de 269 milisegundos.]\[6]

[1]: https://www.getpostman.com
\[3]: {% image\_buster /assets/img\_archive/postman\_variable.png %} \[4]: {% image\_buster /assets/img\_archive/postman\_post.png %} \[5]: {% image\_buster /assets/img\_archive/postman\_get.png %} \[6]: {% image\_buster /assets/img\_archive/postman\_response.png %} \[7]: {{site.baseurl}}/developer\_guide/rest\_api/basics/#endpoints \[8]: {{site.baseurl}}/api/api\_key/
