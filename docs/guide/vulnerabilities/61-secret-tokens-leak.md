# Secret Tokens Leak

<b>Severity</b>: <b><font color="orange">Medium</font></b><br>
<b>Test name</b>: Secret Tokens Leak

<table id="simple-table">
    <tr>
        <th><strong>Summary</strong></th>
    </tr>
</table>

Secret tokens, passwords, API keys, and other sensitive information are used in authentication processes and allow users to access a website, an application or API. After verifying the secret information, a user can get permitted for this secret access to the application. 

Since it is convenient to store sensitive information in a repository with easy access for development, some applications hardcode secret tokens in their source code. This allows an attacker to gain such sensitive information using certain techniques and take control over the systems the tokens give access to. For example, if configuration files are stored in a public Git repository or have even been committed, the attacker is able to find them in GitHub (or any other Web UI for public Git repositories).

Another case is when an attacker decompiles an Android application and recognizes secret tokens in the code. Afterward, with the enumeration of API endpoints, the attacker is able to compromise API requests.


<table id="simple-table">
    <tr>
        <th><strong>Impact</strong></th>
    </tr>
</table>

Secret Tokens Leak allows the attacker to perform the following:
* Get administrative access to a system and manipulate data or manage the account
* Create a new privileged user and use it in the future
* Gain personal information of the system members
* Denial of service upon executing different requests with high frequency



<table id="simple-table">
    <tr>
        <th><strong>Location</strong></th>
    </tr>
</table>

* The issue can be found in the **source code** on the **server side**.
* The issue can be found in the **source code** on the **client side**.

<table id="simple-table">
    <tr>
        <th><strong>Remedy suggestions</strong></th>
    </tr>
</table>

* Secret Tokens should never be hardcoded in the source code of your application.
* Store Secret Tokens in environment variables if possible. If environment variables are being used, make sure to only read them in a single config file.
* Do not store configuration files in a source code repository. Such files have to be stored separately and be uploaded or created in the application during the release/deployment process.
* If secure information is stored in your application, it should be encrypted. 


<table id="simple-table">
    <tr>
        <th><strong>Classifications</strong></th>
    </tr>
</table>

* CWE-200
* CVSS:3.1/AV:N/AC:H/PR:N/UI:N/S:U/C:N/I:L/A:N 


<table id="simple-table">
    <tr>
        <th><strong>References</strong></th>
    </tr>
</table>

[https://cheatsheetseries.owasp.org/cheatsheets/Key_Management_Cheat_Sheet.html](https://cheatsheetseries.owasp.org/cheatsheets/Key_Management_Cheat_Sheet.html)

