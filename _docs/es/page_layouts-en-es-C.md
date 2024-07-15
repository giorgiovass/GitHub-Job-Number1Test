---
nav_title: Diseños de página
article: Diseños de página
description: Estos son los diseños de página que se pueden asignar a la tecla `page_layout` en el front matter YAML de una página.
page_order: 2
noindex: verdadero
---

#  Diseños de página

> Estos son los diseños de página que se pueden asignar a la [`page_layout`]({{site.baseurl}}/contributing/yaml_front_matter/metadata/#page-layout) tecla en el front matter YAML de una página. Para obtener más información general, consulte [Acerca de la gestión de contenido]({{site.baseurl}}/contributing/content_management/#layouts).

## Requisitos previos

Para usar un diseño de página, necesitarás agregar la clave [`page_layout`]({{site.baseurl}}/contributing/yaml_front_matter/metadata/#page-layout) a tu front matter YAML.

```markdown
---
nav_title: Getting started
article_title: Getting started with Braze Docs
page_layout: PAGE_LAYOUT_VALUE
---
```

Reemplace `PAGE_LAYOUT_VALUE` con uno de los valores de las siguientes secciones.

## Diseños visuales

### página de API

El valor `api_page` se utiliza para aplicar el formato de la página API. En el siguiente ejemplo, este formato se aplica a la página de [Integraciones de lista]({{site.baseurl}}/api/endpoints/cdi/get_integration_list/):

{% tabs local %}
{% tab example output %}
![An example page using the 'api_page' layout.]({% image_buster /assets/img/contributing/styling_examples/layouts/api_page.png %})
{% endtab %}
{% endtabs %}

### Guía del desarrollador

El `dev_guide` valor se utiliza para aplicar el formato de la guía del desarrollador. En el siguiente ejemplo, este formato se aplica a la página de [Catálogos Endpoints]({{site.baseurl}}/api/endpoints/catalogs): 

{% tabs local %}
{% tab example output %}
![An example page using the 'dev_guide' layout.]({% image_buster /assets/img/contributing/styling_examples/layouts/dev_guide.png %})
{% endtab %}
{% endtabs %}

### Página destacada

El valor `featured` se utiliza para aplicar el formato de página destacada. En el siguiente ejemplo, este formato se aplica a la página de [Eventos Predictivos]({{site.baseurl}}/user_guide/sage_ai/predictive_suite/predictive_events):

{% tabs local %}
{% tab example output %}
![An example page using the 'featured' layout.]({% image_buster /assets/img/contributing/styling_examples/layouts/featured.png %})
{% endtab %}
{% endtabs %}

### Página de glosario

El valor `glossary_page` se utiliza para aplicar el formato de la página del glosario. En el siguiente ejemplo, este formato se aplica a la página [Tipos de notificaciones push]({{site.baseurl}}/user_guide/message_building_by_channel/push/types):

{% tabs local %}
{% tab example output %}
![An example page using the 'glossary_page' layout.]({% image_buster /assets/img/contributing/styling_examples/layouts/glossary_page.png %})
{% endtab %}
{% endtabs %}

{% alert tip %}
En ciertos diseños, un valor como `"guide_top_text:"` podría beneficiarse de tener formato Markdown. Puede usar el formato Markdown para ciertos valores YAML. Para hacerlo, agregue `>` como el valor YAML y sangra el texto después.
<br>
Por ejemplo:<br>
guide_top_text: ><br>
    \# Este es un formato de Markdown de ejemplo
{% endalert %}

## Otros diseños

### Configuración en blanco

El valor `blank_config` se utiliza para ocultar una página en Braze Docs y redirigir automáticamente a los usuarios a `www.braze.com/docs`. Para obtener más información, consulte [Redirigir URL]({{site.baseurl}}/contributing/content_management/redirecting_urls/?tab=home%20page#redirecting-a-page).

### Redirigir

El valor `redirect` se utiliza para redirigir la URL a un encabezado en la página. Para obtener más información, consulte [Redirigir URL]({{site.baseurl}}/contributing/content_management/redirecting_urls/#redirecting-a-heading).
