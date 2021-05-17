---
layout: single
classes: wide
title: Schedule
permalink: /schedule/
author_profile: true
---
{% for schedule in site.schedules limit:1 %}
{% assign start_time = schedule.timeline | first %}
{% capture offset %}{% include minutes.liquid time=start_time %}{% endcapture %}
<h1 id="page-title" class="page__title" itemprop="headline">{{ schedule.semester | markdownify | remove: "<p>" | remove: "</p>" }} {{ schedule.year | markdownify | remove: "<p>" | remove: "</p>" }} ({{ schedule.start }} - {{ schedule.end }})</h1>

<div class="schedule">
  <ul class="schedule-timeline" style="min-width: {{ schedule.schedule | size | times: 130 }}px">
    {% for time in schedule.timeline %}
    <li class="schedule-time">{{ time }} </li>
    {% endfor %}
  </ul>
  <ul class="schedule-group">
    {% for day in schedule.schedule %}
    <li class="schedule-day">
      <h2 class="schedule-header">{{ day.name }}</h2>
      {% if day.events %}
      <ul class="schedule-events" style="height: {{ schedule.timeline | size | times: 40 }}px">
      {% for event in day.events %}
        {% capture start %}{% include minutes.liquid time=event.start %}{% endcapture %}
        {% capture end %}{% include minutes.liquid time=event.end %}{% endcapture %}
        {% assign top = start | minus: offset | times: 40 | divided_by: 30 %}
        {% assign height = end | minus: start | times: 40 | divided_by: 30 %}
        <li class="schedule-event {% if event.class %}{{ event.class }}{% else %}{{ event.name | slugify }}{% endif %}"
            style="top: {{ top }}px; height: {{ height }}px;">
          <div class="name">{{ event.name }}</div>
          <div class="time">{{ event.start }}–{{ event.end }}</div>
          {% if event.location %}
          <div class="location">{{ event.location }}</div>
          {% endif %}
        </li>
      {% endfor %}
      </ul>
      {% endif %}
    </li>
    {% endfor %}
  </ul>
</div>

{% endfor %}
<div class="notice--info"><strong>Note:</strong> Check the <a href="https://sonoma.edu/academics/calendar" target=_blank>academic calendar</a> for important dates.</div>
