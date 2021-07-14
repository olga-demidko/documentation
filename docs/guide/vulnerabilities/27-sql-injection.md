# SQL Injection: Blind Time Based

<b>Severity</b>: <b><font color="red">High</font></b><br>
<b>Test name</b>: SQL Injection (SQLI)

<table id="simple-table">
    <tr>
        <th><strong>Summary</strong></th>
    </tr>
</table>

A SQL injection attack is the insertion (injection) of a malicious SQL query via the input data from a client to an application. As a result, an attacker can execute any SQL query on the client's database with the access rights that are granted to the application. It means that the attacker can read, update, or delete sensitive data, or even administrate operations on the server side.

Blind Time Based is a specific type of the SQL Injection, which uses intentional database pausing to obtain sensitive information for further attack. At that, the database returns the results indicating that the SQL query has been executed successfully.


<table id="simple-table">
    <tr>
        <th><strong>Impact</strong></th>
    </tr>
</table>

This vulnerability allows an attacker to:
* Modify application data
* Bypass protection mechanism
* Read application data

<table id="simple-table">
    <tr>
        <th><strong>Example</strong></th>
    </tr>
</table>

A basic request to demonstrate Blind Time Based SQL Injection (MySQL) is the following:
```
SELECT name, price FROM products WHERE id=100-IF(MID(VERSION(),1,1) = '5', SLEEP(20), 0)
```

If the server response takes more than 20 seconds, it means that this database server is running MySQL version 5.x. Although the request will return the same result as without the injection (just one Product), the execution time of the request allows the attacker to get the required information for further attack.


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

* Use the prepared statements with variable binding (aka parameterized queries). Parameterized queries force the developer to first define all the SQL code, and then pass each parameter (given below) to the query later. This coding style allows the database to distinguish between code and data, regardless of the input type a user supplies.
    * Java EE – use `PreparedStatement()` with bind variables
    * .NET – use parameterized queries like `SqlCommand()` or `OleDbCommand()` with bind variables
    * PHP – use PDO with strongly typed parameterized queries (using `bindParam()`)
    * Hibernate - use  `createQuery()` with bind variables (called named parameters in Hibernate)
    * SQLite - use `sqlite3_prepare()` to create a statement object
* Avoid generation of dynamic SQL inside stored procedures. If it can't be avoided, the stored procedure must use input validation or proper escaping to make sure that all user supplied input to the stored procedure can't be used to inject SQL code into the dynamically generated query.
* Use the least privilege approach to provide defense in depth and minimize the potential damage of a successful SQL injection attack. Minimize the privileges assigned to every database account in your environment (do not assign DBA or admin type access rights to your application accounts).

<table id="simple-table">
    <tr>
        <th><strong>Classifications</strong></th>
    </tr>
</table>

* CWE-89
* CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:N


<table id="simple-table">
    <tr>
        <th><strong>References</strong></th>
    </tr>
</table>

* [https://cwe.mitre.org/data/definitions/89.html](https://cwe.mitre.org/data/definitions/89.html)
* [https://www.owasp.org/index.php/Blind_SQL_Injection](https://www.owasp.org/index.php/Blind_SQL_Injection)
