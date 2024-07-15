---
nav_title: Solución de problemas
article: Solución de problemas
description: Pasos de solución de problemas para problemas comunes que puede experimentar mientras contribuye a Braze Docs.
page_order: 9
noindex: verdadero
---

# Solución de problemas

> Si lo que're having trouble contributing to Braze Docs, review these common issues first. If the issue you' estás experimentando no está en la lista, [háznoslo saber](https://github.com/braze-inc/braze-docs/issues/new?assignees=&labels=issue&projects=&template=report_an_issue.md&title=) para que podamos añadirlo aquí.

## La redirección no está funcionando

Si un [redirect que configuraste]({{site.baseurl}}/contributing/content_management/redirecting_urls/) en el archivo de redirección global (`assets/js/broken_redirect_list.js`) no está funcionando, verifica tu cadena de URL para cualquier carácter en mayúscula. Si encuentras alguno, conviértelos a minúsculas (incluso si el nombre de archivo correspondiente en el `_docs` directorio contiene caracteres en mayúsculas).

{% tabs local %}
{% tab before %}
```javascript
validurls['/docs/hidden/WIP_Partnerships/WIP_Guidelines'] = '/docs/contributing/home/';
```
{% endtab %}

{% tab after %}
```javascript
validurls['/docs/hidden/wip_partnerships/wip_guidelines'] = '/docs/contributing/home/';
```
{% endtab %}
{% endtabs %}

## El enlace de referencia cruzada devuelve un 404

Si un [enlace de referencia cruzada]({{site.baseurl}}/contributing/content_management/cross_referencing/) en su página (como `{% raw %}[Braze Developer Guide]({{site.baseurl}}/developer_guide/home){% endraw %}`) devuelve una página 404, verifique la URL para la siguiente cadena.

```plaintext
%7B%7Bsite.baseurl%7D%7D
```

Una URL que contiene esta cadena será similar a la siguiente:

```plaintext
https://www.braze.com/docs/user_guide/personalization_and_dynamic_content/connected_content/%7B%7Bsite.baseurl%7D%7D/user_guide/administrative/app_settings/message_activity_log_tab
```

Si encuentras esta cadena en la URL, uno o más de tus enlaces de referencia cruzada están rodeados de [etiquetas sin procesar de Liquid](https://shopify.dev/docs/api/liquid/tags/raw).

{% tabs local %}
{% tab liquid raw tag %}
<code>
&#123;% raw %} &#123;% endraw %}
</code>
{% endtab %}
{% endtabs %}

Mueva estas etiquetas para que solo rodeen el contenido de Liquid que desea mostrar como raw.

{% tabs local %}
{% tab before %}
<code>
&#123;% raw %} Learn how to use Liquid's <code>&#123;&#123; page_title }} tag. For more information, see <mem_29a1d163-33c7-4b9c-85b0-d96755f59a98 href="#">Liquid tags</mem_29a1d163-33c7-4b9c-85b0-d96755f59a98>. &#123;% endraw %}
</code>
{% endtab %}

{% tab after %}
<code>
Learn how to use Liquid's &#123;% raw %} &#123;&#123; page_title }} &#123;% endraw %} tag. For more information, see <mem_e30abf69-564f-4cf9-adaa-d2f0caf73c1f href="#">Liquid tags</mem_e30abf69-564f-4cf9-adaa-d2f0caf73c1f>.
</code>
{% endtab %}
{% endtabs %}
