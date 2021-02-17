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
  To enable Google for an organization –
  </td>
  </tr>
</table>

1. Log in to NexPloit.
2. Select the **Organization** option in the left pane to display the Organization page.
3. Scroll down to the **AUTHENTICATION** section.\
![authentication-panel](media/google/authentication-panel.png ':size=45%')
4. Click the ![dots-button](media/google/dots-button.png ':size=1%') button next to Google and then click the Install button.\
![google-install](media/google/google-install.png ':size=45%')
5. Set up your Google SSO settings. You must – 
  * Select the default role to which users are assigned during their first login.
  * Select whether to require the members of your organization to use a valid linked SSO account to access your organization.
  * Specify the domain to be used by users when logging in.

  ![google-setup](media/google/google-setup.png ':size=45%')
6. Click the **Continue** button.
7. You are redirected to the Google login page. Sign in to your Google account.\
![google-login](media/google/google-login.png ':size=45%')

## Using Google SSO
The SSO option becomes available once Google SSO is configured for the organization.

To log in to Google using SSO –
1. In the login screen, click the **Single Sign On (SSO)** button.\
![np-login-sso](media/google/np-login-sso.png ':size=45%')
2. Enter your NexPloit organization name and click **Continue**.\
![np-login-sso-org-name](media/google/np-login-sso-org-name.png ':size=45%')
3. Select **Google**.\
![select-google-login](media/google/select-google-login.png ':size=45%')
4. You are redirected to the Google login page. Enter your Google credentials.\
![google-login](media/google/google-login.png ':size=45%')