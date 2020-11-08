# Configure Azure Active Directory SSO for NexPloit

![aad-logo](media/aad-logo.png)

## About
To make it much easier for users to access our solutions, it is possible to configure "Single Sign On" (SSO) with Azure Active Directory.

## Enable Azure Active Directory SSO Organization
To configure an Azure Active Directory SSO integration, an admin shall:
1. Add an app in the "App registrations" section. Set the callback URL to `https://nexploit.app/adfs/callback`:\
![aad-sso-1](media/aad-sso-1.png ':size=45%')
    * Copy-paste the Application (client) ID into NexPloit client akin to Okta:\
    ![aad-sso-2](media/aad-sso-2.png ':size=45%')
    * Open the "Endpoints" tab and copy-paste the OpenID Connect metadata document endpoint value (`https://login.microsoftonline.com/4e2adb87-2f36-439f-8047-a30b7857fc62/v2.0/.well-known/openid-configuration` on the screenshot) into NexPloit client as _Metadata URL_ akin to Okta:\
    ![aad-sso-3](media/aad-sso-3.png ':size=45%')
2. In the "Authentication" tab, set _Logout URL_ to `https://nexploit.app/logout/adfs`:\
![aad-sso-4](media/aad-sso-4.png ':size=45%')
3. Add a client secret in the "Certificates & secrets" tab and copy its value to NexPlout client akin to Okta:\
![aad-sso-5](media/aad-sso-5.png ':size=45%')
4. Manually add `email`, `offline_access`, `openid` and `profile` permissions in the "API permissions" tab:\
![aad-sso-6](media/aad-sso-6.png ':size=45%')
5. Add `email` claim to the **ID** token:\
![aad-sso-7](media/aad-sso-7.png ':size=45%')
6. **Manually** set `Email` fields (look up for `vl*******@neuralegion.com` on the screenshot) in the "Users" interface for each user. It is **not** set by default by AAD and required for login to work.

Now go to your NexPloit account and perform the following:
1. Go to the "Organization" tab.\
![go-to-organization](media/go-to-organization.png ':size=45%')
2. Scroll down to the "AUTHENTICATION" panel and click the ![dots-button](media/dots_button.png ':size=1%') next to "AD FS".\
![ad-fs](media/ad-fs.png ':size=45%')
3. Click "Install" on the menu that pops up.\
![install](media/install.png ':size=45%')
4. Fill in the information according to the details you have gathered in the steps above and click the ![continue-button](media/continue_button.png ':size=8%').\
![ad-fs-form](media/ad-fs-form.png ':size=45%')

