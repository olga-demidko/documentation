<!DOCTYPE html>
<html>
 <head>
  <meta charset="utf-8">
  <title>Кнопка</title>
 </head>
 <body> 
  <form>
   <p><input type="button" value=" Back to tests "></p>
  </form>
 </body>
</html>


# Sensitive Cookie Without HttpOnly Flag

<b>Severity</b>: <b><font color="#1B49D4">Low</font></b><br>
<b>Test name</b>: Cookie Security Check

<table id="simple-table">
    <tr>
        <th><strong>Summary</strong></th>
    </tr>
</table>

Web pages originally have no memory. Therefore, a website will treat the same user as a new visitor each time they navigate to another page of the site, or will define the current navigation as a new visit of the same user. 

Web session cookies enable the website to keep track of user's movement from page to page, so they do not get asked for the information they have already given to the site. The web session is a sequence of network HTTP request and response transactions associated with the same user. 

Web applications can create sessions to keep track of anonymous users after the very first user request. The most common example is the shopping cart feature of any e-commerce site. When a user (anonymous) visits one page of a catalog and selects some items, the session cookie remembers the user’s selection, so the shopping cart will have the items selected by the user. Without session cookies, if the user clicks “checkout", the new page does not recognize their activities on the prior pages, and the shopping cart is always left empty.

Additionally, web applications will use sessions after the user has authenticated. This ensures the ability to identify the user on any subsequent requests, apply security access controls and authorized access to the user’s private data, as well as to increase the usability of the application. Therefore, current web applications can provide session capabilities for both pre- and post-authentication.

<table id="simple-table">
    <tr>
        <th><strong>Impact</strong></th>
    </tr>
</table>

The disclosure, capture, prediction, brute force, or fixation of the session ID may lead to session hijacking (or sidejacking) attacks, where an attacker is able to fully impersonate a victim user in the web application. Usually, the attacker's goal is to get access to the web application as any valid or legitimate user.


<table id="simple-table">
    <tr>
        <th><strong>Location</strong></th>
    </tr>
</table>

* The issue can be found in the **source code** on the **server side**.
* The issue can be found in the **server configuration**.

<table id="simple-table">
    <tr>
        <th><strong>Remedy suggestions</strong></th>
    </tr>
</table>

1. **Protection of the entire information**. Session IDs and generation of identifiers (IDs or tokens) must meet the following properties:
    * **Session ID Name Fingerprinting**<br>
        The name used by the session ID should not be extremely descriptive and should not offer unnecessary details about the purpose and meaning of the ID. It is recommended to change the default session ID name of the web development framework to a generic name, such as "id". The cookies should be hard to find.
    * **Session ID Length**<br>
        The session ID must be long enough to prevent brute force attacks, where an attacker can go through the whole range of ID values and verify the existence of valid sessions. The session ID length must be at least 128 bits (16 bytes).
    * **Session ID Entropy (robustness)**<br> 
        The session ID must be unpredictable (random enough) to prevent guessing attacks, where an attacker is able to guess or predict the ID of a valid session through statistical analysis techniques. Additionally, a random session ID is not enough, it must also be unique to avoid duplicated IDs. 
    * **Session ID Content**<br>
        The session ID content must be meaningless to prevent information disclosure attacks, where an attacker is able to decode the contents of the ID and extract details of the user, the session, or the inner workings of the web application. The attacker should not be able to perform a statistical analysis on a dataset to understand how it is generated. The session ID must simply be an identifier on the client side, and its value must never include sensitive information.

2. **Protection of access to information**. The session management implementation defines the exchange mechanism that will be used between the user and the web application to share and continuously exchange the session ID.
    * **Built-in Session Management Implementations**<br>
        Web development frameworks, such as J2EE, ASP .NET, PHP, and others, provide their own session management features and associated implementation. It is recommended to use these built-in frameworks versus building a homemade one from scratch.
    * **Used vs. Accepted Session ID Exchange Mechanisms**<br>
        A web application should use cookies for session ID exchange management. If a user submits a session ID through a different exchange mechanism, such as a URL parameter, the web application should avoid accepting it as part of a defensive strategy to stop session fixation.
    * **Transport Layer Security**<br>
        In order to protect the session ID exchange from active eavesdropping and passive disclosure in the network traffic, it is essential to use an encrypted HTTPS (TLS) connection for the entire web session.
    * **Cookie attributes**<br>
        * The `Secure` cookie attribute instructs web browsers to only send the cookie through an encrypted HTTPS (SSL/TLS) connection. It is necessary to configure (enable) the `Secure` attribute for session cookies.
        * The `HttpOnly` cookie attribute instructs web browsers not to allow client-side scripts (for example, JavaScript) an ability to access the cookies. It is necessary to configure (enable) the `HttpOnly` attribute for session cookies.
        * The `SameSite` cookie attribute allows a server to define a cookie making it impossible for the browser to send this cookie along with cross-site requests. Consider configuring (enable) the `SameSite` attribute for session cookies.


<table id="simple-table">
    <tr>
        <th><strong>Classifications</strong></th>
    </tr>
</table>

* CWE-539
* CVSS:3.1/AV:N/AC:L/PR:N/UI:R/S:U/C:H/I:H/A:L

<table id="simple-table">
    <tr>
        <th><strong>References</strong></th>
    </tr>
</table>

https://developer.mozilla.org/en-US/docs/Glossary/Session_Hijacking