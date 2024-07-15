---
title: «Tinta móvil»
article_title: Tinta móvil
alias: "/partners/movable_ink/"
description: «Este artículo de referencia describe la asociación entre Braze y Movable Ink, una plataforma de software basada en la nube que ofrece a los profesionales del marketing digital una forma de crear experiencias visuales atractivas y únicas que emocionen a los clientes. «
page_type: compañero
search_tag: Socio

---

# Tinta móvil

> [Movable Ink](https://www.movableink.com/) es una plataforma de software basada en la nube que ofrece a los profesionales del marketing digital una forma de crear experiencias visuales atractivas y únicas que emocionen a los clientes. La plataforma Movable Ink ofrece valiosas opciones de personalización que se pueden insertar fácilmente en sus campañas. 

Amplíe nuestras capacidades creativas aprovechando las funciones creativas inteligentes de Movable Ink, como el sondeo, el temporizador de cuenta regresiva y la función de rascar. La integración de Movable Ink y Braze permite un enfoque más completo de los mensajes dinámicos basados en datos, proporcionando a los usuarios elementos en tiempo real sobre las cosas que importan.

## Prerrequisitos

| Requisito | Descripción |
|---|---|
| Cuenta Movable Ink | Se requiere una cuenta de Movable Ink para aprovechar esta asociación. |
| Fuente de datos | Tendrá que conectar una fuente de datos a Movable Ink. Esto se puede hacer mediante CSV, importación de sitios web o API. Asegúrese de pasar los datos con un identificador unificador entre Braze y Movable Ink (por ejemplo,`external_id`).
{: .reset-td-br-1 .reset-td-br-2}

## Casos de uso
- Resúmenes mensuales o de fin de año personalizados.
- Personalice dinámicamente las imágenes para las notificaciones por correo electrónico, push o enriquecidas en función del último comportamiento conocido.<br>
	Por ejemplo: 
	- Uso de un mensaje push enriquecido para crear dinámicamente un cronograma de eventos extrayendo datos de la API. 
	- Usar la función de temporizador de cuenta regresiva para notificar a los usuarios cuando se acerca una gran oferta (por ejemplo, Black Friday, San Valentín, ofertas navideñas, etc.)
	- Usa la función Scratch Off como una forma divertida e interactiva de desembolsar códigos promocionales.

## Capacidades compatibles con Movable Ink

Intelligent Creative tiene muchas ofertas que los usuarios de Braze pueden aprovechar. En la siguiente lista se muestran las funciones compatibles. 

| Capacidad de tinta móvil | Característica | Notificación push enriquecida | Mensajería en la aplicación / Content Cards / Email | Detalles |
| ---------------------- |---| ---------------------- | -------------------------------- | ------- |
| Optimizador creativo | Mostrar contenido A/B | ✗ | ✔ | |
|| Optimizar | ✗ | ✔* | \* Debe usar la solución de Deeplinking de Branch |
| Reglas de segmentación | Fecha | ✔* | ✔ | \* Se admiten pero no se recomiendan porque las notificaciones push se almacenan en caché al recibirlas y no se actualizan |
|| Día de la semana | ✔* | ✔ | \* Se admiten pero no se recomiendan porque las notificaciones push se almacenan en caché al recibirlas y no se actualizan |
|| Hora del día | ✔* | ✔ | \* Se admiten pero no se recomiendan porque las notificaciones push se almacenan en caché al recibirlas y no se actualizan |
| Historias/actividad conductual | | ✔* | ✔* | \* El identificador de usuario único utilizado para Braze debe estar vinculado al identificador de su ESP |
| Enlaces profundos dentro de la aplicación | | ✔* | ✔* | \* Para ofrecer una experiencia optimizada a sus clientes, utilice una solución de enlace profundo establecida a través de Branch o una solución validada con el equipo de experiencia del cliente de Movable Ink. |
| Apps | Temporizador de cuenta regresiva | ✔* | ✔ | \* Se admiten pero no se recomiendan porque las notificaciones push se almacenan en caché al recibirlas y no se actualizan |
|| Sondeos | ✗ | ✔* | \* Después de votar, dejará la aplicación para ser una página de destino móvil |
|| Rasca | ✔* | ✔* | \* Al hacer clic, saldrá de la aplicación para disfrutar de la experiencia Scratch Off |
|| Video | ✔* | ✔* | \* Solo GIF animados, <br>Para Android, Braze requiere \[soporte para GIF] \[Soporte para GIF] en la implementación |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3  .reset-td-br-4}

