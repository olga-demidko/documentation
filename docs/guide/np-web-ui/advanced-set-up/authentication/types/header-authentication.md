# Configuring the Header Authentication in NexPloit
You can use the header authentication method if the login-protected resources within the application you want to scan require one or more static header authentication tokens. 

  >[!NOTE|label:Note]
  In case a specified authentication token expires, the authentication object will no longer provide NexPloit with the ability to reach authenticated resources of that particular target.

## Prerequisites
 *   You are an active user on [nexploit.app](https://nexploit.app/scans).
*   Your application and authenticated resources are accessible to NexPloit, either directly from the Internet or via a Repeater. 

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

  ![header-auth](../media/header-name-description.png ':size=45%')

    * In the **Authentication Setup** section, from the **Name** dropdown list, select the header you want to add to each request, for example authentication cookies. And then enter the header value in the **Value** field. 
        * To add more fields for parameters, click ![plus-icon](../media/plus-icon.png ':size=2%') at the upper-right of the relevant setup section. 
        * To delete a parameter, click ![trash-icon](../media/trash-icon.png ':size=3%') next to the relevant Value field.

  ![header-setup](../media/header-setup.png ':size=45%')

   > [!TIP|label:Pro Tip]
   There are cases when MFA is required  ONLY on initial IP login. This means that our scan IP can be validated once and will not require any further MFA validations. For that case, you need to identify which cookie supports the completed MFA/2FA and include a valid cookie as a part of your authentication object.

5. In the **Invalid Authentication Response** section, select the options you want to use during the application scanning to determine if the authenticated session is no longer valid and the authenticated resources cannot be reached. The options define how the application responds in case the authentication session fails:
    *   **Detect using response status** - enter the HTTP response that will tell you about the authentication failure.
    *   **Detect using header pattern** - enter the header and Regex pattern that will tell about the authentication failure.
    *   **Detect using body pattern** - Enter the body pattern that will tell you about the authentication failure.

  
  ![invalid-response](../media/invalid-response.png ':size=45%') 

7. In the **Validation URL** field, enter the URL of an authenticated resource within your application, and then click  ![test-button](../media/test-button.png ':size=17%'). The preliminary testing helps you verify if the authentication object has been configured correctly.

    ![test-authentication](../media/test-authentication.png ':size=45%') 

    *   A valid authentication object returns three success messages indicated in the relevant  **Test Results** sections: 
        *   **Detection of the invalid session**
        *   **Valid session flow**

  ![header-testing](../media/header-testing.png ':size=45%') 

      In this case, you can save the configured object and add it to your scans.

    * If the test results include a failure message, go back to the object configurations and verify their correctness. Use the test request/response data to find a certain failure and fix it.

