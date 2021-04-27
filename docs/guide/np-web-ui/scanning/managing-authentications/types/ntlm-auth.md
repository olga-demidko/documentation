# Configuring the NTLM Authentication in Nexploit
If the target network uses the NTLM protocol to verify user’s access rights, you need to set up an NTLM authentication object. The protocol requires a user to be authenticated by providing a username and a corresponding password. After the user’s log-in credentials have been recognized, the network can then check access rights and allow the user to enter. 

Therefore, you can grant Nexploit access to an NTLM authenticated network you are going to use for a scan by providing  your credentials, workstation name and the network domain. 

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

![ntlm-details](../media/ntlm-details.png ':size=45%')

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
       From the <b>Authentication type</b> drop-down list, select <b>NTLM authentication</b>.
    </td>
  </tr>
</table>

#### Authentication  Setup 

In this section, set up a valid authentication request to be sent to the end-point API. For that, complete the **Authentication Setup** fields.

![ntlm-setup](../media/ntlm-setup.png ':size=45%')

<table id="simple-table">
  <tr>
    <th width="25%"><b>Field</b></th>
    <th width="75%"><b>Guidelines</b></th>
  </tr>
  <tr>
    <td width="25%"><b>Username</b></td>
    <td width="75%" >
        Enter the NTLM username. 
    </td>
  </tr>
  <tr>
    <td width="25%"><b> Password</b></td>
    <td width="75%" >
        Enter the NTLM  password.
    </td>
  </tr>
  <tr>
    <td width="25%"><b>Domain</b></td>
    <td width="75%" >
        Enter the domain of the NTLM network you need to get access to. 
    </td>
  </tr>
  <tr>
    <td width="25%"><b>Workstation</b></td>
    <td width="75%" >
        Enter your workstation name, for example a computer name. The maximum length of a workstation name is 64 characters.
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