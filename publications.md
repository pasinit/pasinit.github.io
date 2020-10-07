---
layout: page
title: Publications
---

{% assign hashes = site.data.publications %}
{% capture posts %}
  {% for hash in hashes %}
    |{{ hash.year }}###{{ hash.paper-type }}###{{ hash.doc-url }}###{{ hash.journal-url }}###{{ hash.title }}###{{ hash.booktitle }}###{{ hash.journal }}###{{ hash.authors }}###{{ hash.code }}###{{ hash.bibtex }}###
  {% endfor %}
{% endcapture %}
{% assign sortedhashes = posts | split: '|' | sort %}
{% for hash in sortedhashes %}
  {% assign hashitems = hash | split: '###' %}
  [comment]: <> {{ hashitems[0] }}
  {% if hashitems[4] == "" or hashitems[4] == nil %}
    {% break %}
  {% endif %}

  {% if hashitems[1] == "inproceedings" and hashitems[2] != "" %}
  * <a href="{{ hashitems[2] }}">{{ hashitems[4] }}</a>
  {% elsif hashitems[1] == "article" and hashitems[3] != "" %}
  * <a href="{{ hashitems[3] }}">{{ hashitems[4] }}</a>
  {% else %}
  * <a href="{{ hashitems[8] }}">{{ hashitems[4] }}</a>
  {% endif %}<br/>
  
  {{ hashitems[7] }}.
  {% if hashitems[1] == "inproceedings" %}*In: {{ hashitems[5] }}*, {{ hashitems[0]}}.
  {% elsif hashitems[1] == "article" %}*{{ hashitems[6] }}*, {{ hashitems[0]}}.
  {% endif %}
  {% if hashitems[9] != "" %}
 <code style="
     background: #f7f7f7;
     border-radius: 0.35em;
     border: solid 2px #efefef;
     font-family: 'Courier New', monospace; 
     display: block;
     overflow: scroll;
     white-space: nowrap;
 ">{{ hashitems[9] | linebreaksbr }}</code>
  {% endif %}

{% endfor %}


