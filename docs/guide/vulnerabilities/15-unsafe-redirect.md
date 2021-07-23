<a class="not-decorated-link" href="#/guide/vulnerabilities/overview.md">< Back to tests</a>

# Unsafe Redirect

<b>Severity</b>: <b><font color="#DE8800">Medium</font></b><br>
<b>Test name</b>: Unsafe Redirect

<table id="simple-table">
    <tr>
        <th><strong>Summary</strong></th>
    </tr>
</table>

An unvalidated redirect is a situation when your web application forces the user’s browser to open another external URL. Unvalidated redirects are possible if the web application uses a URL that is taken from untrusted input. By modifying the untrusted URL input to a malicious site, an attacker may successfully launch a phishing scam and steal user credentials.
The following example shows what kind of URL an attacker can create to exploit this vulnerability:
```
http://www.your_web_site.com/redirect?url=http://dangerous_web_site.com
```



<table id="simple-table">
    <tr>
        <th><strong>Impact</strong></th>
    </tr>
</table>

This vulnerability allows an attacker to bypass protection mechanisms,  gain privileges or assume identity. 


<table id="simple-table">
    <tr>
        <th><strong>Location</strong></th>
    </tr>
</table>

* The issue can be found in the **source code** on the **server side**.
* The issue can be found in the **source code** on the **client side**.


<table id="simple-table">
    <tr>
        <th><strong>Remedy suggestions</strong></th>
    </tr>
</table>

The best solution to avoid unvalidated redirects is not to use any redirects or forwards. However, if the website or web application cannot function properly without redirects or forwards, there is a number of ways how to handle them safely:
* If you have a limited number of the destination URLs to redirect, all of them can be stored in long time storage (for example, database) with specific identifiers. Such identifiers can be used as request parameters that redirect to the relevant URL. 
* If it is not possible to list destination pages, and user input cannot be avoided, ensure that the supplied value is valid, appropriate for the application, and authorized for the user.
    * Sanitize the input by creating a list of trusted URLs (lists of hosts or a regex). Use the whitelist approach. 
    * Remove the hostname from the redirection URL, so that it may only redirect to a different path on the same domain as the application.
* Lead all redirects to a notification message / special page with the information that the user is leaving your site. So that the user should confirm the redirect.

<table id="simple-table">
    <tr>
        <th><strong>Classifications</strong></th>
    </tr>
</table>

* CWE-601
* CVSS:3.1/AV:N/AC:L/PR:N/UI:R/S:U/C:N/I:H/A:N


<table id="simple-table">
    <tr>
        <th><strong>References</strong></th>
    </tr>
</table>

* [https://cwe.mitre.org/data/definitions/601.html](https://cwe.mitre.org/data/definitions/601.html)
* [https://www.owasp.org/index.php/Unvalidated_Redirects_and_Forwards_Cheat_Sheet](https://www.owasp.org/index.php/Unvalidated_Redirects_and_Forwards_Cheat_Sheet)
* [https://www.neuralegion.com/discovering-and-remediating-open-redirect-vulnerabilities/](https://www.neuralegion.com/discovering-and-remediating-open-redirect-vulnerabilities/ )

<a class="not-decorated-link" href="#/guide/vulnerabilities/overview.md">< Back to tests</a>