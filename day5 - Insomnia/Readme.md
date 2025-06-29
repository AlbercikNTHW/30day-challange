Challenge: Insomnia (HTB – Retired)<br>
Category: Web <br>
Difficulty: Easy<br>
Vulnerability: Broken Authentication (JWT bypass) 
<br>
<h1>Description</h1>


A vulnerable CodeIgniter application contains a flawed login check that uses `if (! count($json_data) == 2)` instead of verifying that both username and password are provided. Because this condition always evaluates to false for any non-empty input, the login endpoint never rejects a request missing the password. An attacker can exploit this by submitting only the `"administrator"` username, receiving a valid admin-signed JWT in response, placing it into a cookie, and then calling `/index.php/profile` to read the contents of `flag.txt`.

<ul>
    <li>Take target IP from argv and build URLs for /login and /profile.</li>
    <li>POST to /index.php/login with JSON {"username":"administrator"} to bypass the password check.</li>
    <li>Parse the JSON response with regex "token"\s*:\s*"([^"]+)" to grab the JWT.</li>
    <li>GET /index.php/profile with header Cookie: token=<jwt>.</li>
    <li>Extract HTB{…} from the HTML body and print the flag.</li>
</ul>
