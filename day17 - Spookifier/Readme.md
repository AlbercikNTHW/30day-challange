Challenge: Spookifier (HTB)<br>
Category: Web <br>
Difficulty: easy <br>
Vulnerability: Server-Side Template Injection in Jinja2 <br>
<h1>Description</h1> The “description” field is injected directly into a Jinja2 template that’s rendered without any sanitization. By breaking out of the template context with a crafted Jinja2 expression, you can execute arbitrary Python code on the server.

<ul> <li>Send a POST with Content-Type: application/json and a JSON body containing “description”.</li> <li>The server calls render_template_string on your “description”, evaluating your payload.</li> <li>Use SSTI to run OS commands, e.g. copy /flag.txt into a web-accessible folder.</li> <li>Retrieve the flag by requesting http://{HOST}/static/uploads/flag.txt</li> </ul>
