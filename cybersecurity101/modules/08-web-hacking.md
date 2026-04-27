# Web Hacking

This module covers essential concepts for web application security testing, including web basics, JavaScript, SQL fundamentals, and Burp Suite usage.

## Web Application Basics

Web applications are software programs that run on web servers and are accessed through web browsers. They are composed of three main components:

### Client-Side
- HTML (HyperText Markup Language): The structure and content of web pages
- CSS (Cascading Style Sheets): The presentation and styling
- JavaScript: The interactive behavior and dynamic content

### Server-Side
- Backend logic and processing
- Database interactions
- Authentication and authorization
- API endpoints

### HTTP Protocols
- **GET**: Retrieve data from a server
- **POST**: Submit data to be processed
- **PUT**: Update existing data
- **DELETE**: Remove data

## JavaScript Essentials

JavaScript is the primary language used for client-side web development and plays a crucial role in web security testing.

### Key Concepts
- DOM Manipulation: Accessing and modifying the Document Object Model
- Event Handling: Responding to user interactions
- AJAX/Fetch: Asynchronous requests to server endpoints
- Cookies: Client-side data storage
- LocalStorage: Persistent client-side storage

### Security Implications
- XSS (Cross-Site Scripting): Injecting malicious scripts into web pages
- CSRF (Cross-Site Request Forgery): Forcing users to perform actions they didn't intend
- Client-side validation bypasses
- Information leakage through console logs and debug features

## SQL Fundamentals

SQL (Structured Query Language) is used to communicate with and manipulate databases.

### Common SQL Operations
- **SELECT**: Retrieve data from a database
- **INSERT**: Add new records
- **UPDATE**: Modify existing records
- **DELETE**: Remove records

### SQL Injection Basics
SQL injection occurs when untrusted user input is used to construct dynamic SQL queries. This can allow attackers to:

1. **Read Data**: Access sensitive information
2. **Modify Data**: Change, insert, or delete data
3. **Bypass Authentication**: Bypass login checks
4. **Perform Administrative Actions**: Execute admin-level operations

### Types of SQL Injection
- **In-band**: Same channel used to inject data and extract it (e.g., UNION-based)
- **Error-based**: Information extracted through database errors
- **Out-of-band**: Using different channels (DNS, email, second request) to extract data
- **Blind**: Information extracted through boolean responses or timing delays

## Burp Suite Basics

Burp Suite is a powerful web application security testing tool that provides interception, manipulation, and analysis capabilities.

### Interface Overview

The Burp Dashboard is divided into four quadrants:

1. **Tasks**: Background tasks like "Live Passive Crawl"
2. **Event Log**: Records actions and connection details
3. **Issue Activity**: Vulnerability scanner results (Professional only)
4. **Advisory**: Detailed vulnerability information and remediations (Professional only)

### Navigation

- **Module Selection**: Top menu bar switches between modules
- **Sub-Tabs**: Second menu bar provides module-specific settings
- **Keyboard Shortcuts**:
  - `Ctrl + Shift + D`: Dashboard
  - `Ctrl + Shift + T`: Target tab
  - `Ctrl + Shift + P`: Proxy tab
  - `Ctrl + Shift + I`: Intruder tab
  - `Ctrl + Shift + R`: Repeater tab

### Proxy Configuration

The Burp Proxy intercepts and logs requests between the client and server:

**Key Features:**
- Intercept and modify requests before they reach the server
- Capture and log all traffic (even when intercept is off)
- WebSocket support for real-time communication
- Response interception (configurable via rules)

**Settings:**
- Match and Replace: Use regex to modify requests/responses
- Response Interception: Control when server responses are intercepted

### Target Tab

The Target tab provides three sub-tabs:

1. **Site Map**: Tree structure of visited pages and API endpoints
2. **Issue Definitions**: Comprehensive list of web vulnerabilities for reference
3. **Scope Settings**: Control which domains/IPs are included in testing

### Burp Browser

Built-in Chromium browser pre-configured with the proxy:

**Installation Requirements:**
- Available in Community Edition
- Click "Open Browser" in the Proxy tab
- Linux root users may need sandbox configuration

### Scoping

Scoping limits proxy interception to specific targets:

**How to Set Scope:**
1. Switch to Target tab
2. Right-click target from the left list
3. Select "Add To Scope"
4. Choose to stop logging out-of-scope traffic

**Enable Scope-Based Interception:**
- Go to Proxy settings
- Select "URL Is in target scope" in "Intercept Client Requests" section

### Certificate Installation

To bypass certificate warnings when using HTTPS sites:

1. Download CA Certificate: Navigate to `http://burp/cert` (downloads `cacert.der`)
2. Import to Firefox: `about:preferences` → "View Certificates" → "Import"
3. Set Trust: Check "Trust this to identify websites" and click OK

### XSS Bypass Example

**Scenario**: Testing a support form at `http://MACHINE_IP/ticket/` for reflected XSS

**Steps:**
1. Activate Burp Proxy with intercept ON
2. Submit form with legitimate data
3. Intercept the request in Burp
4. Change the email field to: `<script>alert("Succ3ssful XSS")</script>`
5. Select and URL encode with `Ctrl + U`
6. Forward the request

**Client-side filters** are common bypass techniques:
- Commenting out code: `<!-- <script> -->
- Using HTML entities: `&lt;script&gt;`
- URL encoding: `%3Cscript%3E`
- Encoding the payload after the opening tag: `<s%63ript>alert(1)</s%63ript>`

### Useful Extensions

**Built-in Modules:**
- Comparer: Compare data at word or byte level
- Sequencer: Test randomness of tokens and generated values

**Extensions:**
- Written in Java, Python, or Ruby
- Loaded via Extender module
- BApp Store for third-party modules
- Logger++ for enhanced logging

## Practice Exercise

Test the support form at `http://MACHINE_IP/ticket/` for:
1. Reflective XSS vulnerabilities
2. Client-side filter bypasses
3. SQL injection in form inputs

Use Burp Proxy to intercept and manipulate requests, and verify your findings through the Burp Dashboard.