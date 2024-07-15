---
nav_title: Líquido
article_title: Líquido
page_order: 0
layout: dev_guide
search_rank: 3
guide_top_header: "Personalización mediante etiquetas líquidas"
guide_top_text: "Braze puede sustituir automáticamente los valores de un usuario determinado en sus mensajes. Coloque la expresión dentro de dos conjuntos de llaves para notificar a Braze que va a utilizar un valor interpolado. Dentro de estos corchetes, los valores de usuario que desee sustituir deben estar rodeados por un conjunto adicional de corchetes con un signo de dólar delante de ellos.<br><br>Para obtener más información sobre Liquid, consulte nuestra guía <b><a href='https://learning.braze.com/path/dynamic-personalization-with-liquid'>Personalización dinámica con Liquid</a></b> ¡Ruta de aprendizaje de Braze!"
description: "Esta página de aterrizaje cubre todo lo relacionado con Liquid, como las etiquetas de personalización compatibles, los filtros, la configuración de valores predeterminados y mucho más".

guide_featured_title: "Artículos de sección"
guide_featured_list:
- name: Uso de líquido
  link: /docs/user_guide/personalization_and_dynamic_content/liquid/using_liquid/
  image: /assets/img/braze_icons/beaker-02.svg
- name: Etiquetas de personalización admitidas
  link: /docs/user_guide/personalization_and_dynamic_content/liquid/supported_personalization_tags/
  image: /assets/img/braze_icons/tag-01.svg
- name: Operadores
  link: /docs/user_guide/personalization_and_dynamic_content/liquid/operators/
  image: /assets/img/braze_icons/code-02.svg
- name: Filtros
  link: /docs/user_guide/personalization_and_dynamic_content/liquid/filters/
  image: /assets/img/braze_icons/flag-02.svg
- name: Filtros avanzados
  link: /docs/user_guide/personalization_and_dynamic_content/liquid/advanced_filters/
  image: /assets/img/braze_icons/settings-01.svg
- name: Configuración de valores predeterminados
  link: /docs/user_guide/personalization_and_dynamic_content/liquid/setting_default_values/
  image: /assets/img/braze_icons/table.svg
- name: Lógica de mensajería condicional
  link: /docs/user_guide/personalization_and_dynamic_content/liquid/conditional_logic/
  image: /assets/img/braze_icons/columns-01.svg
- name: Anulación de mensajes
  link: /docs/user_guide/personalization_and_dynamic_content/liquid/aborting_messages/
  image: /assets/img/braze_icons/refresh-ccw-01.svg
- name: Casos de uso de líquidos
  link: /docs/user_guide/personalization_and_dynamic_content/liquid/liquid_use_cases/
  image: /assets/img/braze_icons/list.svg
- name: Preguntas frecuentes
  link: /docs/user_guide/personalization_and_dynamic_content/liquid/faq/
  image: /assets/img/braze_icons/annotation-question.svg
  
---

## Acerca de Liquid

> Liquid es un lenguaje de plantillas de código abierto desarrollado por Shopify y escrito en Ruby. En Braze, Liquid se utiliza para convertir los datos del perfil de un usuario en mensajes. 

Por ejemplo, puede recuperar un atributo personalizado de un perfil de usuario que sea un tipo de datos entero y redondear ese valor al número entero más cercano. Para obtener más información sobre la sintaxis y el uso de Liquid, consulte [**Etiquetas de personalización admitidas**][1].

El lenguaje de plantillas líquidas admite el uso de objetos, etiquetas y filtros.

- [**Objetos**]({{site.baseurl}}/user_guide/personalization_and_dynamic_content/liquid/) Le permiten insertar atributos personalizados en sus mensajes.
- [**Etiquetas**]({{site.baseurl}}/user_guide/personalization_and_dynamic_content/liquid/supported_personalization_tags/) Le permiten insertar datos en la mensajería y usar lógica condicional para enviar mensajes si se cumplen las condiciones de los esquemas. Por ejemplo, puede usar etiquetas para incluir lógica inteligente, como instrucciones "if", en sus campañas.
- [**Filtros**]({{site.baseurl}}/user_guide/personalization_and_dynamic_content/liquid/filters/) Le permiten volver a formatear atributos personalizados y contenido dinámico. Por ejemplo, puede convertir una marca de tiempo, como *2016-09-07 08:43:50 UTC*, en una fecha, como *7 de septiembre de 2016*.

