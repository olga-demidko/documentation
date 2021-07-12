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
                <li><a href="#/guide/vulnerabilities/216-jwt-role-bypass.md">JWT Role Bypass</li>
            </ul>
        </td>
    </tr>
     <tr>
        <td><b>Broken SAML Authentication</b></td>
        <td>Tests for secure implementation of SAML authentication in the application</td>
        <td><a href="#/guide/vulnerabilities/214-broken-saml-auth.md">Broken SAML Authentication</a></td>
    </tr>
    <tr>
        <td><b>Brute Force Login</b></td>
        <td>Tests for availability of commonly used credentials</td>
        <td><a href="#/guide/vulnerabilities/204-brute-force-login.md">Brute Force Login</a></td>
    </tr>
    <tr>
        <td><b>Common Files Exposure</b></td>
        <td>Tests if common files that should not be accessible are accessible</td>
        <td><a href="#/guide/vulnerabilities/203-exposed-common-file.md">Exposed Common File</a></td>
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
        <td><a href="#/guide/vulnerabilities/31-default-login-location.md">Default Login Location</a></td>
    </tr>
    <tr>
        <td><b>Improper Assets Management</b></td>
        <td>Tests if older or development versions of API endpoints are exposed and can be used to get unauthorized access to data and privileges</td>
        <td><a href="#/guide/vulnerabilities/215-improper-assets-management.md">Improper Assets Management</a></td>
    </tr>
    <tr>
        <td><b>Insecure TLS Configuration</b></td>
        <td>Tests SSL/TLS ciphers and configurations for vulnerabilities</td>
        <td><a href="#/guide/vulnerabilities/220-insecure-tls-configuration.md">Insecure TLS Configuration</a></td>
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
        <td><a href="#/guide/vulnerabilities/28-local-file-inclusion.md">Local File Inclusion (LFI)</a></td>
    </tr>
    <tr>
        <td><b>Exposed AWS S3 Buckets Details<br><i>(Open Buckets)</i></b></td>
        <td>Tests if exposed AWS S3 links lead to anonymous read access to the bucket</td>
        <td><a href="#/guide/vulnerabilities/207-open-bucket.md">Open Bucket</a></td>
    </tr>
      <tr>
        <td><b>Exposed Database Details<br><i>(Open Database)</i></b></td>
        <td>Tests if exposed database connection strings are open to public connections</td>
         <td>
            <ul>
                <li><a href="#/guide/vulnerabilities/205-open-database.md">Open Database</a></li>
                <li><a href="#/guide/vulnerabilities/206-open-database.md">Exposed Database Connection String</a></li>
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
        <td><a href="#/guide/vulnerabilities/217-prototype-pollution.md">Prototype Pollution</a></td>
    </tr>
    <tr>
        <td><b>Remote File Inclusion (RFI)</b></td>
        <td>Tests vulnerable parameters for accessing a remote file</td>
        <td><a href="#/guide/vulnerabilities/remote-file-inclusion.md">Remote File Inclusion (RFI)</a></td>
    </tr>
</table>