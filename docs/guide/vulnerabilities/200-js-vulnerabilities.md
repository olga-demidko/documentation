# JavaScript Component with Known Vulnerabilities

<b>Severity</b>: <b><font color="#DE8800">Medium</font></b><br>
<b>Test name</b>: Known JavaScript Vulnerabilities

<table id="simple-table">
    <tr>
        <th><strong>Summary</strong></th>
    </tr>
</table>

XMost web applications are highly composed. They use frameworks and libraries from a variety of commercial or open sources. In most cases, at the moment of implementation of a new dependency, a vulnerability has not been found in it yet. With time, a vulnerability can be found in that dependency. This will require updating the source code of the component itself, as well as upgrading to a newer version of the component in the applications that use it. 

As a first step of an attack, an attacker typically performs the application foot-printing to discover the platform, dependencies, frameworks, and server on which the application is built. With this information, the attacker can look up publicly known Common Vulnerabilities and Exposures (CVEs) published for that platform/component and apply them toward the target application. The attackers are unlikely to invest their time and effort to design a custom exploit to break into your systems (especially if they can find security flaws within one of your applications or application dependencies easily).

The component with a known vulnerability could be the operating system itself, the CMS used, the web server, some plugin installed, or even a library used by one of these plugins. The impact is impossible to grade as it completely depends on the vulnerable component and the vulnerability it suffers from. 



<table id="simple-table">
    <tr>
        <th><strong>Location</strong></th>
    </tr>
</table>

* The issue can be found in the **source code** on the **server side**.
* The issue can be found in the **source code** on the **client side**.


<table id="simple-table">
    <tr>
        <th><strong>Remedy suggestions</strong></th>
    </tr>
</table>

**Fixing the issue:**<br>
A JavaScript component was found to have a known public vulnerability, please see the additional information section below for specific information on each issue.
 * Make sure to update the component to its latest version, or at least to the latest stable vulnerabilities free version. If it is not possible, consider removing/replacing that dependency.

**Preventing the issue:**
* A one-time fix will solve the current issue, but will not prevent similar cases in the future. You need to take a set of measures to continuously monitor and react to new vulnerabilities identified in the components you use.
* Remove unused dependencies, unnecessary features, components, files, and documentation.
* Continuously inventory the versions of both client-side and server-side components (for example, frameworks, libraries) and their dependencies using special tools. Continuously monitor sources like CVE ([https://cve.mitre.org/](https://cve.mitre.org/)) and NVD ([https://nvd.nist.gov/](https://nvd.nist.gov/)) for vulnerabilities in the components. Use software composition analysis tools to automate the process. Subscribe to email alerts for security vulnerabilities related to the components you use.
* Only obtain components from official sources over secure links. Prefer signed packages to reduce the chance of including a modified, malicious component.
* Monitor the libraries and components that are unmaintained or do not create security patches for older versions.



<table id="simple-table">
    <tr>
        <th><strong>References</strong></th>
    </tr>
</table>

* [https://cve.mitre.org/](https://cve.mitre.org/)
* [https://nvd.nist.gov/](https://nvd.nist.gov/)