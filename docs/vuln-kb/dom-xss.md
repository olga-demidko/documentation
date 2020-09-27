# What is "DOM-based Cross-Site Scripting" and how can you prevent it?

DOM XSS stands for Document Object Model-based Cross-site Scripting. This kind of XSS attack occurs when an application receives some client-side JavaScript that processes data from an unsafe, or untrusted source by writing the data to a potentially dangerous sink within the DOM instead of writing data in HTML which would present a regular XSS.



### 🌎 Section Map <!-- {docsify-ignore} -->
  - [What is DOM?](#what-is-dom)
  - [How do DOM XSS attacks work?](#how-do-dom-xss-attacks-work)
  - [What are Source & Sink?](#what-are-source-amp-sink)
  - [How Do Attackers Exploit DOM XSS Vulnerabilities?](#how-do-attackers-exploit-dom-xss-vulnerabilities)
  - [Defending Against DOM XSS Attacks](#defending-against-dom-xss-attacks)
  - [The similarities and differences between Standard XSS and DOM-based XSS](#the-similarities-and-differences-between-standard-xss-and-dom-based-xss)
  - [Another example for a DOM XSS attack](#another-example-for-a-dom-xss-attack)

<hr style="height:2px;background-color:#d1d3d4">

#### What is DOM?

The Document Object Model is a programming interface that gives developers the ability to access the document (webpage) and manipulate it by executing operations, therefore this interface defines the structure of documents by connecting the scripting language to the actual webpage.

<hr style="height:2px;background-color:#d1d3d4">

#### How do DOM XSS attacks work?
Let’s say we have a websiste with code that creates a welcome message to a user. As an example, the following HTML page `vulnerable.site/welcome.html` contains this code:

```html
<HTML>
<TITLE>Welcome!</TITLE>
Hi
<SCRIPT>
var pos=document.URL.indexOf("name=")+5;
document.write(document.URL.substring(pos,document.URL.length));
</SCRIPT>
<BR>
Welcome
…
</HTML>
```

Normally, this HTML page would be used for welcoming the user, e.g.:
```html
http://www.vulnerable.site/welcome.html?name=Joe
```

However, a request such as the one below would result in a possible XSS condition:
```html
http://www.vulnerable.site/welcome.html?name=<script>alert(document.cookie)</script>
```

<hr style="height:2px;background-color:#d1d3d4">

#### What are Source & Sink?

Let's walk through the website scenario we decribed above:

1. The victim’s browser receives this link, sends an HTTP request to `www.vulnerable.site`, and receives the above (static!) HTML page.

2. The victim’s browser then starts parsing this HTML into DOM. The DOM contains an object called `document`, which contains a property called `URL`, and this property is populated with the URL of the current page, as part of DOM creation.

3. When the parser processes the JavaScript code, it executes it and it modifies the raw HTML of the page. In this case, the code references `document.URL`, and so, a part of this string is embedded at parsing time in the HTML.

4. The string is then parsed and the JavaScript code `(alert(…))` is executed in the context of the same page, hence the XSS condition.

The logic behind the DOM XSS is that an input from the user, AKA **Source**, goes to an execution point, AKA **Sink**. In the previous example, our source was `document.write` and the sink was `alert(document.cookie)`. 

After the malicious code is executed by the website, you can simply exploit this DOM-based cross-site scripting vulnerability to steal the cookies from the user’s browser or change the behavior of the page on the web application as you please.

<hr style="height:2px;background-color:#d1d3d4">

#### How Do Attackers Exploit DOM XSS Vulnerabilities?

##### Source
A source is a JavaScript property that contains data that an attacker could potentially control:
- `document.URL`
- `document.referrer`
- `location`
- `location.href`
- `location.search`
- `location.hash`
- `location.pathname`

##### Sink
A sink is a DOM object or function that allows JavaScript code execution or HTML rendering.

- `eval`
- `setTimeout`
- `setInterval`
- `document.write`
- `element.innerHTML`

Any application is vulnerable to DOM-based cross-site scripting if there is an executable path via which data can develop from source to sink.

Different sources and sinks have various properties and behaviors that can impact exploitability, and determine what methods are used. Additionally, the application’s scripts might execute validation or other processing of data that must be accommodated when aiming to exploit a vulnerability.

In reality, the attacker would encode the URL payload so the script is not visible. Some browsers, for example, Mozzila may automatically encode the < and > characters in the document.URL when the URL is not directly typed in the address bar, and therefore it is not vulnerable to the attack shown in the example above. 

Embedding a script directly in the HTML is just one attack access point, other scenarios do not require these characters, nor embedding the code into the URL directly. Therefore, browsers in general are not entirely immune to DOM XSS either.

![Execution flow of DOM-based XSS attacks](media/xss-attack.png ':size=40%')

<hr style="height:2px;background-color:#d1d3d4">

#### Defending Against DOM XSS Attacks

You cannot detect DOM XSS attacks from the server-side. The malicious payload doesn’t even reach the server in most cases. Due to this, it can’t be sanitized in the server-side code. The root of the issue is in client-side code, the code of the page. 

You’re free to utilize any prevention techniques for DOM XSS that you can use for standard XSS attacks. There’s only one thing you need to pay attention to. For DOM XSS attacks you need to review and sanitize the client-side code instead of the server-side code.

There are several things to keep in mind if you want to prevent DOM XSS attacks:
1. **Refrain from using data that was received from the client for any kind of client-side sensitive actions (redirection or rewriting).**
2. **Sanitize client-side code. Do this by inspecting references to DOM objects, especially those that pose threat like referrer, URL, location, and so on. This is important in cases where the DOM can be modified.**

3. **Use intrusion prevention systems. Any that are able to inspect inbound URL parameters and can prevent the serving of inappropriate pages are fit for the job.**

<hr style="height:2px;background-color:#d1d3d4">

#### The similarities and differences between Standard XSS and DOM-based XSS 

What’s the difference between a classic XSS and a DOM-based XSS? Let’s go over the key difference:

|  | Standard XSS | DOM-based XSS |
| -- | -- | -- |
| **The root cause** | The root of both the classic XSS and a DOM-based vulnerability is the source code. | Same as standard XSS. |
| **Premises** | For classic XSS, the premise is the malicious embedding of client-side data by the server in the outbound HTML pages. | For DOM-based XSS, it’s the malicious referencing and use of DOM objects in the client-side. |
| **The page type** | Classic XSS attacks target dynamic page types. | DOM-based XSS attacks can target both static and dynamic page types. |
| **What can detect them** | Logs and intrusion detection systems can detect classic XSS attacks. | DOM-based XSS can remain unnoticed server-side if the hacker uses evading techniques. |
| **How to identify vulnerabilities** | For both classic and DOM-based XSS attacks you use vulnerability detection tools that can perform automatic penetration testing. The code also needs to be reviewed. | The only difference is that for classic XSS you do it server-side, while for DOM XSS you do it client-side. |
| **Preventing these vulnerabilities** | Intrusion prevention systems and sanitation for the server-side for classic XSS. | It’s the same for DOM XSS, but you sanitize the client-side instead of the server-side. |


<hr style="height:2px;background-color:#d1d3d4">

#### Another example for a DOM XSS attack
Let’s say we have a code that creates a form. This form lets a user select a timezone. The query string also has a default timezone. It’s defined by the `defaulttimezone` parameter. The code would look something like this:

Select your Time Zone:

```html
<select><script>

document.write("<OPTION value=1>"+document.location.href.substring(document.location.href.indexOf("defaulttimezone=")+8)+"</OPTION>");
document.write("<OPTION value=2>CET</OPTION>");

</script></select>
```

The `http://www.some.site/page.html?defaulttimezone=CST` URL then invokes the page. 

In order to launch a DOM-based XSS attack, hackers can now send a URL that looks like this:

```html
http://www.example.site/page.html?defaulttimezone=<script>alert(document.cookie)</script>
```

When an unsuspecting user clicks this link the browser sends a request for `/page.html?defaulttimezone=<script>alert(document.cookie)</script>` to `www.example.site.`

What does the server do now? It responds with a page that contains the malicious Javascript code. The browser now creates a DOM object for that page and the document.location object will contain this string:

```html
http://www.example.site/page.html?defaulttimezone=<script>alert(document.cookie)</script>
```

**Where is the problem?**

The original Javascript code on this page won’t expect the `defaulttimezone` parameter to have any HTML markup. Because of this, it will echo it into the DOM during runtime. Any browser will render the resulting page and end up executing the malicious script `(alert(document.cookie))`.

Keep in mind that the server’s HTTP response won’t contain the attacker’s payload. The payload will reveal itself in the client-side script at runtime. It happens when the flawed script opens the DOM variable `(document.location)` while assuming that it isn’t malicious.

With this out of the way, how are DOM-based XSS attacks different than others of this kind? First, the HTML page is static. In the case of other XSS attacks, malicious scripts are put into the source code of the page. Second, the script code doesn’t reach the server when the # character is used. # is seen as a fragment, so the browser won’t forward it. Due to this the server-side attack detection tools won’t detect or identify this kind of attack. Yet, there are cases of some URL types where the payload gets to the server and it is detected.

Common XSS vulnerabilities have completely different characteristics from DOM-based XSS vulnerabilities. Hackers who utilize DOM-based XSS attacks exploit DOM-objects by manipulating them and client-side properties.
