---
layout: archive
title: "Sitemap"
permalink: /sitemap/
author_profile: true
---

{% include base_path %}

A list of all the posts and pages found on the site. For you robots out there, there is an [XML version]({{ base_path }}/sitemap.xml) available for digesting as well.

<h2>Pages</h2>
{% for post in site.pages %}
  {% include archive-single.html %}
{% endfor %}

<h2>Posts</h2>
{% for post in site.posts %}
  {% include archive-single.html %}
{% endfor %}

{% capture written_label %}'None'{% endcapture %}

{% raw %}
{% include base_path %}

A list of all the posts and pages found on the site. For you robots out there, there is an [XML version]({{ base_path }}/sitemap.xml) available for digesting as well.

{% assign excluded_pages = "Archive Layout with Content,Posts by Category,Posts by Collection,Markdown,Page not in menu,Page Archive,Portfolio,Posts by Tags,Talk map,Teaching,Terms and Privacy Policy,Jupyter notebook markdown generator" | split: "," %}
{% assign excluded_collections = "portfolio,talks,teaching,posts" | split: "," %}

<h2>Pages</h2>
<ul>
{% for p in site.pages %}
{% unless excluded_pages contains p.title %}
<li><a href="{{ p.url | relative_url }}">{{ p.title }}</a></li>
{% endunless %}
{% endfor %}
</ul>

<h2>Posts</h2>
{% if site.posts.size > 0 %}
<ul>
{% for post in site.posts %}
<li><a href="{{ post.url | relative_url }}">{{ post.title }}</a></li>
{% endfor %}
</ul>
{% else %}
<p>No posts found.</p>
{% endif %}

{% for collection in site.collections %}
{% unless collection.output == false or collection.label == "posts" or excluded_collections contains collection.label %}
<h2>{{ collection.label | capitalize }}</h2>
<ul>
{% for post in collection.docs %}
<li><a href="{{ post.url | relative_url }}">{{ post.title }}</a></li>
{% endfor %}
</ul>
{% endunless %}
{% endfor %}
{% endraw %}

{% for collection in site.collections %}
{% unless collection.output == false or collection.label == "posts" or excluded_collections contains collection.label %}
  {% capture label %}{{ collection.label }}{% endcapture %}
  {% if label != written_label %}
  <h2>{{ label }}</h2>
  {% capture written_label %}{{ label }}{% endcapture %}
  {% endif %}
{% endunless %}
{% for post in collection.docs %}
  {% unless collection.output == false or collection.label == "posts" or excluded_collections contains collection.label %}
  {% include archive-single.html %}
  {% endunless %}
{% endfor %}
{% endfor %}{% endraw %}
