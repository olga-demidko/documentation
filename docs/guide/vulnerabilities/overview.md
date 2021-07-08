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
        <td>TTests if the application uses and implements cookies with secure attributes</td>
        <td>
            <ul>
                <li><a href="#/guide/vulnerabilities/40-sensitive-cookie.md">Sensitive Cookie in HTTPS Session Without Secure Attribute</a></li>
                <li><a href="#/guide/vulnerabilities/exposed-common-file.md">Sensitive Cookie Without HttpOnly Flag</a></li>
                <li><a href="#/guide/vulnerabilities/exposed-common-file.md">Sensitive Cookie Weak Session ID</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td><b>Remote File Inclusion (RFI)</b></td>
        <td>Tests vulnerable parameters for accessing a remote file</td>
        <td><a href="#/guide/vulnerabilities/remote-file-inclusion.md">Remote File Inclusion (RFI)</a></td>
    </tr>
</table>