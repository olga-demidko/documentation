<a class="not-decorated-link" href="#/guide/vulnerabilities/overview.md">< Back to tests</a>

# SQL Database Error Message in Response

<b>Severity</b>: <b><font color="#1B49D4">Low</font></b><br>
<b>Test name</b>: SQL Injection (SQLI)

<table id="simple-table">
    <tr>
        <th><strong>Summary</strong></th>
    </tr>
</table>

A SQL injection attack is the insertion (injection) of a malicious SQL query via the input data from a client to an application. As a result, an attacker can execute any SQL query on the client's database with the access rights that are granted to the application. It means that the attacker can read, update, or delete sensitive data, or even administrate operations on the server side.

Database Error in Response is a specific type of the SQL Injection, when an attacker uses error messages thrown by the database server to obtain sensitive information about the target (structure, version, operating system),  and even to return full query results. 


<table id="simple-table">
    <tr>
        <th><strong>Impact</strong></th>
    </tr>
</table>

Leakage of sensitive data

<table id="simple-table">
    <tr>
        <th><strong>Example</strong></th>
    </tr>
</table>

In some cases, an error-based SQL injection alone is enough for an attacker to enumerate an entire database. Basically, any incorrect SQL instruction identified when parsing or executing the SQL will generate an error (MySQL):
1. The unprotected application executes the following query containing the user’s input `Laptops`:
```
SELECT name, price FROM products WHERE category = 'Laptops'
```
2. Instead of `Laptops`, an attacker can submit the input which will break the SQL query like `" ''' -- "`. <br>As a result, the database will return the following database error:
``` 
1064 - You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near ''' at line 1
```
3. The following SQL will be executed:
```
SELECT name, price FROM products WHERE category = ''' -- 
```
4. As the application is not protected, the database error will not be handled correctly and the end user will be able to see the content of this error. Depending on the error, this allows the attacker to get information about the database, which can be used for a further attack.


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

* In the code, configure proper reporting of the database errors, so that the error messages are never sent to the client web browser. While error logs are very useful during web application development, they should be disabled in the production environment, or logged to a file with restricted access instead. 
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
* CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N


<table id="simple-table">
    <tr>
        <th><strong>References</strong></th>
    </tr>
</table>

* [https://cwe.mitre.org/data/definitions/89.html](https://cwe.mitre.org/data/definitions/89.html)
* [https://www.owasp.org/index.php/Testing_for_SQL_Server](https://www.owasp.org/index.php/Testing_for_SQL_Server)
* [https://www.neuralegion.com/what-are-sql-injections-and-how-can-they-be-prevented/](https://www.neuralegion.com/what-are-sql-injections-and-how-can-they-be-prevented/)

<a class="not-decorated-link" href="#/guide/vulnerabilities/overview.md">< Back to tests</a>