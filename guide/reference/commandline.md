<h2 id="commandline">Configuration Variables</h2>

Running `neomutt` with no arguments will make NeoMutt attempt to
read your spool mailbox. However, it is possible to read other mailboxes and to
send messages from the command line as well.

<table summary="Command line options">
	<caption>Command line options</caption>
	<colgroup><col><col></colgroup>
	<thead><tr>
		<th>Option</th>
		<th>Description</th>
	</tr></thead>
	<tbody>
		{% for option in site.data..reference.commandline %}
			<tr>
				<td>{{ option.opt }} {% if option.arg %}<code>{{ option.arg }}</code>{% endif %}
				</td>
				<td>{{ option.desc}}</td>
			</tr>
		{% endfor %}
	</tbody>
</table>

<dl>
<dt>To read messages in a mailbox or exit immediately</dt>
<dd><code>neomutt[ -nz] [ -F config ] [ -m type ] [ -f mailbox ]</code></dd>

<dt>To compose a new message</dt>
<dd><code>neomutt[ -Enx] [ -F config ] [ -b address ] [ -c address ] [ -H draft ] [ -i include ] [ -s subject ] [ -a file [...] --] { address | mailto_url ...}</code></dd>
</dl>

NeoMutt also supports a "batch" mode to send prepared messages. Simply
redirect input from the file you wish to send. For example,
```
neomutt -s "data set for run #2" professor@bigschool.edu &lt; ~/run2.dat
```
will send a message to `professor@bigschool.edu` with a subject of ''data
set for run #2''. In the body of the message will be the contents of the
file ''~/run2.dat''.


An include file passed with `-i` will be used as the body of the message. When
combined with `-E`, the include file will be directly edited during message
composition. The file will be modified regardless of whether the message is
sent or aborted.

A draft file passed with `-H`  will be used as the initial header and body for
the message. Multipart messages can be used as a draft file. When combined with
`-E`, the draft file will be updated to the final state of the message after
composition, regardless of whether the message is sent, aborted, or even
postponed. Note that if the message is sent encrypted or signed, the draft file
will be saved that way too.

All files passed with `-a <file>` will be attached as a MIME part to the
message. To attach a single or several files, use `--` to separate files and
recipient addresses:
```
neomutt -a image.png -- some@one.org
```
or
```
neomutt -a *.png -- some@one.org
```

Note: The `-a` option must be last in the option list.


In addition to accepting a list of email addresses, NeoMutt also accepts a URL
with the `mailto:` schema as specified in RFC2368. This is useful when
configuring a web browser to launch NeoMutt when clicking on mailto links.
```
neomutt mailto:some@one.org?subject=test&amp;cc=other@one.org
```
