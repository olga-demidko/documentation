# Configuring the Header Authentication in NexPloit
You can use the header authentication method if the login-protected resources within the application you want to scan require one or more static header authentication tokens. 

  >[!NOTE|label:Note]
  In case a specified authentication token expires, the authentication object will no longer provide NexPloit with the ability to reach authenticated resources of that particular target.

## Prerequisites
 *   You are an active user on [nexploit.app](https://nexploit.app/scans).
*   Your application and authenticated resources are accessible to NexPloit, either directly from the Internet or via a Repeater. 

## Step-by-Step Guide
1. Go to [nexploit.app](https://nexploit.app/scans).
2. On the default **Scans** page, click **My Authentications**.

    ![my-authentications](../media/my-authentications.png ':size=45%')

 3. On the **My Authentications** page, click ![plus-icon](media/authentications/plus-icon.png ':size=2%') next to **AUTHENTICATION**.