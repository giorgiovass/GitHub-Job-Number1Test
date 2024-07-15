---
nav_title: Regalo
article_title: Regal
description: Este artículo de referencia describe la asociación entre Braze y Regal, una solución de ventas por teléfono y SMS que le permite utilizar datos de ambas fuentes para crear experiencias personalizadas para sus clientes.
alias: /partners/regal/
page_type: socio
search_tag: Socio

---

# Regal

> Regal.io][6] es la solución de ventas por teléfono y SMS diseñada para impulsar más conversaciones para que puedas alcanzar tus objetivos de crecimiento mucho más rápido.

Al integrar Regal y Braze, puede crear una experiencia más coherente y personalizada en todos sus puntos de contacto con el cliente.
- Envía el siguiente mejor correo electrónico o notificación push desde Braze según lo que se diga en una conversación telefónica en Regal.
- Disparar una llamada en Regal cuando un cliente de alto valor hace clic en un correo electrónico de marketing de Braze pero no convierte.

## Requisitos previos

| Requisito | Descripción |
| ----------- | ----------- |
| Cuenta regia | Se requiere una cuenta de Regal para aprovechar esta asociación. |
| Clave API de Regal | Una clave API de Regal permitirá enviar eventos de Braze a Regal.<br><br>Envíe un correo electrónico a [support@regal.io](mailto:support@regal.io) para obtener esta clave. |
| Transformación de Datos de Braze | La transformación de datos está actualmente en acceso temprano. Póngase en contacto con su gerente de éxito del cliente de Braze si está interesado en participar en el acceso anticipado. Esto es necesario para recibir datos de Regal. |
{: .reset-td-br-1 .reset-td-br-2}

## Integration: Enviando datos de Braze a Regal

La siguiente sección describe cómo usar Braze como una fuente para enviar el perfil de cliente y los datos de eventos a Regal usando Braze Canvas o webhooks de campaña.

### Paso 1: Crear nuevos contactos en Regal

Cree un Canvas o campaña que envíe webhooks a Regal cada vez que se cree un nuevo contacto en Braze que desee que esté disponible para llamadas y mensajes de texto en Regal. 

1. Cree un Canvas o campaña titulada "Crear nuevo contacto para Regal" y seleccione **Basado en acciones** como el tipo de entrada.

2. Establezca la lógica del disparador como **Evento Personalizado** y seleccione el evento que se activa cuando se crea un contacto con un número de teléfono. Regal también recomienda agregar un filtro adicional en el campo del teléfono que asegure que esté configurado.

3. En su nueva plantilla de webhook, complete los siguientes campos:
   - **URL del webhook**: <https://events.regalvoice.com/events>
   - **Cuerpo de la solicitud**: Texto sin procesar

#### Encabezados de solicitud y método

Regal.io también requiere un encabezado HTTP para la autorización y un método HTTP. Lo siguiente ya estará incluido dentro de la plantilla como un par clave-valor en la pestaña **Configuración**:
{% raw %}
- **Método HTTP**: POST
- **Encabezados de solicitud**:
    - **Autorización**: `{{<REGAL_API_KEY>}}`
    - **Tipo de Contenido**: application/json
{% endraw %}

#### Cuerpo de la solicitud

El único campo requerido a continuación es la propiedad `traits.phone`. El resto es opcional. Sin embargo, si incluyes `optIn`, debes incluir `optIn.channel` y `optIn.subscribed`.

```json
{
    "userId": "<uniqueIdentifier>", //this is optional
    "traits": {
        "phone": "<phoneNumber>",
        "email": "<email>",
        "firstName": "<firstName>",
        "lastName": "<lastName>",
        "optIn": [
            {
                "channel": "voice",
                "source": "<leadSource>",
                "subscribed": true
            },
            {
                "channel": "sms",
                "source": "<leadSource>",
                "subscribed": true
            }
        ],
        "custom1": "<custom1>",
        "custom2": "<custom2>"
    },
    "eventSource": "braze"
}
```

