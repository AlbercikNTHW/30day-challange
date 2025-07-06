Challenge: Labyrinth Linguist (HTB) <br>
Category: Web <br>
Difficulty: easy <br>
Vulnerability: SSTI
<br>
<h1>Description</h1>

The application blindly inserts your text parameter into an Apache Velocity template and renders it without
sanitization, exposing a server-side template injection flaw. You can craft a Velocity expression that navigates Java’s
object graph to execute arbitrary commands. Using the SSTImap tool streamlines exploitation and flag retrieval:

<ul>
    <li>Define your target endpoint as http://<host>/?text= and clone the SSTImap repository.
    <li>Change into the SSTImap directory.
    <li>Run SSTImap</li>
    <li>SSTImap auto-generates a Velocity SSTI payload that executes cat /flag* on the server.
    <li>The tool captures and displays the contents of /flag directly from the HTTP response.
</ul>
