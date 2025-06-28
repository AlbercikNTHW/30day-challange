Challenge: Templated (HTB – Retired)<br>
Category: Web <br>
Difficulty: Easy  <br>
Vulnerability: Server-Side Template Injection (SSTI)<br>

<h1>Description</h1>

The challenge presents a Flask/Jinja2 web application that reflects any nonexistent path into a 404 template without sanitization. By injecting Jinja2 expressions into the URL, you can execute arbitrary Python code on the server—ultimately importing the `os` module and reading `flag.txt`.  

The exploitation script performs the following steps:  
<ul>  
  <li>Reads the target’s address from the command line and prepends “http://” if needed.</li>  
  <li>Sends a GET request to <b>http://IP/{{8*8}}</b>b> to confirm SSTI (expects “64”).</li>  
  <li>If “64” appears in the response, prints “[+] Target is vulnerable! (Jinja2 SSTI confirmed)”.</li>  
  <li>Constructs the flag payload:  
    <code>{{self.__init__.__globals__['__builtins__']['__import__']('os').popen('cat flag.txt').read()}}</code>.  
  </li>  
  <li>Sends a second GET request to cat the flag.txt file on the target.</li>  
  <li>Uses a regex `HTB\{.*?\}` to extract the flag from the response body.</li>  
  <li>Prints the flag to the console.</li>  
</ul>
