# Repeater Scripts Overview
If you use a Repeater to scan a target, you can manipulate the scan request before dispatching it to the target. NexPloit allows you to create a script that can add, change or compute some part of the request after you apply it for a specific Repeater. You can load a script file to the Repeater which should modify the request using the [nexpoilt.app](https://nexploit.app/scans) or  NexPloit CLI.

You can also create and apply the Repeater scripts using the NexPloit API. More information about it is provided on [our API documentation page](https://nexploit.app/api/v1/docs/#/Scripts).

 >[!NOTE|label:Note]
 Custom scripts are supported only for the scans run via a Repeater.

The most common case of using a Repeater script to manipulate a request is when you need to calculate a hash message authentication code (HMAC) token. The code involves a hash function in combination with a secret key.  The HMAC authorization is required to enable interaction between the server and NexPloit. For each new request, the server generates a new HMAC code that should match (signed by) the token encoded in the Repeater script. Therefore, signing the server HMAC ensures the request authenticity.

 >[!WARNING|label:Important]
In a script, you should specify how exactly the server calculates the HMAC code to allow NexPloit to provide a valid HMAC token. NexPloit can reach targets ONLY after a successful HMAC authorization with the relative server. 

The Repeater scripts also help you send some custom dynamic values per host and various other request pre-processing steps.

### Script Implementation Flow

You first need to create a script file and then load it to a specific Repeater. It may take a few minutes before the file reaches the Repeater and updates it. 

When receiving a scan request from NexPloit (step 2 on the diagram below), the  Repeater applies the code from the loaded script to the request (step 3) and dispatches the modified request to the local target. 

![scripts-implementation](../media/repeaters-scripts/repeater-chart.png ':size=45%')

### Building Parameters of Scripts

A script code must include a function with the hardcoded name ‘handle’ and a composite of any custom parameters (variables) . The script parameters are used for computing dynamic data, for example an authorization token, which can be added to the scan request. Here is a simple example of a script code.  

```js
const { createHmac } = require('crypto');              
const handle = ({ method, url, headers, body }) => {   
  const version = 'v1';                                
  const secret = 'someSecret';                         
  const timestamp = Date.now();                        
  const signature = createHmac('sha256', secret).update(\'\${version}:\${timestamp}:\${body}`).digest('base64'); 

  return { url, method, body, headers: { ...headers, 'x-request-timestamp': timestamp, 'x-request-signature': signature } };                                       
};                                                     
exports.handle = handle;                               
```

The most common script parameters that may be applied for calculating an authorization token are given below.

<table id="simple-table">
  <tr>
    <th width="25%"><b>Parameter</b></th>
    <th width="75%"><b>Description</b></th>
  </tr>
  <tr>
    <td width="25%">{ createHmac }</td>
    <td width="75%">
      The parameter which specifies the Node.js crypto module to be used for encoding some request values, for example an HMAC token.
      <br><br>
      You can find more info about the module <a href="https://nodejs.org/api/crypto.html">here</a>.
    </td>
  </tr>
  <tr>
    <td width="25%">handle</td>
    <td width="75%">
      The function which accepts the following parameters from each request automatically:
      <ul>
          <li>method (string)</li>
          <li>url (string)</li>
          <li>headers (hash map)</li>
          <li>body (string)</li>
      </ul>
      And must also return the same four parameters in the expected order.
      <br><br>
      <font color="orange"><b>Important:</b></font> The <b>exports.handle</b> command is required to enable the handle function.
    </td>
  </tr>
  <tr>
    <td width="25%">custom parameters</td>
    <td width="75%">
      Any custom parameters that are required for modifying the request, for example ‘version’, ‘secret’, ‘timestamp’, ‘signature’, etc.
    </td>
  </tr>
</table>
