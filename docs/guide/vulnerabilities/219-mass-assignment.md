# Mass Assignment

<b>Severity</b>: <b><font color="#DE8800">Medium</font></b><br>
<b>Test name</b>: Mass Assignment

<table id="simple-table">
    <tr>
        <th><strong>Summary</strong></th>
    </tr>
</table>

Some software frameworks support the Massive Assignment feature. This is a convenient way of populating an entity with user inputs using a single line of code. It populates the attributes of the entity by assigning the input data directly to the corresponding properties. 
Mass Assignment vulnerability allows an attacker to modify object properties, which are not supposed to be changed by the user, by assigning user input data (for example, JSON) without proper validation.

<table id="simple-table">
    <tr>
        <th><strong>Impact</strong></th>
    </tr>
</table>

This vulnerability may lead to:
* Privilege escalation. The attacker is able to change permission related properties
* Data tampering by changing process related properties (for example, total price)
* Bypass of security mechanisms

<table id="simple-table">
    <tr>
        <th><strong>Example (privilege escalation)</strong></th>
    </tr>
</table>

1. The source code of User entity in the application:
    ```js
    <?php
    class User 
    {
        private string $email;
        private string $role;

        // Getter & setter 
        ...
    }
    ```
2. The request which changes the user's email:
```
PUT https://www.{your_web_site}.com/api/user/{user_id}
{"email": "new@mail.com"}
```
3. The attacker fulfills the request with the following payload:
```
{"email": "new@mail.com", "role": "SuperAdmin"}
```
4. If an API request is vulnerable to mass assignment, the attacker gets the Super Admin privilege.

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

* Avoid mass assignment data in your application if possible (avoid using functions that automatically bind a client’s input into code variables or internal objects). Instead of that, assign data for each property separately.
* Specify a whitelist of attributes / properties (safe attributes / properties) which can be modified by a client.
* Specify a blacklist of attributes / properties which cannot be modified by a client.
* Validate values for each attribute which is used in mass assignment. Explicitly define and enforce schemas for the input data  payloads.



<table id="simple-table">
    <tr>
        <th><strong>Classifications</strong></th>
    </tr>
</table>

* CWE-915
* CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N


<table id="simple-table">
    <tr>
        <th><strong>References</strong></th>
    </tr>
</table>

* [https://cwe.mitre.org/data/definitions/915.html](https://cwe.mitre.org/data/definitions/915.html) 
* [https://raw.githubusercontent.com/OWASP/API-Security/master/2019/en/dist/owasp-api-security-top-10.pdf](https://raw.githubusercontent.com/OWASP/API-Security/master/2019/en/dist/owasp-api-security-top-10.pdf)
* [http://blog.carnal0wnage.com/2011/12/insecure-object-mapping.html](http://blog.carnal0wnage.com/2011/12/insecure-object-mapping.html)
* [https://cheatsheetseries.owasp.org/cheatsheets/Mass_Assignment_Cheat_Sheet.html](https://cheatsheetseries.owasp.org/cheatsheets/Mass_Assignment_Cheat_Sheet.html)