# OKTA SSO
![okta](media/okta/okta-logo.png ':size=15%')

## Configuring NexPloit OIDC Using Okta
To simplify user access to NeuraLegion solutions, Single Sign On (SSO) can be configured for Okta.
>[!NOTE|label:Note]
Currently, Okta/NexPloit OIDC integration only supports SP-initiated SSO.

## Enabling Okta for the Organization
To enable Okta for an organization –
1. Log in to your Okta organization account.
2. Add the NexPloit app, if it is not already added and assign users to the app.
3. Set up redirection URLs, if required. Set them to `https://nexploit.app/okta/callback`.
4. Copy the client ID and client secret plus metadata URLs. The format of metadata URLs is `https://{org_slug}.okta.com/.well-known/openid-configuration`.
5. Log in to NexPloit.
6. Select the **Organization** option in the left pane to display the Organization page.
7. Scroll down to the **AUTHENTICATION** section.\
![authentication-panel](media/okta/authentication-panel.png ':size=45%')
8. Click ![dots](media/okta/dots-button.png ':size=1%') next to Okta and then click the **Install** button.\
![okta-install](media/okta/okta-install.png ':size=45%')
9. Enter your Okta integration details and click Continue.\
![okta-settings](media/okta/okta-settings.png ':size=45%')

After Okta SSO is set up, an email is sent to all the users in your organization informing them to confirm their accounts and link their Okta profiles to NexPloit profiles.

## Using Okta SSO
The SSO option becomes available once Okta SSO is configured for the organization.
To log in to Okta using SSO –
1. In the login screen, click the **Single Sign On (SSO)** button.\
![sso-button](media/okta/sso-button.png ':size=45%')
2. Enter your NexPloit organization name and click **Continue**.\
![sso-organization](media/okta/sso-organization.png ':size=45%')
3. Select **Okta**.\
![sso-okta](media/okta/sso-okta.png ':size=45%')
4. You are redirected to the Okta login page. Enter your Okta credentials and click **Sign In**.\
![okta-login](media/okta/okta-login.png ':size=45%')
