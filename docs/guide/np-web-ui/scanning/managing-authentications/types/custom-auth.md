# Configuring the Custom Multi-Step Authentication in NexPloit
If you need to create a custom authentication flow consisting of multiple stages, you should use the custom multi-step authentication method. 

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

  ![custom-auth](../media/custom-auth-details.png ':size=45%')

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
      From the <b>Authentication type</b> drop-down list, select <b>Custom multi-step Authentication</b>.
    </td>
  </tr>
</table>

#### Authentication Flow Setup

In this section, build the authentication flow. You can create a single-stage flow or add as many stages as the NexPloit engine should pass through to access the authenticated resource.

Start the setup with creating the first stage. In the **Name** field, enter the stage name that can be used further for creation of interpolation expressions. 

![stage-name](../media/stage-name.png ':size=45%')

#### Request 

In this section, set up a valid authentication request to be sent to the end-point API. For that, complete the **Authentication Setup** fields.

   ![custom-request](../media/custom-request.png ':size=45%')


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
    Enter the URL of the relevant API end-point. The URL can contain an interpolation string that you can create using the <a href="/#/guide/np-web-ui/scanning/managing-authentications/syntax.md">String Interpolation Syntax</a>.
    </td>
  </tr>
  <tr>
    <td width="25%"><b>Headers</b></td>
    <td width="75%" >       
    Enter an additional header that you want to add to each request and specify its value. You can interpolate the header name and value using the <a href="/#/guide/np-web-ui/scanning/managing-authentications/syntax.md">String Interpolation Syntax</a>. <br><br> 
    </td>
  </tr>
  <tr>
    <td width="25%"><b>Body</b></td>
    <td width="75%" >
        Enter the HTTP request body to use it with the request sent to the API end-point, for example:{“user”: “foo”, “pass”: “bar”}’. You can interpolate the body using the <a href="/#/guide/np-web-ui/scanning/managing-authentications/syntax.md">String Interpolation Syntax</a>.
    </td>
  </tr>
  <td width="25%"><b>Maximum number of redirects to follow</b></td>
    <td width="75%" >
        Enter the maximum number of redirections that Nexploit should follow during the authentication process.
  </table>

  
  * For some parameters, you can add more fields by clicking ![plus-icon](../media/plus-icon.png ':size=2%') at the upper-right of the relevant setup section. 
  * To delete a parameter, click ![trash-icon](../media/trash-icon.png ':size=3%') next to the relevant Value field.

#### Valid Response 

In this section, select the options you want to use during the application scanning to determine that the authenticated resource has been reached. The options define how the application responds in case a full authentication flow passes successfully.

 ![valid-response](../media/custom-valid-response.png ':size=45%')

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

To add another stage required for authentication, click **+ ADD ANOTHER STAGE**.

#### Authorized Requests Setup 

In this section, specify the values to be appended to each request sent to an authenticated resource.

![custom-auth-request](../media/custom-auth-request.png ':size=45%') 

<table id="simple-table">
  <tr>
    <th width="25%"><b>Field</b></th>
    <th width="75%"><b>Guidelines</b></th>
  </tr>
  <tr>
    <td width="25%"><b>Headers </b></td>
    <td width="75%" >
       Specify the name and expected value template of an additional header to be appended to each request. To create the value template, use the <a href="/#/guide/np-web-ui/scanning/managing-authentications/syntax.md">String Interpolation Syntax</a> 
    </td>
  </tr>
  <tr>
    <td width="25%"><b>Content-Type </b></td>
    <td width="75%" >
        Specify the content type of the request body.<br>
        <font color="blue"><b>Note:</b></font> Currently only <code>application/json</code> is supported.
    </td>
  </tr>
  <tr>
    <td width="25%"><b>XPath to parameter</b></td>
    <td width="75%" >
       Specify the exact location of the parameter in the object sent with the requests to the target.
    </td>
  </tr>
  </tr>
  <tr>
    <td width="25%"><b>Value</b></td>
    <td width="75%" >
       Specify the template of the expected value (interpolation string) to be embedded into the target parameter. To create the value template, use the <a href="/#/guide/np-web-ui/scanning/managing-authentications/syntax.md">String Interpolation Syntax</a>.
    </td>
  </tr>
</table>


* For some parameters, you can add more fields by clicking ![plus-icon](../media/plus-icon.png ':size=2%') at the upper-right of the relevant setup section. 
* To delete a parameter, click ![trash-icon](../media/trash-icon.png ':size=3%') to the left of the relevant field.

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
       Currently only the HTTP protocol is supported. 
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

 * A valid authentication object returns three success messages indicated in the relevant  **Test Results** sections: 
     *   **Test Authentication Triggers**
     *   **Authentication call** for each stage
     *   **Access Protected Resource**

 ![test-results](../media/custom-results.png ':size=45%') 

In this case, you can save the configured object and add it to your scans.

 * If the test results include a failure message, go back to the object configurations and verify their correctness. Use the test request/response data to find a certain failure and fix it.
