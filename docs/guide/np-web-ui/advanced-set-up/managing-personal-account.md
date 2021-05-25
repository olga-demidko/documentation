# Managing Your Personal Account Preferences
The following operations are provided for managing your personal account:
* [Accessing Your Personal Account](#Accessing-Your-Personal-Account)
* [Editing Your Name](#Editing-Your-Name)
* [Setting a Password](#Setting-a-Password)
* [Configuring 2FA Policy](#Configuring-2FA-Policy)
* [Setting Time and Date](#Setting-Time-and-Date)
* [Setting Your Notification Preferences](#Setting-Your-Notification-Preferences)
* [Managing Your Personal API Keys (Authentication Tokens)](#Managing-Your-Personal-API-Keys-Authentication-Tokens)

## Accessing Your Personal Account
To access your personal account, click ![User-Button](media/user-button.png ':size=3%') in the upper-right corner of the **Scans** page, and then select **User Settings**.


![Personal-Account](media/personal-account.png ':size=60%')

On the **User Settings** page, you can change your personal settings and preferences.


![Profile-Page](media/profile-page.png ':size=60%')

## Editing Your Name
To edit your name, in the **PROFILE** section, enter your first and last names and click **Save**.


![Edit-Name](media/edit-name.png ':size=60%')

## Setting a Password

If your account has been created via SSO or Social Login, you can create a password to enable direct login to Nexploit. To set a new password or change the existing one, follow these steps:
1. In the lower-right corner of the **PROFILE** section, click **Set password**.
   Nexploit sends you an email with further instructions.  

![Set-password](media/set-password.png ':size=60%')  

2. Follow the instructions provided in the email.

## 	Configuring 2FA Policy
### Enabling 2FA
To enable 2FA for your account, follow these steps:
1. In the **TWO-FACTOR AUTHENTICATION** section, click **Set up using an app**.

![Enable-2FA](media/enable-2fa-1.png ':size=60%')

2. Follow the displayed instructions. 
3. After you finish, paste the provided authentication code into the text box at the bottom of the dialog box and click **Enable**.

![Enable-2FA](media/enable-2fa-2.png ':size=35%')

### Disabling 2FA for Your Account
To disable 2FA for your account, in the **TWO-FACTOR AUTHENTICATION** section, click **Disable**.

>[!NOTE|label:Note]
A user cannot disable their own 2FA policy if an organization-wide 2FA policy is set.

![Disable-2FA](media/2fa-disable.png ':size=35%')

## Changing 2FA Device

To change the 2FA device, follow these steps: 

1. In the **TWO-FACTOR AUTHENTICATION** section, click **Change using an app**.

![Change-2FA-Service](media/change-2fa-device.png ':size=35%')

2. Follow the displayed instructions. 
3. After you finish, paste your authentication code into the text box at the bottom of the dialog box and click **Enable**.

![Change-2FA-Service-2](media/enable-2fa-2.png ':size=35%')

## Setting Time and Date

All your activity on Nexploit, scan runs and details are time-bound. That is why to ensure proper management of the activity log and scans history, you need to verify the date and time settings.  

The current date and time are shown at the top of the **DATE SETTINGS** section. To change the time and date formats, follow these steps:

1. From the **Time Zone** drop-down list, select your time zone.
2. From the **Date Format** drop-down list,  select the format for date indication. 
3. Select the first day of the week and the time format using the relative buttons.

![date-settings](media/date-settings.png ':size=60%')

## Setting Your Notification Preferences
You can define the events related to a certain object type that will be posted in your feed (activity log). Nexploit also allows you to select the types of events you will be notified about via email as well as to deny some specific warnings. 

To enable or disable such event notifications, you simply need to select or clear the relative check boxes in the **FEED SETTINGS**, **EMAIL NOTIFICATION SETTINGS** and **CONSENTS** sections. After you complete the selection, click **Save**.


![Notification-Settings](media/notifications.png ':size=60%')

## 	Managing Your Personal API Keys (Authentication Tokens)
To enable some Nexploit operations and integrations, you will need an authentication token (API key). You can either create an API key in the **Organizatio**n tab or on your **User Settings** page. To create a personal API key, follow these steps:

1. In the **MANAGE YOUR USER API KEYS** section, click **+ New API key**.

![Create-new-API-Key-Button](media/new-api-key-button.png ':size=60%') 

2. Assign the API key a name, select which access scopes to allow it and which type of actions (such as read or write) it is permitted to perform. Read more about the access scopes [here](/guide/np-web-ui/advanced-set-up/managing-scopes/personal-api-key.md). 

![Personal-API-Key-Prompt](media/personal-api-key-prompt.png ':size=35%')

3. Click **Create**.<br>

   On the popup, copy the generated key and save it to a safe place since as soon as you navigate away from this popup, you will not be able to restore this key.<br>
   The created keys without the entire values are listed in the **MANAGE YOUR API KEYS** section.


