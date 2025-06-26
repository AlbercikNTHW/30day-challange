<h1>Description</h1>
<br>
The challenge presents a web application that embeds a correctPin value in a JavaScript object within the page source. This PIN must be submitted in a POST request to /flag in order to retrieve the flag.

The script performs the following steps:

1.Sends a GET request to the target's root endpoint to retrieve the HTML content.

2.Parses the HTML using a regular expression to extract the correctPin value.

3.Sends a POST request to /flag with the extracted PIN in JSON format.

4.Parses the response for a flag using a regex that matches the HTB flag format (HTB{...}).

5. The flag is printed to the console.
