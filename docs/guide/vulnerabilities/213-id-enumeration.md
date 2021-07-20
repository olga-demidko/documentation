# Enumerable Integer-Based ID

<b>Severity</b>: <b><font color="#1B49D4">Low</font></b><br>
<b>Test name</b>: User ID Enumeration

<table id="simple-table">
    <tr>
        <th><strong>Summary</strong></th>
    </tr>
</table>

An enumeration attack allows an attacker to check whether a user exists in the system by looking for differences in the server response based on the validity of submitted credentials/user's information. That will not allow the attackers to log in to the system immediately, but it gives them a part of the necessary information. 
The main targets for this attack are places where the attacker can enter data about an assumed user and make conclusions depending on the response from the server. The most vulnerable areas for enumeration are a site login page and the "forgot password" functionality. 

Revealing the vulnerability:
1. Submit user’s information via one of the pages / API.
2. Analyze the response from the server. Find differences in the response for the valid and invalid request data.

<table id="simple-table">
    <tr>
        <th><strong>Impact</strong></th>
    </tr>
</table>

* Data leakage
* Access to unauthorized information



<table id="simple-table">
    <tr>
        <th><strong>Example</strong></th>
    </tr>
</table>

**Example 1:**
1. On the login page, the attacker enters one of the assumed usernames and any password to submit the login request.
2. If the server responds differently depending on the entered username, the attacker will be able to conclude whether a user with the corresponding username exists in the system:
    * The response from the server looks like _"Login failed, invalid username"_, the attacker concludes that this username does not exist in the system.
    * The response from the server looks like _"Login failed, invalid password"_, the attacker concludes that this username exists in the system.

**Example 2:**
1. On the "forgot password" page, the attacker enters one of the assumed usernames to submit the password reset request.
2. If the server responds differently depending on the entered username, the attacker will be able to conclude whether a user with the corresponding username exists in the system:
    * The response from the server looks like _"This email address doesn't exist in our database"_, the attacker concludes that this username does not exist in the system.
    * The response from the server looks like _"We just sent you a password reset link"_, the attacker concludes that this username exists in the system.


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

* An application should respond (both HTTP and HTML) in a generic manner:
    * Using any of the authentication mechanisms (login, password reset or password recovery), an application must respond with a generic error message regardless of whether:
        * The user ID or password was incorrect.
        * The account does not exist.
        * The account is locked or disabled.
    * The account registration feature should also be taken into consideration, and the same approach of generic error message can be applied based on the case in which the user exists.

* Correct response examples:
    * Login: _"Login failed; Invalid username or password"_.
    * Password recovery: _"If that email address is in our database, we will send you an email to reset your password"_.
    * Account creation: _"A link to activate your account has been sent to the provided address"_.


<table id="simple-table">
    <tr>
        <th><strong>Classifications</strong></th>
    </tr>
</table>

* CWE-203
* CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N


<table id="simple-table">
    <tr>
        <th><strong>References</strong></th>
    </tr>
</table>

* [https://cwe.mitre.org/data/definitions/203.html](https://cwe.mitre.org/data/definitions/203.html)
* [https://owasp.org/www-project-web-security-testing-guide/latest/4-Web_Application_Security_Testing/03-Identity_Management_Testing/04-Testing_for_Account_Enumeration_and_Guessable_User_Account](https://owasp.org/www-project-web-security-testing-guide/latest/4-Web_Application_Security_Testing/03-Identity_Management_Testing/04-Testing_for_Account_Enumeration_and_Guessable_User_Account)