---
nav_title: Descripción general del SDK para desarrolladores
article_title: Descripción general del SDK para desarrolladores
description: «Este artículo de referencia sobre la incorporación proporciona una descripción técnica para los desarrolladores del SDK de Braze. En él se analizan los análisis predeterminados que rastrea el SDK, el bloqueo de la recopilación automática de datos y la versión activa del SDK de tu aplicación. «
page_order: 0
---

# [![Braze Learning course]({% image_buster /assets/img/bl_icon3.png %})](https://learning.braze.com/path/developer/sdk-integration-basics){: style="float:right;width:120px;border:0;" class="noimgborder"}Descripción general del SDK para desarrolladores

> Antes de empezar a integrar los SDK de Braze, es posible que se pregunte qué es exactamente lo que está creando e integrando. Es posible que sienta curiosidad por saber cómo puede personalizar el SDK para que se adapte mejor a sus necesidades. Este artículo puede ayudarte a responder a todas tus preguntas sobre el SDK. 

¿Eres un especialista en marketing que busca un resumen básico del SDK? En su lugar, consulta [nuestra descripción general sobre][1] vendedores.

En resumen, el SDK de Braze:
* Recopila y sincroniza los datos de usuario en un perfil de usuario consolidado
* Recopila automáticamente los datos de la sesión, la información del dispositivo y los tokens push
* Captura datos de participación de marketing y datos personalizados específicos de su empresa
* Potencia las notificaciones push, los mensajes integrados en la aplicación y los canales de mensajería de Content Card

## Rendimiento de la aplicación

Braze no debería tener un impacto negativo en el rendimiento de tu aplicación.

Los SDK de Braze ocupan muy poco espacio. Cambiamos automáticamente la velocidad a la que borramos los datos de los usuarios en función de la calidad de la red, además de permitir el control manual de la red. Realizamos automáticamente por lotes las solicitudes de API del SDK para asegurarnos de que los datos se registren rápidamente y, al mismo tiempo, mantener la máxima eficiencia de la red. Por último, la cantidad de datos enviados por el cliente a Braze en cada llamada a la API es extremadamente pequeña.

## Compatibilidad con SDK

El SDK de Braze está diseñado para comportarse muy bien y no interferir con otros SDK presentes en tu aplicación. Si tienes algún problema que crees que puede deberse a una incompatibilidad con otro SDK, ponte en contacto con el soporte de Braze.

## Análisis y gestión de sesiones predeterminados

Nuestro SDK recopila automáticamente ciertos datos de usuario, por ejemplo, la primera aplicación utilizada, la última aplicación utilizada, el recuento total de sesiones, el sistema operativo del dispositivo, etc. Si sigues nuestras guías de integración para implementar nuestros SDK, podrás aprovechar esta [recopilación de datos predeterminada]({{site.baseurl}}/user_guide/data_and_analytics/user_data_collection/sdk_data_collection/). Si consulta esta lista, puede evitar almacenar la misma información sobre los usuarios más de una vez. Con la excepción del inicio y el final de la sesión, todos los demás datos rastreados automáticamente no se tienen en cuenta para la asignación de puntos de datos.

{% alert note %}
Todas nuestras funciones son configurables, pero es una buena idea implementar completamente el modelo de recopilación de datos predeterminado.

