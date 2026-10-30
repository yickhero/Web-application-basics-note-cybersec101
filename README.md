# Web-application-basics-note-cybersec101
Here are my notes after finishing tryhackme web application basics
Web application basics
Front-end:
HTML is a foundation aspect of web applications. It is a set of instructions or code that instructs a web browser on what to display and how to display it
CSS in web applications describes a standard appearance, such as certain colours, types of text and layout
JS is part of a web application front end that enables more complex activity in the web browser
Back-end:
Database - used to store data in a structured way
Infrastructures components such as web servers, application servers, storage, various networking devices
WAF (web application firewall) is an optional component for web applications. It helps filter out dangerous requests away from the web server
URL:
A URL (uniform resource loader) is a web address that lets you access all kinds of online content-whether it’s a webpage, a video or other media
HTTP Messages
HTTP Requests: sent by the user to trigger actions on the web application
HTTP Responses: sent by the server in response to the user;s request
Each message contains: Start Line, Headers, Empty Line, body
HTTP request 
The request line (or start line) has three parts: HTTP method, URL path, and the HTTP version
HTTP methods are: GET, POST, PUT (REPLACE), DELETE, PATCH (UPDATE), HEAD (getting header), OPTIONS (tells you what methods are available for a specific resource), TRACE (similar to options but for debugging), CONNECT
Attackers often try to manipulate the URL path so its crucial to validate the URL path to prevent unauthorised access, sanitise the path to avoid injection attacks and protect sensitive data by conducting privacy and risk assessments
Request headers allow extra information to be conveyed to the web server about the request 
HTTP requests such as POST and PUT has difference formats such as URL Encoded (where data is structured in pairs of key and value where key=value and multiple key pairs are separated by an &

Another example is form data which allows multiple data blocks to be sent where each block is separated by a boundary string

Other examples are json and xml
HTTP response: status line and status codes:
When you interact with a web application the server sends back an HTTP response to let you know whether your request was successful
Status line gives you three pieces of info:
1. HTTP version
2. Status code
3. Reason phrase
Status code categories:
Informational Responses (100-199)
 These codes mean the server has received part of the request and is waiting for the rest. It’s a "keep going" signal.
Successful Responses (200-299)
 These codes mean everything worked as expected. The server processed the request and sent back the requested data.
Redirection Messages (300-399)
 These codes tell you that the resource you requested has moved to a different location, usually providing the new URL.
Client Error Responses (400-499)
 These codes indicate a problem with the request. Maybe the URL is wrong, or you’re missing some required info, like authentication.
Server Error Responses (500-599)
 These codes mean the server encountered an error while trying to fulfil the request. These are usually server-side issues and not the client’s fault.
Common status codes:
100 (Continue) The server got the first part of the request and is ready for the rest.
200 (OK) The request was successful, and the server is sending back the requested resource.
301 (Moved Permanently) The resource you’re requesting has been permanently moved to a new URL. Use the new URL from now on.
404 (Not Found) The server couldn’t find the resource at the given URL. Double-check that you’ve got the right address.
500 (Internal Server Error) Something went wrong on the server’s end, and it couldn’t process your request.
HTTP response: Headers and Body:
Http response examples
Other common response headers are 
1. set cookie: Set-Cookie: sessionId=38af1337es7a8  (sends cookies from the server to the client, which the client then sends back with future requests
2. Cache-control: Cache-Control: max-age=600  (tells the client how long it can cache the response before checking with the server again
3. Location: Location: /index.html  (used for redirection, tells the client where to go next if the resource has moved)
Security Headers
Examples of security headers are:
1. CSP header is an additional security layer that can help mitigate against common attacks like Cross-Site Scripting (XSS), A CSP provides a way for administrators to say what domains or sources are considered safe 

2. HSTS (Strict-transport-security) header ensures that web browsers will always connect over HTTPS 

3. The X-Content-Type-Options header can be used to instruct browsers not to guess the MIME type of a resource but only use the Content-Type header 

4. Referrer-policy header controls the amount of information sent to the destination web server when a user is redirected from the source web server, such as when they click a hyperlink. The header is available to allow a web administrator to control what information is shared 

JavaScript Essentials:
Three ways to declare a variables are: var, let and const (While var is function-scoped, both let, and const are block-scoped, offering better control over variable visibility within specific code blocks
You can use JavaScript externally: <script src=”script.js”></scipt> 
You can use JavaScript internally: <script> let x =5; lety=10; let result =x+y; </script>
The alert function displays a message in a dialogue box with an “OK” button

The prompt function displays a dialogue box that asks the user for input. It returns the entered value when the user clicks “OK” or null if the user clicks cancel e.g:
 name = prompt("What is your name?");
alert("Hello " + name);

The confirm function displays a dialogue box with a message and two buttons: “OK” and “Cancel”

Minification in JS is the process of compressing JS files by removing all unnecessary characters, such as spaces, line breaks, comments
Obfuscation is often used to make JS harder to understand by adding undesired code
JS best practise includes:
1. Avoid relying on client-side validation only
2. Refrain from adding untrusted libraries
3. Avoid hardcoded secrets
SQL fundamentals
Relational database: table-based
Non-relational databases: key-value, graph, wide column, document. Examples:
 {
    _id: ObjectId("4556712cd2b2397ce1b47661"),
    name: { first: "Thomas", last: "Anderson" },
    date_of_birth: new Date('Sep 2, 1964'),
    occupation: [ "The One"],
    steps_taken : NumberLong(4738947387743977493)
}
Primary key is used to ensure that the data collected in a certain column is unique
Foreign keys is a column in a table that also exists in another table within the database
SQL:
To create a database: CREATE DATABASE <database_name>;
To view database: SHOW DATABASES;
To use database: USE <database_name>;
To drop database: DROP database <database_name>
To create table example:
mysql> 
CREATE TABLE book_inventory (
book_id INT AUTO_INCREMENT PRIMARY KEY,
book_name VARCHAR(255) NOT NULL,
publication_date DATE
);
To show tables: SHOW TABLES;
To know what columns are contained within a table, we can describe them: DESCRIBE <table_name>

To change dataset: ALTER TABLE <table_name>
				ADD page_count INT
To drop table: DROP TABLE <table_name>;
To create new records in a table: INSERT INTO books (id, name, published_data, description
VALUES (1, "Android Security Internals", "2014-10-14", "An In-Depth Guide to Android's Security Architecture");
To read or retrieve information from a table: SELECT * FROM books;
Or another example: SELECT name, description FROM books
To modifies an existing record within a table: UPDATE books
SET description = “something new”
WHERE id =1;
To remove records from a table: DELETE FROM books WHERE id = 1;
Clause is a part of a statement that specifies the criteria of the data being manipulated e.g. DISTINCT, GROUP BY, ORDER BY and HAVING
DISTINCT is used to avoid duplicate records when doing a query, returning only unique values
GROUP BY clause aggregates data from multiple records and groups the query results in columns e.g.: SELECT name, COUNT*
FROM books
GROUP BY name DESC;
HAVING clause is used with other clauses to filter groups or results of records based on a condition e.g.:
SELECT name, COUNT *
FROM books
GROUP BY name
HAVING name LIKE ‘%Hack%’;
LIKE operator is commonly used in conjunction with clauses like WHERE in order to filter for specific patterns within a column e.g.:
SELECT *
FROM books
WHERE description LIKE “%guide%”;
The between operator allows us to set test if a value exists within a defined range e.g.:
WHERE id BETWEEN 2 AND 4;
CONCAT() function is used to add two or more strings together:
SELECT CONCAT(name, “ is a type of “, category, “ book.”) AS book_info FROM books;
GROUP_CONCAT() function can help us to concatenate data from multiple rows into one field e.g.
SELECT category, GROUP_CONCAT(name SEPARATOR ", ") AS books
    FROM books
    GROUP BY category;
SUBSTRING() function will retrieve a substring from a string within a query, starting at a determined position e.g.
SELECT SUBSTRING(published_date, 1, 4) AS published_year FROM books;
LENGTH() function returns the number of characters in a string e.g.:
SELECT SUBSTRING(published_date, 1, 4) AS published_year FROM books;
COUNT() function returns the number of records within an expression:
SELECT SUBSTRING(published_date, 1, 4) AS published_year FROM books;
SUM(), MAX(), MIN() functions are exactly as it describes
Burp Suite: The Basics
Burp Suite key features:
Proxy: The Burp Proxy is the most renowned aspect of Burp Suite. It enables interception and modification of requests and responses while interacting with web applications.
Repeater: Another well-known feature. Repeater allows for capturing, modifying, and resending the same request multiple times. This functionality is particularly useful when crafting payloads through trial and error (e.g., in SQLi - Structured Query Language Injection) or testing the
functionality of an endpoint for vulnerabilities.
Intruder: Despite rate limitations in Burp Suite Community, Intruder allows for spraying endpoints with requests. It is commonly utilized for brute-force attacks or fuzzing endpoints.
Decoder: Decoder offers a valuable service for data transformation. It can decode captured information or encode payloads before sending them to the target. While alternative services exist
for this purpose, leveraging Decoder within Burp Suite can be highly efficient.
Comparer: As the name suggests, Comparer enables the comparison of two pieces of data at either the word or byte level. While not exclusive to Burp Suite, the ability to send potentially large data segments directly to a comparison tool with a single keyboard shortcut significantly accelerates the process.
Sequencer: Sequencer is typically employed when assessing the randomness of tokens, such as session cookie values or other supposedly randomly generated data. If the algorithm used for generating these values lacks secure randomness, it can expose avenues for devastating attacks.
Burp suite dashboard layout:
Tasks: The Tasks menu allows you to define background tasks that Burp Suite will perform while you use the application. In Burp Suite Community, the default “Live Passive Crawl” task, which automatically logs the pages visited, is sufficient for our purposes in this module. Burp Suite Professional offers additional features like on-demand scans.
Event log: The Event log provides information about the actions performed by Burp Suite, such as starting the proxy, as well as details about connections made through Burp.
Issue Activity: This section is specific to Burp Suite Professional. It displays the vulnerabilities identified by the automated scanner, ranked by severity and filterable based on the certainty of the vulnerability.
Advisory: The Advisory section provides more detailed information about the identified vulnerabilities, including references and suggested remediations. This information can be exported into a report. In Burp Suite Community, this section may not show any vulnerabilities.
Short cuts:
Ctrl + shift + D → Dashboard
Ctrl + Shift + T → Target tab
Ctrl + Shift + P → Proxy tab
Ctrl + shift + I → Intruder tab
Ctrl + Shift + R → Repeater tab
Two types of settings:
Global Settings: These settings affect the entire Burp Suite installation and are applied every time you start the application. They provide a baseline configuration for your Burp Suite environment.
Project Settings: These settings are specific to the current project and apply only during the session. However, please note that Burp Suite Community Edition does not support saving projects, so any project-specific options will be lost when you close Burp.
Key points in burp proxy:
Intercepting Requests: When requests are made through the Burp Proxy, they are intercepted and held back from reaching the target server. The requests appear in the Proxy tab, allowing for further actions such as forwarding, dropping, editing, or sending them to other Burp modules. To disable the intercept and allow requests to pass through the proxy without interruption, click the Intercept is on button. 
Taking Control: The ability to intercept requests empowers testers to gain complete control over web traffic, making it invaluable for testing web applications.
Capture and Logging: Burp Suite captures and logs requests made through the proxy by default, even when the interception is turned off. This logging functionality can be helpful for later analysis and review of prior requests.
WebSocket Support: Burp Suite also captures and logs WebSocket communication, providing additional assistance when analysing web applications.
Logs and History: The captured requests can be viewed in the HTTP history and WebSockets history sub-tabs, allowing for retrospective analysis and sending the requests to other Burp modules as needed.
Features in the proxy settings:
Response Interception: By default, the proxy does not intercept server responses unless explicitly requested on a per-request basis. The "Intercept responses based on the following rules" checkbox, along with the defined rules, allows for a more flexible response interception. 
Match and Replace: The "Match and Replace" section in the Proxy settings enables the use of regular expressions (regex) to modify incoming and outgoing requests. This feature allows for dynamic changes, such as modifying the user agent or manipulating cookies. 
The target tab in burp suite consists:
Site map: This sub-tab allows us to map out the web applications we are targeting in a tree structure. 
Issue definitions: Although Burp Community does not include the full vulnerability scanning functionality available in Burp Suite Professional, we still have access to a list of all the vulnerabilities that the scanner looks for 
Scope settings: This setting allows us to control the target scope in Burp Suite. It enables us to include or exclude specific domains/IPs to define the scope of our testing. By managing the scope, we can focus on the web applications we are specifically targeting and avoid capturing unnecessary traffic. 