El ejemplo de carga útil anterior asume que todos sus contactos han aceptado la suscripción para voz y SMS. Si eso no es cierto, puede eliminar la propiedad `optIn` de lo anterior y configurar un Canvas o campaña separado para actualizar un contacto en Regal cuando se recoja `optIn`.

### Paso 2: Actualizar información de suscripción 

Si la suscripción y la cancelación pueden ocurrir en diferentes partes de la experiencia del usuario en su aplicación, es importante actualizar Regal a medida que los usuarios se suscriben o cancelan. A continuación se muestra un lienzo recomendado para cómo enviar información de suscripción actualizada a Regal. Supone que guardas esto como un campo de perfil de Braze, pero si no, el desencadenante puede ser fácilmente un evento en tu cuenta de Braze que representa a un usuario optando por suscribirse o darse de baja. (El ejemplo a continuación es para la suscripción por teléfono, pero puede configurar un Canvas o campaña similar para la suscripción por SMS si los recopila por separado).

1. Crear un nuevo Canvas o campaña titulada "Enviar Opt In o Out a Regal".

2. Seleccione una de las siguientes opciones de activación y seleccione cualquier campo que represente el estado de aceptación del usuario. Si envía un evento a Braze para representar la suscripción o la cancelación, utilice ese evento como desencadenante en su lugar.
    - Campo de perfil de usuario actualizado
    - Actualizar el estado del grupo de suscripción
    - Estado de suscripción

3. En su nueva plantilla de Webhook, complete los siguientes campos:
   - **URL del webhook**: <https://events.regalvoice.com/events>
   - **Cuerpo de la solicitud**: Texto sin procesar

#### Encabezados de solicitud y método

Regal.io también requiere un encabezado HTTP para la autorización y un método HTTP. Lo siguiente ya estará incluido dentro de la plantilla como un par clave-valor, pero en la pestaña **Configuración**:
{% raw %}
- **Método HTTP**: POST
- **Encabezados de solicitud**:
    - **Autorización**: `{{<REGAL_API_KEY>}}`
    - **Tipo de Contenido**: application/json
{% endraw %}

#### Cuerpo de la solicitud

Puede agregar atributos adicionales del perfil de usuario en esta carga útil también si desea asegurarse de que más atributos estén actualizados simultáneamente.

```json
{
    "userId": "<uniqueIdentifier>", //this is optional
    "traits": {
        "phone": "<phoneNumber>",
        "optIn": [
            {
                "channel": "voice",
                "source": "<leadSource>",
                "subscribed": "<voice_optin_subscribed>"
            },
            {
                "channel": "sms",
                "source": "<leadSource>",
                "subscribed": "<voice_optin_subscribed>"
            }
        ]
    },
    "eventSource": "braze"
}
```

### Paso 3: Enviar eventos personalizados

Finalmente, configure un Canvas o campaña para cada uno de los eventos clave que desea enviar a Regal - Regal recomienda enviar cualquier evento que sea importante para activar SMS y llamadas en Regal (como un evento en cada paso del flujo de registro o compra) o que se utilizará como criterio de salida para que los contactos salgan de las campañas de Regal.

Por ejemplo, a continuación se muestra un flujo de trabajo para enviar a Regal un evento cuando un usuario completa el primer paso de una aplicación.

1. Crear un nuevo Canvas o campaña titulada "Enviar evento de paso 1 de solicitud completado a Regal".

2. Establezca la lógica del nodo de activación como **Evento Personalizado** y seleccione el nombre del evento que desea enviar a Regal, como "Paso de Aplicación 1 Completado".

3. En su nueva plantilla de Webhook, complete los siguientes campos:
   - **URL del webhook**: <https://events.regalvoice.com/events>
   - **Cuerpo de la solicitud**: Texto sin procesar

#### Encabezados de solicitud y método