<br>Si es necesario para su caso de uso, puede [limitar la recopilación de ciertos datos](#blocking-data-collection) una vez finalizada la integración.
{% endalert %}

## Carga y descarga de datos

El SDK de Braze almacena en caché los datos (sesiones, eventos personalizados, etc.) y los carga periódicamente. Solo después de que se hayan cargado los datos, los valores se actualizarán en el panel de control. El intervalo de carga tiene en cuenta el estado del dispositivo y se rige por la calidad de la conexión de red:

|Calidad de la conexión de red |    Intervalo de descarga de datos|
|---|---|
|Genial    |10 segundos|
|Buena    |30 segundos|
|Pobre    |60 segundos|
{: .reset-td-br-1 .reset-td-br-2}

Si no hay conexión de red, los datos se almacenan en caché localmente en el dispositivo hasta que se restablezca la conexión de red. Cuando se restablezca la conexión, los datos se cargarán en Braze.

Braze envía datos al SDK al principio de una sesión en función de los segmentos en los que se encuentra el usuario en el momento de la sesión. Los nuevos mensajes de la aplicación no se actualizarán durante la sesión. Sin embargo, los datos del usuario durante la sesión se procesarán continuamente a medida que los envíe el cliente. Por ejemplo, un usuario caducado (usó la aplicación por última vez hace más de 7 días) seguirá recibiendo contenido dirigido a los usuarios inactivos en su primera sesión en la aplicación.

## Bloqueo de la recopilación de datos

Es posible (aunque no se sugiere) bloquear la recopilación automática de determinados datos de la integración del SDK o incluir en listas de permitidos los procesos que lo hacen. 

No se recomienda bloquear la recopilación de datos porque la eliminación de los datos analíticos reduce la capacidad de personalización y segmentación de la plataforma. Por ejemplo:

- Si decides no integrar completamente la ubicación en uno de los SDK, no podrás personalizar tus mensajes según el idioma o la ubicación. 
- Si decides no realizar la integración para la zona horaria, es posible que no puedas enviar mensajes dentro de la zona horaria de un usuario. 
- Si decides no integrar la información visual de un dispositivo específico, es posible que el contenido de los mensajes no esté optimizado para ese dispositivo.

Recomendamos encarecidamente integrar completamente los SDK para aprovechar al máximo las capacidades de nuestro producto.

{% tabs %}
{% tab Web SDK %}

Puede simplemente no integrar ciertas partes del SDK o usarlo [`disableSDK`](https://js.appboycdn.com/web-sdk/latest/doc/modules/braze.html#disablesdk)para un usuario. Este método sincronizará los datos registrados antes de la llamada y hará que `disableSDK()` se ignoren todas las llamadas posteriores al Braze Web SDK para esta página y las cargas futuras de la página. Si desea reanudar la recopilación de datos en un momento posterior, puede utilizar el [`enableSDK()`](https://js.appboycdn.com/web-sdk/latest/doc/modules/braze.html#enablesdk)método en el futuro para reanudar la recopilación de datos. Puedes obtener más información sobre esto en nuestro artículo [Cómo deshabilitar el seguimiento web]({{site.baseurl}}/developer_guide/platform_integration_guides/web/analytics/disabling_tracking/).

{% endtab %}
{% tab Android SDK %}

Puede usarlo [`setDeviceObjectAllowlist`](https://braze-inc.github.io/braze-android-sdk/kdoc/braze-android-sdk/com.braze.configuration/-braze-config/-builder/set-device-object-allowlist.html?query=fun%20setDeviceObjectAllowlist(deviceObjectAllowlist:%20EnumSet%3CDeviceKey%3E):%20BrazeConfig.Builder)para configurar el SDK para que solo envíe un subconjunto de claves o valores de objetos del dispositivo de acuerdo con una lista de permitidos establecida. Esto debe habilitarse mediante [`setDeviceObjectAllowlistEnabled`](https://braze-inc.github.io/braze-android-sdk/kdoc/braze-android-sdk/com.braze.configuration/-braze-config/-builder/set-device-object-allowlist-enabled.html?query=fun%20setDeviceObjectAllowlistEnabled(enabled:%20Boolean):%20BrazeConfig.Builder).

{% alert important %}
Si la lista está vacía, **no** se enviarán datos del dispositivo a Braze.
{% endalert %}

{% endtab %}
{% tab Swift SDK %}

Puedes asignar un conjunto de campos aptos a [`configuration.devicePropertyAllowList`](https://braze-inc.github.io/braze-swift-sdk/documentation/brazekit/braze/configuration-swift.class/devicepropertyallowlist)on your `Braze.Configuration` para especificar una lista de campos permitidos para los campos del dispositivo que recopila el SDK. La lista completa de campos se define en [`Braze.Configuration.DeviceProperty`](https://braze-inc.github.io/braze-swift-sdk/documentation/brazekit/braze/configuration-swift.class/deviceproperty). Para desactivar la recopilación de todos los campos del dispositivo, establezca el valor de esta propiedad en un conjunto vacío (`[]`).

{% alert important %}
De forma predeterminada, el SDK Braze Swift recopila todos los campos. La eliminación de algunas propiedades del dispositivo puede deshabilitar las funciones del SDK.
{% endalert %}

Para obtener más información sobre el uso, consulte [Almacenamiento]({{site.baseurl}}/developer_guide/platform_integration_guides/swift/storage) en la documentación del SDK de Swift.

{% endtab %}
{% endtabs %}

## ¿Qué versión del SDK tengo?

Para usar el panel de control para ver la versión del SDK de una aplicación en particular, visita **Configuración > Configuración de la aplicación**. La versión de **Live SDK muestra la versión** más alta del SDK de Braze utilizada por tu aplicación en vivo más reciente para al menos el 5% de tus usuarios.

![Una aplicación llamada Swifty en un espacio de trabajo. La versión de Live SDK es la 6.6.0.][2]{: style="max-width:80%"} 

{% alert tip %}
Si tienes una aplicación para iOS, puedes confirmar que estás usando el SDK de [Swift en lugar del antiguo SDK]({{site.baseurl}}/developer_guide/platform_integration_guides/swift/initial_sdk_setup/overview) de [Objective-C para iOS]({{site.baseurl}}/developer_guide/platform_integration_guides/ios/initial_sdk_setup/overview) si tu **versión de Live SDK** es igual o superior a 5.0.0, que fue la primera versión publicada del SDK de Swift.
{% endalert %}

[1]: {{site.baseurl}}/user_guide/onboarding_with_braze/web_sdk/
[2]: {% image_buster /assets/img/live-sdk-version.png %}