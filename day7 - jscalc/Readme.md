Challenge: jscalc (HTB)<br>
Category: Web<br>
Difficulty: Easy<br>
Vulnerability: Remote Code Execution (Unsafe eval in Node.js)
<br>
<h1>Description</h1>

The /api/calculate endpoint simply takes your input, passes it to JavaScript’s eval, and returns whatever you produce. 
A single POST to /api/calculate with a formula that calls require('fs').readFileSync('../flag.txt','utf-8') will make the server echo the flag’s contents in its response.<br>

<ul>
    <li>Take the target IP from argv[1] and set the calculation endpoint URL: <b>http://{IP}/api/calculate</b>.</li>
    <li>Prepare a JSON body with formula set to require('fs').readFileSync('../flag.txt','utf-8').</li>
    <li>Send a POST request with header <b>Content-Type: application/json</b> containing that payload.</li>
    <li>Receive the raw flag text in the response and extract it with a regex like HTB\{.*?\}.</li>
    <li>Print the matched flag.</li>
</ul>
