# Exposed Database Connection String

<b>Severity</b>: <b><font color="#1B49D4">Low</font></b><br>
<b>Test name</b>: Exposed Database Details

<table id="simple-table">
    <tr>
        <th><strong>Summary</strong></th>
    </tr>
</table>

The database is used as the main storage for sensitive data in the majority of products. Protecting the data your company collects and manages is essential. A proper security of your database can prevent the attack, which  may lead to financial loss, reputational damage, destruction of customer’s  trust, and non-compliance with governmental regulations.

A database connection string specifies information about the data source and the means of connecting to it. The connection strings are generally used by the application tier to connect to the backend database used for storing the application data. Even if the database connection string is properly secured, it reveals the information that could be abused. 

The connection strings may include:
* Hostname or IP address of the server housing the database. The port number used for the connection.
* Type of the data source.
* Type of the technology used to communicate with the data source.
* Name of the database containing the data.
* Network libraries used for the connection.
* Username and password for the account used to authenticate to the database.<br>



<table id="simple-table">
    <tr>
        <th><strong>Impact</strong></th>
    </tr>
</table>

Leakage of sensitive data

<table id="simple-table">
    <tr>
        <th><strong>Location</strong></th>
    </tr>
</table>

The issue can be found in the **source code** on the **client side**.

<table id="simple-table">
    <tr>
        <th><strong>Remedy suggestions</strong></th>
    </tr>
</table>

It is hardly  necessary for applications to disclose database connection strings to the clients. The reason for showing the database connection string on the user-visible pages should be reviewed. If possible, all the database connection strings need to be removed from the user-visible web pages.


<table id="simple-table">
    <tr>
        <th><strong>Classification</strong></th>
    </tr>
</table>

* CWE-284
* CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N

<table id="simple-table">
    <tr>
        <th><strong>References</strong></th>
    </tr>
</table>

[https://owasp.org/www-project-proactive-controls/v3/en/c3-secure-database](https://owasp.org/www-project-proactive-controls/v3/en/c3-secure-database)