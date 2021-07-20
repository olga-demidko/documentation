# Insecure HTTP Method
<b>Severity</b>: <b><font color="#1B49D4">Low</font></b><br>
<b>Test name</b>: HTML Injection

<table id="simple-table">
    <tr>
        <th><strong>Summary</strong></th>
    </tr>
</table>

HTTP offers a number of methods that can be used to perform actions on the web server. Many of these methods are designed to assist developers in deploying and testing HTTP applications. These HTTP methods can be used for malicious purposes if the web server is misconfigured. 
Insecure HTTP methods can potentially pose a security risk for a web application, as they allow an attacker to modify the files stored on the web server and, in some scenarios, steal the credentials of legitimate users.

The following HTTP methods are considered as insecure:
* **PUT** - This method allows a client to upload new files on the web server. An attacker can exploit it by uploading malicious files (for example, an asp file that executes commands by invoking cmd.exe), or by simply using the victim’s server as a file repository.
* **DELETE** - This method allows a client to delete a file on the web server. An attacker can exploit it as a very simple and direct way to deface a website or to execute a DOS attack.
* **CONNECT** - This method can allow a client to use the web server as a proxy.
* **TRACE** - This method simply echoes back to the client whatever string has been sent to the server, and is used mainly for debugging purposes.<br> This method, originally assumed harmless, can be used to mount an attack known as Cross Site Tracing (see links at the bottom of the page).
The insecure HTTP methods should be disabled. If an application needs one or more of these methods, it is important to check that their usage is properly limited to trusted users and safe conditions.


<table id="simple-table">
    <tr>
        <th><strong>Impact</strong></th>
    </tr>
</table>

This vulnerability allows an attcker to modify the application data.



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

1. Disable insecure HTTP methods (`PUT`, `DELETE`, `CONNECT`, and `TRACE`) on the production web server:
    * Apache: add the following lines to `.htaccess` :<br>
    ```
    RewriteEngine On
    RewriteCond %{REQUEST_METHOD} ^(PUT|DELETE|CONNECT|TRACE) 
    RewriteRule .* - [F]
    ```

    * Nginx:  add the following lines to `nginx.conf` :
    ```
    if ($request_method ~ ^(PUT|DELETE|CONNECT|TRACE)$ ) 
    {
    return 405; 
    }
    ```

2. If it is not possible to disable insecure HTTP methods, make sure that their usage is properly limited to trusted users and safe conditions.




<table id="simple-table">
    <tr>
        <th><strong>Classifications</strong></th>
    </tr>
</table>

* CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N 


<table id="simple-table">
    <tr>
        <th><strong>References</strong></th>
    </tr>
</table>

[https://owasp.org/www-project-web-security-testing-guide/](https://owasp.org/www-project-web-security-testing-guide/)

