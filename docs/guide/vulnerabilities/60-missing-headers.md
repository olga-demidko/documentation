# Missing Security Headers 

<b>Severity</b>: <b><font color="#DE8800">Medium</font></b><br>
<b>Test name</b>: Headers Security Check

<table id="simple-table">
    <tr>
        <th><strong>Summary</strong></th>
    </tr>
</table>

Browsers support many HTTP headers that can improve web application security. The HTTP security headers are exchanged between a web client (usually browser) and a server to specify the security-related details of the HTTP communication. Some HTTP headers that are indirectly related to privacy and security can also be considered as the HTTP security headers. 

By enabling certain headers in your web application and server settings, you can increase your web application resistance to many common attacks. Implementing the right headers is a crucial aspect of a best-practice application setup.

**List of the most important HTTP Security Headers:**
* _Strict-Transport-Security:_ enforces usage of HTTPS instead of HTTP communication
* _X-Frame-Options:_ manages possibility to load the current page into any iframe
* _X-Content-Type-Options:_ controls the MIME Type Sniffing function in web browsers
* _Content-Security-Policy:_ controls permitted content sources and many other parameters
* _X-Permitted-Cross-Domain-Policies:_ manages cross-domain requests from Flash and PDF documents
* _Referrer-Policy:_ determines which information from the _Referer_ header should be included in the requests 
* _Clear-Site-Data:_ clears the  browsing data (cookies, storage, cache) associated with the requested website. This header can be used during a logout process to ensure that the browsing data on the client side is removed.
* _Cross-Origin-Embedder-Policy:_ prevents a document from loading any cross-origin resources that are not permitted for the document
* _Cross-Origin-Opener-Policy:_ ensures that a top-level document does not share a browsing context group with cross-origin documents
* _Cross-Origin-Resource-Policy:_ allows defining a policy that lets websites and applications enable protection from certain requests received from other origins

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

**Proposed values for the most important HTTP Security Headers:**
* Strict-Transport-Security: `max-age=31536000 ; includeSubDomains`
* X-Frame-Options: `deny`
* X-Content-Type-Options: `nosniff`
* Content-Security-Policy: `default-src 'self' data:; object-src 'none'; child-src 'self'; frame-ancestors 'none'; upgrade-insecure-requests; block-all-mixed-content`
* X-Permitted-Cross-Domain-Policies: `none`
* Referrer-Policy: `no-referrer`
* Clear-Site-Data: `"cache","cookies","storage"`.<br> _Note:_ This header can be used during a logout process to ensure that the browsing data on the client side is removed.
* Cross-Origin-Embedder-Policy: `require-corp`
* Cross-Origin-Opener-Policy: `same-origin`
* Cross-Origin-Resource-Policy: `same-origin`

**Web server syntax:**
* Apache: `Header always set [HEADER_NAME] [PROPOSED_VALUE]`
* Nginx: `add_header [HEADER_NAME] [PROPOSED_VALUE] always;`

To find the detailed recommendations on correct configuration and all possible values of the HTTP Response Headers, see the **References** section below.

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
* [https://owasp.org/www-project-secure-headers](https://owasp.org/www-project-secure-headers)
