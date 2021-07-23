<a class="not-decorated-link" href="#/guide/vulnerabilities/overview.md">< Back to tests</a>

# XML External Entity Injection

<b>Severity</b>: <b><font color="#DB1E54">High</font></b><br>
<b>Test name</b>: XML External Entity Injection

<table id="simple-table">
    <tr>
        <th><strong>Summary</strong></th>
    </tr>
</table>

XML External Entity vulnerability allows an attacker to upload an XML file with a reference to an external entity without validation. The attacker exploits weakly configured XML parsers, which process the XML code. The attack can lead to gaining confidential information and even to Remote Code Execution (RCE).

<table id="simple-table">
    <tr>
        <th><strong>Impact</strong></th>
    </tr>
</table>

The vulnerability may expose the application to the following attack vectors:
* Gain sensitive information
* Disclose internal content via HTTP(S) requests or launch a CSRF attack to any unprotected internal services
* Execute a malicious URL, possibly allowing the arbitrary code to be executed under the application account
* Cause denial of the services (DoS) 


<table id="simple-table">
    <tr>
        <th><strong>Example</strong></th>
    </tr>
</table>

**Example 1: Accessing a local resource**
```xml
<?xml version="1.0" encoding="ISO-8859-1"?>
<!DOCTYPE credentials [
    <!ELEMENT credentials (user, password)>
    <!ELEMENT user (#PCDATA)>
    <!ELEMENT password (#PCDATA)>
    <!ENTITY xxe SYSTEM  "file:///etc/passwd" >
]>
<credentials>
    <user>&xxe;</user>
    <password>mypass</password>
</credentials>
```

**Example 2: Remote code execution**

```xml
<?xml version="1.0" encoding="ISO-8859-1"?>
<!DOCTYPE foo [ 
    <!ELEMENT foo ANY >
    <!ENTITY xxe SYSTEM "expect://id" >
]>
<credentials>
    <user>&xxe;</user>
    <password>mypass</password>
</credentials>
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

1. Disable Document Type Declaration (DTD) completely.
2. If it is not possible to disable DTD completely, then external entities and external document type declarations must be disabled according to each specific parser.
    * PHP
    ```
    libxml_disable_entity_loader(true);
    ```
    * Java (Xerces)
    ```
    DocumentBuilderFactory dbf = DocumentBuilderFactory.newInstance();
    dbf.setFeature("http://xml.org/sax/features/external-general-entities", false);
    dbf.setFeature("http://xml.org/sax/features/external-parameter-entities", false);
    dbf.setFeature("http://apache.org/xml/features/disallow-doctype-decl", true);
    ```


<table id="simple-table">
    <tr>
        <th><strong>Classifications</strong></th>
    </tr>
</table>

* CWE-611
* CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:L


<table id="simple-table">
    <tr>
        <th><strong>References</strong></th>
    </tr>
</table>

* [https://cwe.mitre.org/data/definitions/611.html](https://cwe.mitre.org/data/definitions/611.html)
* [https://www.owasp.org/index.php/XML_External_Entity_(XXE)_Processing](https://www.owasp.org/index.php/XML_External_Entity_(XXE)_Processing)
* [https://www.neuralegion.com/what-is-an-xml-external-entity-xxe-injection/](https://www.neuralegion.com/what-is-an-xml-external-entity-xxe-injection/)


<a class="not-decorated-link" href="#/guide/vulnerabilities/overview.md">< Back to tests</a>