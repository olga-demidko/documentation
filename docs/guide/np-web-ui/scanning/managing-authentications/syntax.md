# String Interpolation Syntax

The string interpolation syntax is designed for configuring authentication objects. It controls data coordinating between the consequent requests and responses. 

The syntax allows you to create a template (interpolation string) for the value to be extracted from the specified location. You can only create the template based on the previous authenticated requests and responses. 

The interpolation string uses the double curly braces `{{` and `}}` as delimiters and consists of three parts:
1. Stage name (specified in the **Authentication Flow Setup** section) 
2. Source (`request` or `response`)
3. Location in the source (`headers` or `body`)<br>

_Example:_ `{{ stage1.response.body }}`

For data transformation there is `|` as a pipe operator, which supports parameters and chaining.<br>
_Example:_ `{{ stage1.response.headers | get: '/Set-Cookie' | match: /sid=(.+)/ : 1 }}`


### Supported Pipes <!-- {docsify-ignore} -->
**get**<br>
Returns the value associated with the XPath, or undefined if there is none.<br>
_Format:_ `{{ value_expression | get : xpath }}`<br>
_Parameters:_
* `xpath` - xpath string<br>

_Example:_ `{{ stage1.response.headers | get: '/Set-Cookie' }}`

**match**<br>
Retrieves the result of matching a string against a regular expression.<br>
_Format:_ `{{ value_expression | match : regex : group }}`<br>
_Parameters:_
* `regex` - regular expression
* `group` - number of the capture group (optional, default 1)<br>

_Example:_ `{{ stage1.response.body | match: /sid=(.+)/ : 1 }}`

**encode**<br>
Encodes the value to some format.<br>
_Format:_ `{{ value_expression | encode : format }}`<br>
_Parameters:_
* format - `base64` or `none` (optional, default `none`)<br>

_Example:_ `{{ stage1.response.body | encode: 'base64' }}`

