Regal.io también requiere un encabezado HTTP para la autorización y un método HTTP. Lo siguiente ya estará incluido dentro de la plantilla como un par clave-valor, pero en la pestaña **Configuración**:
{% raw %}
- **Método HTTP**: POST
- **Encabezados de solicitud**:
    - **Autorización**: `{{<REGAL_API_KEY>}}`
    - **Tipo de Contenido**: application/json
{% endraw %}

#### Cuerpo de la solicitud

Puede agregar atributos adicionales del perfil del usuario en esta carga útil si desea asegurarse de que más atributos estén actualizados simultáneamente.

```json
{
    "userId": "<uniqueIdentifier>", //this is optional
    "traits": {
        "phone": "<phoneNumber>",
        "firstName": "<firstName>",
        "lastName": "<lastName>",
        "custom1": "<custom1>",
        "custom2": "<custom2>",
        "custom3": "<custom3>"
    },
    "name": "Application Step 1 Completed",
    "properties": {
      "educationalLevel": "<educationalLevel>",
      "preferredLocation": "<preferredLocation>",
      "preferredSubject": "<preferredSubject>",
      "readytoCommit": true
    },
    "eventSource": "braze"
}
```

#### Atributos de contacto actualizados

Si bien no es necesario, Regal recomienda enviar también cualquier campo de datos clave del perfil del usuario en las cargas útiles de los eventos de sus flujos de trabajo de eventos para garantizar que Regal tenga acceso a los atributos de contacto más actualizados en el momento en que los eventos clave estén disponibles.

{% alert note %}
Si tienes preguntas sobre qué eventos son importantes enviar a Regal o cómo configurar mejor estos Lienzos y campañas, contacta a support@regal.io.
{% endalert %}

## Integration: Enviando datos de Regal a Braze

Esta sección describe cómo obtener eventos de informes de Regal como `SMS.sent` y `call.completed` en Braze para que puedan aparecer en tus perfiles de Braze y estar disponibles en la herramienta de segmentación de Braze, Canvas y campañas. Esta integración utiliza Regal Reporting Webhooks y Braze Data Transformation para automatizar el flujo de datos.

### Paso 1: Crear una Transformación de Datos en Braze

{% alert important %}
La transformación de datos está actualmente en acceso temprano. Póngase en contacto con su gerente de éxito del cliente de Braze si está interesado en participar en el acceso anticipado.
{% endalert %}

Braze recomienda crear una transformación según el webhook de Regal que planea enviar a Braze. 

Para crear una Transformación de Datos:
1. Navega a la página de **Transformaciones** en tu panel de control de Braze.
2. Dale un nombre a tu transformación y haz clic en **Crear transformación**.
3. De la lista de transformaciones, haga clic en <i class="fa-solid fa-ellipsis-vertical" title="Ver acciones"></i> y seleccione **Copiar URL del webhook**.

![][4]

### Paso 2: Habilitar webhooks de informes en Regal

Para configurar los webhooks de informes:
1. Ve a la aplicación Regal y abre la página de **Configuración**.

2. En la sección **Reporting Webhooks**, haga clic en **Create Webhooks**.

3. En la entrada del endpoint del webhook, agregue la URL del webhook de transformación de datos de Braze para la transformación de datos asociada.

![][5]{: style="max-width:60%;"}

#### Actualizando un punto final
Cuando editas un endpoint, puede tardar hasta 5 minutos en actualizarse la caché y enviar eventos a tu nuevo endpoint.
#### Reintentos
Actualmente, no hay reintentos en estos eventos. Si no se recibe una respuesta dentro de 5 segundos, el evento se descarta y no se vuelve a intentar. Regal añadirá reintentos en una versión futura.
#### Eventos
La \[guía de Webhooks de informes][7] de Regal incluye la lista completa de eventos de informes que publican. Allí puedes ver definiciones de propiedades y ejemplos de cargas útiles también.

