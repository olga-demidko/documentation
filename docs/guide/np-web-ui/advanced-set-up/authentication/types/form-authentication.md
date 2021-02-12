# Configuring the Form Authentication in NexPloit
You can use the form authentication if the login-protected resources within the application you want to scan use the application/x-www-form-urlencoded content type of the HTTP requests. 

The form authentication type is set by default when you create an authentication object in NexPloit.  

## Prerequisites
*   You are an active user on [nexploit.app](https://nexploit.app/scans).
*   Your application and authenticated resources are accessible to NexPloit, either directly from the Internet or via a Repeater.

## Form Authentication Setup Fields 
The table below lists and describes the **Authentication Setup** fields in the **Form Authentication** section.

| **Field** | **Guidelines** |
| :-- | :-- |
| **URL** | Enter the relevant URL for the HTTP request. The POST method is set by default for the form authentication. **Pro Tips**:
*   This is **not** the URL where the login form resides, but the URL where the form request is sent to. The form host URL can be the same as the request URL, but can be different as well. You can get the **Request URL** in the **Headers** section of the relevant login request.
*   Form login type will encode any URL-encoded values as required by the protocol, this means that values (user, pass) should be entered without encoding to avoid double encoding issues.| 
| **Parameter name** | Enter the form parameters from the request body. For example,_ _username and password. |
| **Parameter value** | Enter the values of the form parameters (credentials) from the request bodies. |
| **Additional headers** | (Optional)_ Select an additional header that you want to add to each request and enter its value. For example, additional cookies that might be needed for the authentication such as host-related metadata. 
**Pro Tips**: 
*   Make sure that the values you use for the additional headers are static and must not be changed between scans. 
*   If your application uses cookies that are set via the Set-Cookie header in the response, then you do not need to extract and reuse the cookies. Any Set-Cookie header will be automatically used during authentication.  
*   There are cases when MFA is required  ONLY on initial IP login. This means that our scan IP can be validated once and will not require any further MFA validations. For that case, you need to identify which cookie supports the completed MFA/2FA and include a valid cookie as a part of your authentication object, typically using the **Additional Headers** field. |

## Step-by-Step Guide
1. Go to [nexploit.app](https://nexploit.app/scans).
2. On the default **Scans** page, click **My Authentications**.

    ![my-authentications](../media/my-authentications.png ':size=45%')

3. On the **My Authentications** page, click ![plus-icon](../media/plus-icon.png ':size=2%') next to **AUTHENTICATION**.

    ![auth-plus](../media/auth-plus.png ':size=45%')

4. On the **CREATE & TEST AUTHENTICATION** popup, do the following:
    *    In the **Authentication name** field, enter the authentication object name.
    *   _(Optional_) In the **Description** field, enter the authentication object description. For example, you can specify the application type or other information that helps you distinguish your created object.

  ![form-description](../media/form-name-description.png ':size=45%')

    * Complete the Authentication Setup fields.
        * For some parameters, you can add more fields by clicking ![plus-icon](../media/aplus-icon.png ':size=2%') at the upper-right of the relevant setup section. 
        * To delete a parameter, click ![trash-icon](../media/trash-icon.png ':size=2%') next to the relevant Value field.

   ![form-setup](../media/form-setup.png ':size=45%')

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

7. In the **Validation URL** field, enter the URL of an authenticated resource within your application, and then click  ![test-button](../media/test-button.png ':size=2%'). The preliminary testing helps you verify if the authentication object has been configured correctly.

    ![test-authentication](../media/test-authentication.png ':size=45%') 

    *   A valid authentication object returns three success messages indicated in the relevant  **Test Results** sections: 
        *   **Detection of the invalid session**
        *   **Authentication call**
        *   **Valid session flow**

  ![test-results](../media/test-results.png ':size=45%') 

    In this case, you can save the configured object and add it to your scans.

    * If the test results include a failure message, go back to the object configurations and verify their correctness. Use the test request/response data to find a certain failure and fix it.
