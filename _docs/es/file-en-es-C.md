---
nav_title: Campañas API
article_title: Campañas API
page_order: 5
description: "Este artículo de referencia cubre cómo generar un ID de campaña para incluirlo en sus llamadas API y cómo configurar esa campaña".
page_type: referencia
tool: Campañas

---
# Campañas API

> Este artículo de referencia cubre cómo generar un `campaign_id` incluir en sus llamadas API y cómo configurar esa campaña.

Las campañas API se suelen utilizar para mensajería transaccional. Al crear campañas API (no [campañas activadas por API]({{site.baseurl}}/user_guide/engagement_tools/campaigns/building_campaigns/delivery_types/api_triggered_delivery/)), el panel de Braze solo se usa para generar un `campaign_id`, que le permite realizar un seguimiento de los análisis para los informes de campaña. También puedes generar un ID de variación de mensaje, que es diferente para cada variante de tu campaña. 

Luego enviará esa información a su equipo de desarrollo para usarla en la solicitud de API, junto con:
- Copia de campaña
- Membresía de la audiencia
- Activos

Una vez que comience la campaña, podrá ver los resultados en el panel. Las campañas API utilizan las [API de mensajería]({{site.baseurl}}/api/endpoints/messaging/)de Braze, que tienen las mismas opciones de informes detallados y reorientación que las campañas creadas completamente a través del panel.

{% alert warning %}
Debido a que las campañas API suelen ser transaccionales, todos los usuarios son elegibles para las campañas API, incluso aquellos en su Grupo de Control Global.
{% endalert %}

## Crear una nueva campaña

Vaya a **Mensajería** > **Campañas** y haga clic en **Crear campaña**, luego seleccione **Campañas API**. Ahora puede continuar con la configuración de su campaña API.

Una [campaña activada por API]({{site.baseurl}}/user_guide/engagement_tools/campaigns/building_campaigns/delivery_types/api_triggered_delivery/) es diferente de una campaña API.

## Configura tu campaña

Para configurar su campaña, realice los siguientes pasos:

1. Agregue un título descriptivo para que pueda encontrar los resultados en nuestra página de campañas después de haber enviado sus mensajes.
2. Haga clic en **Agregar mensaje** y agregue los tipos de mensajes que se incluirán en su campaña API. Esto le permitirá generar un `campaign_id` y un ID de variación del mensaje, que difiere para cada canal que incluya. 
3. Opcionalmente, puede agregar un evento de conversión para realizar un seguimiento de las conversiones de los usuarios en una acción específica o en un objetivo de campaña.
4. Haga clic en **Guardar campaña** y estará listo para comenzar su campaña API.

## llamadas API

Después de guardar su campaña de API, incluya lo siguiente en su solicitud de API: 
- el generado `campaign_id` Los campos con su solicitud de API se indicaron en los [puntos finales de envío de mensajes][2].
- Un [objeto de mensaje]({{site.baseurl}}/api/objects_filters/#messaging-objects) para cada plataforma incluida en la campaña. En el objeto del mensaje, proporcione el ID de variación del mensaje. Esto especificará que las estadísticas deben recopilarse y mostrarse bajo esa variante. Se admiten los siguientes objetos de mensaje: Android, Tarjetas de contenido, correo electrónico, iOS, Kindle, SMS/MMS, web push y webhook.

[2]: {{site.baseurl}}/api/endpoints/messaging/#send-endpoints
