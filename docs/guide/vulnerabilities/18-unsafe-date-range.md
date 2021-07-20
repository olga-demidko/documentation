# Unsafe Date Range

<b>Severity</b>: <b><font color="#DE8800">Medium</font></b><br>
<b>Test name</b>: Unsafe Date Range

<table id="simple-table">
    <tr>
        <th><strong>Summary</strong></th>
    </tr>
</table>

Unvalidated Date Range is a type of vulnerability that might cause DoS and other types of resource consumption. This vulnerability usually occurs in dynamic tables where a user can set a date range to get information, or reports generation interfaces where the user can specify a date range. The issue comes into play where the range is not limited to a specific reasonable timeframe (one week, one month for example). 

<table id="simple-table">
    <tr>
        <th><strong>Impact</strong></th>
    </tr>
</table>

The vulnerability allows an attacker to:
* Execute unauthorized code or commands
* Read and modify memory
* Read files or directories
* Cause denial of services (DoS)

<table id="simple-table">
    <tr>
        <th><strong>Example</strong></th>
    </tr>
</table>

1. Let's assume we have functionality that displays all orders in a store for a certain period of time: 
```
https://{your_web_site}.com/orders?startDate=2021-01-01&endDate=2021-01-07
```
2. As a result, the user can see a list of orders for one week. The request took about 0.2 seconds. 
3. By changing the requests parameters, an attacker can select an excessively long period of time, which will result in an unwanted load on the server. 
```
https://{your_web_site}.com/orders?startDate=2019-01-01&endDate=2021-01-01
```
4. As a result, the attacker can see a list of orders for two years. The request took an unexpectedly long time (for example, 10 seconds), and the server has been under unnecessary and unwanted load.

5. The attacker can make similar requests in large amounts to cause the server to run out of resources and crash the system.


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

It is necessary to fully validate and restrict the date range selection available to the user on both the client and the server sides. Depending on the usage scenario, select the minimum and maximum dates, dates range and apply strict validation to these parameters. 

In the situations where you need to keep an extensive date range (for example, preparation of annual reports), consider moving the business logic to a separate component that will run in the background (for example, microservice) and will be protected from DOS attacks.


<table id="simple-table">
    <tr>
        <th><strong>Classifications</strong></th>
    </tr>
</table>

* CWE-20
* CVSS:3.1/AV:N/AC:L/PR:N/UI:R/S:U/C:N/I:H/A:N


<table id="simple-table">
    <tr>
        <th><strong>References</strong></th>
    </tr>
</table>

* [https://cwe.mitre.org/data/definitions/20.html](https://cwe.mitre.org/data/definitions/20.html)
* [https://www.owasp.org/index.php/Improper_Data_Validation](https://www.owasp.org/index.php/Improper_Data_Validation)
