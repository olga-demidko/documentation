# String Interpolation Syntax

The string interpolation syntax is designed for configuring authentication objects. It controls data coordinating between the consequent requests and responses. 

The syntax allows you to create a template (interpolation string) for the value to be extracted from the specified location. You can only create the template based on the previous authenticated requests and responses. 

The interpolation string uses the double curly braces `{{` and `}}` as delimiters and consists of two general parts:

1. **Location** of the data to be transformed.
2. **Functions** separated by the `|` operator. The functions support chaining with the same operator.

_Format:_ `{{ location | function 1 | function 2 }}`

The parts comprise the following components:

<table id="simple-table">
  <tr>
    <th width="25%"><b>Part</b></th>
    <th width="75%"><b>Components</b></th>
  </tr>
  <tr>
    <td width="25%"><b>Location </b></td>
    <td width="75%" >
    <ol>
       <li> Stage name </li>
       <li>Source: <code>response</code></li>
       <li>Location: <code>url</code>, <code>headers</code>, <code>body</code></li>
    </ol>
    <em>Format:</em> <code>{{ &#60stage_name&#62.&#60source&#62.&#60location&#62 | &#60function&#62 }}</code>
    <p><em>Example:</em> <code>{{ stage1.response.headers | &#60function&#62 }}</code>
    </td>
  </tr>
  <tr>
    <td width="25%"><b>Function</b></td>
    <td width="75%" >
       <ol>
         <li> Pipe: <code>get</code>, <code>match</code>, <code>encode</code>
         <li> Parameter separated from the pipe by a colon
        </ol>
        <em>Format:</em> <code>{{ &#60location&#62 | &#60pipe&#62: &#60parameter&#62 }}</code>
        <p> <em>Example:</em> <code>{{  stage1.response.headers  | get: '/Set-Cookie' }}</code>
        <p> <em>Example with chained functions:</em> <br><code>{{ stage1.response.headers | get: '/Set-Cookie' | match: /sid=(.+)/ : 1 }} </code><br>
        <p><b>Note:</b> The functions are applied in the relative order. It means that in the example above,  first <code>get</code> will be applied and then  <code>match</code>.
    </td>
  </tr>
  </table>


### Supported Pipes <!-- {docsify-ignore} -->
**get**<br>
Returns the value associated with the XPath, or undefined if there is none.<br>

_Parameters:_
* `xpath` - xpath string<br>

_Format:_ `{{ <location> | get: <xpath> }}`<br>
_Example:_ `{{ step1.response.headers | get: '/Set-Cookie' }}`

**match**<br>
Retrieves the result of matching a string against a regular expression.<br>

_Parameters:_
* `regex` - regular expression
* `group` - number of the capture group (optional, default 1)<br>

_Format:_ `{{ <location> | match: < regex> : <group> }}`<br>
_Example:_ `{{ step1.response.body | match: /sid=(.+)/ : 1 }}`

**encode**<br>
Encodes the value to some format.<br>

_Parameters:_
* format - `base64` or `none` (optional, default `none`)<br>

_Format:_ `{{ <location> | encode: <format> }}`<br>
_Example:_ `{{ step1.response.body | encode: 'base64' }}`



### Generating Mock Data  <!-- {docsify-ignore} -->

If you need to generate random data to use it during configuration of an authentication object , you can apply one of the following  [Faker.js](https://github.com/marak/Faker.js/) data generators:

* `uuid`<br>
  _Example:_  `{{ $faker.datatype.number }}`

*  `number`<br>
  _Example:_  `{{ <$faker>.datatype.uuid }}`















