
<!---DEFAULT RATE LIMIT-->

{% if include.endpoint == "default" %} Aplicamos el límite de velocidad de soldadura fuerte regular de 250.000 solicitudes por hora a este punto final, como se documenta en los [límites de velocidad]({{site.baseurl}}/api/api_limits/) API.

<!---PUT /scim/v2/Users/YOUR_ID_HERE--->
{% elsif include.endpoint == "update dashboard user" %}
This endpoint has a rate limit of 5000 requests per day. This rate limit is shared with the `/scim/v2/Users/` GET, DELETE, and POST endpoints as they are documented in [API rate limits]({{site.baseurl}}/api/api_limits/).

<!---GET /scim/v2/Users/YOUR_ID_HERE--->
{% elsif include.endpoint == "look up dashboard user" %}
This endpoint has a rate limit of 5000 requests per day, per one company. This limit is shared with the `/scim/v2/Users/` PUT, GET, DELETE, and POST endpoints as documented in [API rate limits]({{site.baseurl}}/api/api_limits/).

<!---DELETE /scim/v2/Users/YOUR_ID_HERE--->
{% elsif include.endpoint == "delete dashboard user" %}
This endpoint has a rate limit of 5000 requests a day, per company. This rate limit is shared with the `/scim/v2/Users/` PUT, GET, and POST endpoints as documented in [API rate limits]({{site.baseurl}}/api/api_limits/).

<!---POST /scim/v2/Users--->
{% elsif include.endpoint == "create dashboard user" %}
This endpoint has a rate limit of 5000 requests per day, per organization. This rate limit is shared with the `/scim/v2/Users/` PUT, GET, and DELETE endpoints as documented in [API rate limits]({{site.baseurl}}/api/api_limits/).

<!---GET /scim/v2/Users--->
{% elsif include.endpoint == "look up dashboard user email" %}
This endpoint has a rate limit of 5000 requests per day, per company. This rate limit is shared with the `/scim/v2/Users/` PUT, GET, DELETE, and POST endpoints as documented in [API rate limits]({{site.baseurl}}/api/api_limits/).

<!---/users/external_id/rename-->
<!---/users/external_id/remove-->

{% elsif include.endpoint == "external id migration" %} Aplicamos un límite de tasa de 1.000 solicitudes por minuto a este punto final, como se documenta en los [límites de tasa]({{site.baseurl}}/api/api_limits/) API.

<!---/users/track-->

{% elsif include.endpoint == "users track" %} Aplicamos un límite de velocidad base de 50.000 solicitudes por minuto a este endpoint para todos los clientes. Cada solicitud `/usuarios/pista` puede contener hasta 75 objetos de evento, 75 objetos de atributo y 75 objetos de compra. Cada objeto (matriz de eventos, atributos y compras) puede actualizar a un usuario cada uno. En total, esto significa que se pueden actualizar un máximo de 225 usuarios en una sola llamada. Además, un solo perfil de usuario puede ser actualizado por varios objetos.

