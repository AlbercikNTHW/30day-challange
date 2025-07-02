Challenge: Neonify (HTB)<br>
Category: Web<br>
Difficulty: Easy<br>
Vulnerability: Server-Side Template Injection
(New Line bypass)<br>

<h1>Description</h1>

The neon parameter is validated against a strict regex (/^[A-Za-z]+$/) that rejects any non-letter characters—so
payloads containing <, %,=, etc., are normally blocked. However, the validator only inspects the substring after the
    last newline in your input, ignoring everything before it. We can exploit this by placing our ERB injection on the
    first line and a single harmless letter after a \n. The filter sees only that letter, lets the input through, and
    the ERB renderer then processes the entire payload—executing our first-line code.
    
  <ul>
    <li>Build the target URL from <code>argv[1]</code>: <b>http://{HOST}/</b>.</li>
    <li>Craft the payload so the first line is your ERB injection and the second line is a letter:
        <code><%= File.open("flag.txt").read %>\nA</code>.</li>
    <li>URL-encode it for form submission: <code>%3C%25%3D+File.open("flag.txt").read+%25%3E%0AA</code>, then assign to
        the <code>neon</code> field.</li>
    <li>Send a POST request with header <b>Content-Type: application/x-www-form-urlencoded</b> containing that payload.
    </li>
    <li>The regex filter only checks “A” (letters only), passes the request, and the ERB engine executes your injection
        on line one—reading flag.txt.</li>
    <li>Extract the flag from the response using a regex like HTB\{.*?\} and print it.</li>
    </ul>
