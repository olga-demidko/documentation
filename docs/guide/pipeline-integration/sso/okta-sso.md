<table id="integrations" >
  <tr>
    <td width="70%">
      <h1>Okta</h1>
    </td>
    <td width="30%" style="text-align:center" rowspan="3">
      <img src="guide/pipeline-integration/sso/media/okta/okta-new-logo.png" width="200" height="250"></img>
    </td>
  </tr>
  <tr>
    <td style="text-align:left;vertical-align:text-top;padding:0px">
    <h2>Configuring Nexploit OIDC Using Okta</h2>
    </td>
  </tr>
  <tr>
  <td>
  To simplify user access to NeuraLegion solutions, Single Sign On (SSO) can be configured for Okta.
  </td>
  </tr>
</table>

>[!NOTE|label:Note]
Currently, Okta/Nexploit OIDC integration only supports SP-initiated SSO.

## Enabling Okta for the Organization
To enable Okta for an organization, follow these steps:
1. Log in to your Okta organization account.
2. Add the Nexploit app, if it has not been already added, and assign users to the app.
3. Set the redirection URL to `https://nexploit.app/okta/callback`.
4. Copy the client ID, client secret and metadata URL. The metadata URL format is `https://{org_slug}.okta.com/.well-known/openid-configuration`.
5. Log in to Nexploit.
6. In the left pane, select the **Organization** option, and go to the **ORGANIZATION SETTINGS** section.
7. From the **Requires SSO provider**, select **Okta**, and then click **Connect**.

  ![okta-sso](media/okta/okta-sso.png ':size=45%')

8. Enter the OKTA authentication details and click **Continue**.

  ![okta-settings](media/okta/auth-okta.png ':size=45%')

After Okta SSO is set up, an email is sent to all the users in your organization informing them to confirm their accounts and link their Okta profiles to Nexploit profiles.

## Using Okta SSO
The SSO option becomes available once Okta SSO is configured for the organization.
To log in to Nexploit using Okta SSO, follow these steps: 
1. On the login page, click **Single Sign On (SSO)**.

  ![sso-button](media/okta/sso-button.png ':size=45%')

2. Enter your Nexploit organization name and click **Continue**.

  ![sso-organization](media/okta/sso-organization.png ':size=45%')

3. Select **Sign in with Okta**.

4. You are redirected to the Okta login page. Enter your Okta credentials and click **Sign In**.

  ![okta-login](media/okta/okta-login.png ':size=25%')