## Integración

### Paso 1: Crear una fuente de datos para Movable Ink

Los clientes deberán crear una fuente de datos que puede ser un CSV, una importación de sitios web o una integración de API.

![Different data source options that will appear: CSV Upload, Website, or API Integration.]({% image_buster /assets/img/movable_ink/movable_ink1.png %})

{% tabs local %}
{% tab CSV Data Source %}
- **Fuente de datos CSV**: Cada fila debe tener al menos una columna de segmento y una columna de contenido. Una vez cargado el CSV, selecciona las columnas que se deben usar para segmentar el contenido. \[Ejemplo de archivo CSV] ({% image_buster /assets/download_file/movable_ink_CSV.csv %})

![The fields that will show up when selecting "CSV" as your data source.]({% image_buster /assets/img/movable_ink/movable_ink2.png %})
{% endtab %}
{% tab Website Data Source %}
- **Fuente de datos del sitio web**: Cada fila debe tener al menos una columna de segmento y una columna de contenido. Una vez cargado el CSV, selecciona las columnas que se deben usar para segmentar el contenido.
  - Dentro de este proceso, necesitarás mapear:
    - Qué campos se usarán como segmentos
    - Qué campos desea como campos de datos que se puedan personalizar dinámicamente en la creatividad (por ejemplo, atributos de usuario o atributos personalizados como nombre, apellidos, ciudad, etc.)

![The fields that will show up when selecting "Website" as your data source.]({% image_buster /assets/img/movable_ink/movable_ink3.png %})
{% endtab %}
{% tab API Integrations %}
- **Integraciones de API**: Usa la API de tu empresa para impulsar el contenido directamente desde una respuesta de la API.

![The fields that will show up when selecting "API Integration" as your data source]({% image_buster /assets/img/movable_ink/movable_ink4.png %})
{% endtab %}
{% endtabs %}

### Paso 2: Crea una campaña en la plataforma Movable Ink

Desde la pantalla de inicio de Movable Ink, crea una campaña. Puedes seleccionar entre un correo electrónico desde HTML, un correo electrónico desde una imagen o un bloque que se pueda usar en cualquier canal, incluidos los mensajes push, los mensajes integrados en la aplicación y las tarjetas de contenido (se sugiere).
También te sugerimos que eches un vistazo a las distintas opciones de contenido disponibles a través de los bloques.

![An image of what the Movable Ink platform looks like when creating a new Movable Ink campaign.]({% image_buster /assets/img/movable_ink/movable_ink5.png %}){: style="max-width:70%"}

Movable Ink tiene un editor sencillo para arrastrar y soltar elementos como texto, imágenes, etc. Si ha rellenado la fuente de datos, puede generar dinámicamente una imagen mediante las propiedades de los datos. Además, también puedes crear alternativas dentro de este flujo para los usuarios si la campaña se envía y un usuario no cumple con los criterios de personalización.

![The Movable Ink block editor showing the different customizable elements.]({% image_buster /assets/img/movable_ink/create_campaign2.png %})

Antes de terminar tu campaña, asegúrate de previsualizar las imágenes dinámicas y probar los parámetros de consulta para ver qué aspecto tendrán las imágenes al ser vistas. Cuando esté completo, se generará una URL dinámica que luego podrá insertarse en Braze.

