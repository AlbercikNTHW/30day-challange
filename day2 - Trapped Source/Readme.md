Challenge: Trapped Source (HTB – Retired) <br> Category: Web <br> Difficulty: Easy <br> Vulnerability: Information Disclosure

<h1>Description</h1>
<br>
The challenge presents a web application that embeds a correctPin value in a JavaScript object within the page source. This PIN must be submitted in a POST request to /flag in order to retrieve the flag.

The script performs the following steps:
<ul>
<li>Sends a GET request to the target's root endpoint to retrieve the HTML content.</li>
<li>Parses the HTML using a regular expression to extract the correctPin value.</li>
<li>Sends a POST request to /flag with the extracted PIN in JSON format.</li>
<li>Parses the response for a flag using a regex that matches the HTB flag format.</li>
<li>The flag is printed to the console.</li>

