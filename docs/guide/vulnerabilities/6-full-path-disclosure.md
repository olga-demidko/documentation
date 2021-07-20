# Full Path Disclosure

<b>Severity</b>: <b><font color="#DE8800">Medium</font></b><br>
<b>Test name</b>: Full Path Disclosure

<table id="simple-table">
    <tr>
        <th><strong>Summary</strong></th>
    </tr>
</table>

 All attacks get started with preparation and analysis of a victim’s server and used software. Attackers use different techniques to lead a victim’s application to crash or incorrect behavior. Due to that, the shown error message may contain information about a full path to the file where the error happened. In addition, different search engines can be used to find errors by special keywords with a combination of the victim’s domain name. 


<table id="simple-table">
    <tr>
        <th><strong>Impact</strong></th>
    </tr>
</table>

Full Path Disclosure vulnerability allows an attacker to get the following information:
* Operating system type
* Web root folder
* Folder structure
* Used third party libraries and their versions
* Server software and the software version



<table id="simple-table">
    <tr>
        <th><strong>Example</strong></th>
    </tr>
</table>

**Example 1:** Changing the expected scalar type to array
* Expected request: `https://your_web-site.com?page=about`
* Actual request: `https://your_web-site.com?page[]=about`<br>
An attacker can also change the cookie value for `your_web-site.com`

**Example 2:**
"Googling" errors on `your_web-site.com`<br>
Search requests: 
* `"mysql_connect" site:your_web-site.com`
* `"failed to open stream" site:your_web-site.com`
* `"headers already sent" site:your_web-site.com`

With the detailed information about errors/warnings, an attacker is able to find vulnerabilities for any component of the victim’s application. In combination with other vulnerabilities (for example, SQL Injection, File Inclusion), it's possible to steal configuration files or even replace them (for example, to use another database).

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


* Disable showing errors to users. The errors should be logged to files or a special logging system. Instead of general error information, a special HTML page can be shown.
ASP.NET:
```
<customErrors defaultRedirect="GenericError.htm" mode="On">
  <error statusCode="500" redirect="InternalError.htm"/>
</customErrors>
```
* Avoid showing debug information / sensitive logs to users. Consider using a special log management software to standardize logs information.
* Deny access for search engines to the URLs which should not be indexed (for example, API endpoints). Here is an example of the _"robots.txt"_ file (blocks all bots for all pages):
```
User-agent: *
Disallow: /
```
* Minimize the usage of third-party libraries. Keep the latest versions of the used third-party libraries and system components.



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

* [https://cwe.mitre.org/data/definitions/200.html](https://cwe.mitre.org/data/definitions/200.html)
* [https://www.owasp.org/index.php/Full_Path_Disclosure](https://www.owasp.org/index.php/Full_Path_Disclosure)
