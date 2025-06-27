🎃Challenge: PumpkinSpice (HTB – Retired)
<br>
Category: Web
<br>
Difficulty: Easy 
<br>
Vulnerability: XSS -> SSRF -> RCE

<h1>Description</h1>
<br>
PumpkinSpice is a simple web challenge where you must exploit an XSS vulnerability in the “address” parameter. That flaw leads to an SSRF and, ultimately, a successful RCE on the server.
<br>
The script performs the following steps:
<ul>
<li>Read target: grab the host (IP or domain) from sys.argv[1].</li>
<li>Craft XSS payload: <b>fetch("/api/stats?command=cp%20/flag%20/app/static/albercik.txt")</b></li>
<li>Inject payload: send a POST to /add/address with address=<script>…</script> in the form body</li>
<li>Trigger XSS & SSRF: headless Chrome visits GET /addresses, renders your stored script and executes it, issuing a fetch to /api/stats?command=…</li>
<li>Achieve RCE: the /api/stats handler runs subprocess.check_output(command, shell=True), so cp /flag /app/static/albercik.txt executes on the server</li>
<li>Wait for bot: sleep for 4 seconds to give the bot time to visit /addresses, execute the payload and complete the copy</li>
<li>Grab the flag: send a GET request to /static/albercik.txt to fetch the now-public flag file and print the contents of albercik.txt</li>
</ul>

