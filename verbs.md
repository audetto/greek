---
layout: default
title: Νεοελληνικά ρήματα
---

# {{ site.data.verbs | size }} νεοελληνικά ρήματα

<input type="text" id="searchInput" onkeyup="filterTable()" placeholder="Αναζήτηση..." style="width: 100%; padding: 12px; margin-bottom: 12px; border: 1px solid #ddd; border-radius: 4px;">

<table id="verbsTable">
  <thead>
    <tr style="cursor: pointer;">
      <th onclick="sortTable(0)">Ενεστώτας <span class="no-print">&#x21C5;</span></th>
      <th onclick="sortTable(1)">Φωνή <span class="no-print">&#x21C5;</span></th>
      <th onclick="sortTable(2)">Αόριστος <span class="no-print">&#x21C5;</span></th>
      <th onclick="sortTable(3)">Μέλλοντας <span class="no-print">&#x21C5;</span></th>
      <th onclick="sortTable(4)">Παρατατικός <span class="no-print">&#x21C5;</span></th>
      <th onclick="sortTable(5)">Προστ. (Εν.) <span class="no-print">&#x21C5;</span></th>
      <th onclick="sortTable(6)">Προστ. (Πληθ.) <span class="no-print">&#x21C5;</span></th>
      <th onclick="sortTable(7)">Σημασία <span class="no-print">&#x21C5;</span></th>
      <th onclick="sortTable(8)">Κατηγορία <span class="no-print">&#x21C5;</span></th>
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
      <td>{{ verb.category | default: "" }}</td>
    </tr>
  {% endfor %}
{% endfor %}
  </tbody>
</table>

<script>
function normalizeGreek(text) {
  // Decompose characters (separate letter from accent) and remove the accent mark
  return text.normalize('NFD').replace(/[\u0300-\u036f]/g, "").toUpperCase();
}

function filterTable() {
  var input, filter, table, tr, td, i, txtValue;
  input = document.getElementById("searchInput");
  filter = normalizeGreek(input.value);
  table = document.getElementById("verbsTable");
  tr = table.getElementsByTagName("tr");
  for (i = 1; i < tr.length; i++) {
    // Search all cells in the row
    if (normalizeGreek(tr[i].textContent).indexOf(filter) > -1) {
      tr[i].style.display = "";
    } else {
      tr[i].style.display = "none";
    }
  }
}

function sortTable(n) {
  var table, rows, switching, i, x, y, shouldSwitch, dir, switchcount = 0;
  table = document.getElementById("verbsTable");
  switching = true;
  dir = "asc";
  while (switching) {
    switching = false;
    rows = table.rows;
    for (i = 1; i < (rows.length - 1); i++) {
      shouldSwitch = false;
      x = rows[i].getElementsByTagName("TD")[n];
      y = rows[i + 1].getElementsByTagName("TD")[n];
      
      // Use Greek locale comparison for correct accent sorting
      var cmp = x.textContent.localeCompare(y.textContent, 'el');

      if (dir == "asc") {
        if (cmp > 0) { shouldSwitch = true; break; }
      } else if (dir == "desc") {
        if (cmp < 0) { shouldSwitch = true; break; }
      }
    }
    if (shouldSwitch) {
      rows[i].parentNode.insertBefore(rows[i + 1], rows[i]);
      switching = true;
      switchcount ++;
    } else {
      if (switchcount == 0 && dir == "asc") { dir = "desc"; switching = true; }
    }
  }
}
</script>
