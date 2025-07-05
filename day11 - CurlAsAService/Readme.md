Challenge: CurlAsAService (HTB) <br> 
Category: Web <br>
Difficulty: Easy <br>
Vulnerability: SSRF <br>

<h1>Description</h1>
The /api/curl endpoint naively interpolates whatever you send under the ip field into a curl
command and executes it via shell_exec(). By abusing curl’s -T (upload) flag together with -vv and --trace-ascii -, you
can force a PUT of the local /flag file back over HTTP into the response stream and dump it straight to your console. No
exfil server needed—curl will show you the flag in the request body and trace output.

<ul>
    <li>Send a POST with Content-Type: application/x-www-form-urlencoded</li>
    <li>The server runs:
        <pre>curl --proto =http,https -sSL 127.0.0.1 -T /flag -vv --trace-ascii - 2>&1</pre> and prints the entire
        transaction (including /flag contents) in its HTTP response.
    </li>
    <li>Use <code>re.search(r"HTB\{.*?\}", response.text)</code> to extract the flag.</li>
</ul>
