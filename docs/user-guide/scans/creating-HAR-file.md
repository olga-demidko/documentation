# Creating a HAR file
A HAR file is basically a recording of a user session with an application. It can be gathered in a few ways - you can either use a QA tool (such as Selenium) or gather it manually with your web browser's built in DevTools.

## Gathering a HAR file using DevTools

1. In your browser, open the DevTools (in most browsers you can do that by hitting the F12 key on your keyboard). Once open, go to the "Network" tab.

![devtools](media/devtools.png ':size=100%')

2. Make sure that the "Preserve log" and "Disable cache" checkboxes are checked.

![checkboxes](media/devtools-settings.png ':size=100%')

3. With the devtools panel open, browse to your application. You'll see all the requests recorded in the devtools panel.

  !> **Pro Tip:** You don't have to record your whole application or to begin at the main page, but remember that to scan parts of your application that rquire authentication, you have to include the login part of your application in your recording.

![requests](media/requests.png ':size=100%')

4. Interact with your application just like a normal user would. Remember to go over all the parts you'd like to have in the scope of your scan.

5. Once you've recorded all the application parts you wanted, right click on any of the requests in the devtools panel and choose the "Save all as HAR" option.

![save-as-har](media/save-as-har.png ':size=100%')

6. Save the file in your desired location, and then upload it to NexPloit (when [starting a new scan](user-guide/scans/new-scan.md)).