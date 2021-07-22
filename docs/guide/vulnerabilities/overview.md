# Vulnerability Guide

This section lists all vulnerabilities (issues) that can be detected by Nexploit and provides detailed information about each of them.

<table id="simple-table">
    <tr>
        <th width="25%"><strong>Test name</strong></th>
        <th width="40%"><strong>Description</strong></th>
        <th width="35%"><strong>Detectable vulnerabilities</strong></th>
    </tr>
        <tr>
        <td><b>Broken JWT Authentication</b></td>
        <td> Tests for secure implementation of JSON Web Token (JWT) in the application</td>
        <td>
            <ul>
                <li><a href="#/guide/vulnerabilities/36-broken-jwt-auth.md">Broken JWT Authentication</a></li>
            </ul>
        </td>
    </tr>
     <tr>
        <td><b>Broken SAML Authentication</b></td>
        <td>Tests for secure implementation of SAML authentication in the application</td>
        <td>
            <ul>
                <li><a href="#/guide/vulnerabilities/214-broken-saml-auth.md">Broken SAML Authentication</a></li>
            </ul>
        </td>
    </tr>
    <tr>
        <td><b>Brute Force Login</b></td>
        <td>Tests for availability of commonly used credentials</td>
        <td>
            <ul>
                <li><a href="#/guide/vulnerabilities/204-brute-force-login.md">Brute Force Login</a></li>
            </ul>
        </td>
    </tr>
    <tr>
        <td><b>Business Constraint Bypass</b></td>
        <td>Tests if the limitation of number of retrievable items via an API call is configured properly</td>
        <td>
            <ul>
                <li><a href="#/guide/vulnerabilities/210-business-constraint-bypass.md">Business Constraint Bypass</a></li>
            </ul>
        </td>
    </tr>
    <tr>
        <td><b>Client-Side XSS</b><br><i>(DOM Cross-Site Scripting)</i></td>
        <td>Tests if various application DOM parameters are vulnerable to JavaScript injections </td>
        <td>
            <ul>
                <li><a href="#/guide/vulnerabilities/2-xss.md">Reflective Cross-site scripting (rXSS)</a></li>
                <li><a href="#/guide/vulnerabilities/1-xss.md">Persistent Cross-site scripting (pXSS)</a></li>
            </ul>
        </td>
    </tr>
    <tr>
        <td><b>Common Files Exposure</b></td>
        <td>Tests if common files that should not be accessible are accessible</td>
        <td>
            <ul>
                <li><a href="#/guide/vulnerabilities/203-exposed-common-file.md">Exposed Common File</a></li>
            </ul>
        </td>
    </tr>
    <tr>
        <td><b>Cookie Security Check</b></td>
        <td>Tests if the application uses and implements cookies with secure attributes</td>
        <td>
            <ul>
                <li><a href="#/guide/vulnerabilities/40-sensitive-cookie.md">Sensitive Cookie in HTTPS Session Without Secure Attribute</a></li>
                <li><a href="#/guide/vulnerabilities/41-sensitive-cookie.md">Sensitive Cookie Without HttpOnly Flag</a></li>
                <li><a href="#/guide/vulnerabilities/225-sensitive-cookie.md">Sensitive Cookie Weak Session ID</li>
            </ul>
        </td>
    </tr>
     <tr>
        <td><b>Cross-Site Request Forgery (CSRF)</b></td>
        <td>Tests application forms for vulnerable cross-site filling and submitting</td>
        <td>
            <ul>
                <li><a href="#/guide/vulnerabilities/11-csrf.md">Unauthorized Cross-Site Request Forgery (CSRF)</a></li>
                <li><a href="#/guide/vulnerabilities/208-csrf.md">Authorized Cross-Site Request Forgery (CSRF)</a></li>
            </ul>
        </td>
        <tr>
        <td><b>Cross-Site Scripting (XSS)</b></td>
        <td>Tests if various application parameters are vulnerable to JavaScript injections</td>
        <td>
            <ul>
                <li><a href="#/guide/vulnerabilities/2-xss.md">Reflective Cross-Site Scripting (rXSS)</a></li>
                <li><a href="#/guide/vulnerabilities/1-xss.md">Persistent Cross-Site Scripting (pXSS)</a></li>
            </ul>
        </td>
    </tr>
     <tr>
        <td><b>Default Login Location</b></td>
        <td>Tests if login form location in the target application is easy to guess and accessible</td>
        <td>
            <ul>
                <li><a href="#/guide/vulnerabilities/31-default-login-location.md">Default Login Location</a></li>
            </ul>
        </td>
    </tr>
    <tr>
        <td><b>Directory Listing</b></td>
        <td>Tests if server-side directory listing is possible</td>
        <td>
            <ul>
                <li><a href="#/guide/vulnerabilities/26-directory-listing.md">Directory Listing</a></li>
            </ul>
        </td>
    </tr>
    <tr>
        <td><b>Email Header Injection</b></td>
        <td>Tests if it is possible to send emails to other addresses through the target application mailing server, which can lead to spam and phishing</td>
        <td>
            <ul>
                <li><a href="#/guide/vulnerabilities/222-email-header-injection.md">Email Header Injection</a></li>
            </ul>
        </td>
    </tr>
    <tr>
        <td><b>Exposed AWS S3 Buckets Details</b><br><i>(Open Buckets)</i></td>
        <td>Tests if exposed AWS S3 links lead to anonymous read access to the bucket</td>
        <td>
            <ul>
                <li><a href="#/guide/vulnerabilities/207-open-bucket.md">Exposed AWS S3 Buckets Details</a></li>
            </ul>
        </td>
    </tr>
      <tr>
        <td><b>Exposed Database Details</b><br><i>(Open Database)</i></td>
        <td>Tests if exposed database connection strings are open to public connections</td>
         <td>
            <ul>
                <li><a href="#/guide/vulnerabilities/205-open-database.md">Exposed Database Details</a></li>
                <li><a href="#/guide/vulnerabilities/206-open-database.md">Exposed Database Connection String</a></li>
            </ul>
        </td>
    </tr>
     <tr>
        <td><b>Full Path Disclosure (FPD)</b></td>
        <td>Tests if various application parameters are vulnerable to exposure of errors that include full webroot path</td>
        <td>
            <ul>
                <li><a href="#/guide/vulnerabilities/6-full-path-disclosure.md">Full Path Disclosure</a></li>
            </ul>
        </td>
    </tr>
    <tr>
        <td><b>Headers Security Check</b></td>
        <td>Tests for proper Security Headers configuration</td>
        <td>
            <ul>
                <li><a href="#/guide/vulnerabilities/60-misconfigured-headers.md">Misconfigured Security Headers</a></li>
                <li><a href="#/guide/vulnerabilities/60-missing-headers.md">Missing Security Headers</a></li>
                <li><a href="#/guide/vulnerabilities/60-insecure-policy-configuration.md">Insecure Content Secure Policy Configuration</a></li>
            </ul>
        </td>
    </tr>
    <tr>
        <td><b>HTML Injection</b></td>
        <td>Tests if various application parameters are vulnerable to HTML injection</td>
        <td>
            <ul>
                <li><a href="#/guide/vulnerabilities/44-html-injection.md">HTML Injection</a></li>
            </ul>
        </td>
    </tr>
    <tr>
        <td><b>Improper Assets Management</b></td>
        <td>Tests if older or development versions of API endpoints are exposed and can be used to get unauthorized access to data and privileges</td>
        <td>
            <ul>
                <li><a href="#/guide/vulnerabilities/215-improper-assets-management.md">Improper Assets Management</a></li>
            </ul>
        </td>
    </tr>
     <tr>
        <td><b>Insecure HTTP Method</b><br><i>(HTTP Method Fuzzer)</td>
        <td>Tests enumeration of possible HTTP methods for vulnerabilities</td>
        <td>
            <ul>
                <li><a href="#/guide/vulnerabilities/43-insecure-http-method.md">Insecure HTTP Method</a></li>
            </ul>
        </td>
    </tr>
    <tr>
        <td><b>Insecure TLS Configuration</b></td>
        <td>Tests SSL/TLS ciphers and configurations for vulnerabilities</td>
        <td>
            <ul>
                <li><a href="#/guide/vulnerabilities/220-insecure-tls-configuration.md">Insecure TLS Configuration</a></li>
            </ul>
        </td>
    </tr>
    <tr>
        <td><b>Known JavaScript Vulnerabilities</b><br><i>(JavaScript Vulnerabilities Scanning)</i></td>
        <td>Tests for known JavaScript component vulnerabilities</td>
        <td>
            <ul>
                <li><a href="#/guide/vulnerabilities/200-js-vulnerabilities.md">JavaScript Component with Known Vulnerabilities</a></li>
            </ul>
        </td>
    </tr>
    <tr>
        <td><b>Known WordPress Vulnerabilities</b><br><i>(WordPress Scan)</i></td>
        <td>Tests for known WordPress vulnerabilities and tries to enumerate a list of users</td>
        <td>
            <ul>
                <li><a href="#/guide/vulnerabilities/201-wordpress.md">WordPress Component with Known Vulnerabilities</a></li>
            </ul>
        </td>
    </tr>
   <tr>
        <td><b>LDAP Injection</b></td>
        <td>Tests if various application parameters are vulnerable to unauthorized LDAP access </td>
        <td>
            <ul>
                <li><a href="#/guide/vulnerabilities/12-ldap-injection.md">LDAP Injection</a></li>
                <li><a href="#/guide/vulnerabilities/223-ldap-error.md">LDAP Error</a></li>
            </ul>
        </td>
    </tr>
    <tr>
        <td><b>Local File Inclusion (LFI)</b></td>
        <td>Tests if various application parameters are vulnerable to loading of unauthorized local system resources</td>
        <td>
            <ul>
                <li><a href="#/guide/vulnerabilities/28-local-file-inclusion.md">Local File Inclusion (LFI)</a></li>
            </ul>
        </td>
    </tr>
        <tr>
        <td><b>Mass Assignment</b></td>
        <td>Tests if it is possible to create requests with additional parameters to gain privilege escalation</td>
        <td>
            <ul>
                <li><a href="#/guide/vulnerabilities/219-mass-assignment.md">Mass Assignment</a></li>
            </ul>
        </td>
    </tr>
     <tr>
        <td><b>OS Command Injection</b></td>
        <td>Tests if various application parameters are vulnerable to Operation System (OS) commands injection</td>
        <td>
            <ul>
                <li><a href="#/guide/vulnerabilities/23-os-command-injection.md">OS Command Injection</a></li>
                <li><a href="#/guide/vulnerabilities/209-os-command-injection.md">Blind Time Based OS Command Injection</a></li>
            </ul>
        </td>
    </tr>
    <tr>
        <td><b>Prototype Pollution</b></td>
        <td>Tests if it is possible to inject properties into existing JavaScript objects</td>
        <td>
            <ul>
                <li><a href="#/guide/vulnerabilities/217-prototype-pollution.md">Prototype Pollution</a></li>
            </ul>
        </td>
    </tr>
    <tr>
        <td><b>Remote File Inclusion (RFI)</b></td>
        <td>Tests if various application parameters are vulnerable to loading of unauthorized remote system resources</td>
        <td>
            <ul>
                <li><a href="#/guide/vulnerabilities/17-remote-file-inclusion.md">Remote File Inclusion (RFI)</a></li>
            </ul>
        </td>
    </tr>
     <tr>
        <td><b>Secret Tokens Leak</b></td>
        <td>Tests for exposure of secret API tokens or keys in the target application</td>
        <td>
            <ul>
                <li><a href="#/guide/vulnerabilities/61-secret-tokens-leak.md">Secret Tokens Leak</a></li>
            </ul>
        </td>
    </tr>
     <tr>
        <td><b>Server Side Template Injection (SSTI)</b></td>
        <td>Tests if various application parameters are vulnerable to server-side code execution</td>
        <td>
            <ul>
                <li><a href="#/guide/vulnerabilities/30-ssti.md">Server Side Template Injection (SSTI)</a></li>
            </ul>
        </td>
    </tr>
     <tr>
        <td><b>Server Side Request Forgery (SSRF)</b></td>
        <td>Tests if various application parameters are vulnerable to internal resources access</td>
        <td>
            <ul>
                <li><a href="#/guide/vulnerabilities/39-ssrf.md">Server Side Request Forgery (SSRF)</a></li>
            </ul>
        </td>
    </tr>
    <tr>
        <td><b>SQL Injection (SQLI)</b></td>
        <td>SQL Injection tests vulnerable parameters for SQL database access</td>
        <td>
            <ul>
                <li><a href="#/guide/vulnerabilities/32-sql-injection.md">SQL Injection: Blind Boolean Based</a></li>
                <li><a href="#/guide/vulnerabilities/27-sql-injection.md">SQL Injection: Blind Time Based</a></li>
                <li><a href="#/guide/vulnerabilities/3-sql-injection.md">SQL Injection</a></li>
                <li><a href="#/guide/vulnerabilities/37-sql-injection.md">SQL Database Error Message in Response</a></li>
            </ul>
        </td>
    </tr>
    <tr>
        <td><b>Unrestricted File Upload</b></td>
        <td>Tests if file upload mechanisms are validated properly and denies upload of malicious content</td>
        <td>
            <ul>
                <li><a href="#/guide/vulnerabilities/29-unrestricted-file-upload.md">Unrestricted File Upload</a></li>
            </ul>
        </td>
    </tr>
     <tr>
        <td><b>Unsafe Date Range</b><br><i>(Date Manipulation)</i></td>
        <td>Tests if date ranges are set and validated properly</td>
        <td>
            <ul>
                <li><a href="#/guide/vulnerabilities/18-unsafe-date-range.md">Unsafe Date Range</a></li>
            </ul>
        </td>
    </tr>
     <tr>
        <td><b>Unsafe Redirect</b><br><i>(Unvalidated Redirect)</i></td>
        <td>Tests if various application parameters are vulnerable to injectinon of a malicious link which can redirect a user without validation</td>
        <td>
            <ul>
                <li><a href="#/guide/vulnerabilities/15-unsafe-redirect.md">Unsafe Redirect</a></li>
            </ul>
        </td>
    </tr>
    <tr>
        <td><b>User ID Enumeration</b></td>
        <td>Tests if it is possible to collect valid user ID data by interacring with the target application</td>
        <td>
            <ul>
                <li><a href="#/guide/vulnerabilities/213-id-enumeration.md">Enumerable Integer-Based ID</a></li>
            </ul>
        </td>
    </tr>
     <tr>
        <td><b>Version Control System Data Leak</b></td>
        <td>Tests if it is possible to access Version Control System (VCS) resources</td>
        <td>
            <ul>
                <li><a href="#/guide/vulnerabilities/22-version-control-systems.md">Version Control System Data Leak</a></li>
            </ul>
        </td>
    </tr>
    <tr>
        <td><b>XML External Entity Injection</b></td>
        <td>Tests if various XML parameters are vulnerable to XML parsing of unauthorized external entities</td>
        <td>
            <ul>
                <li><a href="#/guide/vulnerabilities/33-xml-xxe.md">XML External Entity Injection</a></li>
            </ul>
        </td>
    </tr>
</table>