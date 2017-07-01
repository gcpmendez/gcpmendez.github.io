---
layout: post
title: Archivos
skip_related: false
---


{% assign totalwords = 0 %}
{% for post in site.posts %}
  {% assign wordcount = post.content | number_of_words %}
  {% assign totalwords = totalwords | plus: wordcount %}
{% endfor %}

{% assign months = "Enero|Febrero|Marzo|Abril|Mayo|Junio|Julio|Agosto|Septiembre|Octubre|Noviembre|Diciembre" | split: "|" %}
{% assign m = site.posts.last.date | date: "%-m" | minus: 1 %}
{% assign day = site.posts.last.date | date: "%d" %}
{% assign month = months[m] %}
{% assign year = site.posts.last.date | date: "%Y" %}

Desde el {{ day }} de {{ month }}, he escrito {{ totalwords }} palabras sobre desarrollo web, herramientas de desarrollo, desarrollo de sofware, ... . Espero que te hayas disfrutado leyendo algunas de esas palabras. Mis publicaciones favoritas se encuentran en negrita en la página principal.


<div id="archive">
{% for post in site.posts %}
  {% assign currentdate = post.date | date: "%Y" %}
  {% if currentdate != date %}
    {% unless forloop.first %}</ul>{% endunless %}
<h2>{{ currentdate }}</h2>
<ul>
    {% assign date = currentdate %}
  {% endif %}
  <li {% if post.favorite and post.layout != "writeup" %}class="favorite"{% endif %}>
    <a href="{{ post.url }}">{{ post.title }}{% if post.layout == "writeup" %} (Book Writeup){% endif %}</a>
  </li>
  {% if forloop.last %}</ul>{% endif %}
{% endfor %}
</div>

