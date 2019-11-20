---
layout: home
limit: 10
show_excerpts: true
entries_layout: list
---

{% if post.excerpt != post.content %}
    <a href="{{ site.baseurl }}{{ post.url }}">Read more</a>
{% endif %}
