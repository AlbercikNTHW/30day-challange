Challenge: BlinkerFluids (HTB)<br>
Category: Web  <br>
Difficulty: Easy <br>
Vulnerability: Blind Code Injection (CVE-2021-23639)  <br>

<h1>Description</h1>

The target uses an outdated version of the `marked` Markdown parser (< v4.0.0) that is vulnerable to CVE-2021-23639. This flaw allows an attacker to inject and execute arbitrary JavaScript on the server during the Markdown-to-HTML conversion phase.  

Under the hood, `marked` let you specify a “lang” hint on fenced code blocks (e.g. ```js) and would invoke that language’s runtime when rendering. By abusing the `js` hint, you can call Node’s `require("child_process").execSync()` to run shell commands. Since the parser runs as part of the invoice-creation API, your payload executes on the server with full privileges.  

The typical exploitation flow is:  
<ul>
  <li>Run a local HTTP server on port 8000 to catch exfiltrated flags.</li>
  <li>Expose that server via ngrok (or any HTTP tunnel) to obtain a public URL.</li>
  <li>Craft a Markdown payload with a JS code fence that executes a `curl` back to your tunnel, embedding the contents of <code>/flag.txt</code>.</li>
  <li>POST the payload to <code>/api/invoice/add</code> in JSON under the <code>markdown_content</code> field.</li>
  <li>The server’s Markdown renderer executes your JS, which sends the flag to your public endpoint.</li>
  <li>Harvest the flag from your local server’s logs or ngrok dashboard.</li>
</ul>
