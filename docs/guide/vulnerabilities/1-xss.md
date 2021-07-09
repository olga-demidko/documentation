# Persistent Cross-Site Scripting (pXSS)

<b>Severity</b>: <b><font color="red">High</font></b><br>
<b>Test name</b>: Cross-Site Scripting (XSS)

<table id="simple-table">
    <tr>
        <th><strong>Summary</strong></th>
    </tr>
</table>

The application stores malicious data in a long time storage (usually a database on the server side). The malicious code is returned to the client as part of the HTTP response from the server (to the same or different client/user), and the client interprets it as trustworthy. The dangerous data can be later included in dynamic content. As a result, an attacker can do anything that a victim (user) can on the client side (access any cookies, session tokens and other).

<table id="simple-table">
    <tr>
        <th><strong>Impact</strong></th>
    </tr>
</table>

This vulnerability allows an attacker to:
* Execute unauthorized code or commands
* Bypass protection mechanism
* Read the target application data
* Deface the target application

<table id="simple-table">
    <tr>
        <th><strong>Location</strong></th>
    </tr>
</table>

The issue can be found in the **source code** on the **server side**.

<table id="simple-table">
    <tr>
        <th><strong>Remedy suggestions</strong></th>
    </tr>
</table>

Since the information is returned from the server-side, the most effective solution is to prevent dangerous data from being created on the server.
The general recommendations are the following:
* Treat all user input as untrusted. All user inputs should be strictly filtered and precisely validated (whitelist approach). 
* Encode the output data to prevent it from being interpreted as active content. Use the appropriate encoding technique depending on where the user input is to be used: HTML, URL, JavaScript, or CSS encoding. A common mistake is to use HTML entity encoding everywhere.  It is important to understand that HTML entity encoding protects you from injections inside the body of the HTML document (line `<div>` tag). But it doesn't work if you put untrusted data inside the `<script>` tag anywhere, or an event handler attribute like `onmouseover`, or inside CSS, or in a URL. You MUST use the encode syntax, which is suitable for the part of the HTML document you are putting untrusted data into. To make sure that these rules are properly implemented, we recommend using a security-focused encoding library, for example:
    * Java: OWASP Java Encoder ([https://owasp.org/www-project-java-encoder](https://owasp.org/www-project-java-encoder))
    * .NET: AntiXssEncoder Class ([https://docs.microsoft.com/en-us/dotnet/api/system.web.security.antixss.antixssencoder?view=netframework-4.8](https://docs.microsoft.com/en-us/dotnet/api/system.web.security.antixss.antixssencoder?view=netframework-4.8))
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
* [https://www.neuralegion.com/blog/cross-site-scripting-xss/](https://www.neuralegion.com/blog/cross-site-scripting-xss/)
* [https://www.neuralegion.com/blog/xss/](https://www.neuralegion.com/blog/xss/)
* [https://www.neuralegion.com/blog/cross-site-scirpting-prevention/](https://www.neuralegion.com/blog/cross-site-scirpting-prevention/)
