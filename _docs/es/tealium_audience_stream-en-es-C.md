---
nav_title: Tealium AudienceStream
article_title: Tealium AudienceStream
page_order: 2
alias: /partners/tealium_audience_stream/
description: "Este artículo de referencia describe la asociación entre Braze y Tealium, un centro de datos universal que le permite conectar datos móviles, web y alternativos a otras fuentes de terceros".
Socio page_type:
search_tag: Partner

---

# Tealium AudienceStream

> Tealium [AudienceStream](https://docs.tealium.com/server-side/getting-started/audiencestream-cdp/introduction/) es un motor de segmentación de clientes omnicanal y acción en tiempo real. AudienceStream toma los datos que fluyen a EventStream y crea perfiles de visitantes que representan los atributos más importantes del compromiso de sus clientes con su marca. 

La integración Braze and Tealium aprovecha los perfiles de visitantes de AudienceStream. Los comportamientos compartidos segmentan estos perfiles para crear conjuntos de visitantes con rasgos comunes, conocidos como audiencias. Estas audiencias pueden ayudar a alimentar su pila de tecnología de marketing en tiempo real a través de conectores. 

{% alert important %}
Tealium AudienceStreams y EventStreams ofrecen acciones de conector por lotes y no por lotes. El conector no discontinuo se debe usar cuando las solicitudes en tiempo real son importantes para el caso de uso y no hay preocupaciones sobre alcanzar las especificaciones de límite de velocidad de API de Braze. Póngase en contacto con el [soporte]({{site.baseurl}}/braze_support/) técnico de Braze o su gerente de éxito de cliente si tiene alguna pregunta.
{% endalert %}

## Requisitos previos

| Nombre | Descripción |
| ---- | ----------- |
| Cuenta Tealium | Se requiere una [cuenta Tealium](https://my.tealiumiq.com/) con acceso del lado del servidor. También recomendamos utilizar las integraciones del lado del cliente para aprovechar esta asociación. |
| REST API key | Una clave API Braze REST con permisos de `users.track`, `users.delete` y `subscription.status.set`.<br><br>Esto se puede crear en **Braze dashboard > Developer Console > REST API Key > Create New API Key**|
| \[Braze REST endpoint][6] | Tu URL de endpoint REST. Tu endpoint dependerá de la [URL de Brazo]({{site.baseurl}}/api/basics/#endpoints). |
{: .reset-td-br-1 .reset-td-br-2}

## Integración

### Paso 1: Configurar atributos e insignias

#### Comprender los atributos

El primer paso para usar AudienceStream es crear atributos. Los atributos le permiten definir las características importantes que representan los hábitos, preferencias, acciones y compromiso de un visitante con su marca. 

**Atributos de visita**: Los atributos de visita se refieren a la visita (o sesión) actual del usuario. Los datos almacenados en estos atributos persisten durante la visita. Algunos atributos de visita de ejemplo incluyen:
- Duración de la visita (Número)
- Navegador actual (cadena)
- Dispositivo actual (cadena)
- Cuenta (Número)

**Atributos del visitante**: Los atributos del visitante se refieren al usuario actual. Los datos almacenados en estos atributos persisten durante toda la vida del usuario. Algunos atributos de visitante de ejemplo incluyen: 
- Valor del pedido de por vida (número)
- Nombre (cadena)
- Fecha de nacimiento (Fecha)
- Compras Marcas (Tally)

Visite [Tealium][1] para obtener una lista completa de los tipos de datos disponibles.

##### Enriquecimiento de atributos

Una vez que identifique sus atributos deseados, puede configurarlos con [enriquecimientos](https://docs.tealium.com/server-side/getting-started/audiencestream-cdp/attributes-enrichments/), reglas de negocio que determinan cuándo y cómo actualizar los valores de los atributos. Cada tipo de datos ofrece su propia selección de enriquecimientos para manipular el valor del atributo. Esto está asociado con la configuración "CUANDO". Las siguientes opciones están disponibles para cada visita y atributo de visitante:

- Nuevo visitante: ocurre la primera vez que un visitante visita su sitio.
- Nueva visita: ocurre en una nueva visita de un visitante.
- Cualquier evento: ocurre en cualquier evento.
- Visita Finalizada: se produce cuando finaliza una visita.

También puede crear una condición personalizada, llamada regla, que determinará cuándo se producirá el enriquecimiento.

#### Insignias

Las insignias son atributos especiales del visitante que representan patrones de comportamiento valiosos. Las insignias se asignan o quitan a los visitantes según la lógica de sus enriquecimientos. Esta lógica generalmente combina múltiples condiciones para capturar segmentos de visitantes o establece un umbral para cuando se alcanza un valor particular.

#### Ejemplo de atributo e insignia

{% tabs local %}
{% tab Attribute %}

Cree un atributo de visitante "Valor de pedido de por vida" que calcule la cantidad acumulada gastada (`order_total`) por el cliente para todos los pedidos completados (evento de compra). Para configurar el valor del pedido de por vida en su cuenta Tealium, siga las siguientes instrucciones:

1. Vaya a **AudienceStream > Atributos de visitante/visita** y haga clic en **Añadir atributo**.
2. Seleccione el ámbito como **Visitante** y haga clic en **Continuar**.
3. Seleccione el tipo de datos **Número** y haga clic en **Continuar**.
4. Introduzca el nombre del atributo, "Lifetime Order Value".
5. Haga clic en **Agregar enriquecimiento** y seleccione **Número de incrementos**.
6. Seleccione el atributo que contiene el valor a incrementar en (`order_total`).
7. Deja "CUANDO" en "Cualquier evento" y haz clic en **Crear una nueva regla**.
8. Cree una regla que identifique cuándo se ha producido un evento de compra.
9. Haga clic en **Guardar** y, a continuación, en **Finalizar**.

Ahora, todos los clientes tendrán un atributo de valor de pedido de por vida vinculado a ellos.

{% endtab %}
{% tab Badge %}

Puedes crear insignias que te ayuden a clasificar y orientar a tus usuarios por ciertos atributos que comparten. Para el siguiente ejemplo, creamos una insignia VIP para usuarios con un "valor de pedido de por vida" de más de $500.

1. Vaya a **AudienceStream > Atributos de visitante/visita** y haga clic en **Añadir atributo**.
2. Seleccione el ámbito como **Visitante** y haga clic en **Continuar**.
3. Seleccione el tipo de datos **Badge** y haga clic en **Continuar**.
4. Introduzca el nombre de la placa, "VIP".
5. Haga clic en **Añadir enriquecimiento** y seleccione **Asignar insignia**.
6. Deje "CUANDO" en "Cualquier evento".
7. Cree una regla para la asignación de insignias seleccionando **Crear regla**. Asigne un título a esta regla, y usando el atributo anterior creado, establezca la regla en "...tiene atributo "Lifetime Order Value mayor que 500".
8. Haga clic en **Guardar** y, a continuación, en **Finalizar**.

{% endtab %}
{% endtabs %}

### Paso 2: Crear una audiencia

En la página principal de Tealium, seleccione **Audiences** en **AudienceStream** en la barra lateral de navegación. Aquí, puede crear una audiencia de usuarios con atributos comunes. La entrada o salida de un usuario de esta audiencia será el desencadenante de la acción del conector, configurada en el siguiente paso, que transmite esta información al perfil de usuario en Braze. 

Primero, nombra a tu audiencia y luego considera qué atributos se aplicarían al tipo de audiencia que estás tratando de crear. Por ejemplo, para crear una audiencia de usuarios VIP, puedes crear una audiencia de visitantes que tengan la **insignia VIP**.

Asegúrese de **guardar / publicar** su audiencia cuando termine.

### Paso 3: Crear un conector de eventos

Un conector es una integración entre Tealium y otro proveedor utilizado para transmitir datos. Estos conectores contienen acciones que representan las API compatibles con su socio. 

1. Desde la barra lateral en Tealium en **Server-Side**, navega a **AudienceStream > Audience Connectors**.
2. Seleccione el botón azul **\+ Añadir conector** para mirar a través del mercado de conectores. En el nuevo cuadro de diálogo que aparece, utilice la búsqueda de focos para encontrar el conector **Braze**.
3. Para agregar este conector, haga clic en la baldosa del conector **Soldadura**. Al hacer clic, puede ver el resumen de la conexión y una lista de la información requerida, las acciones compatibles y las instrucciones de configuración. La configuración comprende tres pasos: fuente, configuración y acción.

#### Fuente

En el diálogo **Fuente** que aparece, seleccione la audiencia que creó en el paso anterior y un activador que considere apropiado para su situación. También puede activar el tope de frecuencia para controlar la frecuencia con que se activa esta acción. 

![\]({% image_buster /assets/img/tealium/create_source.png %}){: style="max-width:90%;"}

#### Configuración

A continuación, aparecerá un diálogo de **configuración**. Seleccione **Agregar conector** en la parte inferior de la página. Nombra tu conector y proporciona tu endpoint de Braze API y la clave de Braze REST API aquí.

![\]({% image_buster /assets/img/tealium/create_configuration.png %}){: style="max-width:70%;"}

Si ha creado un conector anteriormente, puede usar uno existente de la lista de conectores disponibles y modificarlo para que se ajuste a sus necesidades con el icono del lápiz o eliminarlo con el icono de la papelera. 

Después de crear o seleccionar un conector para vincular a esta audiencia, haga clic en Listo para continuar.

#### Acción

A continuación, nombra tu acción de conector y selecciona un tipo de acción que enviará datos según la asignación que configures. Aquí, asignará los atributos Braze a los nombres de atributos Tealium. Dependiendo del tipo de acción que elija, habrá una variada selección de campos requeridos por Tealium. Los siguientes son ejemplos y explicaciones de estos campos.

{% alert important %}
No todos los campos ofrecidos son obligatorios.

![\]({% image_buster /assets/img/tealium/minimize.gif %}){: style="max-width:90%"}
{% endalert %}

{% tabs local %}
{% tab Track User (Batch and Non-Batch) %}

Esta acción le permite realizar un seguimiento de los atributos de usuario, evento y compra en una sola acción. Aunque la acción Track User es la misma para AudienceStream y EventStream, Tealium recomienda establecer asignaciones de atributos de usuario con acciones de AudienceStream y las asignaciones de eventos y compras con acciones de EventStream.

| Parámetros | Descripción |
| ---------- | ----------- |
| ID de usuario | Utilice este campo para asignar el campo ID de usuario de Tealium a su equivalente de Braze. Mapee uno o más atributos de ID de usuario. Cuando se especifican varios ID, el primer valor no en blanco se selecciona en función del siguiente orden de prioridad: ID externo, ID de soldadura fuerte, nombre de alias y etiqueta de alias.<br><br>\- El ID externo y el ID de soldadura fuerte no deben especificarse si se importan fichas push.<br>\- Si se especifica un alias de usuario, se debe establecer el nombre del alias y la etiqueta del alias. <br><br>Para obtener más información, consulte el punto final de Braze [`/users/track`]({{site.baseurl}}/api/endpoints/user_data/post_user_track/). |
| Atributos de usuario | Utilice los nombres de campo de perfil de usuario existentes de Braze para actualizar los valores de perfil de usuario en el panel de Braze o agregue sus propios datos de [atributos de usuario]({{site.baseurl}}/api/objects_filters/user_attributes_object/) personalizados a los perfiles de usuario.<br><br>\- Por defecto, se crearán nuevos usuarios si uno no existe.<br>\- Al configurar **Update Existing Only** en `true`, solo se actualizarán los usuarios existentes y no se creará ningún usuario nuevo.<br>\- Si un atributo Tealium está vacío, se convertirá en null y se eliminará del perfil de usuario de Braze. Se deben usar enriquecimientos si no se deben enviar valores nulos a Braze para eliminar un atributo de usuario. |
| Modificar atributos de usuario | Utilice este campo para incrementar o disminuir ciertos atributos de usuario<br><br>\- Los atributos enteros pueden ser incrementados por enteros positivos o negativos.<br>\- Los atributos del array pueden modificarse añadiendo o eliminando valores de arrays existentes. |
| Evento | Un evento representa una sola ocurrencia de un evento personalizado por un usuario en particular en una marca de tiempo. Utilice este campo para rastrear y asignar atributos de evento como los del [objeto evento]({{site.baseurl}}/api/objects_filters/event_object/) Braze. <br><br>\- Se requiere `Name` de atributos de evento para cada evento mapeado.<br>- `Time` de atributos de evento se establece automáticamente en ahora a menos que se mapee explícitamente. <br>\- Por defecto, se crearán nuevos eventos si uno no existe. Al establecer `Update Existing Only` en `true`, solo se actualizarán los eventos existentes y no se creará ningún evento nuevo.<br>\- Mapear atributos de tipo array para agregar múltiples eventos. Los atributos de tipo matriz deben tener la misma longitud.<br>\- Los atributos de valor único se pueden utilizar y aplicar a cada evento. |
| Plantilla de evento | Proporcionar plantillas de eventos para ser referenciadas en los datos del cuerpo. Las plantillas se pueden usar para transformar datos antes de enviarlos a Braze. Consulte la [Guía de plantillas](https://docs.tealium.com/server-side/connectors/webhook-connectors/trimou-templating-engine/) de Tealium para obtener más información. |
| Variable de plantilla de evento | Proporcione variables de plantilla de eventos como entrada de datos. Consulte la [Guía de variables](https://docs.tealium.com/server-side/connectors/webhook-connectors/template-variables/) de plantilla de Tealium para obtener más información. |
| Compra | Utilice este campo para rastrear y asignar atributos de compra de usuario como los del [objeto de compra]({{site.baseurl}}/api/objects_filters/purchase_object/) de soldadura fuerte.<br><br>\- Los atributos de compra `Product ID`, `Currency` y `Price` son necesarios para cada compra mapeada.<br>\- Compra atributo `Time` se establece automáticamente a ahora a menos que se mapee explícitamente.<br>\- Por defecto, se crearán nuevas compras si no existe una. Al establecer `Update Existing Only` en `true`, solo se actualizarán las compras existentes y no se creará ninguna nueva compra.<br>\- Mapear atributos de tipo array para agregar varios artículos de compra. Los atributos de tipo matriz deben tener la misma longitud.<br>\- Se pueden utilizar atributos de valor único que se aplicarán a cada elemento.|
| Plantilla de compra | Las plantillas se pueden usar para transformar datos antes de que se envíen a Braze.<br>\- Defina una plantilla de compra si necesita soporte para objetos anidados.<br>\- Cuando se define una plantilla de compra, se ignorará la configuración configurada en la sección de compras de su acción.<br>\- Consulte la [Guía de Plantillas](https://docs.tealium.com/server-side/connectors/webhook-connectors/trimou-templating-engine/) de Tealium para obtener más información.|
| Variable de plantilla de compra | Proporcione variables de plantilla de producto como entrada de datos. Consulte la [Guía de variables](https://docs.tealium.com/server-side/connectors/webhook-connectors/template-variables/) de plantilla de Tealium para obtener más información. |
{: .reset-td-br-1 .reset-td-br-2}

![\]({% image_buster /assets/img/tealium/track_user_example2.png %}){: style="max-width:90%"}

{% endtab %}
{% tab Delete User (Non-Batch) %}

Esta acción le permite eliminar usuarios del panel de Braze.

| Parámetros | Descripción |
| ---------- | ----------- |
| ID de usuario | Utilice este campo para asignar el campo Tealium User ID a su equivalente de Braze.<br><br>\- Mapear uno o más atributos de ID de usuario. Cuando se especifican varios ID, el primer valor no en blanco se selecciona en función del siguiente orden de prioridad: ID externo, ID de soldadura fuerte, nombre de alias y etiqueta de alias.<br>\- Al especificar un alias de usuario, Alias Name y Alias Label deben establecerse.<br><br>Para obtener más información, consulte el punto final de Braze [`/users/delete`]({{site.baseurl}}/api/endpoints/user_data/post_user_delete/). |
{: .reset-td-br-1 .reset-td-br-2}

![\]({% image_buster /assets/img/tealium/track_user_delete2.png %}){: style="max-width:90%"}

{% endtab %}
{% tab Update User Subscription Group Status (Non-Batch) %}
Esta acción le permite agregar o quitar usuarios de Braze SMS o grupos de suscripción de correo electrónico.

| Parámetros | Descripción |
| ---------- | ----------- |
| Tipo de grupo | Utilice este campo para indicar si se trata de un grupo de suscripción SMS o Email. |
| Tipo de actualización | Asigne esta acción a un evento de cancelación de suscripción o suscripción 
| Atributos | \- ID del grupo de suscripción (requerido): El ID del grupo de suscripción relacionado con el tipo de grupo asignado en el campo anterior.<br>\- ID externo: El ID externo del usuario.<br><br>Grupo de email específico:<br>Email: La dirección de correo electrónico del usuario.<br>**Si el ID externo no está definido, se requerirá el correo electrónico.**<br><br>Grupo SMS específico:<br>Teléfono: El número de teléfono en formato E.164. Por ejemplo, +14155552671.<br>**Si el ID externo no está definido, se requerirá el teléfono.** |
{: .reset-td-br-1 .reset-td-br-2}

![\]({% image_buster /assets/img/tealium/update_subscription.png %}){: style="max-width:90%"}

{% endtab %}
{% endtabs %}

Seleccione **Finalizar**.

#### Resumen

Vea el resumen del conector que creó. Si desea modificar las opciones elegidas, seleccione **Atrás** para editar o **Finalizar** para completar.

Su conector ahora se muestra en la lista de conectores de su página de inicio de Tealium.

Asegúrese de guardar o publicar su conector cuando termine. Las acciones que configuraste se dispararán cuando se cumplan las conexiones de activación. 

### Paso 4: Pruebe su conector Tealium

Después de que el conector esté funcionando, debes probarlo para asegurarte de que funciona correctamente. La forma más sencilla de probar esto es utilizar la **herramienta de rastreo** Tealium. Para empezar a usar Trace, asegúrate de haber añadido la extensión del navegador Tealium Tools.

1. Para iniciar un nuevo rastreo, seleccione **Rastreo** en la barra lateral en Opciones del **lado del servidor**. Haga clic **en Inicio** y capture el ID de rastreo.
2. Abra la extensión del navegador e introduzca el Trace ID en AudienceStream Trace.
3. Examina el registro en tiempo real.
4. Busque la acción que desea validar haciendo clic en la entrada **Acciones activadas** para expandir.
5. Busque la acción que desea validar y vea el estado del registro. 

Consulte Tealium's [Trace documentation][21] for more detailed instructions on implementing Tealium' Trace tool.

## Demostración de integración

<div class="video-container">
  <iframe width="560" height="315" src="https://drive.google.com/file/d/1m2JI4vdFt3fDePBdVvVcQWEjbC82ApGA/preview" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

## Sobreedades potenciales del punto de datos

Hay tres formas principales en las que podrías alcanzar accidentalmente excesos de datos al integrar Braze through Tealium:

#### Envío de datos duplicados - solo enviar Braze deltas de atributos
Tealium 't send Braze deltas of user attributes. For example, if you have an EventStream action that tracks a user'su nombre, correo electrónico y número de teléfono celular, Tealium enviará los tres atributos a Braze cada vez que se active la acción. Tealium no buscará lo que cambió o se actualizó y enviará solo esa información.<br><br> 
**Solución**: <br>Puedes revisar tu backend para evaluar si un atributo ha cambiado o no, y si es así, llama a los métodos relevantes de Tealium para actualizar el perfil de usuario. **Esto es lo que suelen hacer los usuarios que integran Braze directamente.** <br>**OR**<br> Si 't store your own version of a user profile in your backend and can'no sabe si los atributos cambian o no, puede usar AudienceStream y [crear enriquecimientos](https://docs.tealium.com/server-side/attributes/manage-enrichments/add-enrichment/) para enviar solo atributos de usuario cuando los valores hayan cambiado. 

#### Envío de datos irrelevantes o sobrescritura innecesaria de datos
Si tiene varios EventStreams dirigidos a la misma fuente de eventos, **todas las acciones habilitadas para ese conector** se dispararán automáticamente cada vez que se active una sola acción, **esto también podría resultar en que los datos se sobrescriban en Braze.**<br><br>
**Solución**: <br>Configure una especificación de evento o feed separado para rastrear cada acción. <br>**OR**<br> Desactive las acciones (o conectores) que no desea disparar utilizando las palancas del panel de control de Tealium.

#### Inicializando Braze demasiado pronto
Los usuarios que se integran con Tealium usando la etiqueta Braze Web SDK pueden ver un aumento drástico en su MAU. **Si Braze se inicializa en la carga de la página, Braze creará un perfil anónimo cada vez que un usuario web navegue al sitio web por primera vez.** Algunos pueden querer rastrear solo el comportamiento del usuario cuando los usuarios han completado alguna acción, como "Iniciar sesión" o "Video visto", para reducir su recuento de MAU. <br><br>
**Solución**: <br>Configure [reglas de carga](https://docs.tealium.com/iq-tag-management/load-rules/about/) para determinar exactamente cuándo y dónde se carga una etiqueta en su sitio.

[1]: https://docs.tealium.com/server-side/attributes/about/
[15]: {% image_buster /assets/img/tealium/create_configuration.png %}
[6]: {{site.baseurl}}/api/basics?redirected=true#endpoints
[21]: https://docs.tealium.com/server-side/connectors/trace/about/
[17]: {% image_buster /assets/img/tealium/save_publish.png %}
