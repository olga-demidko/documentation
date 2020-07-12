# Organization Administration {docsify-ignore}
1. To get to your organization's settings go to the **Organization** tab on the left of your dashboard.

![Organization Administration 01](media/organization-administration-01.png ':size=100%')

2. You will reach the **Organization** page, where you can:
  - [Configure 2FA Policy](#2fa-policy-configuration)
  - [See Organization Plan Details](#organization-plan-details)
  - [Manage Users](#user-management)
    - [Add Users](#adding-new-user)
  - [Manage Groups](#group-management)
    - [Create New Groups](#creating-new-groups)
    - [Add / Remove a User From a Group](#adding-or-removing-a-user-from-a-group)
  - [Manage Organization API Keys](#managing-organization-api-keys)

![Organization Administration 02](media/organization-administration-02.png ':size=100%')

## 2FA Policy Configuration
You can require all the users in your organization to use 2FA. Before you apply this policy it is recommended that you notify your users so that they have time to enable 2FA for their accounts.
To apply this policy simply tick the checkbox under the **ORGANIZATION SETTINGS** panel.

In addition, an admin can see the 2FA status of all users in the organization under the **MEMBERS** panel.

!> **Note:** An organization-wide 2FA policy can not be set to mendatory untill all admin users set up their own 2FA.

!> **Note:** When enabling an organization-wide 2FA policy, users without 2FA already set up will have their account disabled until they do. An email notification will be sent automatically to each user in this case.

![Organization Policies 03](media/organization-administration-03.png ':size=100%')

## Organization Plan Details
In the Organization Plan Details panel you can see information about you plan, such as whether you are using NexPloit or NexDast, how much storage does your Organization have in total, the plan's expiration date and more.

![Organization Policies 12](media/organization-administration-12.png ':size=100%')

## User Management
Here you can manage the users in your organization

### Adding new Users
1. To add a new user to your organization simply click the ![Organization_Policies_01](media/new-user_button.png ':size=3%') button at the top of the page.

![Organization Policies 02](media/organization-administration-04.png ':size=100%')

2. You can update user information and role in the organization. Once done, just click the ![Invite_button](media/invite_button.png ':size=5%') button. Possible user roles are:

- **Owner** - has unrestricted access to the whole organization.
- **Admin** - Can add, modify and delete groups and members, can make billing and plan changes.
- **User** - Can be given access to scans
- **Team Leader** - Can manage memberships and modify settings of groups the belong to.
- **Billing Manager** - Can manage subscription and billing settings.

![Organization Policies 03](media/organization-administration-05.png ':size=100%')

## Group Management
Here you can manage groups of users

### Creating new Groups
To create a new group, simply click the ![new-group_button](media/new-group_button.png ':size=3%') button at the top of the page.

![Organization Policies 04](media/organization-administration-06.png ':size=100%')

Now fill in the details of the group and set you desired settings (integrations, concurrent scans limit) and add members to the group. Once done just click the ![new-group_button](media/create_button.png ':size=5%') button at the top.

![Organization Policies 05](media/organization-administration-07.png ':size=100%')

### Adding or Removing a User From a Group

To add or remove a user from an existing group, first select this user from the members panel.

![Groups 03](media/organization-administration-10.png ':size=100%')

Now just tick the checkboxes next to the groups you'd like this user to be a member of.

![Groups 04](media/organization-administration-11.png ':size=100%')

## Managing Organization API Keys

To get a new API key, simply go to the **MANAGE YOUR USER API KEYS** panel and click the ![api_button](media/api_button.png ':size=14%') button.

![Organization Policies 05](media/organization-administration-08.png ':size=100%')

Now give the API key a name and select which scopes to apply to it and click the ![create_button](media/create_button.png ':size=5%') button.

![Organization Policies 06](media/organization-administration-09.png ':size=100%')