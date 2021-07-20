# Server Side Request Forgery (SSRF)

<b>Severity</b>: <b><font color="#DB1E54">High</font></b><br>
<b>Test name</b>: Server Side Template Injection (SSTI)

<table id="simple-table">
    <tr>
        <th><strong>Summary</strong></th>
    </tr>
</table>

Some web applications take the input URL parameter and retrieve the response content of a request. This allows an attacker to execute the Server Side Request Forgery (SSRF) attack by sending any request to any URL address through the victim application on the web server. It is possible if the application does not validate the URL parameter.


<table id="simple-table">
    <tr>
        <th><strong>Impact</strong></th>
    </tr>
</table>

Server Side Request Forgery attack allows the attacker to:
* Gain sensitive information on the server
* Get access to internal services
* Get access to Databases if the access is allowed for internal network
* Scan host ports on internal networks


<table id="simple-table">
    <tr>
        <th><strong>Example (PHP)</strong></th>
    </tr>
</table>

1. Let’s imagine the following code is used on the server side for specific reasons (_"image.php"_):
    ```js
    <?php
    if (isset($_GET['url'])){
        $image = fopen($_GET['url'], 'rb');

     header("Content-Type: image/png");
        fpassthru($image);
    }
    ```
2. The following URL can be used to retrieve the web server statistics:
    ```
    https://www.{your_web_site}.com/image.php?url=http://localhost/server-status
    ```
3. The following URL can be used to retrieve the `passwd` file content:
    ```
    https://www.{your_web_site}.com/image.php?url=file:///etc/passwd

    ```
4. The following URL can be used to retrieve the meta-data of the cloud service:
    ``` 
    https://www.{your_web_site}.com/image.php?url=http://169.254.169.254/latest/meta-data/
    ```
    _Note:_ `169.254.169.254` is a special IP address of the AWS EC2 instance metadata, that is used here as an example only.

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

* Restrict supported protocols in your web application. Disable any unused schema, for example `ftp://, dict://, file:///, gopher://`.
* Sanitize input by creating a list of trusted URLs (lists of hosts or a regex). Use the whitelist approach.
* If a microservice architecture is used, then it is required to integrate a cross-service authentication mechanism (communication between all internal services should be authenticated).
* AWS: IMDSv2 is an additional defense mechanism for AWS that mitigates some instances of SSRF if you are using a cloud environment. Migrate to IMDSv2 and disable old IMDSv1. Check out AWS documentation for more details.


<table id="simple-table">
    <tr>
        <th><strong>Classifications</strong></th>
    </tr>
</table>

* CWE-918
* CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:L/A:N  


<table id="simple-table">
    <tr>
        <th><strong>References</strong></th>
    </tr>
</table>

* [https://cwe.mitre.org/data/definitions/918.html](https://cwe.mitre.org/data/definitions/918.html)
* [https://owasp.org/www-community/attacks/Server_Side_Request_Forgery](https://owasp.org/www-community/attacks/Server_Side_Request_Forgery)
* [https://www.neuralegion.com/blog/ssrf-server-side-request-forgery/](https://www.neuralegion.com/blog/ssrf-server-side-request-forgery/)
