Challenge: Amidst Us (HTB)<br>
Category: Web  <br>
Difficulty: Easy  <br>
Vulnerability: Remote Code Execution via PIL.ImageMath.eval  
<br>
<h1>Description</h1>
The “background” array values are injected directly into an f-string that’s evaluated by PIL.ImageMath.eval.  
By breaking out of the numeric context in the first element of “background”, you can run arbitrary Python code on the server.

<ul>
  <li>Send a POST with Content-Type: application/json</li>
  <li>The server decodes your image, plugs “background” values into ImageMath.eval, and executes your code, copying the flag to a public folder.</li>
  <li>Retrieve the flag by requesting http://{HOST}/static/uploads/flag.txt</li>
</ul>
