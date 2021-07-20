# Version Control System Data Leak

<b>Severity</b>: <b><font color="#DE8800">Medium</font></b><br>
<b>Test name</b>: Version Control System Data Leak

<table id="simple-table">
    <tr>
        <th><strong>Summary</strong></th>
    </tr>
</table>

Most of the web applications store code in Version Control System (VCS). It is used for developers to store and synchronize work between developers. The metadata of changes for folders or files during development (VCS metadata) is stored in special repository folders and files, such as `.svn`, `.git`.

When VCS metadata is deployed along with the source code of the web application, the attacker can exploit this misconfiguration to download the entire source code along with other sensitive data. 


<table id="simple-table">
    <tr>
        <th><strong>Impact</strong></th>
    </tr>
</table>

Version Control Systems data leak may lead to:
* Leakage of sensitive information, such as hard-coded database credentials, API keys, etc.
* Gaining access to the entire source code of the application. Afterwards, it can be used to find other vulnerabilities which may escalate to more dangerous attacks, which may be unknown to the attacker since the source code was not accessible.


<table id="simple-table">
    <tr>
        <th><strong>Example</strong></th>
    </tr>
</table>

Detecting Version Control Systems Data Leak for GIT:
1. Fulfill one of the next requests to check if the repository folder is accessible 
```
https://www.{your_web_site}.com/git/
```
or
```
https://www.{your_web_site}.com/.git
```

2. If you get a `404 HTTP Code (Not Found)`, it means that `.git` is not available on the server. If you get the `403 HTTP Code (Forbidden)`, it means that the `.git` folder exists on the server, but it cannot be easily accessed. Anyway, it gives information to the attacker, and they can plan future attacks to retrieve VCS metadata.


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

1. Remove the VCS metadata (repository folders `.svn`, `.git`) from your production web server.
2. If it is not possible to remove repository folders, ensure that you deny access to the repository folders (`.svn`, `.git`) via your web server configuration:
    * Apache + GIT:
    ```  
    <DirectoryMatch "^/.*/\.git/">
        Require all denied
    </DirectoryMatch>
    ```
    * Nginx + GIT:
    ```
    location ~ /.git/ {
        deny all;
    }
    ```


<table id="simple-table">
    <tr>
        <th><strong>Classifications</strong></th>
    </tr>
</table>

* CWE-527
* CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:N


<table id="simple-table">
    <tr>
        <th><strong>References</strong></th>
    </tr>
</table>

[https://cwe.mitre.org/data/definitions/527.html](https://cwe.mitre.org/data/definitions/527.html)