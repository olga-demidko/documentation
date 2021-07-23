<a class="not-decorated-link" href="#/guide/vulnerabilities/overview.md">< Back to tests</a>

# Directory Listing

<b>Severity</b>: <b><font color="#DE8800">Medium</font></b><br>
<b>Test name</b>: Directory Listing

<table id="simple-table">
    <tr>
        <th><strong>Summary</strong></th>
    </tr>
</table>

Directory Listing vulnerability allows showing a list of directories and files on the server side for a directory path specified in the URL. The web server on the victim site can be configured to list the directory content if an index file (such as _"index.html"_, _"index.php"_, _"default.jsp"_) does not exist. Even when the directory listing is disabled, an attacker is able to use search engines with a combination of the victim’s domain name to find the directory content for the target path which had previously enabled the directory listing setting. In addition, an attacker may guess the location of sensitive files using automated tools.


<table id="simple-table">
    <tr>
        <th><strong>Impact</strong></th>
    </tr>
</table>

This vulnerability allows an attacker to:
* Expose directory architecture of the web application
* Get file information (filename, creation time, size)
* Gain source code of your application or configuration files
* Determine used third party libraries and their versions
* Download logs or database dumps


<table id="simple-table">
    <tr>
        <th><strong>Example</strong></th>
    </tr>
</table>

1. The directory listing is enabled on the web server where your website is located. The _"config"_ folder is in the web root folder and does not have an index file. 
2. A user makes the following request: 
```
https://www.{your_web_site}.com/config
```

3. The response shows the directory content of the _"config"_ folder :
```
.git/                   2021-05-01 17:00  -
environment/            2021-05-01 17:00  -
db.php                  2021-05-01 17:00  333
params.php              2021-05-01 17:00  3.3K
db_dump.sql             2021-05-01 17:00  300K
install.log             2021-05-01 17:00  30M
```


<table id="simple-table">
    <tr>
        <th><strong>Location</strong></th>
    </tr>
</table>

The issue can be found in the **server configuration**.

<table id="simple-table">
    <tr>
        <th><strong>Remedy suggestions</strong></th>
    </tr>
</table>

* Disable the directory listing setting on your web server by changing the web server configuration.
    * Apache
    ```   
    <Directory /var/www/your_web_site.com>
        Options -Indexes
    </Directory>
    ```
    * Nginx
    ```     
    location /var/www/your_web_site.com {
        autoindex off;
    }
    ```
* Change the directory structure and move sensitive files (configs, source code, logs, dumps) above the web root folder of the web application.
* If it is impossible to disable the directory listing, then put an index file (such as _"index.htm"_) into each directory which is below the web root folder, so your web server will display this file instead of displaying the directory content.




<table id="simple-table">
    <tr>
        <th><strong>Classification</strong></th>
    </tr>
</table>

* CWE-548
* CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N

<table id="simple-table">
    <tr>
        <th><strong>References</strong></th>
    </tr>
</table>

* [https://cwe.mitre.org/data/definitions/548.html](https://cwe.mitre.org/data/definitions/548.html)
* [https://www.owasp.org/index.php/Top_10-2017_A6-Security_Misconfiguration](https://www.owasp.org/index.php/Top_10-2017_A6-Security_Misconfiguration)

<a class="not-decorated-link" href="#/guide/vulnerabilities/overview.md">< Back to tests</a>