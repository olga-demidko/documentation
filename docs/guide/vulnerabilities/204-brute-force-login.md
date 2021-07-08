# Brute Force Login

<b>Severity</b>: <b><font color="red">High</font></b><br>
<b>Test name</b>: Brute Force Login

<table id="simple-table">
    <tr>
        <th><strong>Summary</strong></th>
    </tr>
</table>

A brute-force attack is an attempt of an attacker to discover a password by systematically trying every possible combination of letters, numbers, and symbols until revealing the correct combination. An attacker can always discover a password through the brute-force attack, but the downside is that it could take years to find it (depending on the password length and complexity, there could be trillions of possible combinations).

<table id="simple-table">
    <tr>
        <th><strong>Impact</strong></th>
    </tr>
</table>

This vulnerability allows an attacker to get access to privileged information.

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

* Review the existing Password Policy and, if necessary, increase the credentials complexity (length, lower/upper case, special symbols) to make brute-forcing a more time-consuming operation. A "strong" password policy makes it difficult or even impossible for one to guess the password through either manual or automated means.
* Review the existing Password Policy and, if necessary, increase the credentials complexity (length, lower/upper case, special symbols) to make brute-forcing a more time-consuming operation. A "strong" password policy makes it difficult or even impossible for one to guess the password through either manual or automated means.
* Multi-factor authentication (MFA) is by far the best defence against the majority of password-related attacks, including  the brute-force attacks. It should be implemented wherever possible; however, depending on the audience of the application, it may not be practical or feasible to enforce the use of MFA. 
* CAPTCHA can help prevent automated login attempts against accounts. However, many CAPTCHA implementations have weaknesses that can be solved using automated techniques or outsourced services. The use of CAPTCHA should be considered as a defence-in-depth control to make the brute-force attacks more time-consuming and expensive, rather than as a preventative.


<br>

<table id="simple-table">
    <tr>
        <th><strong>Classifications</strong></th>
    </tr>
</table>

* CWE-307
* CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N 


<table id="simple-table">
    <tr>
        <th><strong>References</strong></th>
    </tr>
</table>

* [https://en.wikipedia.org/wiki/Brute-force_attack](https://en.wikipedia.org/wiki/Brute-force_attack)
* [https://owasp.org/www-community/controls/Blocking_Brute_Force_Attacks](https://owasp.org/www-community/controls/Blocking_Brute_Force_Attacks)
