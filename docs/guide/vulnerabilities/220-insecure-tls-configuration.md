# Insecure TLS Configuration

<b>Severity</b>: <b><font color="red">High</font></b><br>
<b>Test name</b>: Insecure TLS Configuration

<table id="simple-table">
    <tr>
        <th><strong>Summary</strong></th>
    </tr>
</table>

Secure Socket Layer (SSL) is the protocol that was originally used to provide encryption for HTTP traffic (HTTPS). There are two publicly released versions of SSL: v2 and v3. Both of these versions  have critical cryptographic weaknesses and should no longer be used.
The next version of the protocol (effectively SSL 3.1) was named Transport Layer Security (TLS) version 1.0. Subsequently, TLS versions 1.1, 1.2 and 1.3 have been released.

The old versions of the SSL protocols have numerous weaknesses, and should no longer be used. Web applications should only support TLS 1.2 and TLS 1.3, with all other protocols disabled.

TLS supports multiple ciphers, but not all of them ensure a high level of security. Wherever possible, only GCM (Galois/Counter Mode) ciphers should be enabled.


<table id="simple-table">
    <tr>
        <th><strong>Impact</strong></th>
    </tr>
</table>

A wrong configuration may lead to the following:
* An attacker may read the contents of traffic (confidentiality)
* An attacker may modify traffic (integrity)
* An attacker may replay requests against the server (replay prevention)
* Inability for the client to verify that they are connected to the real server when using the client certificate (authentication)

<table id="simple-table">
    <tr>
        <th><strong>Location</strong></th>
    </tr>
</table>

The issue can be found in the **server's TLS configuration code**.

<table id="simple-table">
    <tr>
        <th><strong>Remedy suggestions</strong></th>
    </tr>
</table>

It is necessary to configure the web server to support the actual versions of the TLS and ciphers. Please find more the configuration guidelines in the **References** section. 
* When configuring nginx, refer to the values of `ssl_protocols`.
* When configuring Apache, refer to the values of `SSLProtocol`.

<table id="simple-table">
    <tr>
        <th><strong>Classifications</strong></th>
    </tr>
</table>

* CWE-295
* CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:L/A:N

<table id="simple-table">
    <tr>
        <th><strong>References</strong></th>
    </tr>
</table>

* [https://ssl-config.mozilla.org/](https://ssl-config.mozilla.org/)
* [https://cheatsheetseries.owasp.org/cheatsheets/Transport_Layer_Protection_Cheat_Sheet.html](https://cheatsheetseries.owasp.org/cheatsheets/Transport_Layer_Protection_Cheat_Sheet.html)
* [https://wiki.mozilla.org/Security/Server_Side_TLS](https://wiki.mozilla.org/Security/Server_Side_TLS)
