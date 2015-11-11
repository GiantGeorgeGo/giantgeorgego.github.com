---
layout: page
title: O Captain! My Captain! 
---
{% include JB/setup %}
<i>github: https://github.com/GiantGeorgeGo</i>  
<i>email : zhihang.yeah@gmail.com</i>  

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

