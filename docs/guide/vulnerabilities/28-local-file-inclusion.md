# Local File Inclusion (LFI)

<b>Severity</b>: <b><font color="red">High</font></b><br>
<b>Test name</b>: Local File Inclusion (LFI)

<table id="simple-table">
    <tr>
        <th><strong>Summary</strong></th>
    </tr>
</table>

Local File Inclusion is an attack applicable to web applications that dynamically include local files or scripts. When such a web application takes user input (URL, parameter value, etc.) and passes it into file include commands, the web application might be tricked into including local files with sensitive information. As a result, sensitive information can be shown for the attacker. In addition, if your application allows uploading files without proper validation, the attacker is able to upload a file with a malicious code to the server and execute that code. But in this case, the attacker should know the uploaded file path.

<table id="simple-table">
    <tr>
        <th><strong>Impact</strong></th>
    </tr>
</table>

* Remote code execution on the server
* Disclosure of potentially severe information
* Gathering of local usernames and logs
* Crash of the server

<table id="simple-table">
    <tr>
        <th><strong>Example (PHP)</strong></th>
    </tr>
</table>

1. Web application supports the following URL:
```
https://www.{your_web_site}.com/page?file=contact-form.php
```
2. On the server side, the script exploits the provided parameter using the following code:
```php
<?php
include("pages/" . $_REQUEST['file']);
```
3. An attacker is able to change the requested URL so that the file that is located locally on the server is passed to the script:
```
https://www.{your_web_site}.com/page?file=../../../../../etc/passwd
```
4. As a result, the attacker will be able to retrieve the content of the file located on the server. The following content can be shown as the response:
```
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
games:x:5:60:games:/usr/games:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
```

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

* The most effective solution is to avoid passing user-submitted input to any file system / framework API. 
* If you have a limited number of the allowed files to include, all of them can be stored as corresponding records in long time storage (for example, database) with specific identifiers. Such identifiers can be used as the request parameters to identify and include only allowed files.
* If it is not possible to list the allowed files, and the user input cannot  be avoided, ensure that the supplied values are valid. Sanitize the input by creating a list of trusted files. Use the whitelist approach.




<table id="simple-table">
    <tr>
        <th><strong>Classifications</strong></th>
    </tr>
</table>

* CWE-90
* CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:N/A:N

<table id="simple-table">
    <tr>
        <th><strong>References</strong></th>
    </tr>
</table>

* [https://www.owasp.org/index.php/Testing_for_Local_File_Inclusion](https://www.owasp.org/index.php/Testing_for_Local_File_Inclusion)
* [https://www.neuralegion.com/local-file-inclusion-lfi-what-is-lfi-and-how-to-deal-with-it/](https://www.neuralegion.com/local-file-inclusion-lfi-what-is-lfi-and-how-to-deal-with-it/)
* [https://www.neuralegion.com/blog/local-file-inclusion-lfi/](https://www.neuralegion.com/blog/local-file-inclusion-lfi/)
