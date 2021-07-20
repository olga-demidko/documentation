# LDAP Error

<b>Severity</b>: <b><font color="#DE8800">Medium</font></b><br>
<b>Test name</b>: LDAP Injection

<table id="simple-table">
    <tr>
        <th><strong>Summary</strong></th>
    </tr>
</table>

LDAP Injection is an attack used to exploit web applications that construct LDAP statements based on improperly sanitized user input. 
An application on the server side can send a request to enter the LDAP server with specific filter parameters. The  LDAP server is a gateway to sensitive and valuable information such as user credentials, staff names and roles, networks, devices, phone numbers, etc. 
LDAP Error is the vulnerability type which relies on error messages thrown by the server to obtain information about the targets. Using the error message, an attacker can reveal the structure and change the construction of the LDAP statement so that they can successfully perform the LDAP injection.


<table id="simple-table">
    <tr>
        <th><strong>Impact</strong></th>
    </tr>
</table>

The LDAP injections may lead to the following:
* Bypass authentication. An attacker can gain access without password checking.
* Information disclosure. An attacker can gain a list of some resources or users.
* Attribute disclosure. An attacker can check if an attribute exists.

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

* Escape all variables using the right LDAP encoding function.
* Wherever possible, use the white list approach for input validation. Additional input validation can be used to detect unauthorized input before it is passed to the LDAP query.
* Use the frameworks that automatically protect against the LDAP Injection (like LINQtoAD for .NET).
* To decrease the potential damage of a successful LDAP injection, you should minimize the privileges assigned to the LDAP binding account in your environment.



<table id="simple-table">
    <tr>
        <th><strong>Classifications</strong></th>
    </tr>
</table>

* CWE-90
* CVSS:3.1/AV:N/AC:L/PR:L/UI:N/S:U/C:L/I:N/A:L

<table id="simple-table">
    <tr>
        <th><strong>References</strong></th>
    </tr>
</table>

* [https://www.owasp.org/index.php/LDAP_injection](https://www.owasp.org/index.php/LDAP_injection)
* [https://cwe.mitre.org/data/definitions/90.html](https://cwe.mitre.org/data/definitions/90.html)
* [https://cwe.mitre.org/data/definitions/116.html](https://cwe.mitre.org/data/definitions/116.html)