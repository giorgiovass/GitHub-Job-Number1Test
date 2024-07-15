---
nav_title: Gestión del contenido
article: Administrar contenido
description: "Esta es una visión general de cómo se administra el contenido en Braze Docs".
page_order: 2
noindex: true
---

# Acerca de la gestión de contenidos

> Esta es una descripción general de cómo se administra el contenido en Braze Docs. Para obtener más información sobre un tema específico, elija la página dedicada al tema en la navegación.

## Metodología

Braze Docs se administra utilizando docs-as-code, un método para administrar documentación que refleja el ciclo de vida del desarrollo de software mediante un sistema de control de versiones. Braze Docs utiliza el sistema de control de versiones Git, que permite a los colaboradores trabajar en la misma documentación sin sobrescribir el trabajo de los demás. Para obtener más información, consulte [Acerca del control de versiones y Git](https://docs.github.com/en/get-started/using-git/about-git#about-version-control-and-git).

![The Braze Docs repository's home page on GitHub.]({% image_buster /assets/img/contributing/github/home_page.png %})

## Generador de sitios 

Braze Docs se construye usando Jekyll, un popular generador de sitios estáticos que permite almacenar archivos de contenido y archivos de diseño en directorios separados, como `_docs` para archivos de contenido y `assets` para archivos de diseño. Cuando se construye el sitio, Jekyll combina inteligentemente cada archivo y los almacena como datos XML y HTML en el directorio `_site`. Para obtener más información, consulte [Jekyll Directory Structure](https://jekyllrb.com/docs/structure/).

![The home page for Braze Docs.]({% image_buster /assets/img/contributing/styling_examples/home.png %})

Como colaborador, trabajarás principalmente dentro de los siguientes directorios.

| Directorio                                                                     | Descripción                                                                                                                                                                                                                                                                                                                       |
|-------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [`_docs`](https://github.com/braze-inc/braze-docs/tree/develop/_docs)         | Contiene todo el contenido escrito para Braze Docs como archivos de texto escritos en Markdown. Los archivos de texto se organizan en directorios y subdirectorios que reflejan el sitio de documentos, como `_api` para la [sección API]({{site.baseurl}}/api/home) y `user_guide` para la [sección Guía del usuario]({{site.baseurl}}/user_guide/introduction). |
| [`_includes`](https://github.com/braze-inc/braze-docs/tree/develop/_includes) | Contiene archivos de texto (llamados "incluye") que se pueden reutilizar en cualquier archivo del directorio `_docs`. Normalmente, incluye piezas cortas y modulares de contenido que no usan formato estándar. Los archivos almacenados en esta ubicación son importantes para la [reutilización del contenido](#content-reuse).                                            |
| [`assets`](https://github.com/braze-inc/braze-docs/tree/develop/assets)       | Contiene todas las imágenes de Braze Docs. Cualquier archivo de texto en el directorio `_docs` o `_includes` puede enlazar a este directorio para mostrar una imagen en su página.                                                                                                                                                                         |
{: .reset-td-br-1 .reset-td-br-2}

{% alert tip %}
Para un recorrido completo, vea [Generar una vista]({{site.baseurl}}/contributing/generating_a_preview/) previa.
{% endalert %}

## Páginas

Cada página de Braze Docs se escribe en sintaxis Markdown y se almacena como un archivo Markdown usando la extensión de archivo `.md`. En la parte superior de cada archivo Markdown, la materia frontal YAML se utiliza para agregar metadatos ocultos para cada página.

```markdown
---
METADATA_KEY: METADATA_VALUE
---

# CONTENT
```

Sustitúyase lo siguiente.

| Marcador de posición      | Descripción                                                                                                                              |
|------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| `METADATA_KEY`   | La clave que representa un tipo de metadatos compatible. Para obtener más información, consulte [Metadata]({{site.baseurl}}/contributing/yaml_front_matter/metadata/). |
| `METADATA_VALUE` | El valor asignado a la clave del tipo de metadatos. Para obtener más información, consulte [Metadata]({{site.baseurl}}/contributing/yaml_front_matter/metadata/).  |
| `CONTENT`        | Contenido de la página escrito en sintaxis Markdown.                                                                                           |
{: .reset-td-br-1 .reset-td-br-2}

{% tabs local %}
{% tab example input %}
```markdown
---
nav_title: Contributing to Braze Docs
article: Contributing to Braze Docs
description: "Here's what you need to start contributing to Braze Docs!"
page_order: 0
search_tag: Contributing
---

# Contributing to Braze Docs

> Thanks for contributing to Braze Docs! Every Tuesday and Thursday, we merge community contributions and deploy them to Braze Docs. Use this guide to get your changes merged during our next deployment.
```
{% endtab %}

{% tab example output %}
![Example page on Braze Docs.]({% image_buster /assets/img/contributing/styling_examples/page.png %})
{% endtab %}
{% endtabs %}

{% alert tip %}
Para un recorrido completo, vea [Creación de una página]({{site.baseurl}}/contributing/content_management/pages/#creating-a-page).
{% endalert %}

## Imágenes

Las imágenes se almacenan como archivos PNG dentro de `assets/img`. La estructura del directorio `img` no necesita coincidir con la estructura de Braze Docs; sin embargo, es mejor agrupar las imágenes relacionadas en subdirectorios.

Cada imagen se puede vincular a una o más páginas utilizando la siguiente sintaxis.

{% raw %}
```markdown
![ALT_TEXT.]({% image_buster /assets/img/DIRECTORY/IMAGE.png %})
```
{% endraw %}

Sustitúyase lo siguiente.

| Marcador de posición | Descripción                                                                                                             |
|-------------|-------------------------------------------------------------------------------------------------------------------------|
| `ALT_TEXT`  | El texto alternativo de la imagen. Esto es necesario para hacer Braze Docs igualmente accesible para aquellos que usan lectores de pantalla. |
| `IMAGE`     | La ruta relativa a su imagen a partir del directorio `img`.                                                      |
{: .reset-td-br-1 .reset-td-br-2}

Su imagen en línea debe ser similar a la siguiente:

{% raw %}
```markdown
![The form for creating a new pull request on GitHub.]({% image_buster /assets/img/contributing/getting_started/github_pull_request.png %})
```
{% endraw %}

{% alert tip %}
Para un recorrido completo, vea [Agregar una nueva imagen]({{site.baseurl}}/contributing/content_management/images/#adding-a-new-image).
{% endalert %}

## Secciones

Braze Docs se organiza en [secciones primarias](#primary-sections) y [subsecciones](#subsections).

### Secciones primarias

Las secciones principales de Braze Docs son:

- [Braze Docs Home]({{site.baseurl}})
- [Guía del usuario]({{site.baseurl}}/user_guide/introduction)
- [Guía del desarrollador]({{site.baseurl}}/developer_guide/home)
- [Braze API Guide]({{site.baseurl}}/api/home)
- [Socios tecnológicos]({{site.baseurl}}/partners/home)
- [Braze Help]({{site.baseurl}}/help/home)
- [Contribuyendo a Braze Docs]({{site.baseurl}}/contributing/home/)

Aparte de **contribuir a Braze Docs**, se puede acceder a estas secciones principales en el encabezado del sitio desde cualquier página de Braze Docs.

![The primary sections as shown on the site header on Braze Docs.]({% image_buster /assets/img/contributing/styling_examples/header.png %})

Cada sección primaria se construye utilizando [colecciones Jekyll](https://jekyllrb.com/docs/collections/), lo que permite agrupar el contenido relacionado para facilitar la gestión. Tenga en cuenta que, aunque todas las secciones primarias son colecciones, no todas las colecciones son secciones primarias. Puede encontrar la lista completa de colecciones de Braze Docs en el archivo de configuración de Jekyll, `_config.yml`.

```yaml
collections:
  home:
    title: Documentation
    output: true
    default_nav_url: ''
    page_order: 1
  user_guide:
    title: User Guide
    output: true
    default_nav_url: introduction/
    page_order: 2
  developer_guide:
    title: Developer Guide
    output: true
    default_nav_url: home/
    page_order: 3
  api:
    title: API
    output: true
    default_nav_url: home/
    page_order: 4
  partners:
    title: Technology Partners
    output: true
    default_nav_url: home/
    page_order: 5
  help:
    title: Help
    output: true
    default_nav_url: home/
    page_order: 6
  contributing:
    output: true
    default_nav_url: contributing/
  hidden: # Hidden pages not directly linked via navigation
    title: Braze
    output: true
    hidden: true
  docs_pages: # Site specific pages. ie main redirects and search
    title: Braze
    output: true
    hidden: true
```

Cada colección listada representa un directorio dentro del directorio `_docs`.

```plaintext
braze-docs
└── _docs
    ├── _api
    ├── _contributing
    ├── _developer_guide
    ├── _docs_pages
    ├── _help
    ├── _hidden
    ├── _home
    ├── _partners
    └── _user_guide
```

La página de destino para cada sección primaria es un archivo Markdown estándar con la clave de `page_order:` establecida en `0`.

{% tabs local %}
{% tab example input %}
```markdown
---
page_order: 0
nav_title: Home
article_title: Braze User Guide
layout: user_guide
user_top_header: "Braze User Guide"
---
```
{% endtab %}

{% tab example output %}
![An example landing page on Braze Docs.]({% image_buster /assets/img/contributing/styling_examples/primary_section.png %})
{% endtab %}
{% endtabs %}

### Subsecciones

Todas las secciones principales de Braze Docs contienen una o más subsecciones, cada una de las cuales representa un elemento expandible en la navegación del lado izquierdo.

A diferencia de las secciones primarias, las subsecciones se pueden configurar con o sin una página de destino. Las subsecciones sin páginas de destino son útiles para organizar contenido relacionado entre sí y minimizar el número de páginas no útiles en Braze Docs. Ya sea que una subsección esté configurada con o sin una página de destino, todas las subsecciones representan tanto un directorio como un archivo Markdown en el repositorio. Para ver un ejemplo, vea lo siguiente.

```plaintext
braze-docs
└── _docs
    └── _primary_section
        ├── subsection_a
        │   ├── page_a.md
        │   └── page_b.md
        ├── subsection_b
        │   ├── page_a.md
        │   └── page_b.md
        ├── subsection_a.md # not configured as a landing page
        └── subsection_b.md # configured as a landing page  
```

{% alert tip %}
Para un recorrido completo, vea [Creación de una sección]({{site.baseurl}}/contributing/content_management/sections/#creating-a-section).
{% endalert %}

En el directorio `_primary_section`, `subsection_a` no está configurado con una página de destino, mientras que `subsection_b` está configurado con una página de destino. En el ejemplo siguiente, `subsection_a.md` tiene `config_only:` establecido en `true`, lo que impide que esta página se muestre como una página de destino.

{% tabs local %}
{% tab example input %}
```markdown
---
nav_title: Subsection A
page_order: 0
config_only: true
---
```
{% endtab %}

{% tab example output %}
![The left-side navigation on Braze Docs, showing an example of an expanded section without a landing page.]({% image_buster /assets/img/contributing/styling_examples/subsection_config_only.png %})
{% endtab %}
{% endtabs %}

Sin embargo, `subsection_b.md` no utiliza la clave `config_only:`, por lo que esta página _se_ representa como una página de destino.

{% tabs local %}
{% tab example input %}
```markdown
---
nav_title: Subsection B
page_order: 0
---
```
{% endtab %}

{% tab example output %}
![The left-side navigation on Braze Docs, showing an example of an expanded section with a landing page.]({% image_buster /assets/img/contributing/styling_examples/subsection_landing_page.png %})
{% endtab %}
{% endtabs %}

{% alert note %}
Si bien una subsección con `config_only:` establecida en `true` no se representa como página, el nombre del directorio de la subsección se sigue utilizando en las URL de las páginas de esa subsección. Para obtener más información, consulte [URL](#urls).
{% endalert %}

## Referencias cruzadas

Una referencia cruzada es cuando una página de Braze Docs enlaza con otra página de Braze Docs. Debido a ciertos requisitos del sitio, Braze Docs no admite la [sintaxis estándar Markdown](https://www.markdownguide.org/basic-syntax/) para enlaces de referencia cruzada, por lo que creamos uno con Liquid.

{% raw %}
```markdown
[LINK_TEXT]({{site.baseurl}}/SHORT_URL)
```
{% endraw %}

Sustitúyase el texto siguiente:

| Marcador de posición | Descripción                                        |
|-------------|----------------------------------------------------|
| `LINK_TEXT` | El título de la página o acción relacionada.                  |
| `SHORT_URL` | La URL de la página con `https://www.braze.com` eliminado. |
{: .reset-td-br-1 .reset-td-br-2}

Su enlace de referencia cruzada debe ser similar al siguiente:

{% raw %}
```markdown
Before continuing, [create your SSH token]({{site.baseurl}}/docs/developer_guide/platform_wide/sdk_authentication).
```
{% endraw %}

{% alert tip %}
Para un recorrido completo, vea [Referencias cruzadas]({{site.baseurl}}/contributing/content_management/cross_referencing/).
{% endalert %}

## Reutilización de contenido

Jekyll ofrece la capacidad de reutilizar contenido escrito en todos los documentos utilizando la etiqueta `include`. Incluye se encuentran en el directorio `_includes` y se pueden escribir en Markdown o sintaxis HTML.

```markdown
{% raw %}{% multi_lang_include RELATIVE_PATH/FILE %}{% endraw %}
```

Sustitúyase el texto siguiente:

| Marcador de posición     | Descripción                                                                                                                                                                                                             |
|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `RELATIVE_PATH` | (Opcional) La ruta relativa al archivo desde el directorio `_includes`. Esto solo es necesario si incluyes un archivo de un directorio dentro del directorio `_includes`, como `_includes/braze/upgrade_notice.md`. |
| `FILE`          | Nombre del archivo, incluida la extensión del archivo.                                                                                                                                                                      |
{: .reset-td-br-1 .reset-td-br-2}

{% tabs local %}
{% tab example input %}
{% raw %}
```markdown
# Pages

> Learn how to create, modify, and remove pages on Braze Docs.

{% multi_lang_include contributing/prerequisites.md %}
```
{% endraw %}
{% endtab %}

{% tab example output %}
![Content reuse example on Braze Docs.]({% image_buster /assets/img/contributing/styling_examples/includes.png %})
{% endtab %}
{% endtabs %}

{% alert tip %}
Para un recorrido completo, vea [Reutilizar contenido]({{site.baseurl}}/contributing/content_management/reusing_content).
{% endalert %}

## Diseños

De forma predeterminada, Jekyll utiliza el diseño de `default.html` en el directorio `_layouts` para crear cada página en Braze Docs. Sin embargo, se pueden usar diferentes diseños asignando el diseño a la tecla `layout:` en la materia frontal YAML.

```markdown
---
layout: LAYOUT_VALUE
---
```

Reemplace `LAYOUT_VALUE` con el nombre del archivo de diseño y la extensión de archivo eliminada.

{% tabs local %}
{% tab example input %}
**Árbol de archivos**

```plaintext
braze-docs
└── _layouts
    └── api_page.html
```

**Metadatos en página**

```markdown
---
layout: api_page
---
```
{% endtab %}

{% tab example output %}
![API glossary layout example on Braze Docs.]({% image_buster /assets/img/contributing/styling_examples/layouts/api_page.png %})
{% endtab %}
{% endtabs %}

{% alert tip %}
Para obtener más información, consulte [Diseños de página]({{site.baseurl}}/contributing/yaml_front_matter/page_layouts).
{% endalert %}

## URLs

Las URL en Braze Docs siempre coinciden con la estructura de directorios dentro del repositorio de documentos. Dado el siguiente árbol de archivos de ejemplo, la URL para `page_a.md` sería `https://www.braze.com/docs/primary_section/subsection_a/page_a`.

```plaintext
braze-docs
└── _docs
    └── _primary_section
        └── subsection_a
            └── page_a.md
```

Esto incluye las URL de las páginas ubicadas en una [subsección](#subsections) con `config_only:` establecidos en `true`. Aunque las subsecciones `config_only` no son't rendered as pages, the subsection' el nombre del directorio se sigue utilizando para generar las URL de las páginas de ese directorio. Para ver un ejemplo, vea lo siguiente.

```plaintext
braze-docs
└── _docs
    └── _primary_section
        ├── subsection_a
        │   ├── page_a.md
        │   └── page_b.md
        ├── subsection_b
        │   ├── page_a.md
        │   └── page_b.md
        ├── subsection_a.md # not configured as a landing page
        └── subsection_b.md # configured as a landing page  
```

{% tabs local %}
{% tab subsection a %}

**Por ejemplo landing page**

```markdown
---
nav_title: Subsection A
page_order: 1 
config_only: true
---
```

Dado que `subsection_a.md` está configurada como página de destino, solo `page_a.md` y `page_b.md` recibirán una URL única. `subsection_b.md` **no** recibirá ninguna URL.

**URL de ejemplo**

```plaintext
Subsection A URL: N/A
Page A URL: https://www.braze.com/docs/primary_section/subsection_a/page_a
Page B URL: https://www.braze.com/docs/primary_section/subsection_a/page_b
```
{% endtab %}
{% tab subsection b %}
**Por ejemplo landing page**

```markdown
---
nav_title: Subsection B
page_order: 2 
---
```

Dado que `subsection_b.md` está configurada como página de destino, `page_a.md`, `page_b.md` y `subsection_b.md` recibirán una URL única.

**URL de ejemplo**

```plaintext
Subesction B URL: https://www.braze.com/docs/primary_section/subsection_b
Page A URL: https://www.braze.com/docs/primary_section/subsection_b/page_a
Page B URL: https://www.braze.com/docs/primary_section/subsection_b/page_b
```
{% endtab %}
{% endtabs %}