### Paso 3: Transformar eventos Regal en eventos Braze

La función de [Transformación de Datos]({{site.baseurl}}/data_transformation) de Braze te permite mapear eventos entrantes de Regal en el formato necesario para ser añadidos como atributos, eventos o compras en Braze.

1. Nombra tu Transformación de Datos. Se recomienda configurar una Transformación de Datos por webhook de evento.

2. Para probar la conexión, cree una llamada saliente desde el Regal Agent Desktop a su teléfono celular y envíe el formulario de Resumen de Conversación para crear un evento de llamada completada.

3. Determine what identifiers you will use to map your Regal contacts to your Braze profiles. Los identificadores disponibles en los eventos de Regal incluyen:
   - `userId` - solo se establece en eventos si previamente has enviado este identificador para un contacto
   - `traits.phone`
   - `traits.email` - solo se establece en eventos si previamente has enviado este identificador para un contacto

#### Identificadores compatibles con Braze
- Braze no admite números de teléfono como identificador. Para usar esto como un identificador, el número de teléfono se puede establecer como un \[alias de usuario][8] en Braze.
- Al utilizar la transformación de datos de Braze, la dirección de correo electrónico se puede usar como identificador. Si la dirección de correo electrónico existe como un perfil dentro de Braze, el perfil existente se actualizará. Si la dirección de correo electrónico aún no existe dentro de Braze, se creará un perfil solo de correo electrónico.

## Casos de uso

{% tabs %}
{% tab Trigger an email %}

**Disparar un correo electrónico desde Braze basado en una disposición de llamada en Regal**

A continuación se muestra una carga útil de muestra para un evento `call.completed` en Regal. 

```json
{
  "userId": "123",
  "traits": {
    "phone": "+17625555555",
    "email": "xxx@gmail.com"
  },
  "name": "call.completed",
  "properties": {
    "agent_firstname": "Rebecca",
    "agent_fullname": "Rebecca Greene",
    "agent_id": "xxxx@yourbrand.com",
    "direction": "OUTBOUND",
    "regal_voice_phone": "+19545558563",
    "regal_voice_phone_internal_name": "Sales Line",
    "contact_phone": "+17625555555",
    "call_id": "WTxxxxx9",
    "type": "Outbound Call",
    "disposition": "Converted During Convo",
    "notes": null,
    "objections": null,
    "campaign_name": "Life Insurance Quote Follow Up",
    "campaign_friendly_id": "445",
    "started_at": 1657855046,
    "ended_at": 1657855053,
    "completed_at": 1657855059,
    "talk_time": 7,
    "wrapup_time": 6,
    "handle_time": 13,
    "journey_uuid": null,
    "journey_name": null,
    "journey_friendly_id": null
  },
  "originalTimestamp": "1657855059",
  "eventSource": "Regal Voice"
}
```

A continuación se muestra una transformación de datos de muestra para mapear esto a un evento personalizado en Braze.

