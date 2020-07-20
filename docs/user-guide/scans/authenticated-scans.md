## Authenticated Scans

There are a few ways to scan applications that require authentication, you can either [make a HAR file](user-guide/scans/creating-HAR-file.md) which includes the login process to your application, or add an authentication header to your scan.

### Adding an Authentication Header to Your Scans

1. While in your application, after you've logged in, open the devtools panel of your browser (in most browsers, this can be done by hitting the F12 key on your keyboard) and go to the "Network" tab.

![devtools](media/juice-shop-devtools.png ':size=100%')

2. Perform an action with your application to have some requests recorded in your network panel and then click on one of the recorded requests.

![click-on-request](media/juice-shop-select-request.png ':size=100%')

3. Now scroll down to the "Request Headers" category, and find your authentication header. It might be an authorization bearer (as shown in the example below) or an authentication cookie.

![authentication-header](media/juice-shop-auth-bearer.png ':size=100%')

4. Copy the value of the authentication header.

![copy-authentication-header](media/juice-shop-copy-auth-bearer.png ':size=100%')

5. When inititing a new scan, in the scan creation dialog, go to the "Additional settings" category.

![additional-settings](media/additional-settings.png ':size=100%')

6. In the "Additional headers", add your authentication header. Make sure that the key and the value are exactly the same as they were in the request you copied them from.

![additional-settings-auth](media/additional-settings-auth.png ':size=100%')