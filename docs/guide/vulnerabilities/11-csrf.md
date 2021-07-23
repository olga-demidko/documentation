<a class="not-decorated-link" href="#/guide/vulnerabilities/overview.md">< Back to tests</a>

# Unauthorized Cross-Site Request Forgery (CSRF)

<b>Severity</b>: <b><font color="#1B49D4">Low</font></b><br>
<b>Test name</b>: Cross-Site Request Forgery (CSRF)

<table id="simple-table">
    <tr>
        <th><strong>Summary</strong></th>
    </tr>
</table>

Unauthorized Cross-Site Request Forgery (CSRF) occurs when a malicious resource forces a user's web browser to perform an unwanted action on a trusted website when the user is authenticated. The attack works because the browser requests automatically include all cookies, including session cookies. If the user is authenticated to the site, the site cannot distinguish between legitimate requests and forged requests.

An attacker may deliver a dangerous URL to a user in different ways, for example:
* Send an email with a link to a malicious request.
* Send an email with a 0x0 fake image. The source of the image is a malicious request.
* Develop a fake web application with a prepared form. The form can send a malicious request automatically (`<body onload="document.forms[0].submit()">`) or by clicking a submit button.
* Develop a fake web application with a prepared JavaScript code that will send _"XMLHttpRequest"_.

<table id="simple-table">
    <tr>
        <th><strong>Impact</strong></th>
    </tr>
</table>

The CSRF attack may be executed for the following purposes:
* Send money from one account to another
* Change a user's password or a secret question
* Gain administrative privileges
* Make a purchase with the user's credentials

<table id="simple-table">
    <tr>
        <th><strong>Example</strong></th>
    </tr>
</table>

1. The user is using a bank website `(https://{your-bank}.com)` and has an active session in his browser (for example, this website is opened in one of the browser tabs).
2. An attacker creates a special link to transfer money between two accounts:

```
https://{your-bank}.com/transfer?from=account1&to=account2&amount=1000
```
3. The attacker sends this link to the user in any possible way. For example, the attacker can use an email to send the link that will be shown for the user as a “broken" picture. The body of the email should contain:

```
<img src="https://{your-bank}.com/transfer?from=account1&to=account2&amount=1000/>
```
4. As soon as the user clicks this image, the corresponding URL opens in a new browser tab. As the user still has an active session (see point 1), the money from _"account1"_ will be transferred to _"account2"_. An unwanted action is performed on a trusted site when the user is authenticated.


<table id="simple-table">
    <tr>
        <th><strong>Location</strong></th>
    </tr>
</table>

* The issue can be found in the **source code** on the **server side**.
* The issue can be found in the **server configuration**.


<table id="simple-table">
    <tr>
        <th><strong>Remedy suggestions</strong></th>
    </tr>
</table>

* Check if your framework has built-in CSRF protection and use it.
* Always use the _"SameSite"_ Cookie Attribute for session cookies. Based on your application use cases, _"Lax"_ or _"Strict"_ value should be used.

```
Set-Cookie: JSESSIONID=xxxxx; SameSite=Strict
Set-Cookie: JSESSIONID=xxxxx; SameSite=Lax
```
* Do not use the GET method for state-changing requests. The GET request should be used only for retrieving the information.
* Try to avoid cross-site requests if possible. Modern web browsers support same-origin policy restriction, so do not configure CORS headers on your server.
* If your application supports cross-site requests, then carefully configure CORS headers. Configure allowed domain names in "_Access-Control-Allow-Origin_" header.
    * Nginx: 
    ```
    if ($http_origin ~* (whitelist\.address\.one|whitelist\.address\.two)$) {
    add_header Access-Control-Allow-Origin "$http_origin";
    }
    ```

    * Apache:
    ```
    <IfModule mod_headers.c>
        SetEnvIfNoCase Origin "https://(whitelist\.address\.one|whitelist\.address\.two)$" 
    AccessControlAllowOrigin=$0
        Header set Access-Control-Allow-Origin %{AccessControlAllowOrigin}e 
    env=AccessControlAllowOrigin
    </IfModule>
    ```
    * IIS 7.5+:
    ```
    <system.webServer>
    <httpProtocol>
        <customHeaders>
            <add name="Access-Control-Allow-Headers" value="Origin, X-Requested-With, Content-Type, Accept" />
            <add name="Access-Control-Allow-Methods" value="POST,GET,OPTIONS,PUT,DELETE" />
        </customHeaders>
    </httpProtocol>
            <rewrite>            
                <outboundRules>
                    <clear />                
                    <rule name="AddCrossDomainHeader">
                        <match serverVariable="RESPONSE_Access_Control_Allow_Origin" pattern=".*" />
                        <conditions logicalGrouping="MatchAll" trackAllCaptures="true">
                            <add input="{HTTP_ORIGIN}" pattern="(https://(whitelist\.address\.one|whitelist\.address\.two))" />
                        </conditions>
                        <action type="Rewrite" value="{C:0}" />
                    </rule>           
                </outboundRules>
            </rewrite>
    </system.webServer>
     ```

    * If the cookie is used for storing session information then the cookie have to be "_HTTP-only_" and "_Secured_" one:
    ```
    Set-Cookie: sessionId=some_session_hash; Expires=Thu, 21 Oct 2021 07:28:00 GMT; Secure; HttpOnly
    ```
<br>

<table id="simple-table">
    <tr>
        <th><strong>Classifications</strong></th>
    </tr>
</table>

* CWE-352
* CVSS:3.1/AV:N/AC:L/PR:N/UI:R/S:U/C:N/I:H/A:N 


<table id="simple-table">
    <tr>
        <th><strong>References</strong></th>
    </tr>
</table>

* [https://cwe.mitre.org/data/definitions/352.html](https://cwe.mitre.org/data/definitions/352.html)
* [https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF))
* [https://www.neuralegion.com/what-is-a-cross-site-request-forgery-csrf-attack-how-it-can-be-prevented/](https://www.neuralegion.com/what-is-a-cross-site-request-forgery-csrf-attack-how-it-can-be-prevented/)
* [https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF))
* [https://www.neuralegion.com/blog/csrf-vs-xss/](https://www.neuralegion.com/blog/csrf-vs-xss/)
* [https://www.neuralegion.com/blog/cross-site-request-forgery-csrf/](https://www.neuralegion.com/blog/cross-site-request-forgery-csrf/)

<a class="not-decorated-link" href="#/guide/vulnerabilities/overview.md">< Back to tests</a>