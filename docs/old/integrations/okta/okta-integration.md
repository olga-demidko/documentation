# Configure NexPloit OIDC with Okta

![okta_logo](media/okta-logo.png ':size=30%')


## About
To make it much easier for users to access our solutions, it is possible to configure "Single Sign On" (SSO) with Okta.
 
!> **Note:** The Okta/NexPloit OIDC integration currently supports only "SP-initiated SSO".

## Enable Okta For The Organization
1. Login to your Okta organization account

<!-- ![okta_organization_page1](media/okta-organization-page-01.png ':size=45%') -->

2. Add the NexPloit app, if it is not already added, and assign users to the app.

<!-- ![okta_organization_page2](media/okta-organization-page-02.png ':size=45%') -->

3. Setup redirection urls if required. (set them to https://nexploit.app/okta/callback)

<!-- ![okta_organization_page3](media/okta-organization-page-03.png ':size=45%') -->

4. Copy client id and client secret as well as metadata url. (format of metadata url: https://{org_slug}.okta.com/.well-known/openid-configuration)

<!-- ![okta_organization_page4](media/okta-organization-page-04.png ':size=45%') -->

5. Login to NexPloit and navigate to the [organization page](https://nexploit.app/organization) by clicking on the **Organization** button on the sidebar.

![organization_from_scans](../../media/organization-from-scans.png ':size=45%')

6. Scroll down to the **AUTHENTICATION** section.

![organization_authentication](../../media/organization-authentication.png ':size=45%')

3. Click on **⋮** and then on **Install** next to **Okta**

![organization_okta_install](media/organization-okta-install.png ':size=45%')

4. Fill out your **Okta Integration Details** and click on **Conntinue**

![okta_settings](media/okta-settings.png ':size=45%')

5. This will setup Okta SSO and send an email to all the users in your organization, to confirm their accounts and link the Okta profiles to NexPloit profiles.

## Using Okta SSO
After **Okta SSO** was configured for the organization, the SSO option is available.

1. On the login screen click on **Single Sign On (SSO)** button.

![sso_button](media/sso-button.png ':size=45%')

2. Enter your NexPloit organization name and click on **Continue**

![sso_organization](media/sso-organization.png ':size=45%')

3. Select **Okta** 

![sso_okta](media/sso-okta.png ':size=45%')

4. You will be redirected to the **Okta Login Page**, fill out your details and done.

![okta_login](media/okta-login.png ':size=45%')