Se aplican límites diferentes a los clientes que han comprado **Usuarios activos mensuales - CY 24-25**. Para obtener más detalles sobre estos límites, consulte [Monthly Active Users - CY 24-25 limits]({{site.baseurl}}/api/endpoints/user_data/post_user_track/#monthly-active-users-cy-24-25).

Consulte nuestra página sobre [límites de tarifas]({{site.baseurl}}/api/api_limits/) API para obtener más detalles y comuníquese con su gerente de éxito de cliente si necesita que su límite aumente.

<!---/users/export/ids-->

{% elsif include.endpoint == "users export ids" %} Si te incorporaste a Braze el 22 de agosto de 2024 o después, este endpoint tiene un límite de velocidad de 250 solicitudes por minuto, como se documenta en los [límites de velocidad]({{site.baseurl}}/api/api_limits/) API.

<!---/users/delete-->

{% elsif include.endpoint == "users delete" %} Para los clientes que se incorporaron a la plataforma Braze a partir del 16 de septiembre de 2021, aplicamos un límite de tarifa compartida de 20.000 solicitudes por minuto para este punto final. Este límite de velocidad se comparte con los puntos finales `/users/alias/new`, `/users/identify` y `/users/merge`, como se documenta en los [límites de velocidad]({{site.baseurl}}/api/api_limits/) API.

<!---/users/alias/new-->

{% elsif include.endpoint == "users alias new" %} Para los clientes que se incorporaron con Braze a partir del 16 de septiembre de 2021, aplicamos un límite de tarifa compartida de 20.000 solicitudes por minuto a este endpoint. Este límite de velocidad se comparte con los puntos finales `/users/delete`, `/users/identify`, `/users/merge` y `/users/alias/update`, como se documenta en los [límites de velocidad]({{site.baseurl}}/api/api_limits/) API.

<!---/users/alias/update-->

{% elsif include.endpoint == "users alias update" %} Para los clientes que se incorporaron con Braze a partir del 16 de septiembre de 2021, aplicamos un límite de tarifa compartida de 20.000 solicitudes por minuto a este punto final. Este límite de velocidad se comparte con los puntos finales `/users/delete`, `/users/identify`, `/users/merge` y `/users/alias/new`, como se documenta en los [límites de velocidad]({{site.baseurl}}/api/api_limits/) API.

<!---/users/alias/update-->

{% elsif include.endpoint == "users alias update" %} Para los clientes que se incorporaron con Braze a partir del 16 de septiembre de 2021, aplicamos un límite de tarifa compartida de 20.000 solicitudes por minuto a este punto final. Este límite de velocidad se comparte con los puntos finales `/users/delete`, `/users/identify` y `/users/merge`, como se documenta en los [límites de velocidad]({{site.baseurl}}/api/api_limits/) API.

<!---/users/identify-->

{% elsif include.endpoint == "users identification" %} Para los clientes que se incorporaron con Braze el 16 de septiembre de 2021 o después, aplicamos un límite de tarifa compartida de 20.000 solicitudes por minuto a este punto final. Este límite de velocidad se comparte con los puntos finales `/users/delete`, `/users/alias/new`, `/users/merge` y `/users/alias/update`, como se documenta en los [límites de velocidad]({{site.baseurl}}/api/api_limits/) API.

<!---/users/merge-->

{% elsif include.endpoint == "users merge" %} Para los clientes que se incorporaron con Braze el 16 de septiembre de 2021 o después, aplicamos un límite de tarifa compartida de 20.000 solicitudes por minuto a este punto final. Este límite de velocidad se comparte con los puntos finales `/users/delete`, `/users/alias/new`, `/users/identify` y `/users/alias/update`, como se documenta en los [límites de velocidad]({{site.baseurl}}/api/api_limits/) API.

<!---/custom_attributes-->

{% elsif include.endpoint == "custom\_attributes" %} Para los clientes que se incorporaron con Braze a partir del 16 de septiembre de 2021, aplicamos un límite de tarifa compartida de 1.000 solicitudes por hora a este punto final. Este límite de tasa se comparte con los puntos finales `/eventos`, `/eventos/lista` y `/compras/lista_producto`, como se documenta en los [límites de tasa]({{site.baseurl}}/api/api_limits/) API.

<!---/events-->

{% elsif include.endpoint == "eventos" %} Para los clientes que se incorporaron con Braze a partir del 16 de septiembre de 2021, aplicamos un límite de tarifa compartida de 1.000 solicitudes por hora a este punto final. Este límite de tasa se comparte con los puntos finales `/custom_attributes`, `/events/list` y `/purchases/product_list`, como se documenta en los [límites de tasa]({{site.baseurl}}/api/api_limits/) API.

<!---/events/list-->

{% elsif include.endpoint == "lista de eventos" %} Para los clientes que se incorporaron con Braze a partir del 16 de septiembre de 2021, aplicamos un límite de tarifa compartida de 1.000 solicitudes por hora a este punto final. Este límite de tasa se comparte con los puntos finales `/custom_attributes`, `/eventos` y `/purchas/product_list`, como se documenta en los [límites de tasa]({{site.baseurl}}/api/api_limits/) API.

<!---/purchases/product_list-->

{% elsif include.endpoint == "lista de productos de compras" %} Para los clientes que se incorporaron con Braze a partir del 16 de septiembre de 2021, aplicamos un límite de tarifa compartida de 1.000 solicitudes por hora a este punto final. Este límite de velocidad se comparte con los puntos finales `/custom_attributes`, `/eventos` y `/eventos/lista`, como se documenta en [límites de velocidad]({{site.baseurl}}/api/api_limits/) API.

<!---/messages/send-->
<!---/campaigns/trigger/send-->
<!---/canvas/trigger/send-->

{% elsif include.endpoint == "enviar puntos finales" %} Al especificar un segmento o una audiencia conectada en la solicitud, aplicamos un límite de velocidad de 250 solicitudes por minuto a este punto final. De lo contrario, si se especifica un `id_externo`, este punto final tiene un límite de tasa predeterminado de 250.000 solicitudes por hora compartidas entre `/messages/send`, `/campaigns/trigger/send` y `/canvas/trigger/send`, como se documenta en los [límites de tasa]({{site.baseurl}}/api/api_limits/) API.

<!---/transactional/v1/campaigns/{campaign_id}/send -->

{% elsif include.endpoint == "correo electrónico transaccional" %} Braze Los correos electrónicos transaccionales no están sujetos a un límite de tasa. Dependiendo del paquete elegido, el SLA cubre un número determinado de correos electrónicos transaccionales por hora. Las solicitudes que excedan esa tasa seguirán enviando, pero no están cubiertas por el SLA. El 99.9% de los correos electrónicos se enviarán en menos de un minuto.

<!---/sends/id/create-->

{% elsif include.endpoint == "sends id create" %} El número máximo diario de identificadores de envío personalizados que se pueden crear a través de este punto final es 100 para un espacio de trabajo dado. Cada combinación `de send_id` y `campaign_id` que cree contará para su límite diario. Los encabezados de respuesta para cualquier solicitud válida incluyen el estado actual del límite de tasa, consulte [Límites de tasa]({{site.baseurl}}/api/api_limits/) API para obtener más detalles.

<!---/subscription/status/set-->
{% elsif include.endpoint == "subscription status set" %}
This endpoint has a rate limit of 5,000 requests per minute shared across the `/subscription/status/set` and `/v2/subscription/status/set` endpoint as documented in [API rate limits]({{site.baseurl}}/api/api_limits/).

<!-- Add this phrase back ", as documented in [API rate limits]({{site.baseurl}}/api/api_limits/)" to CDI endpoints for GA -->

<!---GET /cdi/integrations--->
{% elsif include.endpoint == "cdi list integrations" %}
This endpoint has a rate limit of 50 requests per minute.

<!---POST /cdi/integrations/{integration_id}/sync--->
{% elsif include.endpoint == "cdi job sync" %}
This endpoint has a limit of 20 requests per minute.

<!---POST /cdi/integrations/{integration_id}/job_sync_status--->
{% elsif include.endpoint == "cdi job sync status" %}
This endpoint has a rate limit of 100 requests per minute.

{% endif %}

<!---Additional if statement for Messaging endpoints-->

{% if include.category == "puntos finales de mensajes" %}

Los endpoints Braze admiten [solicitudes de API]({{site.baseurl}}/api/api_limits/#batching-api-requests) por lotes. Una sola solicitud a los terminales de mensajería puede llegar a cualquiera de los siguientes:

- Hasta 50 `id_externos` específicos, cada uno con parámetros de mensaje individuales
- Un segmento de cualquier tamaño creado en el panel de Braze, especificado por su `segmento_id`
- Un segmento de audiencia de cualquier tamaño, definido en la solicitud como un objeto de [audiencia conectado]({{site.baseurl}}/api/objects_filters/connected_audience/)

{% endif %}

<!---Additional if statement for /messages/send endpoint-->

{% if include.category == "message send endpoint" %}

Los endpoints Braze admiten [solicitudes de API]({{site.baseurl}}/api/api_limits/#batching-api-requests) por lotes. Una sola solicitud a los terminales de mensajería puede llegar a cualquiera de los siguientes:

- Hasta 50 `id_externos` específicos
- Un segmento de cualquier tamaño creado en el panel de Braze, especificado por su `segmento_id`
- Un segmento de audiencia de cualquier tamaño, definido en la solicitud como un objeto de [audiencia conectado]({{site.baseurl}}/api/objects_filters/connected_audience/)

{% endif %}

{% if include.endpoint == "artículo de catálogo asíncrono" %}

Este punto final tiene un límite de tasa compartida de 16.000 solicitudes por minuto entre todos los puntos finales de artículos de catálogo asíncronos, como se documenta en los [límites de tasa]({{site.baseurl}}/api/api_limits/) API.

{% endif %}

{% if include.endpoint == "artículo de catálogo síncrono" %}

Este punto final tiene un límite de tasa compartida de 50 solicitudes por minuto entre todos los puntos finales de elementos de catálogo síncronos, como se documenta en los [límites de tasa]({{site.baseurl}}/api/api_limits/) API.

{% endif %}

{% if include.endpoint == "catálogo síncrono" %}

Este punto final tiene un límite de velocidad compartida de 50 solicitudes por minuto entre todos los puntos finales de catálogo síncronos, como se documenta en los [límites de velocidad]({{site.baseurl}}/api/api_limits/) API.

{% endif %}

{% if include.endpoint == "campos de catálogo asíncronos" o include.endpoint == "selecciones de catálogo asíncronas" %}

Este punto final tiene un límite de tasa compartida de 50 solicitudes por minuto entre todos los campos de catálogo asíncronos y los puntos finales de selección, como se documenta en los [límites de tasa]({{site.baseurl}}/api/api_limits/) API.

{% endif %}

{% if include.endpoint == "análisis de campañas de exportación" %}

Este punto final tiene un límite de velocidad de 50.000 solicitudes por minuto.

{% endif %}
