<a class="not-decorated-link" href="#/guide/vulnerabilities/overview.md">< Back to tests</a>

# HTML Injection

<b>Severity</b>: <b><font color="#DE8800">Medium</font></b><br>
<b>Test name</b>: HTML Injection

<table id="simple-table">
    <tr>
        <th><strong>Summary</strong></th>
    </tr>
</table>

The application stores a malicious code (injected HTML) in a long time storage (usually a database on the server side). The malicious code is returned to the client as part of the HTTP response from the server (to the same or different client/user), and the client interprets it as trustworthy and displays it. One of the basic targets for the HTML injection is to change the visible content of the application page. An attacker may use a stored HTML injection to inject a visual advertisement of a product that they want to sell. A similar case would be when the attacker injects malicious HTML to harm the reputation of the page.

<table id="simple-table">
    <tr>
        <th><strong>Impact</strong></th>
    </tr>
</table>

* Execution of unauthorized code or commands
* Protection mechanism bypass
* Application defacement



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

The protection against HTML injections is better to consider as general XSS protection in the application. The injection of a malicious code needs to be prevented regardless of the injected code type. Since the information is returned from the server side, the most effective solution is to prevent dangerous data from being created on the server. 

General recommendations are the following:
* Treat all user input as untrusted. All user input should be strictly filtered and precisely validated (the whitelist approach).
* Encode the output data to prevent it from being interpreted as active content. Use the appropriate encoding technique depending on where the user input is to be used: HTML, URL, JavaScript, or CSS encoding. A common mistake is to use HTML entity encoding everywhere. It is important to understand that HTML entity encoding protects you from injections inside the body of the HTML document (like the `<div>` tag). But it doesn't work if you put untrusted data inside the `<script>` tag anywhere, or an event handler attribute like `onmouseover`, or inside CSS, or in a URL. You MUST use the encode syntax, which is suitable for the part of the HTML document you are putting untrusted data into. To make sure that these rules are properly implemented, we recommend using a security-focused encoding library, for example:
    * Java: OWASP Java Encoder ([https://owasp.org/www-project-java-encoder/](https://owasp.org/www-project-java-encoder/))
    * NET: AntiXssEncoder Class ([https://docs.microsoft.com/en-us/dotnet/api/system.web.security.antixss.antixssencoder?view=netframework-4.8](https://docs.microsoft.com/en-us/dotnet/api/system.web.security.antixss.antixssencoder?view=netframework-4.8))



<table id="simple-table">
    <tr>
        <th><strong>Classifications</strong></th>
    </tr>
</table>

* CWE-80
* CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:L/A:N 


<table id="simple-table">
    <tr>
        <th><strong>References</strong></th>
    </tr>
</table>

[https://cwe.mitre.org/data/definitions/80.html](https://cwe.mitre.org/data/definitions/80.html)


<a class="not-decorated-link" href="#/guide/vulnerabilities/overview.md">< Back to tests</a>