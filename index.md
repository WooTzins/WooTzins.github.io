---
layout: default
title: Home
---

# 欢迎来到我的博客

<nav>
  <ul>
    <li><a href="/">主页</a></li>
    <li><a href="/about">关于</a></li>
  </ul>
</nav>

## 最新博客文章

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
      <small>{{ post.date | date: "%B %d, %Y" }}</small>
    </li>
  {% endfor %}
</ul>
