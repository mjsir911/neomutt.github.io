
## Configuration Commands
The following are the commands understood by NeoMutt:

<ul>
	{% for command in site.data.reference.commands %}
	<li>
		<code>{{ command.command }}</code> <code>{{command.arguments}}</code>
	</li>
	{% endfor %}
</ul>
