<a class="not-decorated-link" href="#/guide/vulnerabilities/overview.md">< Back to tests</a>

# Insecure Content Secure Policy Configuration

<b>Severity</b>: <b><font color="#DE8800">Low</font></b><br>
<b>Test name</b>: Headers Security Check

<table id="simple-table">
    <tr>
        <th><strong>Summary</strong></th>
    </tr>
</table>

Browsers support many HTTP headers that can improve web application security. The HTTP security headers are exchanged between a web client (usually browser) and a server to specify the security-related details of the HTTP communication. Some HTTP headers that are indirectly related to privacy and security can also be considered as the HTTP security headers.

By enabling certain headers in your web application and server settings, you can increase your web application resistance to many common attacks. Implementing the right headers is a crucial aspect of a best-practice application setup.

Content Security Policy (CSP) is a computer security standard introduced to prevent cross-site scripting (XSS), clickjacking and other code injection attacks resulting from execution of malicious content in trusted web page context. By using suitable CSP directives in HTTP response headers, you can selectively specify which data sources should be permitted in your web application.

The <i>Content-Security-Policy</i> HTTP header controls permitted content sources and many other parameters.

<table id="simple-table">
    <tr>
        <th><strong>Impact</strong></th>
    </tr>
</table>

This vulnerability may expose the application to the following attack vectors:
* Cross-Site Scripting (XSS)
* Clickjacking
* Code injection

An attacker may:
* Download malware or execute malicious script on the user's machine
* Redirect to the malicious web pages
* Gain credentials or sensitive information

<table id="simple-table">
    <tr>
        <th><strong>Location</strong></th>
    </tr>
</table>

* The issue can be found in the **server configuration**.
* The issue can be found in the **source code** on the **server side**.



<table id="simple-table">
    <tr>
        <th><strong>Remedy suggestions</strong></th>
    </tr>
</table>

Verify that the HTTP Response Headers are configured correctly. If necessary, apply changes to the web server configuration and the application source code. 

**Proposed values for the Content Security Policy HTTP Header:**
* Content-Security-Policy: 
```
default-src 'self' data:; object-src 'none'; child-src 'self'; frame-ancestors 'none'; upgrade-insecure-requests; block-all-mixed-content
```
**Web server syntax:**
* Apache: `Header always set [HEADER_NAME] [PROPOSED_VALUE]`
* Nginx: `add_header [HEADER_NAME] [PROPOSED_VALUE] always;`

**Do not use:**
* X-WebKit-CSP (deprecated): Experimental header used in the past by Chrome and other WebKit-based browsers.
* X-Content-Security-Policy _(deprecated)_: Experimental header used in the past by browsers based on Gecko 2.

To find the detailed recommendations on correct configuration and all possible values of the HTTP Response Headers, refer to the **References** section.

<table id="simple-table">
    <tr>
        <th><strong>Classification</strong></th>
    </tr>
</table>

* CWE-693
* CVSS:3.1/AV:N/AC:H/PR:N/UI:N/S:U/C:N/I:L/A:N


<table id="simple-table">
    <tr>
        <th><strong>References</strong></th>
    </tr>
</table>

* [https://cwe.mitre.org/data/definitions/693.html](https://cwe.mitre.org/data/definitions/693.html)
* [https://cwe.mitre.org/data/definitions/16.html](https://cwe.mitre.org/data/definitions/16.html)
* [https://owasp.org/www-project-secure-headers](https://owasp.org/www-project-secure-headers)


<a class="not-decorated-link" href="#/guide/vulnerabilities/overview.md">< Back to tests</a>