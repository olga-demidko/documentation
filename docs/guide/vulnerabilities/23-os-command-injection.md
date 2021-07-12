# OS Command Injection

<b>Severity</b>: <b><font color="orange">Medium</font></b><br>
<b>Test name</b>: OS Command Injection

<table id="simple-table">
    <tr>
        <th><strong>Summary</strong></th>
    </tr>
</table>

Operating System Command Injection is a vulnerability that allows an attacker to execute operating system (OS) commands on the server that is running an application. The command injections are possible when an application passes unsafe user-supplied data (inputs, forms, cookies, HTTP headers, etc.) to a system shell. 

In this attack, the operating system commands supplied by the attacker are usually executed with the privileges of the vulnerable application. The ability to execute the operating system commands creates a major threat for the application and in most cases makes it completely compromised. In addition, an attacker can use that vulnerability to compromise other parts of the hosting infrastructure (other applications), exploiting trust relationships to pivot the attack to other systems.

<table id="simple-table">
    <tr>
        <th><strong>Impact</strong></th>
    </tr>
</table>

This vulnerability allows an attacker to execute unauthorized code or commands.

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

* Avoid using the entire OS commands for your code. We recommend that you use built-in library functions instead of the OS commands, as they cannot be manipulated to perform unintended tasks. For example, use `mkdir()` instead of `system("mkdir /dir_name")`.
* When your programming language / a built-in library function does not have a corresponding OS command, you will be forced to use the entire OS command. In such situations, the OS command needs to be sanitized before execution. Use the whitelist approach and enable execution only for the validated commands. The arguments should be validated as well.
    * Commands: whitelist approach
    * Arguments require the following validation:
        * Allow the white list approach for the input data: wherever the arguments are explicitly defined.
        * Use Regular Expression(s) to validate the input data: wherever a list of good, allowed characters and the maximum length of the string are defined. Ensure that the metacharacters like & | ; $ > < ` \ ! and white-spaces are not part of the Regular Expression. For example, the following regular expression only allows lowercase letters and numbers and does not include metacharacters. The length is also limited to 3-10 characters: <code>^[a-z0-9]{3,10}$</code>.


<table id="simple-table">
    <tr>
        <th><strong>Classification</strong></th>
    </tr>
</table>

* CWE-78
* CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:N

<table id="simple-table">
    <tr>
        <th><strong>References</strong></th>
    </tr>
</table>

* [https://www.owasp.org/index.php/OS_Command_Injection_Defense_Cheat_Sheet](https://www.owasp.org/index.php/OS_Command_Injection_Defense_Cheat_Sheet)
* [https://cwe.mitre.org/data/definitions/78.html](https://cwe.mitre.org/data/definitions/78.html)
* [https://www.neuralegion.com/operating-system-command-injection-vulnerabilities-and-the-danger-they-present/](https://www.neuralegion.com/operating-system-command-injection-vulnerabilities-and-the-danger-they-present/)