```
// Braze's /users/track endpoint expects timestamps in an ISO 8601 format. To use the Unix timestamp within Regal's call.completed event payload as the event timestamp in Braze must first be converted to ISO 8601. This can be done with the following code:
let unixTimestamp = payload.originalTimestamp;
let dateObj = new Date(unixTimestamp * 1000);
let isoString = dateObj.toISOString();

// This is a default template you can use as a starting point. Feel free to delete this entirely to start from scratch or to delete specific components as you see fit.

// First, this code defines a variable, "brazecall", to build up a /users/track request
// Everything from the incoming webhook is accessible via the special variable "payload". As such, you can template in desired values in your /users/track request with JS dot notation, such as payload.x.y.z

let brazecall = {
 "events": [
   {
     "external_id": payload.userId,
     "name": "Call Completed",
     "time": isoString,
     "_update_existing_only": false,
     "properties": {
       "agent_firstname": payload.properties.agent_firstname,
       "agent_fullname": payload.properties.agent_fullname,
       "agent_id": payload.properties.agent_id,
       "direction": payload.properties.direction,
       "regal_voice_phone": payload.properties.regal_voice_phone,
       "regal_voice_phone_internal_name": payload.properties.regal_voice_phone_internal_name,
       "contact_phone": payload.properties.contact_phone,
       "call_id": payload.properties.call_id,
       "type": payload.properties.type,
       "disposition": payload.properties.disposition,
       "notes": payload.properties.notes,
       "objections": payload.properties.objections,
       "campaign_name": payload.properties.campaign_name,
       "campaign_friendly_id": payload.properties.campaign_friendly_id,
       "started_at": payload.properties.started_at,
       "ended_at": payload.properties.ended_at,
       "completed_at": payload.properties.completed_at,
       "talk_time": payload.properties.talk_time,
       "wrapup_time": payload.properties.wrapup_time,
       "handle_time": payload.properties.handle_time,
       "journey_uuid": payload.properties.journey_uuid,
       "journey_name": payload.properties.journey_name,
       "journey_friendly_id": payload.properties.journey_friendly_id
     }
   }
 ]
};

// After the /users/track request is assigned to brazecall, you will want to explicitly return brazecall to create an output
return brazecall;
```

{% endtab %}
{% tab Update profile attributes %}

**Actualizar los atributos del perfil en Braze basándose en `contact.attribute.edited` eventos de Regal**

A continuación se muestra una carga útil de muestra para un evento `contact.attribute.edited` en Regal. Este evento se activa cada vez que uno de tus agentes aprende algo nuevo en una conversación y actualiza un atributo en el perfil del contacto.

```json
{
  "userId": "123",
  "traits": {
    "phone": "+17625555555",
    "email": "xxx@gmail.com",
  },
  "name": "contact.attribute.edited",
  "properties": {
    "agent_email": "xxxx@yourbrand.com",
    "contact_phone": "+17625555555",
    "changes": {
      "custom_properties": {
        "annual_income": {
          "old_value": "150,000",
          "new_value": "300,000"
        }
      }
    },
    "created_at": "1657855462"
  },
  "originalTimestamp": "1657855462",
  "eventSource": "Regal Voice"
}
```

A continuación se muestra una transformación de datos de ejemplo para asignar los nuevos valores de propiedades personalizadas a los atributos relevantes en sus perfiles de Braze:

```
// This is an example template you can use as a starting point. Feel free to delete this entirely to start from scratch or to delete specific components as you see fit.

// Capture the key's updated property value within the 'changes' object and store this in an attributes variable that can be used in the /users/track request

const changes = payload.properties.changes.custom_properties;

const attributes = {};
for (const key in changes) {
 attributes[key] = changes[key].new_value;
}

// First, this code defines a variable, "brazecall", to build up a /users/track request
// Everything from the incoming webhook is accessible via the special variable "payload". As such, you can template in desired values in your /users/track request with JS dot notation, such as payload.x.y.z

const brazecall = {
 "attributes": [
   {
     "external_id": payload.userId,
     "_update_existing_only": false,
     ...attributes
   }
 ]
};

// After the /users/track request is assigned to brazecall, you will want to explicitly return brazecall to create an output
return brazecall;
```

{% endtab %}
{% tab Keep your experiments in sync %}

**Mantén tus experimentos en Braze y Regal sincronizados usando `contact.experiment.assigned` eventos**

A continuación se muestra una carga útil de muestra para un evento `contact.experiment.assigned` en Regal.

```json
{
  "userId": "123",
  "traits": {
    "phone": "+17625555555",
    "email": "xxx@gmail.com",
  },
  "name": "contact.experiment.assigned",
  "properties": {
    "experiment_name": "Post Call Offer Test",
    "experiment_id": "xxxx-xxxx-xxxx-xxxx",
    "experiment_variant": "Aggressive Offer - 50%",
    "journey_uuid": "xxxx-xxxx-xxxx-xxxx",
    "journey_friendly_id": 220,
    "journey_name": "Post Call Follow Up"
  },
  "originalTimestamp": "1657855118",
  "eventSource": "Regal Voice"
}
```

