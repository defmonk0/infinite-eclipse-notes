{% assign sessions = site.pages %}
{% assign sessions = sessions | where_exp: "doc", "doc.url != '/'" %}
{% assign sessions = sessions | where_exp: "doc", "doc.dir != '/assets/css/'" %}

{% assign dirs = "" | split: "XXX" %}

{% for session in sessions %}
{% assign temp = session.dir | split: "XXX" %}
{% assign dirs = dirs | concat: temp %}
{% endfor %}

{% assign uniqdirs = dirs | uniq | sort_natural %}

<section id="file-index">
	<ul>
		{% for dir in uniqdirs offset:1 %}
		<li>
			{% assign temp = sessions | where_exp: "doc", "doc.dir == dir" %}
			{% assign temp = temp | sort_natural: "name" %}
			{% assign title = temp[0].path | split: '/' %}
			{% assign title = title[1] | split: '.' | last | trim %}
			<h3>{{ title }}</h3>
			<ul style="margin-bottom: 1.5rem;">
			{% for session in temp %}
				<li>
					<a href="{{ site.baseurl }}{{ session.url }}">
						{{ session.name | split: ".md" | first }}
					</a>
				</li>
			{% endfor %}
			</ul>
		</li>
		{% endfor %}
		<li>
			<h3>Current Arc</h3>
			<ul style="margin-bottom: 1.5rem;">
			{% assign temp = sessions | where_exp: "doc", "doc.dir == '/sessions/'" %}
				{% for session in temp %}
					<li>
						<a href="{{ site.baseurl }}{{ session.url }}">
							{{ session.name | split: ".md" | first }}
						</a>
					</li>
				{% endfor %}
			</ul>
		</li>
	</ul>
</section>
