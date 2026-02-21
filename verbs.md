---
layout: default
title: Modern Greek Verbs
---

# Modern Greek Verbs

<table>
  <thead>
    <tr>
      <th>Present</th>
      <th>Voice</th>
      <th>Aorist</th>
      <th>Simple Future</th>
      <th>Imperfect</th>
      <th colspan="2">Imperative</th>
      <th>Meaning</th>
    </tr>
  </thead>
  <tbody>
{% assign sorted_verbs = site.data.verbs | sort: "sort_key" %}

{% for verb in sorted_verbs %}
  {% for voice in verb.voices %}
    {% assign v = voice[1] %}
    <tr>
      <td>{{ v.present | default: "" }}</td>
      <td class="{{ voice[0] }}">{{ voice[0] }}</td>
      <td>{{ v.aorist | default: "" }}</td>
      <td>{{ v.aorist_subjunctive | default: "" | prepend: "θα " }}</td>
      <td>{{ v.imperfect | default: "" }}</td>
      <td>{{ v.imperative.singular | default: "" }}</td>
      <td>{{ v.imperative.plural | default: "" }}</td>
      <td>{{ verb.meaning }}</td>
    </tr>
  {% endfor %}
{% endfor %}
  </tbody>
</table>
