<table id="integrations" >
  <tr>
    <td width="70%">
      <h1>SSO and SCIM Provisioning of Users and Groups with Azure AD
</h1>
    </td>
    <td width="30%" style="text-align:center" rowspan="3">
      <img src="guide/pipeline-integration/sso/media/azure/aad-new-logo.png" width="200" height="250"></img>
    </td>
  </tr>
  <tr>
    <td style="text-align:left;vertical-align:text-top;padding:0px">
      <p>System for Cross-domain Identity Management (SCIM) is a protocol for user management across multiple applications. It allows you to easily provision (add), deprovision (delete) and update (map) user data across multiple applications at once. </p>
      <p>You can set up SCIM provisioning in Azure AD to automatically add the AD application users and groups to your organization on nexploit.app. The added users will be able to access NexPloit using Active Directory Federation Services (AD FS) SSO.</p>
    </td>
  </tr>
</table>

NexPloit supports the following user mapping attributes:
* `userName` (the user’s email address)
* `name.givenName`(first name)
* `name.familyName` (second name)

## Prerequisites

* You are an active user on  [nexploit.app](https://nexploit.app). 
* You have a valid [organization API key](https://kb.neuralegion.com/#/guide/np-web-ui/advanced-set-up/managing-org?id=managing-organization-apicli-authentication-tokens) with the `scim` scope.

## Setup

To enable NexPloit SSO with AD FS, you should first authenticate Azure AD in Nexploit.
1. Register NexPloit in Azure AD. For that, in the **App registrations** section, click **+ New registration**.

  ![azure-register](media/azure/new-registration.png ':size=45%')

  On the **Register an application** page, do the following:<br>
    * Enter `NexPloit` in the **Name** field.<br>
    * In the **Redirect URL (optional)** section, enter `https://nexploit.app/adfs/callback`. <br>
    * Click **Register**.

  ![azure-register](media/azure/register-nexploit.png ':size=45%')

  > [!NOTE|label:Note]
  It may take some time until the predifined application is published in the Azure AD gallery.

2. In the created application, get the following credentials to use them further on nexploit.app:
   * On the application page, copy the **Client ID**.

  ![client-id](media/azure/client-ID.png ':size=45%')

   * In the **Certificates & secrets** tab, create a new secret key and copy its **ID**.

  ![sectret-id](media/azure/secret-key.png ':size=45%')

   * In the **Endpoints** tab, copy the **OpenID Connect metadata document** URL.  
 
  ![metadata-url](media/azure/endpoints.png ':size=45%')

Now go to nexploit.app and do the following:
1. Select the **Organization** option in the left pane.
2. From the **Required SSO provider** drop-down list, select **AD FS**, and then click **Connect**.

  ![sso-connect](media/azure/sso-connect.png ':size=45%')

3. Fill in the **AD FS Authentication** fields with the credentials copied in Azure AD, and then click **Continue**.

  ![setup](media/azure/continue-setup.png ':size=45%')

4. On the Microsoft **Permissions Requested** page, click **Accept**.

Now the AD FS SSO is enabled for all the users of the authenticated application with no limitations. 

> [!TIP|label:Pro Tip]
You can enable a forced AD FS SSO registration by selecting the **Require your organization members to use SSO to access NexPloit** checkbox. When this option is selected, only the registered users (current members of a NexPloit organization) with existing SSO accounts can access NexPloit.

Go to Step-by-Step Guide to configure automatic provisioning of Azure AD users and groups to your NexPloit organization.

## Step-by-Step Guide

#### Enable Provisioning

1. In the **ORGANIZATION SETTING** section, select the **Sync the groups & users from SSO provider to NexPloit** checkbox.

  ![sync-option](media/azure/sync-users-groups.png ':size=45%')

2. In Azure AC, go to the provisioning section of your application and click **Get Started**. 

  ![provisioning](media/azure/provisioning.png ':size=45%')

3. Select one of the following provisioning modes:

  ![provisioning-mode](media/azure/provisioning-mode.png ':size=45%')

    * **Manual** option allows you to add a new user or group to your NexPloit organization manually with immediate synchronization.
    * **Automatic** mode enables adding every new user or group to your NexPloit organization automatically. The automatic provisioning interval is 40 minutes.



4. In the **Admin Credentials** section, do the following:

  ![admin-credentials](media/azure/admin-credentials.png ':size=45%')

   * In the **Tenant URL** field, enter `https://nexploit.app/api/v1/scim`.
   * In the **Secret Token** field, enter the API key created on nexploit.app.

5. Click **Test Connection** to verify the credentials that are authorized for provisioning.

6. _(Optional)_ In the **Settings** section, make sure to set the scope to **Sync only assigned users and groups**. This will ensure that the provisioning will be limited to assigned users/groups only, and that no other Azure AD users will have access to nexploit.app unintendedly.

  ![assigned-users](media/azure/assigned-users.png ':size=45%')

7. Above the **Provisioning mode**, click **Save** to save the configuration.

8. To start provisioning, go back to your application page and click **Start provisioning**.

  ![start-provisioning](media/azure/start-provisioning.png ':size=45%')

#### Assign Azure AD Users and Groups to Your NexPloit Organization

1. In the left pane, select **Users and groups**.
2. Click **+ Add user/group**.

  ![add-users](media/azure/add-users.png ':size=45%')

3. In the **Users and groups** field, click **None Selected**. Select specific users or a group of users to sync them to your NexPloit organization, and then click **Assign**.

  ![add-assignment](media/azure/add-assignment.png ':size=45%')

   * The assigned users will be automatically added to the **MEMBERS** section of your NexPloit organization. 
   * The assigned groups will be automatically added to the **GROUPS** section of your NexPloit organization. 

   ![nexploit-organization](media/azure/nexploit-organization.png ':size=45%')

   > [!NOTE|label:Note]
  If you deprovision a user from the NexPloit application in Azure AD, the relative member turns inactive in your NexPloit organization and is no longer able to log in to nexploit.app using AD FS SSO. 

#### Log in to NexPloit Using AD FS SSO


1. On the login page, click **Single Sign On (SSO)**.

  ![sso-button](media/azure/sso-button.png ':size=45%')

2. Enter the name of the application registered for NexPloit in Azure AD, and then click **Continue**.

  ![sso-organization](media/azure/sso-organization.png ':size=45%')

3. Select **Sign in with AD FS**.

  ![sso-adfs](media/azure/sso-adfs.png ':size=45%')

  You are redirected to the Microsoft login page.

4. Enter your Azure AD user's credentials.

  ![adfs-login](media/azure/adfs-sign-in.png ':size=30%')























