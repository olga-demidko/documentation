# Configuring the Header Authentication in Nexploit
You can use the header authentication method if the login-protected resources within the application you want to scan require one or more static header authentication tokens. 

  >[!NOTE|label:Note]
  In case a specified authentication token expires, the authentication object will no longer provide Nexploit with the ability to reach authenticated resources of that particular target.

## Prerequisites
*  You are an active user on [nexploit.app](https://nexploit.app/scans).
*   Your application and authenticated resources are accessible to Nexploit, either directly from the Internet or via a Repeater. 

## Step-by-Step Guide
1. Go to [nexploit.app](https://nexploit.app/scans).
2. On the default **Scans** page, click **My Authentications**.

  ![my-authentications](../media/my-authentications.png ':size=45%')

3. On the **My Authentications** page, click **+ New Authentication**.

  ![auth-plus](../media/auth-plus.png ':size=45%')

4. In the **CREATE & TEST AUTHENTICATION** dialog box, complete the fields of the following configuration sections.

#### Authentication Details

In this section, specify the details of the authentication object you want to create.

![header-auth](../media/header-name-description.png ':size=45%')

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
       From the <b>Authentication type</b> drop-down list, select <b>Header authentication</b>.
    </td>
  </tr>
</table>

#### Authentication Setup 

In this section, set up a valid authentication request to be sent to the end-point API. 

![header-setup](../media/header-setup.png ':size=45%')

<table id="simple-table">
  <tr>
    <th width="25%"><b>Field</b></th>
    <th width="75%"><b>Guidelines</b></th>
  </tr>
  <tr>
    <td width="25%"><b>Name</b></td>
    <td width="75%" >
    Select the header you need to use for each request and enter its value, for example authentication cookies. <br>To replace or append the selected header to each request, select the relative button below.
    </td>
  </tr>
  <tr>
    <td width="25%"><b> Value</b></td>
    <td width="75%" >
    Enter the header value.
    </td>
  </tr>
</table>

* To add more fields for parameters, click ![plus-icon](../media/plus-icon.png ':size=2%') at the upper-right of the relevant setup section. 
* To delete a parameter, click ![trash-icon](../media/trash-icon.png ':size=3%') next to the relevant **Value** field.

> [!TIP|label:Pro Tip]
There are cases when MFA is required  ONLY on initial IP login. This means that our scan IP can be validated once and will not require any further MFA validations. For that case, you need to identify which cookie supports the completed MFA/2FA and include a valid cookie as a part of your authentication object.

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
  <tr>
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
  
*   A valid authentication object returns three success messages indicated in the relevant  **Test Results** sections: 
     *   **Test Authentication Triggers**
     *   **Access Protected Resource**

  ![header-testing](../media/header-results.png ':size=45%') 

   In this case, you can save the configured object and add it to your scans.

* If the test results include a failure message, go back to the object configurations and verify their correctness. Use the test request/response data to find a certain failure and fix it.

