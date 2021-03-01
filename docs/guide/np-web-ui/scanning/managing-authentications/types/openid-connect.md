# Configuring the OIDC authentication in NexPloit
If you need to grant NexPloit access to the authenticated resources that support OIDC, you should configure an authentication object using the OpenID Connect. 

>[!NOTE|label:Note]
Currently only the **Customer Credentials** grant type of the OIDC is supported.

## Prerequisites
*   You are an active user on [nexploit.app](https://nexploit.app/scans).
*   Your application and authenticated resources are accessible to NexPloit, either directly from the Internet or via a Repeater.

## OpenID Connect Setup Fields 
The table below lists and describes the **Authentication Setup** fields in the **OpenID Connect** authentication section.

<table id="simple-table">
  <tr>
    <th width="25%"> <b><u>Field</u></b></td>
    <th width="75%"><b><u>Guidelines</u></b></td>
  </tr>
  <tr>
    <td width="25%"><b>Discovery document URL</b></td>
    <td width="75%" >
        Provide a discovery document URL (https://your_host/.well-known/openid-configuration) to populate endpoint URLs automatically or leave this field empty to enter endpoint URLs manually.
    </td>
  </tr>
  <tr>
    <td width="25%"><b>Token Endpoint</b></td>
    <td width="75%" >   
        Obtain an access and/or ID token by presenting an authorization grant or refresh token.
    </td>
  </tr>
  <tr>
    <td width="25%"><b>Client ID</b></td>
    <td width="75%" >      
        Enter your app's client ID, unique client identifier preregistered in OpenID Provider.
    </td>
  </tr>
  <tr>
    <td width="25%"><b>Client Secret</b></td>
    <td width="75%" >
        Enter your app's client secret, used to authenticate to the Token Endpoint
    </td>
  </tr>
  <tr>
    <td width="25%"><b>Scope</b></td>
    <td width="75%" >
        Enter a space-separated list of scopes.
    </td>
  </tr>
   <tr>
    <td width="25%"><b>Audience</b></td>
    <td width="75%" >
        <em>(Optional)</em> Enter the intended recipient of the token.
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
    * From the **Authentication type** dropdown list, select **OpenID Connect**.

  ![Open-id](../media/open-id.png ':size=45%')

    * Complete the Authentication Setup fields.

   ![open-id-setup](../media/open-id-setup.png ':size=45%')

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

7. In the **Validation URL** field, do the following:<br>
  a) Enter the URL of an authenticated resource within your application.<br>
  b) If you use a local Repeater to reach the scan target, from the **Repeater** dropdown list, select the Repeater you need for the scan.<br>
  c) Click  ![test-button](../media/test-button.png ':size=17%'). <br>  The preliminary testing helps you verify if the authentication object has been configured correctly.

    ![test-authentication](../media/test-authentication.png ':size=45%') 

    *   A valid authentication object returns three success messages indicated in the relevant  **Test Results** sections: 
        *   **Detection of the invalid session**
        *   **Authentication call**
        *   **Valid session flow**

  ![test-results](../media/test-results.png ':size=45%') 

    In this case, you can save the configured object and add it to your scans.

    * If the test results include a failure message, go back to the object configurations and verify their correctness. Use the test request/response data to find a certain failure and fix it.