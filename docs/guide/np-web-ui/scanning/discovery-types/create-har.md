# Creating a HAR File
<div class="video"> <iframe width="50%"src="https://www.youtube.com/embed/HMpBQ7JkxHI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></div>

An HTTP Archive File (HAR file) is a recorded session of user interaction with an application. The HAR file keeps all the requests and responses between a user and the application you want to target for security scanning. 

Based on the information recorded while navigating through the application, Nexploit can analyze the attack surface of the target and optimize the selected security tests. By loading the HAR file to Nexploit, you ensure the most efficient coverage of the scan target.  

>[!NOTE|label:Note]
The quality of the scan depends directly on the HAR file quality. The more detailed the HAR file, the larger the scan scope can be covered by Nexploit. 

You can use various methods to collect the application behavior information, for example by using a QA tool (such as Selenium). Alternatively, you can create a HAR file manually by using your web browser's built-in DevTools, as described below.

### Step-by-Step Guide <!-- {docsify-ignore} -->
1. In your browser, open the DevTools pane. In most browsers, this can be done using the F12 key on your keyboard or by selecting the **Inspect** option from the browser menu. 

    ![DevTools](../media/open-devtools.png ':size=45%')

2. Select the **Network** tab.

    ![Network-Tab](../media/network-tab.png ':size=45%')

3. Make sure that the **Preserve log** and **Disable cache** checkboxes are selected. This will allow you to persist logs between page refreshes and see the page updates. 

    ![Checkboxes](../media/preserve-log.png ':size=45%')

4. Leave the DevTools pane open and browse to your application. All the application requests are then displayed and recorded in the DevTools panel.

5. Interact with the application in the same way as a normal user would. Remember to use all the resources (parts, options) of the application that you want to be covered by the Nexploit scan.
    > [!TIP|label:Pro Tip]
    If you are using both **Crawler** and **Recording (HAR)** discovery types, there is no need to record all the options in the application or begin at the main page. It is important however to scan the application resources that require authentication. It means that you must log in to such resources so that these actions are included in the recording.

6. Once you complete the recording, right-click any of the requests in the DevTools panel and select the Save all as HAR option.

    ![Save-as-HAR](../media/save-har.png ':size=45%')

7. Save the file in your desired location so that you can select it when [defining a new scan](/guide/np-web-ui/scanning/creating-new-scan.md). 

