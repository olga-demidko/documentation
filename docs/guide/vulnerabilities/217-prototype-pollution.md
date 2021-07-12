# Prototype Pollution

<b>Severity</b>: <b><font color="red">High</font></b><br>
<b>Test name</b>: Prototype Pollution

<table id="simple-table">
    <tr>
        <th><strong>Summary</strong></th>
    </tr>
</table>

Prototype Pollution is a vulnerability which affects applications written with JavaScript programming language. JavaScript is a prototype-based language. To provide inheritance, an object can have a _prototype object_, which acts as a template object that it inherits methods and properties from. An object's _prototype object_ may also have a _prototype object_, which it inherits methods and properties from, and so on. This is often referred to as a _prototype chain_. 

A link is made between the object instance and its _prototype_ ( `__proto__` property, which contains basic functionalities such as `toString`, constructor and `hasOwnProperty`), and the properties and methods are found by walking up the chain of prototypes.
An attacker can change the prototype object of the basic object, so it applies to all JavaScript objects in a running application. A malicious code can be provided through user input in web applications via text fields, headers and files.


<table id="simple-table">
    <tr>
        <th><strong>Impact</strong></th>
    </tr>
</table>

This vulnerability may lead to:
* Denial of service by triggering JavaScript exceptions
* Remote code execution by forcing the code path that the attacker injects
* Escalating to Reflected XSS


<table id="simple-table">
    <tr>
        <th><strong>Example</strong></th>
    </tr>
</table>

Changing the basic method `toString`:<br>
```js
>let user = {name: "Pascal", age: "55"}
>console.log(customer.toString())
// shows: [object Object]
>user.__proto__.toString = ()=>{alert("vulnerability")}
// alert box pops up: "vulnerability"
```

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

* Add `__proto__`to the blacklist and do not copy this field.
* Freeze `Object.prototype` using the `Object.freeze()` function. After that, the `Object.prototype` cannot be modified.
* You can use an object without a prototype object, then modifying the prototype will not be possible:`Object.create(null)`. But the disadvantage is that this object can break some functionality further. For example, someone might want to call `toString()` on this object.
* Use the latest versions of your JavaScript libraries and update them periodically.


<table id="simple-table">
    <tr>
        <th><strong>Classification</strong></th>
    </tr>
</table>

* CWE-400
* CVSS:3.1/AV:N/AC:L/PR:N/UI:R/S:U/C:H/I:H/A:L

<table id="simple-table">
    <tr>
        <th><strong>References</strong></th>
    </tr>
</table>

[https://github.com/Kirill89/prototype-pollution-explained](https://github.com/Kirill89/prototype-pollution-explained)