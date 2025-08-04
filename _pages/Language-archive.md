---
title: 'Language'
layout: categories
permalink: /Language/
taxonomy: Language
author_profile: true
sidebar_main: true
---

{% raw %}{% comment %}
<!--이 페이지는 "Database" 카테고리에 속하는 모든 글들을 찾아서 보여줍니다.-->
{% endcomment %}
{% assign posts = site.categories.Language %}
{% for post in posts %}
{% include archive-single.html type=page.entries_layout %}
{% endfor %}{% endraw %}