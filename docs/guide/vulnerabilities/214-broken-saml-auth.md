<a class="not-decorated-link" href="#/guide/vulnerabilities/overview.md">< Back to tests</a>

# Broken SAML Authentication

<b>Severity</b>: <b><font color="#DB1E54">High</font></b><br>
<b>Test name</b>: Broken SAML Authentication

<table id="simple-table">
    <tr>
        <th><strong>Summary</strong></th>
    </tr>
</table>
The Security Assertion Markup Language (SAML) is an open standard for exchanging authorization and authentication information. The attack surface for SAML authentication is extensive, mostly due to the fact that SAML is XML-based. Combined with the high complexity of the <a href="http://docs.oasis-open.org/security/saml/v2.0/saml-profiles-2.0-os.pdf">SAML specification</a> and the number of parties involved in establishing authentication, we get what often feels like a big ball of mud and all the accompanying implications.

 Most SAML SSO security vulnerabilities are introduced by Service Providers (SPs) improperly validating and processing SAML responses received from Identity Providers (IdPs). To build SAML SSO safely and securely in-house requires significant buy-in and investment by teams. If not done right, you expose your application and your customers to potentially huge security risks.

<table id="simple-table">
    <tr>
        <th><strong>Impact</strong></th>
    </tr>
</table>

This vulnerability allows an attacker to:
* Gain privileges or assume identity
* Bypass protection mechanism
* Bypass athentication mechanism

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

It is necessary to implement the authorization and authentication process according to the SAML specification. The following measures should be taken:
* Validate Message Confidentiality and Integrity:
    * TLS 1.2 is the most common solution to guarantee message confidentiality and integrity at the transport layer.
* Validate Protocol Usage:
    * Define requirements and validate `AuthnRequest` and `Response`.
* Validate Signatures:
    * Always perform schema validation on the XML document. 
    * Securely validate the digital signature.
    * Avoid signature-wrapping attacks.
* Validate Protocol Processing Rules:
    * Validate `AuthnRequest` processing rules.
    * Validate `Response` processing rules.
* Validate Security Countermeasures. Revisit each security threat that exists within the SAML Security document and assert you have applied the appropriate countermeasures for threats that may exist for your particular implementation. Additional countermeasures considered should include:
    * Prefer IP Filtering when appropriate.
    * Prefer short lifetimes on the SAML `Response`.
    * Prefer `OneTimeUse` on the SAML `Response`.
* Identity Provider (IdP) Considerations:
    * Validate X.509 Certificate for algorithm compatibility, strength of encryption, export restrictions.
    * Validate Strong Authentication options for generating the SAML token.
    IDP validation (which IDP mints the token).
    * Use/Trust Root CAs whenever possible.
    * Synchronize to a common Internet timesource.
    * Define levels of assurance for identity verification.
    * Prefer asymmetric identifiers for identity assertions over personally identifiable information (for example, SSNs, etc.).
    * Sign each individual Assertion or the entire Response element.
* Input Validation:
    * Ensure that all SAML providers/consumers do proper input validation.
* Cryptography:
    * Ensure all SAML elements in the chain use strong encryption.
    * Consider deprecating support for insecure XMLEnc algorithms.

<br>

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

* [https://cwe.mitre.org/data/definitions/287.html](https://cwe.mitre.org/data/definitions/287.html)
* [https://cheatsheetseries.owasp.org/cheatsheets/SAML_Security_Cheat_Sheet.html](https://cheatsheetseries.owasp.org/cheatsheets/SAML_Security_Cheat_Sheet.html)


<a class="not-decorated-link" href="#/guide/vulnerabilities/overview.md">< Back to tests</a>