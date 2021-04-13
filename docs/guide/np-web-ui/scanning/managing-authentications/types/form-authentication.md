# Configuring the Form Authentication in Nexploit
You can use the form authentication if the login-protected resources within the application you want to scan use<br> the `application/x-www-form-urlencoded` content type of the HTTP requests. 

The form authentication type is set by default when you create an authentication object in Nexploit.  

## Prerequisites
*   You are an active user on [nexploit.app](https://nexploit.app/scans).
*   Your application and authenticated resources are accessible to Nexploit, either directly from the Internet or via a Repeater.


## Step-by-Step Guide
1. Go to [nexploit.app](https://nexploit.app/scans).
2. On the default **Scans** page, click **My Authentications**.

    ![my-authentications](../media/my-authentications.png ':size=45%')

3. On the **My Authentications** page, click ![plus-icon](../media/plus-icon.png ':size=2%') next to **AUTHENTICATION**.

    ![auth-plus](../media/auth-plus.png ':size=45%')

4. On the **CREATE & TEST AUTHENTICATION** popup, complete the fields of the following configuration sections.

#### Authentication Details 

In this section, specify the details of the authentication object you want to create.

![form-description](../media/form-name-description.png ':size=45%')

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
</table>

#### Authentication  Setup 

In this section, set up a valid authentication request to be sent to the end-point API. For that, complete the **Authentication Setup** fields.

![form-setup](../media/form-setup.png ':size=45%')

<table id="simple-table">
  <tr>
    <th width="25%"><b>Field</b></th>
    <th width="75%"><b>Guidelines</b></th>
  </tr>
  <tr>
    <td width="25%"><b>URL</b></td>
    <td width="75%" >
        Enter the relevant URL for the HTTP request. The POST method is set by default for the form authentication.<br><br>
        <font color="green"><b>Pro Tips:</b></font>
        <ul>
            <li>
                This is <b>not</b> the URL where the login form resides, but the URL where the form request is sent to. The form host URL can be the same as the request URL, but can be different as well. You can get the <b>Request URL</b> in the <b>Headers</b> section of the relevant login request.
            </li>
            <li>
                Form login type will encode any URL-encoded values as required by the protocol, this means that values (user, pass) should be entered without encoding to avoid double encoding issues.
            </li>
        </ul>
    </td>
  </tr>
  <tr>
    <td width="25%"><b>Parameter name</b></td>
    <td width="75%" >
        Enter the form parameters from the request body. For example, username and password.
    </td>
  </tr>
  <tr>
    <td width="25%"><b>Parameter value</b></td>
    <td width="75%" >
        Enter the values of the form parameters (credentials) from the request bodies.
    </td>
  </tr>
  <tr>
    <td width="25%"><b>Maximum number of redirects to follow</b></td>
    <td width="75%" >
        Enter the maximum number of redirections that the Nexploit should follow during the authentication process.
    </td>
  </tr>
  <tr>
    <td width="25%"><b>Additional headers</b></td>
    <td width="75%" >
        <em>(Optional)</em> Select an additional header and enter its value. Then select the relative button to replace or append it to each request. For example, additional cookies that might be needed for the authentication such as host-related metadata.<br><br>
        <font color="green"><b>Pro Tips:</b></font>
        <ul>
            <li>
                Make sure that the values you use for the additional headers are static and must not be changed between scans.
            </li>
            <li>
                If your application uses cookies that are set via the Set-Cookie header in the response, then you do not need to extract and reuse the cookies. Any Set-Cookie header will be automatically used during authentication.  
            </li>
             <li>
                There are cases when MFA is required  ONLY on initial IP login. This means that our scan IP can be validated once and will not require any further MFA validations. For that case, you need to identify which cookie supports the completed MFA/2FA and include a valid cookie as a part of your authentication object, typically using the <b>Additional Headers</b> field.  
            </li>
        </ul>
    </td>
  </tr>
</table>

* For some parameters, you can add more fields by clicking ![plus-icon](../media/plus-icon.png ':size=2%') at the upper-right of the relevant setup section. 
* To delete a parameter, click ![trash-icon](../media/trash-icon.png ':size=3%') next to the relevant **Value** field.

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
    <td width="25%"><b>Protocol </b></td>
    <td width="75%" >
       From the drop-down list, select the <b>HTTPS</b> or <b>WebSockets</b> protocol to be used for authentication. 
    </td>
  </tr>
  <td width="25%"><b>Method </b></td>
    <td width="75%" >
       Select the HTTP method of an active tester end-point (authenticated resource). 
    </td>
  </tr>
  <tr>
    <td width="25%"><b>Validation URL </b></td>
    <td width="75%" >
       Enter the URL of the authenticated (protected) resource to test if the authentication scenario is configured correctly. The validation URL should be different from the authentication URL.   
    </td>
  </tr>
  <tr>
    <td width="25%"><b>Header name </b></td>
    <td width="75%" >
       Select an additional header to be appended to the request sent to the tester end-point. 
    </td>
  </tr>
  <tr>
    <td width="25%"><b>Header value </b></td>
    <td width="75%" >
       Enter the template of the expected value (interpolation string) created using the <a href="/#/guide/np-web-ui/scanning/managing-authentications/syntax.md">String Interpolation Syntax</a>.   
    </td>
  </tr>
  <tr>
    <td width="25%"><b>Body </b></td>
    <td width="75%" >    
       Enter the HTTP request body to be appended to the request sent to the tester end-point, for example:{“user”: “foo”, “pass”: “bar”}’. You can interpolate the body using the <a href="/#/guide/np-web-ui/scanning/managing-authentications/syntax.md">String Interpolation Syntax</a>.   
    </td>
  </tr>
  <tr>
    <td width="25%"><b>Maximum number of redirects to follow </b></td>
    <td width="75%" >
       Enter the maximum number of redirections that Nexploit should follow during the authentication process.   
    </td>
  </tr>
   <tr>
    <td width="25%"><b>Repeater </b></td>
    <td width="75%" >
       If you use a local Repeater to reach the scan target, select it from the drop-down list to connect it to the scan.   
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