Para obtener más información sobre cómo usar la plataforma Movable Ink, visita el \[Centro de asistencia de Movable Ink] \[soporte]

### Paso 3: Obtenga la URL del contenido de Movable Ink

Para incluir contenido de Movable Ink en los mensajes de Braze, debe localizar la URL de origen que Movable Ink le ha proporcionado. 

Para obtener la URL de origen, debe haber configurado el contenido en el panel de control de Movable Ink y, desde allí, terminar y exportar el contenido. En la página de **finalización**, copie la URL de origen (`img src`) de la etiqueta de la creatividad.

![The page that appears once you have completed your Movable Ink campaign, here you find your content URL.]({% image_buster /assets/img/movable_ink/obtain_url.png %}){: style="max-width:80%;"}

A continuación, en la plataforma Braze, pegue la URL en el campo correspondiente. Encontrarás los campos correspondientes a tu canal de mensajería en el paso 4. Por último, reemplaza cualquier etiqueta de combinación (por ejemplo {% raw %} ```&mi_u=%%email%%```{% endraw %}) por la variable Liquid correspondiente (por ejemplo {% raw %} ```&mi_u={{${email_address}}}```{% endraw %}).

### Paso 4: Experiencia audaz

{% tabs local %}
{% tab Email %}
En la plataforma Braze, pega tu etiqueta creativa en el cuerpo del correo electrónico. ![] ({% image_buster /assets/img/movable_ink/web2.png %}){: style="max-width:90%"}<br><br>

{% endtab %}
{% tab Push notification %}

1. En la plataforma Braze:
	- Android Push: Pegue la URL en los campos **Imagen de icono push** e **Imagen de notificación ampliada**.<br>![\]({% image_buster /assets/img/movable_ink/android.png %}){: style="max-width:60%"}<br><br>
	- Push para iOS: Pegue la URL en el campo de enlace **multimedia** e indique el formato de archivo que está utilizando.<br>![\]({% image_buster /assets/img/movable_ink/ios.png %}){: style="max-width:60%"}<br><br>
	- Web push: Pegue la URL en los campos **Imagen de icono push** e **Imagen de notificación grande**.<br>![\]({% image_buster /assets/img/movable_ink/web.png %}){: style="max-width:60%"}<br><br>
2. Para asegurarte de que las imágenes no estén en caché, escribe la URL del mensaje con etiquetas Liquid vacías: <br>{% raw %}```{% if true %}{% endif %}https://movable-ink-image-url-goes-here```{% endraw %}

{% endtab %}
{% tab In-app message %}

1. En la plataforma Braze, pega la URL en el campo **Rich Notification Media**. ![] ({% image_buster /assets/img/movable_ink/image.png %}){: style="max-width:60%"}<br><br>
2. Proporcione una URL única para evitar el almacenamiento en caché. Para confirmar que las imágenes en tiempo real de Movable Ink funcionan y no se verán afectadas por el almacenamiento en caché, usa Liquid para añadir una marca de tiempo al final de la URL de la imagen de Movable Ink.

Para ello, utilice la siguiente sintaxis y sustituya la URL de la imagen según sea necesario:
{% raw %}
```
{% assign timestamp = "now" | date: "%s" %}
{% assign img = "https://movable-ink-image-url-goes-here" | append:timestamp %}
{{img}}
```
{% endraw %}
Esta plantilla tomará el tiempo actual (en segundos), lo añadirá al final de la pestaña de imágenes de Movable Ink (como un parámetro de consulta) y, a continuación, generará el resultado final. Puedes previsualizarlo en la pestaña **Prueba**; esto evaluará el código y mostrará una vista previa.

**3\.** Por último, reevalúe la pertenencia al segmento. Para ello, habilita la `Re-evaluate audience membership and liquid at send-time` opción que se encuentra en el paso **Audiencias objetivo** de una campaña. Si esta opción no está disponible, comunícate con tu gerente de éxito del cliente o con el servicio de atención al cliente de Braze. Esta opción indicará a los SDK de Braze que vuelvan a solicitar la campaña con una URL única cada vez que se active un mensaje en la aplicación.

