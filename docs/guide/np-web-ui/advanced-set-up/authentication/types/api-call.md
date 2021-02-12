# Configuring the API Calls Authentication in NexPloit
If you need to enable NexPloit to reach an authenticated resource by sending API requests with a customized body, you should use the API call authentication method. This authentication method is the most flexible and provides multiple methods of HTTP requests.

## Prerequisites
*   You are an active user on [nexploit.app](https://nexploit.app/scans).
*   Your application and authenticated resources are accessible to NexPloit, either directly from the Internet or via a Repeater.

## API Call Setup Fields 
The table below lists and describes the **Authentication Setup** fields in the **API Calls** section.

<table id="simple-table">
  <tr>
    <td width="25%" style="text-align:center;padding:15px"><b>Field</b></td>
    <td width="75%" style="text-align:center;padding:15px"><b>Guidelines</b></td>
  </tr>
  <tr>
    <td width="25%" style="text-align:left;vertical-align:text-top;padding:15px"><b>Method</b></td>
    <td width="75%" >
        <p>Enter the HTTP method of the relevant API end-point.</p>
    </td>
  </tr>
  <tr>
    <td width="25%" style="text-align:left;vertical-align:text-top;padding:15px"><b>URL</b></td>
    <td width="75%" >
    <p>Enter the URL of the relevant API end-point.</p>
    </td>
  </tr>
  <tr>
    <td width="25%" style="text-align:left;vertical-align:text-top;padding:15px"><b>Body</b></td>
    <td width="75%" >
        <p>Enter the HTTP request body to use with the request sent to the API end-point, for example:{“user”: “foo”, “pass”: “bar”}’.</p>
    </td>
  </tr>
  <tr>
    <td width="25%" style="text-align:left;vertical-align:text-top;padding:15px"><b>Extract from</b></td>
    <td width="75%" >
        <p>Select where in the responses the correct authentication token should be extracted from.</p>
    </td>
  </tr>
  <tr>
    <td width="25%" style="text-align:left;vertical-align:text-top;padding:15px"><ul><li><b>Header</b></li></ul></td>
    <td width="75%" >
        <p>Select if you need the authentication token to be extracted from the response header.</p>
    </td>
  </tr>
  <tr>
    <td width="25%" style="text-align:left;vertical-align:text-top;padding:15px"><ul><b>Header name</b></ul></td>
    <td width="75%" >
        <p>Enter the name of the header to extract the authentication token from.</p>
    </td>
  </tr>
   <tr>
    <td width="25%" style="text-align:left;vertical-align:text-top;padding:15px"><ul><li><b>Body</b></li></ul></td>
    <td width="75%" >
        <p>Select if you need the authentication token to be extracted from the response body.</p>
    </td>
  </tr>
  <tr>
    <td width="25%" style="text-align:left;vertical-align:text-top;padding:15px"><b>Authenticated token extraction regex</b></td>
    <td width="75%" >
        <p>Enter the Regex pattern that extracts the authentication token from the specified location.</p>
        <font color="green"><b>Pro Tips:</b></font>
        <ul>
            <li>
                Make sure the specified Regex captures ONLY the token itself, and not any additional parts of the string such as prefix, suffix, delimiter, padding, etc.
            </li>
        </ul>
    </td>
  </tr>
  <tr>
    <td width="25%" style="text-align:left;vertical-align:text-top;padding:15px"><b>Token encoder</b></td>
    <td width="75%" >
        <p>Select any encoder that you need to use on the token itself, for example Base64.</p>
    </td>
  </tr>
  <tr>
    <td width="25%" style="text-align:left;vertical-align:text-top;padding:15px"><b>Embed in</b></td>
    <td width="75%" >
        <p>Select where in the subsequent authenticated requests the authentication token should be embedded into.</p>
    </td>
  </tr>
  <tr>
    <td width="25%" style="text-align:left;vertical-align:text-top;padding:15px"><ul><li><b>Header</b></li></ul></td>
    <td width="75%" >
        <p>Select if you need the authentication token to be embedded into the request header.</p>
    </td>
  </tr>
  <tr>
    <td width="25%" style="text-align:left;vertical-align:text-top;padding:15px"><ul><b>Target header name</b></ul></td>
    <td width="75%" >
        <p>Enter the name of the header to embed the authentication token into.</p>
    </td>
  </tr>
  <tr>
    <td width="25%" style="text-align:left;vertical-align:text-top;padding:15px"><ul><li><b>Body</b></li></ul></td>
    <td width="75%" >
        <p>Select if you need the authentication token to be embedded into the request body.</p>
    </td>
  </tr>
  <tr>
    <td width="25%" style="text-align:left;vertical-align:text-top;padding:15px"><ul><b>Content type</b></ul></td>
    <td width="75%" >
        <p>Select the content type of the request body.</p>
        <p><font color="blue"><b>Note:</b></font> Currently only `application/json` is supported.</p>
    </td>
  </tr>
   <tr>
    <td width="25%" style="text-align:left;vertical-align:text-top;padding:15px"><ul><b>XPAth</b></ul></td>
    <td width="75%" >
        <p>Enter the exact path to the object to be used in the requests sent to the API end-point.</p>
    </td>
  </tr>
   <tr>
    <td width="25%" style="text-align:left;vertical-align:text-top;padding:15px"><b>Token template string</b></td>
    <td width="75%" >
        <p>Enter the expected token and final pattern to be embedded into the end-point request header or body.</p>
        <p><font color="green"><b>Pro Tip:</b></font> The required syntax is to have the `{{token}}` string in the field, along with any needed prefixes/suffixes. The `{{token}}` part will be replaced with the extracted token from the authentication response.</p>
    </td>
  </tr>
   <tr>
    <td width="25%" style="text-align:left;vertical-align:text-top;padding:15px"><b>Additional headers</b></td>
    <td width="75%" >
        <p><em>(Optional)</em> Select an additional header that you want to add to each request and enter its value. For example, additional cookies that might be needed for the authentication such as host-related metadata. </p>
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



## Step-by-Step Guide
1. Go to [nexploit.app](https://nexploit.app/scans).
2. On the default **Scans** page, click **My Authentications**.

  ![my-authentications](../media/my-authentications.png ':size=45%')

3. On the **My Authentications** page, click ![plus-icon](../media/plus-icon.png ':size=2%') next to **AUTHENTICATION**.

  ![auth-plus](../media/auth-plus.png ':size=45%')

4. On the **CREATE & TEST AUTHENTICATION** popup, do the following:
    *    In the **Authentication name** field, enter the authentication object name.
    *   _(Optional_) In the **Description** field, enter the authentication object description. For example, you can specify the application type or other information that helps you distinguish your created object.
    * From the **Authentication type** dropdown list, select **Header authentication**. 

  ![API-name-description](../media/API-name-description.png ':size=45%')

     * Complete the Authentication Setup fields.
        * For some parameters, you can add more fields by clicking ![plus-icon](../media/plus-icon.png ':size=2%') at the upper-right of the relevant setup section. 
        * To delete a parameter, click ![trash-icon](../media/trash-icon.png ':size=3%') next to the relevant Value field.

   ![api-setup-1](../media/api-setup-1.png ':size=45%')

   ![api-setup-2](../media/api-setup-2.png ':size=45%')

5. In the **Valid Authentication Response** section, select the options you want to use during the application scanning to determine that the authenticated resource has been reached. The options define how the application responds in case a full authentication flow passes successfully:
    *   **Detect using response status** - enter the HTTP response that will tell you about the authentication success.
    *   **Detect using header pattern** - enter the header and Regex pattern that will tell about the authentication success.
    *   **Detect using body pattern** - Enter the body pattern that will tell you about the authentication success.

  ![valid-response](../media/valid-response.png ':size=45%')

6. In the **Invalid Authentication Response** section, select the options you want to use during the application scanning to determine if the authenticated session is no longer valid and the authenticated resources cannot be reached. The options define how the application responds in case the authentication session fails:
    *   **Detect using response status** - enter the HTTP response that will tell you about the authentication failure.
    *   **Detect using header pattern** - enter the header and Regex pattern that will tell about the authentication failure.
    *   **Detect using body pattern** - Enter the body pattern that will tell you about the authentication failure. 

  ![invalid-response](../media/invalid-response.png ':size=45%') 

7. In the **Validation URL** field, enter the URL of an authenticated resource within your application, and then click  ![test-button](../media/test-button.png ':size=17%'). <br> The preliminary testing helps you verify if the authentication object has been configured correctly.

    ![test-authentication](../media/test-authentication.png ':size=45%') 

    *   A valid authentication object returns three success messages indicated in the relevant  **Test Results** sections: 
        *   **Detection of the invalid session**
        *   **Authentication call**
        *   **Valid session flow**

  ![test-results](../media/test-results.png ':size=45%') 

      In this case, you can save the configured object and add it to your scans.

    * If the test results include a failure message, go back to the object configurations and verify their correctness. Use the test request/response data to find a certain failure and fix it.
