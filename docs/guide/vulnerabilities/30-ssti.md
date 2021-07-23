<a class="not-decorated-link" href="#/guide/vulnerabilities/overview.md">< Back to tests</a>

# Server Side Template Injection (SSTI)

<b>Severity</b>: <b><font color="#DB1E54">High</font></b><br>
<b>Test name</b>: Server Side Template Injection (SSTI)

<table id="simple-table">
    <tr>
        <th><strong>Summary</strong></th>
    </tr>
</table>

Some web applications use template engines to generate HTML pages. Server Side Template Injection allows an attacker to inject a malicious code into a template using user input. It is possible if the user input is inserted directly into a template which is stored on the server. As a result, the attacker is able to manipulate the template engine and take control of the server. 

<table id="simple-table">
    <tr>
        <th><strong>Impact</strong></th>
    </tr>
</table>

This vulnerability allows an attacker to:
* Gain sensitive information
* Execute shell commands


<table id="simple-table">
    <tr>
        <th><strong>Example</strong></th>
    </tr>
</table>

1. Vulnerable code stored on server side  (PHP):
    ```
    <?php
    $html = $twig->render("Hello " . $_REQUEST['name']);
    ```
2. Attack requests that lead to the template injection:
    ```
    https://www.{your_web_site}.com/?name={{5*5}}
    https://www.{your_web_site}.com/?name={{_self.env.registerUndefinedFilterCallback("exec")}}{{_self.env.getFilter("(ls -lah)")}}
    ```

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

* Do not insert user input in the templates directly. Pass user inputs into templates as parameters like (Twig):
```
<?php echo $twig->render("Hello {{ name }}", ['name' => $_REQUEST['name']]);
```
* Sanitize the input before passing it into the templates by removing unwanted and risky characters. This minimizes the vulnerabilities for any malicious probing of your templates. HTML and SSI Directive characters <code>< ! # = / . " - > { }</code> should be sanitized with a special sanitization function.
    * PHP:
    ```
    htmlspecialchars("<a href='test'>Test</a>");
    ```
    * NodeJS:
    ```
    const Entities = require('html-entities').AllHtmlEntities;
    const entities = new Entities();
    console.log(entities.encode('{{_self.env.registerUndefinedFilterCallback("exec")}}{{_self.env.getFilter("(ls -lah)")}}');
    ```
    * ASP.NET:
    ```
    System.Web.HttpUtility.HtmlEncode('{{_self.env.registerUndefinedFilterCallback("exec")}}{{_self.env.getFilter("(ls -lah)")}}')
    ```
* Revise the permissions policies for files and folders and set them stricter.
    * Files: 644 - Owner of the file has read and write access, while the group members and other users of the system only have read access.
    * Folders: 755 - Read and execute access for everyone and additionally write access for the owner.
    If direct usage of user input in the template cannot be avoided (for example, due to the specific business requirement to render certain attributes of a template), use it in the isolated sandbox.
* If direct usage of user input in the template cannot be avoided (for example, due to the specific business requirement to render certain attributes of a template), use it in the isolated sandbox.
    * Twig:
    ```   
    {% sandbox %}
        ...
    {% endsandbox %}
    ```


<table id="simple-table">
    <tr>
        <th><strong>Classifications</strong></th>
    </tr>
</table>

* CWE-74
* CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:H/A:N  


<table id="simple-table">
    <tr>
        <th><strong>References</strong></th>
    </tr>
</table>

* [https://www.owasp.org/index.php/Server-Side_Includes_(SSI)_Injection](https://www.owasp.org/index.php/Server-Side_Includes_(SSI)_Injection)
* [https://www.owasp.org/images/7/7e/Owasp_SSTI_final.pdf](https://www.owasp.org/images/7/7e/Owasp_SSTI_final.pdf)

<a class="not-decorated-link" href="#/guide/vulnerabilities/overview.md">< Back to tests</a>