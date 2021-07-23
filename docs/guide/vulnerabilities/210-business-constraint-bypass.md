<a class="not-decorated-link" href="#/guide/vulnerabilities/overview.md">< Back to tests</a>

# Business Constraint Bypass

<b>Severity</b>: <b><font color="#DE8800">Medium</font></b><br>
<b>Test name</b>: Business Constraint Bypass

<table id="simple-table">
    <tr>
        <th><strong>Summary</strong></th>
    </tr>
</table>

Business Constraint Bypass is a type of vulnerability that may cause DoS, other types of resource consumption and (which could be more critical to business) may give access to more data than necessary. The issue arises when design and development teams make mistaken assumptions about how users will interact with the application. This may lead to inadequate validation of user input. For example, if developers assume that the users will pass data exclusively via a web browser, the application may rely entirely on the client side to validate the input. Such validation is easily bypassed by an attacker using an intercepting proxy. To perform an attack, the attacker looks for parameters with numerical values that control the amount of returned data (or other business parameters) and tries to change (increase) them, bypassing the default returned data restriction.


<table id="simple-table">
    <tr>
        <th><strong>Impact</strong></th>
    </tr>
</table>

Sensitive data leakage 


<table id="simple-table">
    <tr>
        <th><strong>Example</strong></th>
    </tr>
</table>

1. An online bookstore provides free access to the first 20 pages of each book. The remaining pages are only available after purchasing the book. The following request only returns 20 pages for users with free access.
```
https://{your_book_store}.com/book/{book_id}/pages-preview
```
2. With the following request, an attacker can bypass the default data return limit (number of pages) with a parameter from the request and get the first 500 pages of the book:
```
https://{your_book_store}.com/book/{book_id}/pages-preview?limit=500
```
3. Alternatively, the attacker could keep the default number of pages to preview (20), but bypass the page number where the counting starts and get pages 21-40:
```
https://{your_book_store}.com/book/{book_id}/pages-preview?offset=20
```
4. As a result, with only a free account, the attacker can grab the entire contents of the book and lead the server to an unexpected load (if 500 pages are requested at once).


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

1. Avoid making implicit assumptions about user behavior or the behavior of other parts of the application. Verify and limit the user input that will be used as business parameters on both client and server sides.
2. Please bear in mind that attackers can see the API requests to your application and manipulate the parameters. Additionally, the use of standard parameters (like limit, offset and others) should be validated and allowed only for those APIs for which it is necessary. Never trust that an API call will not be used or abused by anyone other than your application.

<table id="simple-table">
    <tr>
        <th><strong>Classifications</strong></th>
    </tr>
</table>

* CWE-639
* CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N


<table id="simple-table">
    <tr>
        <th><strong>References</strong></th>
    </tr>
</table>

* [https://cwe.mitre.org/data/definitions/639.html](https://cwe.mitre.org/data/definitions/639.html)


<a class="not-decorated-link" href="#/guide/vulnerabilities/overview.md">< Back to tests</a>