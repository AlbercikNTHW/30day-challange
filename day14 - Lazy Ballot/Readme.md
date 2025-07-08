Challenge: Lazy Ballot (HTB) <br> 
Category: Web <br>
Difficulty: easy <br> 
Vulnerability: NoSQL Injection
<br>
<h1>Description</h1>

The exploit abuses a NoSQL injection in the login API to bypass authentication and pull the flag:

<ul>
    <li>Send a POST to http://&lt;host&gt;/api/login with JSON {"username":"admin","password":{"$ne":"asdasd"}}.</li>
    <li>The MongoDB $ne operator matches any password not equal to "asdasd", logging you in as admin.</li>
    <li>Reuse the session cookie from login to GET http://&lt;host&gt;/api/votes/list.</li>
    <li>The votes list response contains the flag in the format HTB{…}.</li>
    <li>Parse the response with a regex like r"HTB\{.*?\}" to extract and display the flag.</li>
</ul>
