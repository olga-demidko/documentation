# Brute Force Login

<b>Severity</b>: <b><font color="#1B49D4">Low</font></b><br>
<b>Test name</b>: Common Files Exposure

<table id="simple-table">
    <tr>
        <th><strong>Summary</strong></th>
    </tr>
</table>

Most web applications use common files to store application configuration, logs, tokens and other sensitive information. If an attacker is not explicitly authorized and has access to that information, then such applications are vulnerable for exposing. 

That allows an attacker to gain sensitive information and take control over other systems the credentials are used for (for example, third party API). This also allows finding out other secure information about the application.

<table id="simple-table">
    <tr>
        <th><strong>Impact</strong></th>
    </tr>
</table>

Exposed Common File may allow an attacker to:
* Get administrative access to a system and manipulate data or manage the account
* Gain personal information of the system members 
* Get log information (access log or error log)
* Get system configuration

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

* Change the directory structure and move sensitive files (configs, source code, logs, dumps) above the web root folder of the web application.
* Store configuration settings in environment variables where it’s possible. If environment variables are being used, make sure to only read them in a single config file.
* If secure information is being stored inside your application, such information should be encrypted.
* When sensitive information cannot be moved to environment variables, access to it must be restricted by your web server (enforce access only by localhost).
    * Nginx
    ```
    location ^~ /configuration/ {
        deny all;
        return 403;
    }
    ```
    * Apache
    ```
    <DirectoryMatch "^/configuration/">
        Require all denied
    </DirectoryMatch>
    ```

<table id="simple-table">
    <tr>
        <th><strong>Classifications</strong></th>
    </tr>
</table>

* CWE-200
* CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N
 


<table id="simple-table">
    <tr>
        <th><strong>References</strong></th>
    </tr>
</table>

https://cwe.mitre.org/data/definitions/200.html