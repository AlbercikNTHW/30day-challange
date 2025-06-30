Challenge: Passman (HTB)<br>
Category: Web<br>
Difficulty: Easy<br>
Vulnerability: Broken Access Control (GraphQL Vulnerability)
<br>
<h1>Description</h1> 

GraphQL API exposes mutations and queries without any permission checks. By chaining
self-registration, a user login, an unauthorized password reset for the admin account, and a second login, an attacker
can obtain a valid admin JWT and finally call a query to dump flag. <br>
<ul>
<li>Take the target IP from argv[1] and set the GraphQL endpoint URL: <b>http://{IP}/graphql</b>.</li>
<li>Register a new user “albercik” via the RegisterUser mutation.</li>
<li>Login as “albercik” with the LoginUser mutation.</li>
<li>Abuse the insecure UpdatePassword mutation to reset admin’s password.</li>
<li>Login as admin (now password “albercik”) via the same >LoginUser mutation and grab the new admin JWT with the same regex.</li>
<li>After login you got the flag.</li>
