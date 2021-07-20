# Default Login Location

<b>Severity</b>: <b><font color="#1B49D4">Low</font></b><br>
<b>Test name</b>: Default Login Location

<table id="simple-table">
    <tr>
        <th><strong>Summary</strong></th>
    </tr>
</table>

Some web applications have an administrative login section that allows administrating the application content. Default Login Location vulnerability means that an attacker is able to get control over such a section without authentication or via authorization with the default credentials. It is possible if managing interfaces are not properly protected from unauthorized access or the default password has not been changed (the credentials have not been removed).

<table id="simple-table">
    <tr>
        <th><strong>Impact</strong></th>
    </tr>
</table>

Default Login Location vulnerability opens access for attackers to:
* User account provisioning
* Website design and layout
* Data manipulation
* Configuration changes

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

* Administrative section must have authentication. That means each action in that section should be authenticated.
* URL for the login form should not be shown on your public website.
* Default Login Location should be changed if possible.
* Administrative section should be closed for search bots. Example of `robots.txt`:

```
User-agent: *
Disallow: /admin
```

* Comments and links with the information about the default login form should be removed from the HTML code shown by the client application.
* Remove the default credentials or change the password.
* Enable Brute Force Protection for the login form.

<table id="simple-table">
    <tr>
        <th><strong>Classifications</strong></th>
    </tr>
</table>

* CWE-287
* CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N

<table id="simple-table">
    <tr>
        <th><strong>References</strong></th>
    </tr>
</table>

* [https://www.owasp.org/index.php/Top_10-2017_A6-Security_Misconfiguration](https://www.owasp.org/index.php/Top_10-2017_A6-Security_Misconfiguration)
* [https://www.owasp.org/index.php/Enumerate_Infrastructure_and_Application_Admin_Interfaces_(OTG-CONFIG-005)](https://www.owasp.org/index.php/Enumerate_Infrastructure_and_Application_Admin_Interfaces_(OTG-CONFIG-005))
