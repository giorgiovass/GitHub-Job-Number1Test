---
nav_title: Hacer una llamada a la API
article_title: Realizar una llamada a la API de contenido conectado
page_order: 0
description: "Este artículo de referencia cubre cómo realizar una llamada a la API de Connected Content, así como ejemplos útiles y casos de uso avanzados de Connected Content".
search_rank: 2
---

# [![Braze Learning course]({% image_buster /assets/img/bl_icon3.png %})](https://learning.braze.com/connected-content){: style="float:right;width:120px;border:0;" class="noimgborder"}Realizar una llamada a la API

> Usa Contenido conectado para insertar cualquier información a la que se pueda acceder a través de la API directamente en los mensajes que envías a los usuarios. Puede extraer contenido directamente de su servidor web o de API de acceso público.

## Etiqueta de contenido conectado

{% raw %}

Para enviar una llamada de contenido conectado, use el comando `{% connected_content %}` etiqueta. Con esta etiqueta, puede asignar o declarar variables mediante el uso de `:save`. Se puede hacer referencia a aspectos de estas variables más adelante en el mensaje con [Líquido][2].

Por ejemplo, el siguiente cuerpo del mensaje accederá a la dirección URL `http://numbersapi.com/random/trivia` e incluye un dato divertido en tu mensaje:

```
{% connected_content http://numbersapi.com/random/trivia :save result %}
Hi there, here is fun some trivia for you!: {{result.text}}
```

### Adición de variables

También puede incluir atributos de perfil de usuario como variables en la cadena de URL al realizar solicitudes de contenido conectado. 

Por ejemplo, puede tener un servicio web que devuelva contenido basado en un usuario's email address and ID. If you'Al pasar atributos que contienen caracteres especiales, como el signo arroba (@), asegúrese de utilizar el filtro Liquid `url_param_escape` para reemplazar los caracteres no permitidos en las URL por sus versiones de escape compatibles con URL, como se muestra en el siguiente atributo de dirección de correo electrónico.

```
Hi, here are some articles that you might find interesting:

{% connected_content http://www.yourwebsite.com/articles?email={{${email_address} | url_param_escape}}&user_id={{${user_id}}} %}
```
{% endraw %}
{% alert note %}
Los valores de atributo deben estar rodeados por `${}` para funcionar correctamente dentro de nuestra versión de sintaxis de Liquid.
{% endalert %}

Las solicitudes de contenido conectado solo admiten solicitudes GET y POST.

## Manejo de errores

Si la URL no está disponible y alcanza una página 404, Braze renderizará una cadena vacía en su lugar. Si la dirección URL llega a una página HTTP 500 o 502, se producirá un error en la lógica de reintento.

Si el punto de conexión devuelve JSON, puede detectarlo comprobando si el `connected` value es null y, a continuación, [Anular condicionalmente el mensaje][1]. Braze solo permite URL que se comunican a través de los puertos 80 (HTTP) y 443 (HTTPS).

## Rendimiento

Debido a que Braze entrega mensajes a una velocidad muy rápida, asegúrese de que su servidor pueda manejar miles de conexiones simultáneas para que los servidores no se sobrecarguen al extraer contenido. Cuando utilice API públicas, asegúrese de que su uso no infrinja ninguna limitación de velocidad que pueda emplear el proveedor de API. Braze requiere que el tiempo de respuesta del servidor sea inferior a 2 segundos por razones de rendimiento; Si el servidor tarda más de 2 segundos en responder, el contenido no se insertará.

Los sistemas Braze pueden realizar la misma llamada a la API de contenido conectado más de una vez por destinatario. Esto se debe a que es posible que Braze necesite realizar una llamada a la API de contenido conectado para representar una carga útil de mensaje, y las cargas útiles de mensaje se pueden representar varias veces por destinatario para validación, lógica de reintento u otros fines internos. Los sistemas deben ser capaces de tolerar que la misma llamada de contenido conectado se realice más de una vez por destinatario.

## Cosas que debes saber

* Braze no cobra por las llamadas a la API y no contará para la asignación de puntos de datos dada.
* Hay un límite de 1 MB para las respuestas de contenido conectado.
* Las llamadas de contenido conectado se producirán cuando se envíe el mensaje, excepto los mensajes en la aplicación, que realizarán esta llamada cuando se vea el mensaje.
* Las llamadas de contenido conectado no siguen los redireccionamientos.

## Tipos de autenticación

### Uso de la autenticación básica

Si la URL requiere autenticación básica, Braze puede generar una credencial de autenticación básica para que la utilice en su llamada a la API. Puede administrar las credenciales de autenticación básicas existentes y agregar otras nuevas desde **Configuración** > **Contenido conectado**.

{% alert note %}
Si está utilizando el [Navegación antigua]({{site.baseurl}}/navigation), puedes encontrar **Contenido conectado** debajo **Administrar la configuración**.
{% endalert %}

![][34]

Para agregar una nueva credencial, haga clic en **Agregar credencial**. Asigne un nombre a su credencial e introduzca el nombre de usuario y la contraseña.

![][35]{: style="max-width:30%" }

A continuación, puede utilizar esta credencial de autenticación básica en las llamadas a la API haciendo referencia al nombre del token:

{% raw %}
```
Hi there, here is fun some trivia for you!: {% connected_content https://yourwebsite.com/random/trivia :basic_auth credential_name %}
```
{% endraw %}

{% alert note %}
Si eliminas una credencial, ten en cuenta que se anularán todas las llamadas de Connected Content que intenten usarla.
{% endalert %}

