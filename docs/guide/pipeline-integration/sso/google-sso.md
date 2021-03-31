<table id="integrations" >
  <tr>
    <td width="70%">
      <h1>Google SSO</h1>
    </td>
    <td width="30%" style="text-align:center" rowspan="3">
      <img src="guide/pipeline-integration/sso/media/google/google-new-logo.png" width="200" height="250"></img>
    </td>
  </tr>
  <tr>
    <td style="text-align:left;vertical-align:text-top;padding:0px">
      To simplify user access to NeuraLegion solutions, you can configure Single Sign On (SSO) for Google.
    </td>
  </tr>
  <tr>
  <td>
  <h2>Enabling Google for the Organization</h2>
  </td>
  </tr>
  <tr>
  <td>
  To enable Google for an organization, follow these steps:
  </td>
  </tr>
</table>

1. Log in to NexPloit.
2. In the left pane, select the **Organization** option, and go to the **ORGANIZATION SETTINGS** section.
3. From the **Requires SSO provider**, select **Google**, and then click **Connect**.

  ![google-sso](media/google/google-sso.png ':size=45%')

5. On the **GOOGLE AUTHENTICATION** page, do the following:
   * From the **Default Role** drop-down list, select the default role to which users are assigned upon their first login.
  
   * In the ***Domain** field, specify the domain to be used by users when logging in.

  ![google-setup](media/google/auth-google.png ':size=45%')

6. Click **Continue**.<br>
  You are redirected to the Google login page. 
  
7. Sign in to your Google account.

  ![google-login](media/google/google-login.png ':size=30%')

## Using Google SSO
The SSO option becomes available once Google SSO is configured for the organization.

To log in to NexPloit using Google SSO, follow these steps:
1. On the login page, click **Single Sign On (SSO)**.

  ![sso-button](media/google/sso-button.png ':size=45%')

2. Enter your NexPloit organization name and click **Continue**.

  ![sso-organization](media/google/sso-organization.png ':size=45%')

3. Select **Sign in with Google**.<br>
  You are redirected to the Google login page.

4. Enter your Google credentials.

![google-login](media/google/google-login.png ':size=30%')