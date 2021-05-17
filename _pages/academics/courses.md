---
layout: single
author_profile: false
toc: true
toc_label: "Semesters"
title: "Courses"
permalink: /academics/
syllabi_base: /assets/syllabi/
sidebar:
  nav: "academics"
---
{% for sem in site.courses reversed %}
<div class="notice{% if forloop.first %}--primary{% endif %}">
<h1 id="{{ sem.semester }}-{{ sem.year }}">{{ sem.semester }} {{ sem.year }} ({{ sem.start }}-{{ sem.end }})</h1>
<ul>
{% for course in sem.courses %}
{% if course.syllabus %}<li><a href="{{ page.syllabi_base }}{{ course.syllabus }}">{{ course.code }}</a> {{ course.name }}</li>
{% else %}<li>{{ course.code }} {{ course.name }}</li>
{% endif %}
{% endfor %}
</ul>
</div>
{% endfor %}