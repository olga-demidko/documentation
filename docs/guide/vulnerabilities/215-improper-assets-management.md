# Improper Assets Management

<b>Severity</b>: <b><font color="orange">Medium</font></b><br>
<b>Test name</b>: Improper Assets Management

<table id="simple-table">
    <tr>
        <th><strong>Summary</strong></th>
    </tr>
</table>

Improper Assets Management vulnerability allows an attacker to get access to old API version. It is possible if a new API version is released, but the old one is left to keep backward compatibility or by mistake. In addition, it can be a case if unknown or forgotten API requests are not documented, so they are typically not monitored or protected by security tools. 
It may also occur if APIs that are in development have access to data in the production environment. For example, if a user is authenticated in a staging environment and may have access to production APIs with the same authentication token.

<table id="simple-table">
    <tr>
        <th><strong>Impact</strong></th>
    </tr>
</table>

Improper Assets Management allows the attacker to:
* Gain sensitive information
* Get full access to the server through old vulnerable versions of APIs


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

* Separate data for production and non-production environments.
* Remove old API or limit access to it if a newer version is released. Force all clients to move to the latest version if possible.
* All API requests should be documented: Hosts, API endpoint, HTTP method, API parameters and their data types, permitted user roles.
* Each API endpoint should have limited access if the endpoint is not public.
* API security tools must be able to analyze all API traffic and continuously discover APIs.


<table id="simple-table">
    <tr>
        <th><strong>Classifications</strong></th>
    </tr>
</table>

* CWE-284
* CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N

<table id="simple-table">
    <tr>
        <th><strong>References</strong></th>
    </tr>
</table>

* [https://raw.githubusercontent.com/OWASP/API-Security/master/2019/en/dist/owasp-api-security-top-10.pdf](https://raw.githubusercontent.com/OWASP/API-Security/master/2019/en/dist/owasp-api-security-top-10.pdf)

