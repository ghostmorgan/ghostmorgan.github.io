---
bg: "owl.jpg"
layout: page
title: "About"
crawlertitle: "Why and how this blog was created"
permalink: /about/
summary: "About this blog and me"
active: about
---

<p style="text-align: justify;">Hello everybody! My name's Ivan. I'm 23. I live in Stavropol. It's a middle town in south of Russia. It's my personal blog and I really want to share with you my interesting materials. Sometimes I want to write interesting posts about things I like. I'm a computer security specialist, but I've got a lot of hobbies. I'm into history, maths, languages, music, programming, networking, games and so on. It's my first experience in writing, so don't judge me so strictly! Though I don't care! Feel like at home. Love everybody!</p>

You can find out more about me:

<ul style="list-style-type: none;">
{% if site.github_username %}
  <li>
    <a href="https://github.com/{{ site.github_username }}">
      <i class="fa fa-github fa-2x" style="color:#333"></i> GitHub
    </a>
  </li>
{% endif %}

{% if site.linkedin_username %}
  <li>
    <a href="https://www.linkedin.com/in/{{ site.linkedin_username }}">
      <i class="fa fa-linkedin fa-2x" style="color:#007bb5"></i> LinkedIn
    </a>
  </li>
{% endif %}

{% if site.facebook_username %}
  <li>
    <a href="https://www.facebook.com/{{ site.facebook_username }}">
      <i class="fa fa-facebook fa-2x" style="color:#3b5998"></i> Facebook
    </a>
  </li>
{% endif %}

{% if site.instagram_username %}
  <li>
    <a href="https://www.instagram.com/{{ site.instagram_username }}">
      <i class="fa fa-instagram fa-2x" style="color:#e95950"></i> Instagram
    </a>
  </li>
{% endif %}

{% if site.vk_username %}
  <li>
    <a href="https://www.vk.com/{{ site.vk_username }}">
      <i class="fa fa-vk fa-2x" style="color:#45668e"></i> VK
    </a>
  </li>
{% endif %}
</ul>
