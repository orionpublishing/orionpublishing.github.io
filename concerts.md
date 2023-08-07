--- 
layout: page 
---

<h1>Concerts</h1>
<p>A personal log of concerts I have attended.</p>
<p>I have a <a href="photogallery.html">photo gallery</a> here.
{% assign ntot = 0 %}
{% assign artisttot = 0 %}
{% assign venues = "" %}
{% assign cities = "" %}
{% for artist in site.artists %}
    {% assign artisttot = artisttot | plus: 1 %}
    {% for show in artist.shows %}
        {% assign ntot = ntot | plus: 1 %}
        {% for hash in show %}
            {% assign city = hash[1][3].city | strip | split: "," %}
            {% assign city = city[0] %}
            {% assign venue = hash[1][2].venue | strip %}
            {% assign temp = venues | split:',' %}
            {% assign temp2 = cities | split:',' %}
            {% unless temp contains venue %}
            {% assign venues = venues | append: ',' | append: venue %}
            {% endunless %}
            {% unless temp2 contains city %}
            {% assign cities = cities | append: ',' | append: city %}
            {% endunless %}
        {% endfor %}
    {% endfor %}
{% endfor %}
{% assign venues = venues | remove_first: "," | split:',' %}
{% assign cities = cities | remove_first: "," | split:',' %}
<h4>Stats</h4>
<p> Total sets attended: {{ntot}} </p>
<p>Artists/Bands: {{artisttot}}</p>
<p>Venues Attended: {{venues.size}}</p>
<p>Cities: {{cities.size}}</p>
{% for artist in site.artists %}
<hr>
<h3><a href="{{artist.url}}">{{artist.artist}}</a></h3>
{% for show in artist.shows %}
{% assign ntot = ntot | plus: 1 %}
{% for hash in show %}
<b>{{hash[0]}}</b>: {{hash[1][2].venue}}, {{hash[1][3].city}} ({{hash[1][1].role}})<br>
{% endfor %}


{% endfor %}

{% endfor %}

