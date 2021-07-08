# JWT Role Bypass

<b>Severity</b>: <b><font color="red">High</font></b><br>
<b>Test name</b>: Broken JWT Authentication

<table id="simple-table">
    <tr>
        <th><strong>Summary</strong></th>
    </tr>
</table>
JSON Web Token (JWT) is an open standard that defines a compact and self-contained way for transmitting information as a JSON object securely between parties. This information can be verified and trusted because it is digitally signed. JWTs can be signed using a secret (with the HMAC algorithm) or a public/private key pair using RSA. 

JWT is used to carry information related to the identity and characteristics (claims) of a client. This information is signed by the server in order to detect whether the information has been tampered with after it was sent to the client. The token is created during authentication and verified by the server before any processing.

The tokens consist of three parts (each of them is **Base64Url** encoded) separated by dots ("xxxxx.yyyyy.zzzzz"):

* **Header** typically consists of two parts: the type of the token, which is JWT, and the signing algorithm being used, such as HMAC SHA256 or RSA.

```js
{
  "alg": "HS256",
  "typ": "JWT"
}
```


* **Payload** contains claims. The claims are statements about an entity (typically, the user) and additional data. There are three types of claims: registered, public and private.


```js
{
  "sub": "1234567890",
  "name": "John Doe",
  "admin": true
}
```
* **Signature** is used to verify the message which has not been changed along the way. In case of the tokens signed with a private key, it can also verify that the sender of the JWT is who it says they are.


```js

HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  secret)
```

<table id="simple-table">
    <tr>
        <th><strong>Impact</strong></th>
    </tr>
</table>

Improper validation of JWT or usage of JWT operation scheme with a known vulnerability may lead to payload tampering and, as a result, to unauthorized access.

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

* Use a JWT library that is not exposed to the known vulnerabilities. Use the latest version of the JWT library you have chosen and update it regularly. References can be found at [https://jwt.io/#libraries-io](https://jwt.io/#libraries-io).
* During token validation, explicitly request for the expected algorithm to be used (restrict accepted algorithms to the ONE you want to use):

```

// HMAC key - Block serialization and storage as String in JVM memory
private transient byte[] keyHMAC = ...;
...

//Create a verification context for the token requesting
//explicitly the use of the HMAC-256 hashing algorithm
JWTVerifier verifier = JWT.require(Algorithm.HMAC256(keyHMAC)).build();

//Verify the token, if the verification fail then a exception is throwed
DecodedJWT decodedToken = verifier.verify(token);
```
* Restrict URLs of any JWKS/X509 certificates.
* Verify all tokens before processing the payload data. Before the token is validated, its contents cannot be trusted.
* Use the strongest signing process you can afford the CPU time for.
* Use strong keys/secrets and asymmetric keys if the tokens are used across more than one server. 


<table id="simple-table">
    <tr>
        <th><strong>Classifications</strong></th>
    </tr>
</table>

* CWE-287
* CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N


<table id="simple-table">
    <tr>
        <th><strong>References</strong></th>
    </tr>
</table>

[https://cheatsheetseries.owasp.org/cheatsheets/SAML_Security_Cheat_Sheet.html](https://cheatsheetseries.owasp.org/cheatsheets/SAML_Security_Cheat_Sheet.html)