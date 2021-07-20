# LDAP Injection

<b>Severity</b>: <b><font color="#DB1E54">High</font></b><br>
<b>Test name</b>: LDAP Injection

<table id="simple-table">
    <tr>
        <th><strong>Summary</strong></th>
    </tr>
</table>

LDAP injection is an attack used to exploit web applications that construct LDAP statements based on improperly sanitized user input. An application on the server side can send a request to enter the LDAP server with specific filter parameters. The LDAP server is a gateway to sensitive and valuable information such as user credentials, staff names and roles, networks, devices, phone numbers, etc. 


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
        <th><strong>Example</strong></th>
    </tr>
</table>

**Example 1**
1. In a web application, we have the following LDAP statement for authorization:
```
(&(user=username)(password=pass))
```

2. If an attacker sends `user=realUserName)(&)` and any value for password like:
```
(&(user=realUserName)(&))(password=randomPassword))
```

3. LDAP will process only this part `(&(user=realUserName)(&)`. This query is always correct, so the attacker enters the system without a true password.

**Example 2**
1. There is a LDAP statement where `resource1` and  `resource2` are input parameters:

```
(|(resource=resource1)(resource=resource2))
```

2. The LDAP query was changed like: `resource = resource1)(userId=*)`

```
(|(resource=resource1)(userId=*))(resource=resource2))
```

3. The server will ignore the part `(resource=resource2)` (only the first complete filter is processed). As a result, it will list all the resources that correspond to “resource1" and additionally all user objects. 




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
* To decrease the potential damage caused by a successful LDAP injection, you should minimize the privileges assigned to the LDAP binding account in your environment.

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

* [https://cwe.mitre.org/data/definitions/90.html](https://cwe.mitre.org/data/definitions/90.html)
* [https://www.owasp.org/index.php/LDAP_injection](https://www.owasp.org/index.php/LDAP_injection)
* [https://www.neuralegion.com/blog/ldap-injection/](https://www.neuralegion.com/blog/ldap-injection/)