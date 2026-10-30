# Web-application-basics-note-cybersec101
Here are my notes after finishing tryhackme web application basics
# Comprehensive Web Application & Security Notes

## Web Architecture Basics

### Front-End (Client-Side)

* **HTML (HyperText Markup Language):** The foundation of web applications. It provides the structure and instructions on what the web browser should display.
* **CSS (Cascading Style Sheets):** Dictates the appearance, layout, typography, and color schemes of the HTML structure.
* **JavaScript (JS):** Enables complex, dynamic activity and interactivity within the web browser.

### Back-End (Server-Side)

* **Databases:** Used to store, retrieve, and manage data in a structured way.
* **Infrastructure:** Components including web servers, application servers, storage, and networking devices.
* **WAF (Web Application Firewall):** An optional but critical security component that filters dangerous or malicious requests before they reach the web server.

### URLs (Uniform Resource Locators)

A web address used to access online content, whether it is a webpage, video, or API endpoint. Attackers often manipulate URL paths, making it crucial to validate and sanitize paths to prevent unauthorized access and injection attacks.

---

## HTTP Protocol In-Depth

### HTTP Requests

Sent by the client to trigger actions on the server. Every request contains a **Start Line**, **Headers**, an **Empty Line**, and an optional **Body**.

**The Start Line contains:**

1. **HTTP Method:** The action to be performed.
2. **URL Path:** The specific resource being requested.
3. **HTTP Version:** (e.g., HTTP/1.1 or HTTP/2).

**Common HTTP Methods:**

* `GET`: Retrieve data.
* `POST`: Submit new data.
* `PUT`: Replace or create a resource.
* `PATCH`: Update part of a resource.
* `DELETE`: Remove a resource.
* `HEAD`: Retrieve only the response headers (no body).
* `OPTIONS`: Ask the server which methods are permitted for a specific resource.
* `TRACE`: Echoes the received request, primarily for debugging.
* `CONNECT`: Establishes a tunnel to the server.

**Request Body Formats (Common in POST/PUT):**

* **URL Encoded:** Data structured in key-value pairs separated by an ampersand (`key1=value1&key2=value2`).
* **Form Data:** Allows multiple data blocks (like file uploads) separated by a boundary string.
* **JSON / XML:** Standardized data interchange formats.

### HTTP Responses & Status Codes

Sent by the server in response to the client. The **Status Line** includes the HTTP version, a status code, and a reason phrase.

| Range | Category | Description | Common Codes |
| --- | --- | --- | --- |
| **100-199** | Informational | The server received the request; keep going. | `100 Continue` |
| **200-299** | Successful | The request was processed successfully. | `200 OK` |
| **300-399** | Redirection | The resource moved; provides the new URL. | `301 Moved Permanently` |
| **400-499** | Client Error | Problem with the request (bad syntax, unauthorized). | `404 Not Found` |
| **500-599** | Server Error | The server failed to fulfill a valid request. | `500 Internal Server Error` |

### HTTP Headers

Headers convey extra information between the client and server.

**Operational Headers:**

* `Set-Cookie`: Sends cookies from the server to the client for session management (e.g., `Set-Cookie: sessionId=38af1337es7a8`).
* `Cache-Control`: Instructs the client how long to cache the response (e.g., `Cache-Control: max-age=600`).
* `Location`: Used in 3xx responses to tell the client where to redirect.

**Security Headers:**

* **CSP (Content-Security-Policy):** Mitigates Cross-Site Scripting (XSS) by defining which dynamic resources are allowed to load.
* **HSTS (Strict-Transport-Security):** Forces web browsers to always connect via HTTPS.
* **X-Content-Type-Options:** Prevents the browser from MIME-sniffing the response away from the declared content-type.
* **Referrer-Policy:** Controls how much referring routing information is shared when a user clicks a link.

---

## JavaScript Essentials

### Variables and Scope

* `var`: Function-scoped (older standard).
* `let`: Block-scoped (preferred for variables that will change).
* `const`: Block-scoped (preferred for variables that will never change).

### Implementation

**External:** `<script src="script.js"></script>`
**Internal:**

```javascript
<script> 
  let x = 5; 
  let y = 10; 
  let result = x + y; 
</script>

```

### User Interaction Functions

* `alert("Message");` : Displays a dialog box with an "OK" button.
* `prompt("Question");` : Asks for user input. Returns the input string or `null` if cancelled.
* `confirm("Are you sure?");` : Displays a dialog with "OK" (returns true) and "Cancel" (returns false).

### Code Manipulation & Security

