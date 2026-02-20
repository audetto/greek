---
layout: default
title: Modern Greek Verbs
---

# Modern Greek Verbs

<link rel="stylesheet" href="/assets/css/style.css">

<table>
  <thead>
    <tr>
      <th>Lemma</th>
      <th>Voice</th>
      <th>Present</th>
      <th>Imperfect</th>
      <th>Aorist</th>
      <th>Future (aorist subjunctive)</th>
      <th>Imperative (singular)</th>
      <th>Imperative (plural)</th>
    </tr>
  </thead>
  <tbody>
{% assign sorted_verbs = site.data.verbs | sort: "sort_key" %}

{% for verb in sorted_verbs %}
  {% for voice in verb.voices %}
    {% assign v = voice[1] %}
    <tr>
      <td>{{ verb.lemma }}</td>
      <td>{{ voice[0] }}</td>
      <td>{{ v.present | default: "" }}</td>
      <td>{{ v.imperfect | default: "" }}</td>
      <td>{{ v.aorist | default: "" }}</td>
      <td>{{ v.aorist_subjunctive | default: "" | prepend: "θα " }}</td>
      <td>{{ v.imperative.singular | default: "" }}</td>
      <td>{{ v.imperative.plural | default: "" }}</td>
    </tr>
  {% endfor %}
{% endfor %}
  </tbody>
</table>
