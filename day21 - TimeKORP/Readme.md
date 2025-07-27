Challenge: KORP time <br>
Category: Web <br>
Difficulty: easy <br>
Vulnerability: Command injection (format parameter)
<br>
<h1>Description</h1> The application exposes an endpoint that accepts a “format” query parameter and passes it directly into a shell call to date, without any sanitization. By injecting a shell-breaking sequence into the format string, you can chain arbitrary commands. In this case, sending '; cat /flag || ' causes the server to dump the contents of /flag* into the HTTP response.

<li>The script sends a GET request to: <pre><code>http://&lt;target_ip&gt;/?format='; cat /flag || '</code></pre> </li>

<li>The application invokes <code>date</code> unsafely, allowing <code>cat /flag</code> to execute and embed the flag in the response body.</li>

<li>The script then applies a regex (<code>HTB\{.*?\}</code>) to extract the flag from the response and prints it to stdout.</li> </ul>