### Uso de la autenticación de token

Al usar Braze Connected Content, es posible que descubra que ciertas API requieren un token en lugar de un nombre de usuario y una contraseña. En la siguiente llamada se incluye un fragmento de código para hacer referencia y modelar los mensajes.

{% raw %}
```
{% assign campaign_name="New Year Sale" %}
{% connected_content
     https://your_API_link_here/
     :method post
     :headers {
       "X-App-Id": "YOUR-APP-ID",
       "X-App-Token": "YOUR-APP-TOKEN"
  }
     :body campaign={{campaign_name}}&customer={{${user_id}}}&channel=Braze
     :content_type application/json
     :save publication
%}
```
{% endraw %}

### Uso de la autenticación abierta (OAuth)

Algunas configuraciones de API requieren la recuperación de un token de acceso que luego se puede usar para autenticar el punto de conexión de API al que desea acceder.

#### Recuperar el token de acceso

En el siguiente ejemplo se muestra cómo recuperar y guardar un token de acceso en una variable local que se puede utilizar para autenticar la llamada API posterior. Un `:cache_max_age` se puede agregar para que coincida con el tiempo que el token de acceso es válido y reducir el número de llamadas salientes de contenido conectado. Consulte \[Almacenamiento en caché configurable][36] para obtener más información.

{% raw %}
```
{% connected_content
     https://your_API_access_token_endpoint_here/
     :method post
     :headers {
       "Content-Type": "YOUR-CONTENT-TYPE",
       "Authorization": "Bearer YOUR-APP-TOKEN"
  }
     :cache_max_age 900
     :save token_response
%}
```
{% endraw %}

#### Autorización de la API mediante el token de acceso recuperado

Ahora que el token está guardado, se puede crear dinámicamente en la siguiente llamada de Connected Content para autorizar la solicitud:

{% raw %}
```
{% connected_content
     https://your_API_endpoint_here/
     :headers {
       "Content-Type": "YOUR-CONTENT-TYPE",
       "Authorization": "{{token_response}}"
  }
     :body key1=value1&key2=value2
     :save response
%}
```
{% endraw %}

## Lista de direcciones IP permitidas de contenido conectado

Cuando se envía un mensaje mediante contenido conectado desde Braze, los servidores de Braze realizan automáticamente solicitudes de red a nuestros clientes' or third parties' servidores para recuperar datos. Con la lista de direcciones IP permitidas, puede verificar que las solicitudes de contenido conectado provengan realmente de Braze, lo que agrega una capa adicional de seguridad.

Braze enviará solicitudes de contenido conectado desde los siguientes rangos de IP. Los rangos enumerados se agregan de forma automática y dinámica a cualquier clave de API que se haya habilitado para la lista de permitidos. 

Braze tiene un conjunto reservado de direcciones IP que se utilizan para todos los servicios, no todos los cuales están activos en un momento dado. Esto está diseñado para que Braze envíe desde un centro de datos diferente o realice el mantenimiento, si es necesario sin afectar a los clientes. Braze puede usar una, un subconjunto o todas las siguientes direcciones IP enumeradas al realizar solicitudes de contenido conectado.

| Para instancias `US-01`, `US-02`, `US-03`, `US-04`, `US-05`, `US-06`, `US-07`: |
|---|
| `23.21.118.191`
| `34.206.23.173`
| `50.16.249.9`
| `52.4.160.214`
| `54.87.8.34`
| `54.156.35.251`
| `52.54.89.238`
| `18.205.178.15`

| Para instancias `EU-01` y `EU-02`: |
|---|
| `52.58.142.242`
| `52.29.193.121`
| `35.158.29.228`
| `18.157.135.97`
| `3.123.166.46`
| `3.64.27.36`
| `3.65.88.25`
| `3.68.144.188`
| `3.70.107.88`

| Por ejemplo `US-08`: |
|---|
| `52.151.246.51`
| `52.170.163.182`
| `40.76.166.157`
| `40.76.166.170`
| `40.76.166.167`
| `40.76.166.161`
| `40.76.166.156`
| `40.76.166.166`
| `40.76.166.160`
| `40.88.51.74`
| `52.154.67.17`
| `40.76.166.80`
| `40.76.166.84`
| `40.76.166.85`
| `40.76.166.81`
| `40.76.166.71`
| `40.76.166.144`
| `40.76.166.145`

## Solución de problemas

Uso [Webhook.site](https://webhook.site/) para solucionar problemas de las llamadas de contenido conectado. 

1. Cambie la URL de la llamada de contenido conectado por la URL única generada en el sitio.
2. Obtenga una vista previa y pruebe su campaña o paso de Canvas para ver las solicitudes que llegan a este sitio web.

Con esta herramienta, puede diagnosticar problemas con los encabezados de la solicitud, el cuerpo de la solicitud y otra información que se envía en la llamada.

[1]: {{site.baseurl}}/user_guide/personalization_and_dynamic_content/connected_content/aborting_connected_content/
[2]: {{site.baseurl}}/user_guide/personalization_and_dynamic_content/liquid/using_liquid/#liquid-usage-use-cases--overview
[16]: [success@braze.com](mailto:success@braze.com)
[34]: {% image_buster /assets/img_archive/basic_auth_mgmt.png %}
[35]: {% image_buster /assets/img_archive/basic_auth_token.png %}
[36]: {{site.baseurl}}/user_guide/personalization_and_dynamic_content/connected_content/local_connected_content_variables/#configurable-caching
