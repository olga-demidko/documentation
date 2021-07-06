# Broken JWT Authentication

<b>Severity</b>: <b><font color="red">High</font></b><br>
<b>Test name</b>: Broken JWT Authentication

<table id="simple-table">
    <tr>
        <th><strong>Summary</strong></th>
    </tr>
</table>
JSON Web Token (JWT) is an open standard that defines a compact and self-contained way for transmitting information as a JSON object securely between parties. This information can be verified and trusted because it is digitally signed. JWTs can be signed using a secret (with the HMAC algorithm) or a public/private key pair using RSA. 

JWT is used to carry information related to the identity and characteristics (claims) of a client. This information is signed by the server in order to detect whether the information has been tampered with after it was sent to the client. The token is created during authentication and verified by the server before any processing.

The tokens consist of three parts (each of them is **Base64Url** encoded) separated by dots ("xxxxx.yyyyy.zzzzz”):

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
* **Signature** is used to verify the message which has not been changed along the way. In case of the tokens signed with a private key, it can also verify that the sender of the JWT is who it says it is.


```js

HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  secret)
```

<p>

<table id="simple-table">
    <tr>
        <th><strong>Impact</strong></th>
    </tr>
</table>

This vulnerability allows an attacker to:
* Gain Privileges or Assume Identity
* Bypass Protection Mechanism
* Bypass Athentication Mechanism

<p>

<table id="simple-table">
    <tr>
        <th><strong>Example of JWT</strong></th>
    </tr>
</table>

eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9.dyt0CoTl4WoVjAHI9QCwSKhl6d_9rhM3NrXuJttkao

To verify the signature, you should know which algorithm is used to generate it. For that, you may use the "alg" field from the "header". The problem is that the token has not been validated yet, so the "header" has neither been validated yet (that is why we cannot trust the "header" yet). This creates an awkward situation: in order to validate the token, we have to allow attackers to select which method you are going to use to verify the signature. 

The "none" algorithm is a curious addition to JWT. It is intended to be used for situations where the integrity of the token has already been verified. Unfortunately, **some libraries treat the tokens signed with the “none” algorithm as a valid token with a verified signature**. As a result, anyone can create their own "signed" tokens with whatever payload they want, allowing an arbitrary account to access some systems. Composing such a token is easy. Modify the above example header to contain "alg": "none" instead of HS256. Make any desired changes to the payload. Use an empty signature (signature = "").

<p>

<table id="simple-table">
    <tr>
        <th><strong>Location</strong></th>
    </tr>
</table>

The issue can be found in the **source code** on the **server side**.

<p>

<table id="simple-table">
    <tr>
        <th><strong>Remedy suggestions</strong></th>
    </tr>
</table>

* Use a JWT library that is not exposed to this vulnerability. You can find the references at [https://jwt.io/#libraries-io](https://jwt.io/#libraries-io) .
* During the token validation, explicitly request for the expected algorithm to be used (restrict all accepted algorithms to the ONE you want to use). 

```
// HMAC key - Block serialization and storage as String in JVM memory
private transient byte[] keyHMAC = ...;
...

//Create a verification context for the token requesting
//explicitly the use of the HMAC-256 hashing algorithm
JWTVerifier verifier = JWT.require(Algorithm.HMAC256(keyHMAC)).build();

//Verify the token, if the verification fails, then an exception is thrown.
DecodedJWT decodedToken = verifier.verify(token);
```

<p>

<table id="simple-table">
    <tr>
        <th><strong>Classifications</strong></th>
    </tr>
</table>
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:H/A:N

<p>

<table id="simple-table">
    <tr>
        <th><strong>References</strong></th>
    </tr>
</table>

[https://cheatsheetseries.owasp.org/cheatsheets/JSON_Web_Token_Cheat_Sheet_for_Java.html](https://cheatsheetseries.owasp.org/cheatsheets/JSON_Web_Token_Cheat_Sheet_for_Java.html)
