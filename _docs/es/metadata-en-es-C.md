---
nav_title: Metadatos
article: Metadatos
description: Estas son las claves de metadatos que se pueden agregar a la materia principal YAML de una página.
page_order: 0
noindex: verdadero
---

#  Metadatos

> Estas son las claves de metadatos que se pueden agregar a la materia principal YAML de una página. Para obtener más información general, consulte [Acerca de la gestión de contenido]({{site.baseurl}}/contributing/content_management/#pages).

Para agregar metadatos a un archivo Markdown, usa la sintaxis de front matter al principio de tu archivo.

```markdown
---
METADATA_KEY: METADATA_VALUE
---

# Getting started with Braze Docs

If you're new to Braze Docs or docs-as-code, start with our tutorial.
```

Reemplazar lo siguiente:

| Marcador de posición      | Descripción                                                                                                               |
|------------------|---------------------------------------------------------------------------------------------------------------------------|
| `METADATA_KEY`   | La clave que representa un tipo de metadatos compatible. Reemplazar con una [clave de metadatos](#required-keys) de la siguiente sección. |
| `METADATA_VALUE` | El valor asignado a la clave de metadatos. Compruebe los valores admitidos de una clave de metadatos en la siguiente sección.                 |
{: .reset-td-br-1 .reset-td-br-2}

## Claves requeridas

### Título del artículo

La `article_title` clave se usa para establecer el título de la página para los resultados de búsqueda en línea y la pestaña del navegador del usuario final. Esta clave acepta cualquier `string` valor. Para las convenciones de nomenclatura, consulte la [Guía de estilo de documentos de Braze]({{site.baseurl}}/contributing/style_guide/).

{% tabs local %}
{% tab usage example %}
```markdown
---
article_title: Getting started with Braze Docs
---
```
{% endtab %}
{% endtabs %}

### Descripción

La `description` clave se utiliza para establecer la descripción de la página en los resultados de búsqueda en línea. Esta clave acepta cualquier `string` valor de menos de 150 caracteres que esté rodeado por comillas dobles.

{% tabs local %}
{% tab usage example %}
```markdown
---
description: "If you're new to Braze Docs, start with this step-by-step tutorial."
---
```
{% endtab %}
{% endtabs %}

### Título de navegación

La clave `nav_title` se usa para establecer el título de la página en la barra de navegación lateral izquierda en Braze Docs. Esta clave acepta cualquier `string` menos de 30 caracteres. Si la [`hidden`](#hide-page-from-navigation) clave está configurada en `true`, `nav_title` no es necesario.

{% tabs local %}
{% tab usage example %}
```markdown
---
nav_title: Getting started
---
```
{% endtab %}
{% endtabs %}

## Claves opcionales

### Herramienta de compromiso

La clave `tool` se utiliza para configurar las herramientas de participación relacionadas con la página. Esta clave acepta uno o más de los siguientes `string` valores como una lista.

- `dashboard`
- `docs`
- `canvas`
- `campaigns`
- `currents`
- `location`
- `media`
- `reports`
- `segments`
- `templates`

{% tabs local %}
{% tab usage example %}
```markdown
---
tool:
  - currents
  - segments
---
```
{% endtab %}
{% endtabs %}

### Ocultar página de la navegación

La tecla `hidden` se usa para ocultar una página de la navegación del lado izquierdo en Braze Docs. Esta clave acepta los valores booleanos `true` o `false`.

{% tabs local %}
{% tab usage example %}
```markdown
---
hidden: true
---
```
{% endtab %}
{% endtabs %}

### Ocultar página de la búsqueda

La tecla `noindex` se usa para ocultar una página de los resultados de búsqueda internos y externos (como Braze Docs y Google Search). Esta clave acepta los valores booleanos `true` o `false`.

{% tabs local %}
{% tab usage example %}
```markdown
---
noindex: true
---
```
{% endtab %}
{% endtabs %}

### Ocultar tabla de contenido

La tecla `hide_toc` se usa para ocultar la tabla de contenido (TOC) en la página en el lado derecho de la página. Esta clave acepta los valores booleanos `true` o `false`.

{% tabs local %}
{% tab usage example %}
```markdown
---
hide_toc: true
---
```
{% endtab %}
{% endtabs %}

### Ocultar encabezado de la tabla de contenido

De forma predeterminada, la tabla de contenido (TOC) muestra todos los niveles de encabezado. Para mostrar solo niveles de encabezado específicos, use la tecla `toc_headers` para enumerar explícitamente los niveles deseados. Cualquier nivel de encabezado no listado se ocultará del TOC.

Esta clave acepta los siguientes valores de cadena:

- `h1`
- `h2`
- `h3`
- `h4`

{% tabs local %}
{% tab usage example %}
```markdown
---
toc_headers: h2
---
```
{% endtab %}
{% endtabs %}

### Canal de mensajería

La `channel` clave se usa para configurar los canales de mensajería relacionados de una página. Esta clave acepta uno o más de los siguientes `string` valores como una lista.

- `content cards`
- `email`
- `in-app messages`
- `news feed`
- `push`
- `sms`
- `webhooks`

{% tabs local %}
{% tab usage example %}
```markdown
---
channel:
  - email
  - news feed
---
```
{% endtab %}
{% endtabs %}

### Navegación solamente

La tecla `config_only` se usa para ocultar el contenido de una página sin ocultarlo en la barra de navegación lateral izquierda. Utilice esta clave cuando [cree una sección sin una página de destino]({{site.baseurl}}/contributing/content_management/sections?tab=without%20landing%20page#step-2-configure-your-section). Esta clave acepta los valores booleanos `true` o `false`.

{% tabs local %}
{% tab usage example %}
```markdown
---
config_only: true
---
```
{% endtab %}
{% endtabs %}

### Anular URL predeterminada

La tecla `permalink` se usa con la tecla [`hidden`](#hide-page-from-navigation) para anular la URL predeterminada de una página en Braze Docs. El valor asignado a `permalink` se antepondrá con `https://www.braze.com/docs` antes de redirigir. Esta clave acepta cualquier `string` valor que cumpla con los siguientes requisitos.

- Los caracteres están en minúsculas
- Las_palabras_están_separadas_por_guiones_bajos (`_`)
- Los "directorios" están separados por barras diagonales (`/`)
- Todos los demás caracteres especiales se eliminan

{% tabs local %}
{% tab usage example %}
```markdown
---
hidden: true
permalink: /support_contact/docs_team/
---
```
{% endtab %}
{% endtabs %}

### Diseño de página

La `layout` tecla se usa para configurar el diseño de una página. Si `layout` no está configurado, se utilizará el diseño `default`. Esta clave acepta cualquiera de los siguientes `string` valores.

- `api_page`
- `dev_guide`
- `featured_video`
- `featured`
- `glossary_page`
- `blank_config`
- `redirect`

Para obtener más información sobre cada valor, consulte [Diseños de página]({{site.baseurl}}/contributing/yaml_front_matter/page_layouts/).

{% tabs local %}
{% tab usage example %}
```markdown
---
page_layout: glossary_page
---
```
{% endtab %}
{% endtabs %}

### Orden de página

La `page_order` clave se usa para [ordenar secciones]({{site.baseurl}}/contributing/content_management/sections/#ordering-a-section) en la barra de navegación del lado izquierdo. Esta clave acepta cualquier número no negativo (como `0`, `20` o `5.5`).

{% tabs local %}
{% tab usage example %}
```markdown
---
page_order: 35.6
---
```
{% endtab %}
{% endtabs %}

### Tipo de página

La clave `page_type` se usa para establecer el formato de una página. Esta clave acepta cualquiera de los siguientes `string` valores.

- `glossary`
- `solution`
- `reference`
- `tutorial`
- `landing`
- `partner`
- `update`

Para obtener más información sobre cada valor, consulte [Tipos de página]({{site.baseurl}}/contributing/yaml_front_matter/page_layouts/).

{% tabs local %}
{% tab usage example %}
```markdown
---
page_type: tutorial
---
```
{% endtab %}
{% endtabs %}

### Plataforma

La clave `platform` se usa para configurar las plataformas relacionadas de la página. Esta clave acepta uno o más [SDKs de Braze]({{site.baseurl}}/developer_guide/home/) como un valor `string` en una lista.

{% tabs local %}
{% tab usage example %}
```markdown
---
platform:
  - iOS
  - Web
  - Android
---
```
{% endtab %}
{% endtabs %}
