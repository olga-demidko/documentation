# Sensitive Cookie in HTTPS Session Without Secure Attribute

<b>Severity</b>: <b><font color="#1B49D4">Low</font></b><br>
<b>Test name</b>: Cookie Security Check

<table id="simple-table">
    <tr>
        <th><strong>Summary</strong></th>
    </tr>
</table>

An HTTP cookie (web cookie, browser cookie) is a small piece of data that a server sends to the user's web browser. The browser may store it and send it back with later requests to the same server. Typically, it is used to tell if two requests came from the same browser (keeping a user logged-in, for example). 

One of the ways to protect sensitive cookies is to ensure that they are sent securely and are not accessed by unintended parties or scripts: use the `Secure` attribute. A cookie with the `Secure` attribute is sent to the server only with an encrypted request over the HTTPS protocol, never with unsecured HTTP (except on localhost). It prevents attackers from accessing cookies easily by intercepting unsecured HTTP requests with plaintext cookies. Insecure sites (with `http:` in the URL) cannot set cookies with the Secure attribute.


<table id="simple-table">
    <tr>
        <th><strong>Impact</strong></th>
    </tr>
</table>

This vulnerability allows an attacker to read the application data. 

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

It is necessary to configure (enable) the `Secure` attribute for sensitive cookies.
* .NET
    * _"Web.config"_ :
    ```
<system.web>
        ...
        <httpCookies requireSSL="true" />
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
    session.cookie_secure = True
    ```

    * During a script (parameter `$secure` should be set to `true`):

    ```
    void session_set_cookie_params ( int $lifetime  [, string $path  [, string $domain [, bool $secure= false  [, bool $httponly= false  ]]]] )
    ```

    * Application cookies (parameter `$secure` should be set to `true`):

    ```
    bool setcookie ( string $name  [, string $value  [, int $expire= 0  [, string $path  [, string $domain  [, bool $secure= false  [, bool $httponly= false  ]]]]]] )
    ```

<table id="simple-table">
    <tr>
        <th><strong>Classifications</strong></th>
    </tr>
</table>

* CWE-614
* CVSS:3.1/AV:N/AC:H/PR:N/UI:N/S:U/C:N/I:L/A:N

<table id="simple-table">
    <tr>
        <th><strong>References</strong></th>
    </tr>
</table>

* [https://owasp.org/www-community/controls/SecureCookieAttribute](https://owasp.org/www-community/controls/SecureCookieAttribute)
* [https://cwe.mitre.org/data/definitions/614.html](https://cwe.mitre.org/data/definitions/614.html)
