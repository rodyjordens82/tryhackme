# 🌐 How the Web Works

This module covers the fundamentals of how the web operates, including HTTP/HTTPS, web servers, browsers, and web application architecture.

## 🎯 Key Topics

- Introduction to the Web
- HTTP and HTTPS Protocols
- Web Servers and Clients
- Web Application Architecture
- Web Security Basics

## 📝 Notes

### Introduction to the Web

**Definition**: The World Wide Web is a system of interlinked hypertext documents accessed via the Internet.

**Key Components**:
- **Clients**: Browsers (Chrome, Firefox, Safari)
- **Servers**: Web servers (Apache, Nginx, IIS)
- **Protocols**: HTTP/HTTPS for communication
- **Resources**: Web pages, images, videos, APIs

**How it Works**:
1. User enters URL in browser
2. Browser requests resource from server
3. Server processes request and sends response
4. Browser renders the response

### HTTP and HTTPS Protocols

**HTTP (HyperText Transfer Protocol)**:
- Stateless protocol for communication
- Uses request/response model
- Runs on port 80

**HTTPS (HTTP Secure)**:
- HTTP with encryption (TLS/SSL)
- Runs on port 443
- Provides security and privacy

**HTTP Methods**:

| Method | Description | Usage |
|--------|-------------|-------|
| **GET** | Retrieve data | Fetch resources |
| **POST** | Send data | Create resources |
| **PUT** | Send data | Update resources |
| **DELETE** | Delete data | Remove resources |
| **PATCH** | Partial update | Modify specific fields |
| **HEAD** | Get headers | Check resource without body |
| **OPTIONS** | Get allowed methods | Check server capabilities |

**HTTP Status Codes**:

| Code | Category | Description |
|-------|----------|-------------|
| 1xx | Informational | Request received, processing continues |
| 2xx | Success | Request successfully processed |
| 3xx | Redirection | Further action needed |
| 4xx | Client Error | Client-side error |
| 5xx | Server Error | Server-side error |

**Common Status Codes**:
- **200 OK**: Request successful
- **201 Created**: Resource created
- **301 Moved Permanently**: Resource moved
- **302 Found**: Temporary redirect
- **304 Not Modified**: Resource not modified
- **400 Bad Request**: Invalid request
- **401 Unauthorized**: Authentication required
- **403 Forbidden**: Access denied
- **404 Not Found**: Resource not found
- **500 Internal Server Error**: Server error
- **502 Bad Gateway**: Invalid response from upstream
- **503 Service Unavailable**: Server unavailable

### Web Servers and Clients

**Web Servers**:
- Software that serves web content
- Common servers: Apache, Nginx, IIS
- Handles HTTP/HTTPS requests
- Serves static and dynamic content

**Clients (Browsers)**:
- Software that requests and displays web content
- Common browsers: Chrome, Firefox, Safari, Edge
- Renders HTML, CSS, JavaScript
- Executes client-side scripts

**Web Server Software**:

| Server | Description | Popularity |
|--------|-------------|------------|
| **Apache** | Open-source, flexible | High |
| **Nginx** | High-performance, reverse proxy | Very High |
| **IIS** | Microsoft's web server | Medium |
| **LiteSpeed** | High-performance alternative | Low |

### Web Application Architecture

**Client-Server Model**:
- Client sends request to server
- Server processes request
- Server sends response to client

**Three-Tier Architecture**:
1. **Presentation Layer**: User interface (HTML, CSS, JavaScript)
2. **Application Layer**: Business logic (server-side code)
3. **Data Layer**: Database (MySQL, PostgreSQL, MongoDB)

**Web Application Components**:
- **Frontend**: HTML, CSS, JavaScript (React, Angular, Vue)
- **Backend**: Server-side code (Node.js, Python, PHP, Ruby)
- **Database**: Data storage (SQL, NoSQL)
- **APIs**: Communication interface (REST, GraphQL)

**RESTful APIs**:
- Representational State Transfer
- Uses HTTP methods (GET, POST, PUT, DELETE)
- Stateless communication
- Resource-based architecture

### Web Security Basics

**Common Web Vulnerabilities**:
- **SQL Injection**: Malicious SQL code in input
- **XSS (Cross-Site Scripting)**: Malicious scripts in web pages
- **CSRF (Cross-Site Request Forgery)**: Unauthorized commands
- **Security Misconfigurations**: Default settings, open ports
- **Sensitive Data Exposure**: Unencrypted data

**Security Best Practices**:
- Use HTTPS for all communications
- Input validation and sanitization
- Proper authentication and authorization
- Secure session management
- Regular security updates and patches
- Security headers (CSP, HSTS)
- Rate limiting and WAF

---

**Reference**: TryHackMe Pre-Security Certification - Module 03
