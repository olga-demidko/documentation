# Managing Your Organization
The **Organization** option enables NexPloit administrators to manage organization-level settings and policies, including –
* [Displaying the Organization Dashboard](#Displaying-the-Organization-Dashboard)
* [Configuring Two-factor Authentication Policy](#Configuring-Two-factor-Authentication-Policy)
* [Defining the Hosts Authorized for Scanning](#Defining-the-Hosts-Authorized-for-Scanning)
* [Viewing Your Organization’s Plan](#Viewing-your-Organizations-Plan)
* [Managing Users](#Managing-Users-Members)
* [Managing Groups](#Managing-groups)

## Displaying the Organization Dashboard
To view the Organization dashboard select the **Organization** option in the left pane. The following displays –\
![Dashboard](media/dashboard.png ':size=45%')

## Configuring Two-factor Authentication Policy
You can require that all users in your organization use Two-factor authentication (2FA). Before applying this policy, we recommend giving your users prior notice so that they have time to enable 2FA for their accounts. 

To apply 2FA to user accounts check the relevant checkbox in the **ORGANIZATION SETTINGS** section.
![2FA](media/2fa.png ':size=45%')

An administrator can see the 2FA status of each user in the organization in the **MEMBERS** section.
>[!NOTE|label:Note]
An organization-wide 2FA policy cannot be set to mandatory until all administrative users have set up their own 2FA.

>[!NOTE|label:Note]
When enabling an organization-wide 2FA policy, the accounts of users without 2FA already set up are disabled until they do so. In this case, an email notification is automatically sent to each affected user.

## Defining the Hosts Authorized for Scanning
As a precaution, NexPloit only allows hosts that are in the authorized list defined below to be scanned. 

To add a target host to the authorized list of hosts –
1. Add a `.nex` file to your application's root directory. To obtain this file, click the `.nex` link at the bottom of the **ORGANIZATION SETTINGS** section.\
![Get-Nex-File](media/get-nex-file.png ':size=45%')
2. Save this file in a convenient place and then put it in your application's root directory. You can reuse this file as many times as needed.

## Viewing Your Organization’s Plan
The Organization **PLAN DETAILS** section displays information about your account with NeuraLegion, such as whether you are using NexPloit, the total storage for your organization, the plan's expiration date and so on. 

To view organization plan details click the **Plan Details** section.\
![Plan-Details](media/plan-details.png ':size=45%')

## Managing Users (Members)
To manage the users in your organization –
* [Add a New User](#Adding-a-User)
* [Delete a User](#Deleting-a-User)

### Adding a User
To add a user –
1. Click the ![Add-User](media/new-user-button.png ':size=4%') button at the top of the page.\
![Add-User](media/new-user-fullscreen.png ':size=45%')\
The following displays –\
![Add-User-Prompt](media/new-user-prompt.png ':size=45%')
2. Update the user’s information and role in the organization. Possible user roles are –
    * **Owner –** Has unrestricted access to the entire organization.
    * **Admin –** Can add, modify and delete groups and members, as well as make billing and plan changes.
    * **User –** Can be given access to scans.
    * **Team Leader –** Can manage group memberships and modify group settings.
    * **Billing Manager –** Can manage subscription and billing settings.
3. Click the **Invite** button.

### Deleting a User
To delete a user –
1. In the **MEMBERS** section, click the row of the user to be deleted.\
![Members](media/members.png ':size=45%')
2. Click the ![Remove-Button](media/remove-button.png ':size=3%') button at the top of the screen.\
![Remove-User](media/remove-user.png ':size=45%')
3. Click the **OK** button in the popup message to confirm the deletion.\
![Remove-User-Prompt](media/remove-user-prompt.png ':size=45%')

## Managing Groups
You can perform the following operations to manage user groups in your organization and to define the scope of scanning access permissions assigned to them –
* [Creating a New Group](#Creating-a-new-group)
* [Adding/Removing a User from a Group](#AddingRemoving-a-User-from-a-Group)

### Creating a New Group
To create a new group – 
1. Click the ![New-Group-Button](media/new-group-button.png ':size=4%') button at the top of the page.\
![New-Group](media/new-group.png ':size=45%')
2. Fill in the details of the group, define the scope of access permissions awarded to the users of this group (integrations, concurrent scans limit) and add members (users) to the group.\
![New-Group-Form](media/new-group-form.png ':size=45%')
3. Click the Create button at the top.

### Adding/Removing a User from a Group
To add or remove a user from a group – 
1. Select the row of the user in the **MEMBERS** section.\
![Members](media/members.png ':size=45%')
2. Check the checkboxes next to the group(s) to which to assign that user as a member.\
![Remove-User-From-Group](media/remove-user-from-group.png ':size=45%')

## Managing Organization API/CLI Authentication Tokens
The following describes how to obtain and manage authentication tokens (also called an API keys) for accessing the NexPloit API and CLI.

To obtain a new API/CLI Authentication Token (API key) –
1. Go to the **MANAGE YOUR ORGANIZATION API KEYS** section and click the ![Create-new-API-Key-Button](media/new-api-key-button.png ':size=18%') button.\
![New-API-Key](media/new-api-key.png ':size=45%')
2. Assign the API key a name, select which scope(s) of access to allow it and which type of actions (such as read or write) it is permitted to perform and click the **Create** button.\
![New-API-Key-Prompt](media/new-api-key-prompt.png ':size=45%')


