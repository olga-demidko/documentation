# Configuring the API Calls Authentication in NexPloit
If you need to enable NexPloit to reach an authenticated resource by sending API requests with a customized body, you should use the API call authentication method. This authentication method is the most flexible and provides multiple methods of HTTP requests.

## Prerequisites
*   You are an active user on [nexploit.app](https://nexploit.app/scans).
*   Your application and authenticated resources are accessible to NexPloit, either directly from the Internet or via a Repeater.

## API Call Setup Fields 
The table below lists and describes the **Authentication Setup** fields in the **API Calls** section.


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