{% endtab %}
{% tab Content Card %}

1. En la plataforma Braze, pega la URL en el campo **Rich Notification Media**. ![] ({% image_buster /assets/img/movable_ink/image.png %}){: style="max-width:60%"}<br><br>
2. Para dispositivos móviles: Las imágenes de Content Cards en iOS y Android se almacenan en caché al recibirlas y no se actualizan. 
  - Como solución alternativa, programa tu campaña como un mensaje periódico diario, semanal o mensual con una fecha de caducidad correspondiente para volver a crear la plantilla de la tarjeta de contenido. Por ejemplo, una tarjeta de contenido que debe actualizarse una vez al día debe configurarse como un envío programado diario con una caducidad de 1 día.
3. Para garantizar que las imágenes en tiempo real de Movable Ink funcionen y no se vean afectadas por el almacenamiento en caché cuando se vuelva a crear la plantilla de la tarjeta de contenido, usa Liquid para añadir una marca de tiempo al final de la URL de la imagen de Movable Ink.

Para ello, utilice la siguiente sintaxis y sustituya la URL de la imagen según sea necesario:
{% raw %}
```
{% assign timestamp = "now" | date: "%s" %}
{% assign img = "https://movable-ink-image-url-goes-here" | append:timestamp %}
{{img}}
```
{% endraw %}
Esta plantilla tomará el tiempo actual (en segundos), lo añadirá al final de la pestaña de imágenes de Movable Ink (como un parámetro de consulta) y, a continuación, generará el resultado final. Puedes previsualizarlo en la pestaña **Prueba**, que evaluará el código y mostrará una vista previa.

{% endtab %}
{% endtabs %}

## Solución de problemas

#### ¿Las imágenes dinámicas no se muestran correctamente? ¿Con qué canal tienes dificultades?
- **Empuje**: Asegúrate de tener una lógica vacía antes de la URL de la imagen de Movable Ink: <br>{% raw %}```{% if true %}{% endif %}https://movable-ink-image-url-goes-here```{% endraw %}
- **Mensajes y tarjetas de contenido integrados en la aplicación**: Asegúrese de que la URL de la imagen sea única para cada impresión. Esto se puede hacer añadiendo el Liquid apropiado para que cada URL sea diferente. Consulta \[instrucciones para enviar mensajes en la aplicación y en la tarjeta de contenido] \[instrucciones]. 
- **La imagen no se carga**: Asegúrese de reemplazar cualquier «etiqueta de combinación» por los campos de Liquid correspondientes en el panel de control de Braze. Por ejemplo: {% raw %} ```https://mi-msg.com/p/rp/image.png?mi_u=%%email%%``` {% endraw %} con {% raw %} ```https://mi-msg.com/p/rp/image.png?mi_u={{${email_address}}}```{% endraw %}.

#### ¿Tienes problemas para mostrar GIFs en Android?
- Android requiere compatibilidad con GIF en la implementación. Sigue el artículo \[personalización de mensajes en la aplicación] \[GIFSupport] para Android si no tienes esta configuración.

[1]: https://www.movableink.com/
\[datasource]: ({% image_buster /assets/img/movable_ink/movable_ink1.png %})
\[support]: https://support.movableink.com/
\[GIFsupport]: {{site.baseurl}}/developer_guide/platform_integration_guides/android/in-app_messaging/customization/gifs/
\[Instructions]: {{site.baseurl}}/partners/message_personalization/dynamic_content/movable_ink/#step-4-braze-experience
[1]: ({% image_buster /assets/img/movable_ink/android.png %})
[2]: ({% image_buster /assets/img/movable_ink/ios.png %})
[3]: ({% image_buster /assets/img/movable_ink/web.png %})