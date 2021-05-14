# Managing Your Organization
The **Organization** option enables Nexploit administrators to manage organization-level settings and policies, including the following:
* [Displaying the Organization Dashboard](#Displaying-the-Organization-Dashboard)
* [Configuring Two-factor Authentication Policy](#Configuring-Two-factor-Authentication-Policy)
* [Defining the Hosts Authorized for Scanning](#Defining-the-Hosts-Authorized-for-Scanning)
* [Viewing Your Organization’s Plan](#Viewing-your-Organizations-Plan)
* [Managing Users](#Managing-Users-Members)
* [Managing Groups](#Managing-groups)
* [Managing User's Roles](#managing-users-roles)
* [Managing Organization API/CLI Authentication Tokens](#managing-organization-apicli-authentication-tokens)

## Displaying the Organization Dashboard
To view your organization dashboard, in the left pane, select the **Organization** option. 

![Dashboard](media/dashboard.png ':size=67%')

## Configuring Two-Factor Authentication Policy
You can require that all users in your organization use two-factor authentication (2FA). Before applying this policy, we recommend giving your users prior notice so that they have time to enable 2FA for their accounts. 

To apply 2FA to user accounts, select the relevant checkbox in the **ORGANIZATION SETTINGS** section.

![2FA](media/2fa.png ':size=45%')

An administrator can see the 2FA status of each user in the organization in the **MEMBERS** section.
>[!NOTE|label:Note]
An organization-wide 2FA policy cannot be set to mandatory until all the administrative users have set up their own 2FA. <p>
When enabling an organization-wide 2FA policy, the users can access their accounts only after they perform 2FA. In this case, an email notification is automatically sent to each affected user.

## Defining the Hosts Authorized for Scanning
As a precaution, Nexploit only allows hosts that are in the authorized list defined below to be scanned. 

To add a target host to the authorized list of hosts, follow these steps:
1. Add a `.nex` file to your application root directory. To obtain this file, click the `.nex` link at the bottom of the **ORGANIZATION SETTINGS** section.

    ![Get-Nex-File](media/get-nex-file.png ':size=45%')

2. Save this file in a convenient place and then put it in your application root directory. 

>[!NOTE|label:Note]
Make sure that the server can serve this file from the webroot (top directory level or just `/` path) along with the other static resources from that location. 

You can reuse this file as many times as needed.

## Viewing Your Organization Plan
The organization **PLAN DETAILS** section displays information about your Nexploit account, for example total storage for your organization, number of engines and the plan expiration date. 

![Plan-Details](media/plan-details.png ':size=45%')

## Managing Users (Members)
You can manage the users in your organization: 
* [Adding a New User](#Adding-a-User)
* [Viewing a User's Profile](#viewing-a-users-profile)
* [Deleting a User](#Deleting-a-User)

### Adding a User
To add a user, follow these steps:
1. Click ![Add-User](media/new-user-button.png ':size=3%') at the top of the page.

    ![Add-User](media/new-user-fullscreen.png ':size=45%')


2. Update the user’s information and role in the organization. 

    ![Add-User-Prompt](media/new-user-prompt.png ':size=30%')

You can assign one of the following roles to the user: 
* **User –** Has access to scans.
* **Admin –** Can add, modify and delete groups and members, as well as make billing and plan changes.
* **Owner –** Has unrestricted access to the entire organization.
* **Team Leader –** Can manage memberships and modify settings of the groups that they are members of.
* **Billing Manager –** Can manage subscription and billing settings.
* **Guest -**  Can only view scan results (if granted access to the project), but cannot create or delete scans.
* Custom roles - The roles with specific access permissions, created by an Admin or an Owner.

3. Click **Invite**.

### Viewing a User’s Profile

A user’s profile allows you to view the following information: 
* User’s name and email
* Assigned role and granted access scopes
* Membership in the groups of the organization

To view a user’s profile, in the **MEMBERS** section, select the user you want to view the information about.

![view-profile](media/view-profile.png ':size=45%')


### Deleting a User
To delete a user, follow these steps:
1. In the **MEMBERS** section, click the row with the user to be deleted.

    ![Members](media/members.png ':size=45%')

2. Click ![Remove-Button](media/remove-button.png ':size=3%') at the top of the screen.

    ![Remove-User](media/remove-user.png ':size=45%')

3. Click **OK** on the dialog box to confirm the deletion.

## Managing Groups
You can perform the following operations to manage user groups in your organization and define the scope of scanning access permissions assigned to them:
* [Creating a New Group](#Creating-a-new-group)
* [Adding/Removing a User from a Group](#AddingRemoving-a-User-from-a-Group)

### Creating a New Group
To create a new group, follow these steps: 
1. Click ![New-Group-Button](media/new-group-button.png ':size=3%') at the top of the page.

    ![New-Group](media/new-group.png ':size=45%')

2. Fill in the details of the group, define the scope of access permissions assigned to the users of this group (integrations, concurrent scans limit) and add members (users) to the group.

    ![New-Group-Form](media/new-group-form.png ':size=45%')

3. In the upper right corner, click **Create**.

### Adding/Removing a User from a Group
To add or remove a user from a group, follow these steps: 
1. Select the row with the user in the **MEMBERS** section.

    ![Members](media/members.png ':size=45%')

2. Do one of the following:
 * Select the checkboxes next to the group(s) to which to add that user as a member.
 * Clear the checkboxes next to the group(s) from which to remove that user.

    ![Remove-User-From-Group](media/remove-user-from-group.png ':size=45%')


## Managing User’s Roles
You can create a custom role with specific access scopes and assign it to a new user (member) of your organization.  Therefore, all the created users can be granted different scanning and management permissions. 

* [Creating a Custom Role](#creating-a-custom-role)
* [Editing a Custom Role](#editing-a-custom-role)
* [Deleting a Custom Role](#deleting-a-custom-role)

### Creating a Custom Role

Initially, the list of roles includes only the default options. View the **Description** column to check the access permissions provided by each role. 

>[!NOTE|label:Note]
Only the Admin and Owner default roles allow to create and manage custom roles. A Team Lead can only view the custom roles created by an Admin or an Owner

To create a custom role with specific permissions, follow these steps:
1. At the top of the **ROLES** section, click ![plus-icon](media/plus-icon.png ':size=3%').

    ![create-role](media/create-role.png ':size=45%')

2. On the **Create Role** popup, do the following:

    ![create-role-](media/create-role-popup.png ':size=30%')

    a.  In the **Name** field, enter a role name.<p>
    b. _(Optional)_. In the **Description** field, enter a short description of the permissions that a user assigned to this role will be granted.<p>
    c. Select the access scopes for the role. You can find more information about each scope at [Managing Access Scopes](guide/np-web-ui/advanced-set-up/managing-roles/overview.md).<br>
    The list of scopes available for selection depends on your role. You cannot select the roles you do not have access to (such scopes are grayed out).<p>
    d. Click **Create**.<br>
    The created role is added to the end of the list. Please switch to another list page or set an extended number of items to be shown on a page to view the recent custom roles.

   ![custom-role](media/custom-role.png ':size=45%') 

### Editing a Custom Role

You can edit a custom role, for example change the description and access scopes. 

>[!NOTE|label:Note]
The default roles are read-only, you cannot edit or delete them. 

To edit a custom role, do the following:
1. Click ![dots-icon](media/dots-button.png ':size=2%') next to the role you want to edit, and then select **Edit**.

 ![edit-role](media/edit-role.png ':size=45%')

2. On the **Edit Role** popup, make changes to the role and click **Save**.

    ![edit-role-popup](media/edit-role-popup.png ':size=30%')


### Deleting a Custom Role

To delete a custom role, do the following:

1. In the **ROLES** list,  click ![dots-icon](media/dots-button.png ':size=2%')  next to the role you want to delete.
2. From the drop-down list, select **Delete**.

    >[!WARNING|label:Important]
The users assigned to the role that you have deleted automatically lose their permissions and become Guests.

  ![delete-role](media/delete-role.png ':size=45%')


## Managing Organization API/CLI Authentication Tokens
On the **Organization** page, you can obtain and manage authentication tokens (also called API keys) for accessing the Nexploit API and CLI.

To create a new API/CLI authentication token (API key), follow these steps:
1. Go to the **MANAGE YOUR ORGANIZATION API KEYS** section and click **Create new API key** .

    ![New-API-Key](media/new-api-key.png ':size=45%')

2. Assign the API key a name, select which scope(s) of access to allow it and which type of actions (such as read or write) it is permitted to perform. 

    ![New-API-Key-Prompt](media/new-api-key-prompt.png ':size=30%')

3. Click **Create**.

