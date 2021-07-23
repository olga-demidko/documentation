<a class="not-decorated-link" href="#/guide/vulnerabilities/overview.md">< Back to tests</a>

# Reflective Cross-Site Scripting (rXSS)

<b>Severity</b>: <b><font color="#DB1E54">High</font></b><br>
<b>Test name</b>: Cross-Site Scripting (XSS)

<table id="simple-table">
    <tr>
        <th><strong>Summary</strong></th>
    </tr>
</table>

The application includes unvalidated and unescaped user input as part of HTML output. The attack principle is as easy as tricking a user to click on a link. When the user visits an infected page (for example, clicks on a URL like `https://{your_web_site}.com?search={malicious_code}`, which they can receive by email), then the script (`{malicious_code}`) supplied by the attacker will be executed in the user's browser during the application runtime.

A successful attack can allow the attacker to execute arbitrary HTML and JavaScript in the user’s browser.  As a result, the attacker gets access to the application and can do anything that the victim (user) can on the client side (access any cookies, session tokens and other).


<table id="simple-table">
    <tr>
        <th><strong>Impact</strong></th>
    </tr>
</table>

This vulnerability allows an attacker to:
* Execute unauthorized code or commands
* Bypass protection mechanism
* Read the application data
* Deface the application

<table id="simple-table">
    <tr>
        <th><strong>Location</strong></th>
    </tr>
</table>

The issue can be found in the **source code** on the **client side**.

<table id="simple-table">
    <tr>
        <th><strong>Remedy suggestions</strong></th>
    </tr>
</table>

* Never insert untrusted data in any locations, except where permitted. If it is possible, do not put any untrusted data into your HTML document.
* Apply the HTML encoding before inserting untrusted data into HTML element content.
* Apply the attribute encode before inserting untrusted data into HTML common attributes.
* Apply the JavaScript encoding before inserting untrusted data into JavaScript data values.
* Apply the CSS encoding and strictly validate the untrusted data before inserting it into HTML style property values.
* Apply the URL encoding before inserting untrusted data into HTML URL parameter values.
* Sanitize HTML markup with a library designed for the job. If your application handles markup (untrusted input that is supposed to contain HTML), it may be very difficult to validate it, and encoding may break all the tags that are supposed to be in the input. To cover that, use a library that can parse and clean HTML formatted text, for example:  HTMLSanitizer ([https://github.com/mganss/HtmlSanitizer](https://github.com/mganss/HtmlSanitizer)), OWASP Java HTML Sanitizer ([https://owasp.org/www-project-java-html-sanitizer/](https://owasp.org/www-project-java-html-sanitizer/)), DOMPurify ([https://github.com/cure53/DOMPurify](https://github.com/cure53/DOMPurify)), or other.
* Avoid JavaScript URLs. Untrusted URLs that include the protocol javascript will execute JavaScript code when used in the URL DOM locations, such as anchor tag HREF attributes or iFrame src locations. Validate all untrusted URLs to ensure they only contain safe schemes such as HTTPS.

<br>

<table id="simple-table">
    <tr>
        <th><strong>Classifications</strong></th>
    </tr>
</table>

* CWE-79
* CVSS:3.1/AV:N/AC:L/PR:N/UI:R/S:U/C:N/I:H/A:N 


<table id="simple-table">
    <tr>
        <th><strong>References</strong></th>
    </tr>
</table>

* [https://cwe.mitre.org/data/definitions/79.html](https://cwe.mitre.org/data/definitions/79.html)
* [https://www.owasp.org/index.php/Cross-site_Scripting_(XSS)](https://www.owasp.org/index.php/Cross-site_Scripting_(XSS))
* [https://www.neuralegion.com/cross-site-scripting-xss-everything-you-need-to-know-about-xss-attacks/](https://www.neuralegion.com/cross-site-scripting-xss-everything-you-need-to-know-about-xss-attacks/)
* [https://www.neuralegion.com/blog/xss/](https://www.neuralegion.com/blog/xss/)
* [https://www.neuralegion.com/blog/cross-site-scirpting-prevention/](https://www.neuralegion.com/blog/cross-site-scirpting-prevention/)


<a class="not-decorated-link" href="#/guide/vulnerabilities/overview.md">< Back to tests</a>