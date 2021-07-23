<a class="not-decorated-link" href="#/guide/vulnerabilities/overview.md">< Back to tests</a>

# Email Header Injection

<b>Severity</b>: <b><font color="#DE8800">Medium</font></b><br>
<b>Test name</b>: Email Header Injection

<table id="simple-table">
    <tr>
        <th><strong>Summary</strong></th>
    </tr>
</table>

Some web applications allow users to send email messages via contact forms to defined recipients. In most cases, such contact form scripts set headers. Afterwards, the headers are converted into SMTP commands, which are then processed by the SMTP server.

Email Header Injection allows an attacker to insert additional malicious headers into the email message via unsafe user input. As a result, these headers will be converted into SMTP commands and processed by the SMTP server. 


<table id="simple-table">
    <tr>
        <th><strong>Impact</strong></th>
    </tr>
</table>

This vulnerability may lead to:
* Sending spam emails.
* Phishing and spoofing attacks. The recipient is made to believe that the email is legitimate. The email usually redirects the victim to a malicious website, which then steals their credentials or infects their computer with malware (via a drive-by-download).
* Denial of Service if the attacker sends a huge amount of emails, so the SMTP server can be overloaded.

<table id="simple-table">
    <tr>
        <th><strong>Example of a spam email</strong></th>
    </tr>
</table>

1. Let’s imagine the following code is used on the server side for sending an email message:

```js
<?php
if(!empty($_POST['name'])) {
  $name = $_POST['name'];
  $email = $_POST['email'];
  $message = $_POST['message'];
  $subject = 'Contact form request';
  #: Set headers
  $headers = "From: $name \n" .
  "Reply-To: $email";
  mail('root@localhost', $subject, $message, $headers); 
}
```

2. Expected request example:

```js
POST /contact.php HTTP/1.1
Host: www.{your_web_site}.com
Payload:
  name=Test User
  email=test.user@test.com
  message=Hello! This is a test message.
```
3. An attacker can send the following request:

```js
POST /contact.php HTTP/1.1
Host: www.{your_web_site}.com
Payload:
  name=Best Seller\nbcc: anyone@mail.com
  email=no-reply@mail.com
  message=Buy my awesome product!
```
4. As a result, the attacker can send a large number of messages anonymously. The attacker may also send phishing emails, where the recipient believes that these messages are originating from a trusted source (your website).

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

* Sanitize user input with special functions according to your programming language. In particular, input containing newlines and carriage returns should be rejected.
* Use certain correct types for supplied user input such as `string`, `float` or `int`. If your application expects an email address, it should be validated with Email pattern.
* Alternatively, consider switching to an email library that automatically prevents such attacks. Use the latest version and upgrade your email library periodically.


<br>

<table id="simple-table">
    <tr>
        <th><strong>Classifications</strong></th>
    </tr>
</table>

* CWE-20
* CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:C/C:N/I:L/A:N  


<table id="simple-table">
    <tr>
        <th><strong>References</strong></th>
    </tr>
</table>

* [https://capec.mitre.org/data/definitions/41.html](https://capec.mitre.org/data/definitions/41.html)
* [https://cwe.mitre.org/data/definitions/20.html](https://cwe.mitre.org/data/definitions/20.html)
* [https://sites.cs.ucsb.edu/~chris/research/doc/sac18_email.pdf](https://sites.cs.ucsb.edu/~chris/research/doc/sac18_email.pdf)
* [https://security.elarlang.eu/cve-2016-4803-dotcms-email-header-injection-vulnerability-full-disclosure.html](https://security.elarlang.eu/cve-2016-4803-dotcms-email-header-injection-vulnerability-full-disclosure.html)


<a class="not-decorated-link" href="#/guide/vulnerabilities/overview.md">< Back to tests</a>