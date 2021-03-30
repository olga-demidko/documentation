# Configuring the API Call Authentication in NexPloit
If you need to enable NexPloit to reach an authenticated resource by sending API requests with a customized body, you should use the API call authentication method. This authentication method is the most flexible and provides multiple methods of HTTP requests.

## Prerequisites
*   You are an active user on [nexploit.app](https://nexploit.app/scans).
*   Your application and authenticated resources are accessible to NexPloit, either directly from the Internet or via a Repeater.


## Step-by-Step Guide
1. Go to [nexploit.app](https://nexploit.app/scans).
2. On the default **Scans** page, click **My Authentications**.

  ![my-authentications](../media/my-authentications.png ':size=45%')

3. On the **My Authentications** page, click ![plus-icon](../media/plus-icon.png ':size=2%') next to **AUTHENTICATION**.

  ![auth-plus](../media/auth-plus.png ':size=45%')

4. On the **CREATE & TEST AUTHENTICATION** popup, complete the fields of the following configuration sections.

#### Authentication Details

In this section, specify the details of the authentication object you want to create.

  ![API-name-description](../media/API-name-description.png ':size=45%')

<table id="simple-table">
  <tr>
    <th width="25%"><b>Field</b></th>
    <th width="75%"><b>Guidelines</b></th>
  </tr>
  <tr>
    <td width="25%"><b>Authentication name</b></td>
    <td width="75%" >
       Enter the authentication object name.
    </td>
  </tr>
  <tr>
    <td width="25%"><b> Description</b></td>
    <td width="75%" >
        <em>(Optional)</em> Enter the authentication object description. For example, you can specify the application type or other information that helps you distinguish your created object.
    </td>
  </tr>
  <tr>
    <td width="25%"><b>Authentication type</b></td>
    <td width="75%" >
      From the <b>Authentication type</b> drop-down list, select <b>API Call</b>.
    </td>
  </tr>
</table>

#### Authentication Setup

In this section, set up a valid authentication request to be sent to the end-point API. For that, complete the **Authentication Setup** fields.

   ![api-setup-1](../media/api-setup-1.png ':size=45%')


<table id="simple-table">
  <tr>
    <th width="25%"><b>Field</b></th>
    <th width="75%"><b>Guidelines</b></th>
  </tr>
  <tr>
    <td width="25%"><b>Method</b></td>
    <td width="75%" >
       Enter the HTTP method of the relevant API end-point.
    </td>
  </tr>
  <tr>
    <td width="25%"><b>URL</b></td>
    <td width="75%" >
    Enter the URL of the relevant API end-point.
    </td>
  </tr>
  <tr>
    <td width="25%"><b>Body</b></td>
    <td width="75%" >
        Enter the HTTP request body to use with the request sent to the API end-point, for example:{“user”: “foo”, “pass”: “bar”}’.
    </td>
  </tr>
  <tr>
    <td width="25%"><b>Extract from</b></td>
    <td width="75%" >
        Select where in the responses the correct authentication token should be extracted from.
    </td>
  </tr>
  <tr>
    <td width="25%"><ul><li><b>Header</b></li></ul></td>
    <td width="75%" >
        Select if you need the authentication token to be extracted from the response header.
    </td>
  </tr>
  <tr>
    <td width="25%"><ul><b>Header name</b></ul></td>
    <td width="75%" >
        Enter the name of the header to extract the authentication token from.
    </td>
  </tr>
   <tr>
    <td width="25%"><ul><li><b>Body</b></li></ul></td>
    <td width="75%" >
        Select if you need the authentication token to be extracted from the response body.
    </td>
  </tr>
  <tr>
    <td width="25%"><b>Authenticated token extraction regex</b></td>
    <td width="75%" >
        Enter the Regex pattern that extracts the authentication token from the specified location.<br><br>
        <font color="green"><b>Pro Tips:</b></font>
        <ul>
            <li>
                Make sure the specified Regex captures ONLY the token itself, and not any additional parts of the string such as prefix, suffix, delimiter, padding, etc.
            </li>
        </ul>
    </td>
  </tr>
  <tr>
    <td width="25%"><b>Token encoder</b></td>
    <td width="75%" >
        Select any encoder that you need to use on the token itself, for example Base64.
    </td>
  </tr>
  <tr>
    <td width="25%"><b>Embed in</b></td>
    <td width="75%" >
        Select where in the subsequent authenticated requests the authentication token should be embedded into.
    </td>
  </tr>
  <tr>
    <td width="25%"><ul><li><b>Header</b></li></ul></td>
    <td width="75%" >
        Select if you need the authentication token to be embedded into the request header.
    </td>
  </tr>
  <tr>
    <td width="25%"><ul><b>Target header name</b></ul></td>
    <td width="75%" >
        Enter the name of the header to embed the authentication token into.
    </td>
  </tr>
  <tr>
    <td width="25%"><ul><li><b>Body</b></li></ul></td>
    <td width="75%" >
        Select if you need the authentication token to be embedded into the request body.
    </td>
  </tr>
  <tr>
    <td width="25%"><ul><b>Content type</b></ul></td>
    <td width="75%" >
        Select the content type of the request body.<br><br>
        <font color="blue"><b>Note:</b></font> Currently only `application/json` is supported.
    </td>
  </tr>
   <tr>
    <td width="25%"><ul><b>XPAth</b></ul></td>
    <td width="75%" >
        Enter the exact path to the object to be used in the requests sent to the API end-point.
    </td>
  </tr>
   <tr>
    <td width="25%"><b>Token template string</b></td>
    <td width="75%" >
        Enter the expected token and final pattern to be embedded into the end-point request header or body.<br><br>
        <font color="green"><b>Pro Tip:</b></font> The required syntax is to have the `{{token}}` string in the field, along with any needed prefixes/suffixes. The `{{token}}` part will be replaced with the extracted token from the authentication response.
    </td>
  </tr>
   <td width="25%"><b>Maximum number of redirects to follow</b></td>
    <td width="75%" >
        Enter the maximum number of redirections that the Nexploit should follow during the authentication process.
    </td>
  </tr>
   <tr>
    <td width="25%"><b>Additional headers</b></td>
    <td width="75%" >
        <em>(Optional)</em> Select an additional header that you want to add to each request and enter its value. For example, additional cookies that might be needed for the authentication such as host-related metadata.<br><br>
         <font color="green"><b>Pro Tips:</b></font>
        <ul>
            <li>
                If your application uses cookies that are set via the Set-Cookie header in the response, then you do not need to extract and reuse the cookies. Any Set-Cookie header will be automatically used during authentication.  
            </li>
             <li>
                MFA required on initial IP login may be handled using a cookie value. For that, you need to identify which cookie holds the completed MFA/2FA and include a valid cookie as a part of your authentication object.  
            </li>
        </ul>
    </td>
  </tr>
  </table>

  * For some parameters, you can add more fields by clicking ![plus-icon](../media/plus-icon.png ':size=2%') at the upper-right of the relevant setup section. 
  * To delete a parameter, click ![trash-icon](../media/trash-icon.png ':size=3%') next to the relevant Value field.

#### Valid Authentication Response 

In this section, select the options you want to use during the application scanning to determine that the authenticated resource has been reached. The options define how the application responds in case a full authentication flow passes successfully.

 ![valid-response](../media/valid-response.png ':size=45%')

  <table id="simple-table">
  <tr>
    <th width="25%"><b>Field</b></th>
    <th width="75%"><b>Guidelines</b></th>
  </tr>
  <tr>
    <td width="25%"><b>Detect using response status</b></td>
    <td width="75%" >
       Enter the HTTP response that will tell you about the authentication success.
    </td>
  </tr>
  <tr>
    <td width="25%"><b>Detect using header pattern</b></td>
    <td width="75%" >
        Enter the header and Regex pattern that will tell about the authentication success.
    </td>
  </tr>
  <tr>
    <td width="25%"><b>Detect using body pattern</b></td>
    <td width="75%" >
       Enter the body pattern that will tell you about the authentication success.
    </td>
  </tr>
</table>


#### Authentication Triggers 

In this section, select the options you want to use during the application scanning to determine if the authentication flow is no longer valid and the authenticated resources cannot be reached. The options define how the application responds in case the authentication flow fails.

![invalid-response](../media/invalid-response.png ':size=45%') 

<table id="simple-table">
  <tr>
    <th width="25%"><b>Field</b></th>
    <th width="75%"><b>Guidelines</b></th>
  </tr>
  <tr>
    <td width="25%"><b>Detect using response status</b></td>
    <td width="75%" >
       Enter the HTTP response that will tell you about the authentication failure.
    </td>
  </tr>
  <tr>
    <td width="25%"><b>Detect using header pattern</b></td>
    <td width="75%" >
        Enter the header and Regex pattern that will tell about the authentication failure.
    </td>
  </tr>
  <tr>
    <td width="25%"><b>Detect using body pattern</b></td>
    <td width="75%" >
       Enter the body pattern that will tell you about the authentication failure. 
    </td>
  </tr>
</table>


#### Valid Session Tester

The preliminary testing helps you verify if the authentication object has been configured correctly.

 ![test-authentication](../media/test-authentication.png ':size=45%') 


<table id="simple-table">
  <tr>
    <th width="25%"><b>Field</b></th>
    <th width="75%"><b>Guidelines</b></th>
  </tr>
  <tr>
    <td width="25%"><b>Validation URL </b></td>
    <td width="75%" >
       Enter the URL of the authenticated resource to be accessed by NexPloit. 
    </td>
  </tr>
  <tr>
    <td width="25%"><b>Repeater  </b></td>
    <td width="75%" >
       If you use a local Repeater to reach the scan target, from the <b>Repeater</b> dropdown list, select the Repeater you need for the scan.   
    </td>
  </tr>
  </table>

Once you have completed the **Valid Session Tester** fields, click **Test Authentication**.

 * A valid authentication object returns three success messages indicated in the relevant  **Test Results** sections: 
     *   **Test Authentication Triggers**
     *   **Authentication call**
     *   **Access Protected Resource**

 ![test-results](../media/auth-results.png ':size=45%') 

In this case, you can save the configured object and add it to your scans.

 * If the test results include a failure message, go back to the object configurations and verify their correctness. Use the test request/response data to find a certain failure and fix it.
