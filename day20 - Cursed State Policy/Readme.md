Challenge: Cursed State Policy (HTB) <br>
Category: Web <br>
Difficulty: Easy <br>
Vulnerability: Content Security Policy Bypass 

<h1>Description</h1> <br> 
The challenge presents a web application that enforces a strict Content Security Policy (CSP)
with a per-request nonce on its script-src directive, and exposes a WebSocket endpoint at /ws. To steal the user’s
session cookie and retrieve the flag, an attacker must bypass the CSP by injecting a
<script> tag carrying the valid nonce via the WebSocket channel.

<ul>
    <li>Launches a WebSocket client connection to <code>ws://&lt;target&gt;/ws</code> using <code>wscat</code>,
        capturing its stdin/stdout.</li>
    <li>Sends an HTTP GET to <code>http://&lt;target&gt;/</code> to fetch response headers.</li>
    <li>Uses a regex on the <code>Content-Security-Policy</code> header to extract the nonce value in the form
        <code>nonce-<em>[0–9a-f]+</em></code>.</li>
    <li>Builds a JSON message of the form
        <code>{"type":"trigger_xss","payload":"&lt;script nonce=\"{nonce}\"&gt;fetch('/callback',{method:'POST',headers:{'Content-Type':'application/json'},body:JSON.stringify({cookies:document.cookie})});&lt;/script&gt;"}</code>.
    </li>
    <li>Writes this JSON payload into the WebSocket stdin, triggering the server to reflect and execute the injected
        script in a browser context under the correct nonce.</li>
    <li>Listens on the WebSocket stdout for any output matching the HTB flag format <code>HTB\{[^}]+\}</code>, then
        prints the flag and exits.</li>
</ul>
