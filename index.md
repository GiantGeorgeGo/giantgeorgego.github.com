---
layout: page
title: Giant George 
---
{% include JB/setup %}
<i>github: https://github.com/GiantGeorgeGo</i>  
<i>email : zhihang.yeah@gmail.com</i>  
<h>O Captain! My Captain!</h>
<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