A continuación se muestra una transformación de datos de muestra para mapear esto a un evento personalizado en Braze.

```
// Braze's /users/track endpoint expects timestamps in an ISO 8601 format. To use the Unix timestamp within Regal's call.completed event payload as the event timestamp in Braze, it must first be converted to ISO 8601. This can be done with the following code:
let unixTimestamp = payload.originalTimestamp;
let dateObj = new Date(unixTimestamp * 1000);
let isoString = dateObj.toISOString();

// This is an example template you can use as a starting point. Feel free to delete this entirely to start from scratch or to delete specific components as you see fit.

// First, this code defines a variable, "brazecall", to build up a /users/track request
// Everything from the incoming webhook is accessible via the special variable "payload". As such, you can template in desired values in your /users/track request with JS dot notation, such as payload.x.y.z
let brazecall = {
 "events": [
   {
     "external_id": payload.userId,
     "_update_existing_only": false,
     "name": "Contact Experiment Assigned",
     "time": isoString,
     "properties": {
       "experiment_name": payload.properties.experiment_name,
       "experiment_id": payload.properties.experiment_id,
       "experiment_variant": payload.properties.experiment_variant,
       "journey_uuid": payload.properties.journey_uuid,
       "journey_friendly_id": payload.properties.journey_friendly_id,
       "journey_name": payload.properties.journey_name
     }
   }
 ]
};

// After the /users/track request is assigned to brazecall, you will want to explicitly return brazecall to create an output
return brazecall;

```
{% endtab %}
{% tab Unsubscribe a contact %}

**Cancelar la suscripción de un contacto en Braze basado en un `contact.unsubscribed` de Regal**

A continuación se muestra una carga útil de muestra para un evento `contact.unsubscribed` en Regal.

```json
{
  "userId": "123",
  "traits": {
    "phone": "+17625555555",
    "email": "xxx@gmail.com",
    "ip": "78.97.213.166"
  },
  "name": "contact.unsubscribed",
  "properties": {
    "new_subscription": true,
    "channel": "voice",
    "text": null,
    "ip": "207.38.149.143",
    "source": "regalvoice.agent_desktop",
    "timestamp": "1657855229"
  },
  "originalTimestamp": "1657855230",
  "eventSource": "Regal Voice"
}
```

A continuación se muestra una muestra de transformación de datos para cancelar la suscripción del contacto en Braze.

```
// This is an example template you can use as a starting point. Feel free to delete this entirely to start from scratch or to delete specific components as you see fit.

// First, this code defines a variable, "brazecall", to build up a /users/track request
// Everything from the incoming webhook is accessible via the special variable "payload". As such, you can template in desired values in your /users/track request with JS dot notation, such as payload.x.y.z

let brazecall = {
 "attributes": [
   {
     "external_id": payload.userId,
     "_update_existing_only": true,
     "subscription_groups" : [{
       "subscription_group_id": "YOUR SUBSCRIPTION GROUP ID",
       "subscription_state": "unsubscribed"
     }]
   }
 ]
};

// After the /users/track request is assigned to brazecall, you will want to explicitly return brazecall to create an output
return brazecall;
```

{% endtab %}
{% endtabs %}

[2]: {% image_buster /assets/img/regal/webhook_rawtext.png %}
[3]: {% image_buster /assets/img/regal/request_header.png %}
[4]: {% image_buster /assets/img/regal/copy_webhook_url.png %}
[5]: {% image_buster /assets/img/regal/edit_webhook.png %}
[6]: https://regal.io
[7]: https://developer.regal.io/docs/reporting-webhooks#events
[8]: {{site.baseurl}}/user_guide/data_and_analytics/user_data_collection/user_profile_lifecycle/#user-aliases