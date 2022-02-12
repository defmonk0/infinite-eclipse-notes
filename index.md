{% assign doclist = site.pages | sort: 'url'  %}

<ul>
	{% for doc in doclist %}
		{% if doc.name != '/' %}
			{% if doc.name contains '.md' or doc.name contains '.html' %}
			<li>
				<a href="{{ site.baseurl }}{{ doc.url }}">
					{{ doc.name | split: ".md" | first }}
				</a>
			</li>
			{% endif %}
		{% endif %}
	{% endfor %}
</ul>
