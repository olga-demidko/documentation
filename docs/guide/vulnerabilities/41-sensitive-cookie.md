<a class="not-decorated-link" href="#/guide/vulnerabilities/overview.md">< Back to tests</a>

# Sensitive Cookie Without HttpOnly Flag

<b>Severity</b>: <b><font color="#1B49D4">Low</font></b><br>
<b>Test name</b>: Cookie Security Check

<table id="simple-table">
    <tr>
        <th><strong>Summary</strong></th>
    </tr>
</table>

An HTTP cookie (web cookie, browser cookie) is a small piece of data that a server sends to the user's web browser. The browser may store it and send it back with later requests to the same server. Typically, it's used to tell if two requests came from the same browser (keeping a user logged-in, for example).

One of the ways to protect sensitive cookies is to ensure that they are not accessed by unintended parties or scripts: use the `HttpOnly` attribute. A cookie with the `HttpOnly` attribute is inaccessible to the JavaScript `Document.cookie` API. The cookie is sent only to the server. For example, cookies that persist server-side sessions do not need to be available to JavaScript, and should have the `HttpOnly` attribute.  This precaution helps mitigate Cross-Site Scripting (XSS) attacks, where an attacker may read the contents of a cookie and use the obtained information.


<table id="simple-table">
    <tr>
        <th><strong>Impact</strong></th>
    </tr>
</table>

The vulnerability allows an attacker to read the application data, gain privileges or assume identity.


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

It is necessary to configure (enable) the Secure attribute for sensitive cookies.
* .NET
    * _"Web.config"_ :
    ```
<system.web>
        ...
        <httpCookies httpOnlyCookies="true" />
</system.web>
```

    * C# :
```js
Response.Cookies.Add(
        new HttpCookie("key", "value")
        {
            .....
            Secure = true
        });
```
* PHP
    * _"php.ini"_ :
    ```
    session.cookie_httponly = True
    ```

    * During a script (parameter `$httponly` should be set to `true`):

    ```
    void session_set_cookie_params ( int $lifetime  [, string $path  [, string $domain [, bool $secure= false  [, bool $httponly= false  ]]]] )
    ```

    * Application cookies  (parameter `$httponly` should be set to `true`):

    ```
    bool setcookie ( string $name  [, string $value  [, int $expire= 0  [, string $path  [, string $domain  [, bool $secure= false  [, bool $httponly= false  ]]]]]] )
    ```

<table id="simple-table">
    <tr>
        <th><strong>Classifications</strong></th>
    </tr>
</table>

* CWE-1004
* CVSS:3.1/AV:N/AC:H/PR:N/UI:N/S:U/C:N/I:L/A:N

<table id="simple-table">
    <tr>
        <th><strong>References</strong></th>
    </tr>
</table>

* [https://www.owasp.org/index.php/HttpOnly](https://www.owasp.org/index.php/HttpOnly)
* [https://cwe.mitre.org/data/definitions/1004.html](https://cwe.mitre.org/data/definitions/1004.html)

<a class="not-decorated-link" href="#/guide/vulnerabilities/overview.md">< Back to tests</a>