{% alert warning %}
Actualmente, Braze no es compatible con el 100% de Liquid de Shopify, solo con ciertas partes que hemos intentado describir en nuestra documentación. Te recomendamos encarecidamente que pruebes todos los mensajes con Liquid antes de enviarlos para reducir el riesgo de errores o de que utilices Liquid no compatible.
{% endalert %}

### Líquido 5

La soldadura fuerte es compatible con líquidos hasta e incluyendo **Liquid 5 de Shopify**. La implementación de Liquid admite la personalización de la sintaxis, los tipos de etiquetas y el control de espacios en blanco. Para obtener más información sobre etiquetas específicas, consulte [Etiquetas de sintaxis]({{site.baseurl}}/user_guide/personalization_and_dynamic_content/liquid/supported_personalization_tags/#syntax-tags).

Los siguientes nuevos filtros de matriz y matemáticos están disponibles para su uso en Liquid a medida que crea su mensajería.
- `at_least`
- `at_most`
- `compact`
- `concat`
- `sort_natural`
- `where`

Refiérase a nuestro [Filtros]({{site.baseurl}}/user_guide/personalization_and_dynamic_content/liquid/filters/) artículo para definiciones.

### Actualizaciones líquidas

Cada elemento de Liquid corresponde a un color, lo que te permite diferenciar tu Liquid de un vistazo en tu editor de Liquid.

![\]({% image_buster /assets/img/liquid_color_code.png %})

También puede aprovechar Liquid predicativo para atributos personalizados, nombres de atributos y mucho más a medida que crea sus mensajes personalizados.

![\]({% image_buster /assets/img/liquid_auto_complete.gif %}){: style="max-width:70%;"}


## Términos que debes conocer

Estos términos se reinterpretan de [**Documentación de Shopify**](https://shopify.github.io/liquid/basics/introduction/) en función de nuestro nivel de soporte.

{% raw %}

| Término | Definición | Ejemplo |  
|---|---|---|
| Líquido | Un lenguaje de plantillas de uso común orientado al cliente creado por Shopify y escrito en Ruby; Se utiliza para cargar/extraer contenido dinámico. | `{{${first_name}}}` insertará el nombre de pila de un usuario en un mensaje. |
| Objeto | Una denotación de una variable y la ubicación del nombre de la variable prevista que indica a Liquid dónde mostrar el contenido en el mensaje. | `{{${city}}}` insertará la ciudad de un usuario en un mensaje. |
| Etiqueta de lógica condicional | Las etiquetas crean lógica y controlan el flujo del contenido del mensaje. En Braze, las etiquetas de lógica condicional se utilizan para crear excepciones y variaciones en los mensajes en función de ciertos criterios predefinidos. | ```{% if ${language} == 'en' %}``` activará su mensaje de la manera designada en el caso de que un usuario haya designado "inglés" como su idioma. |
| Filtros | Se utiliza para cambiar, restringir o volver a formatear la salida del objeto Liquid. A menudo se utiliza para crear operaciones matemáticas. | ```{{"Big Sale" | upcase}}``` hará que las palabras "Gran Venta" aparezcan como "GRAN VENTA" en el mensaje. |
| Operadores | Se utiliza en los mensajes para crear dependencias o criterios que pueden afectar al mensaje que recibe el usuario. | Si un usuario cumple con los criterios definidos en un mensaje etiquetado con `{% custom_attribute.${Total_Revenue} > 0%}`, recibirán el mensaje. De lo contrario, recibirán otro mensaje designado (o no), dependiendo de lo que establezca. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3}

{% endraw %}

<br>

[1]: {{site.baseurl}}/user_guide/personalization_and_dynamic_content/liquid/supported_personalization_tags/
