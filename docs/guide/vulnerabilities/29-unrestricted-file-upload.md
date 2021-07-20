# Unrestricted File Upload

<b>Severity</b>: <b><font color="#DB1E54">High</font></b><br>
<b>Test name</b>: Unrestricted File Upload

<table id="simple-table">
    <tr>
        <th><strong>Summary</strong></th>
    </tr>
</table>

Unrestricted File Upload vulnerability allows an attacker to upload malicious files to a web server without proper validation. The web application takes the uploaded file and saves it in the file system, data storage, or in a database. 

If a malicious file has been uploaded into the file system, the attacker is able to request this file using the URL of the victim’s site. As a result, the attacker can execute any command on the web server. In this case, the attacker should know the uploaded file path.

<table id="simple-table">
    <tr>
        <th><strong>Impact</strong></th>
    </tr>
</table>

Unrestricted File Upload vulnerability allows an attacker to do the following:
* Execute code on the server side and the client side.
* Gain sensitive information. Browse server folders and files.
* Crash the server. Overload the file system or the database.
* Send attacks to other servers. Create spam content.
* Overwrite critical files or personal data.


<table id="simple-table">
    <tr>
        <th><strong>Example of uploading a web-shell script</strong></th>
    </tr>
</table>

1. Consider that you have a web application which allows uploading an account photo without proper validation.
2. Instead of a picture, an attacker uploads a prepared PHP script (_"malicious-file.php"_) using the file picker for the account photo. The content of the PHP script is the following:
```js
<?php 
exec($_GET['c']); // Execute an external command passed to the script as entry parameter
```
3. AAfter the script has been successfully uploaded, the attacker can execute any system command on the web server using the following URL:
```
https://www.{your_web_site}.com/account-photos/malicious-file.php?c=<any-command>
```
4. As a result, the attacker can send a large number of messages anonymously. The attacker may also send phishing emails, where the recipient believes that these messages are originating from a trusted source (your website).

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

* The uploaded file types must be restricted. Use a whitelist of accepted, non-executable file extensions.
* Validate the uploaded files. Limit  the uploaded files amount and maximum file size.
* Make sure that your web server uses only one extension in the filename.
    * Apache
        * Insecure:
        ```
        <FilesMatch ".+\.php">SetHandler application/x-httpd-php</FileMatch>
        ```
        * Secure:
        ```
        <FilesMatch ".+\.php$">SetHandler application/x-httpd-php</FileMatch>
        ```
    * Nginx 
        * Insecure:
        ```     
        location ~* \.php$ {
            fastcgi_pass backend;
            # [...]
        }
        ```
        * Secure:
        ```
        location ~* \.php$ {
         try_files $uri = 404;
            fastcgi_pass backend;
            # [...]
        }
        ```
* The directory with the uploaded files should not have any _"execute"_ permission, and all the script handlers should be removed from these directories.
* When running on a web server that supports case insensitive names, apply the whitelist rule to filter extensions such as .exe or .EXE to disallow a situation where a bypass could be applied to the rules that state what type of file could be uploaded to the server.
* Consider saving the uploaded files in a specially designed data storage rather than in the file system of your web server.
* It is recommended to verify that the uploaded files are not saved with their original name (for example, `text.txt` will be saved as `2504sgbrys3f.txt` - thereby decreasing the chance that an attacker will access the file he has uploaded).


<table id="simple-table">
    <tr>
        <th><strong>Classifications</strong></th>
    </tr>
</table>

* CWE-434
* CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:L/A:L  


<table id="simple-table">
    <tr>
        <th><strong>References</strong></th>
    </tr>
</table>

* [https://www.owasp.org/index.php/Unrestricted_File_Upload](https://www.owasp.org/index.php/Unrestricted_File_Upload)
* [https://cwe.mitre.org/data/definitions/434.html](https://cwe.mitre.org/data/definitions/434.html)