* **Minification:** Compressing JS files by removing spaces, line breaks, and comments to improve load times.
* **Obfuscation:** Intentionally scrambling code to make it difficult for humans to read or reverse-engineer.
* **Best Practices:**
1. Never rely purely on client-side validation (always validate on the backend).
2. Do not include untrusted third-party libraries.
3. Never hardcode secrets, API keys, or passwords in JavaScript.



---

## SQL & Database Fundamentals

### Database Types

* **Relational:** Table-based databases organized into rows and columns (e.g., MySQL, PostgreSQL).
* **Non-Relational (NoSQL):** Document, key-value, or graph-based formats. *(Example: MongoDB storing data as JSON/BSON documents).*

### Database Keys

* **Primary Key:** Ensures the data in a specific column is entirely unique for every record.
* **Foreign Key:** A column that links to the primary key of another table, establishing a relationship.

### Core SQL Commands

```sql
-- Database Management
CREATE DATABASE my_db;
SHOW DATABASES;
USE my_db;
DROP DATABASE my_db;

-- Table Management
CREATE TABLE books (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(255) NOT NULL,
  published_date DATE
);
SHOW TABLES;
DESCRIBE books;
ALTER TABLE books ADD page_count INT;
DROP TABLE books;

-- CRUD Operations (Create, Read, Update, Delete)
INSERT INTO books (name, published_date) VALUES ("Android Security", "2014-10-14");
SELECT name, description FROM books;
UPDATE books SET description = "Revised edition" WHERE id = 1;
DELETE FROM books WHERE id = 1;

```

### Clauses and Operators

* `DISTINCT`: Returns only unique values, avoiding duplicates.
* `GROUP BY`: Aggregates data from multiple records into summary rows.
* `HAVING`: Acts like a `WHERE` clause, but specifically for filtering grouped records.
* `LIKE`: Used in a `WHERE` clause to search for a specified pattern (e.g., `WHERE description LIKE "%guide%"`).
* `BETWEEN`: Tests if a value exists within a defined range.

### Essential SQL Functions

* `CONCAT()`: Joins two or more strings together.
* `GROUP_CONCAT()`: Concatenates data from multiple rows into a single field separated by a delimiter.
* `SUBSTRING()`: Extracts a portion of a string based on a starting position.
* `LENGTH()`: Returns the character count of a string.
* `COUNT()`, `SUM()`, `MAX()`, `MIN()`: Standard mathematical aggregation functions.

---

## Burp Suite Fundamentals

### Key Features

* **Proxy:** Intercepts and modifies HTTP/S requests and responses between the browser and the target application.
* **Repeater:** Captures a single request and allows you to manually modify and resend it multiple times (ideal for testing SQLi or endpoint logic).
* **Intruder:** Automates the sending of customized requests. Used for fuzzing endpoints, brute-forcing, or parameter spraying.
* **Decoder:** Transforms data quickly (URL encoding, Base64, Hex) before sending it to a target.
* **Comparer:** Performs a word or byte-level comparison of two pieces of data (useful for spotting subtle differences in HTTP responses).
* **Sequencer:** Analyzes the randomness and entropy of session tokens and cookies.

### Interface & Navigation

**Keyboard Shortcuts:**

| Shortcut | Destination Tab |
| --- | --- |
| `Ctrl + Shift + D` | Dashboard |
| `Ctrl + Shift + T` | Target |
| `Ctrl + Shift + P` | Proxy |
| `Ctrl + Shift + I` | Intruder |
| `Ctrl + Shift + R` | Repeater |

**Dashboard Layout:**

* **Tasks:** Define background jobs (e.g., Live Passive Crawl).
* **Event Log:** System logs detailing proxy starts, connections, and tool activities.
* **Issue Activity / Advisory:** (Professional Edition) Displays automated vulnerability scanner findings, severity rankings, and remediation advice.

### Proxy Configuration

* **Intercepting Requests:** Pauses traffic before it reaches the server. Allows testers to gain complete control over web traffic manipulation.
* **Capture and Logging:** Burp logs all proxy traffic in the HTTP and WebSocket history tabs, even if interception is toggled off.
* **Response Interception:** By default, responses are not intercepted. This must be explicitly enabled in the settings via rules.
* **Match and Replace:** Uses Regular Expressions (regex) to automatically modify incoming and outgoing traffic (e.g., spoofing User-Agents or swapping cookies on the fly).

### Target Tab

* **Site Map:** Maps out the hierarchical tree structure of the targeted web application as you browse it.
* **Issue Definitions:** A reference library of all vulnerabilities the Burp scanner is capable of detecting.
* **Scope Settings:** Crucial for limiting your testing boundaries. By explicitly including or excluding domains/IPs, you prevent Burp from capturing unnecessary background internet traffic and ensure you only test authorized targets.