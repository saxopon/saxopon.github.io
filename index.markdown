---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
---


Filter searches by text: <input type="text" id="search" placeholder="Filter by name, title, or date..." autofocus>
<p id="record-count"></p>

<table id="results">
    <thead>
        <tr>
            <th>Date</th>
            <th>Class</th>
            <th>Search Name</th>
        </tr>
    </thead>
    <tbody>
        {% for s in site.data.searches.searches %}
        <tr>
            <td>{{ s.date }}</td>
            <td>{{ s.video_title }}</td>
            <td><a href="{{ s.link }}" target="_blank">{{ s.search_name }}</a></td>
        </tr>
        {% endfor %}
    </tbody>
</table>

<script>
    const input= document.getElementById("search");
    const rows = document.querySelectorAll("#results tbody tr");
    const countEl = document.getElementById("record-count");

    function updateCount() {
        const visible = document.querySelectorAll('#results tbody tr:not([style*="display: none"])');
        countEl.textContent = visible.length + " of " + rows.length + " records";
    }

    input.addEventListener("input", function () {
        const q = this.value.toLowerCase();
        rows.forEach(row => {
            row.style.display = row.textContent.toLowerCase().includes(q) ? "" : "none";
        });
        updateCount();
    });

    updateCount();
</script>