# Creating a New Scan
1. In the left pane, select the **Scans** option to display **MY SCANS** list. Each scan appears as a single row.
2. On the **Scans** page, click **New Scan** to create a new scan.

    ![New-Scan-Dialogue](media/new-scan.png ':size=45%')

3. _(Optional)_ In order to make the scanning definition process quicker, in the <u>**Templates** tab</u>, you can select a predefined set of scan settings. NexPloit provides the following types of predefined scan settings:

    ![Templates](media/templates.png ':size=45%')

* **Fast Scan** – This is a preconfigured optimized scan, during which the engine automatically determines which tests to run, based on the data types that are detected. Some tests will be skipped in favor of speed.
* **Comprehensive Scan** – All possible tests are performed during the scan. This is the most thorough scan, which takes the longest time to complete.
* **API Scanning** – Predefined tests that are relevant for API targets.

>[!TIP|label:Pro Tip]
In addition, you can define your own scan templates. See [Managing Scan Templates](guide/np-web-ui/scanning/managing-scan-templates.md) for more information.

4. In the <u> **Scan Details** tab</U>, do the following:

 ![Scan-details](media/scan-details.png ':size=45%')

* In the **Scan name** field, enter any free-text name for this scan.
* From the **Project** dropdown list, select the NexPloit project you want to use for the scan.

>[!NOTE|label:Note]
You can start a scan ONLY if a project is selected. If you do not have any projects in NexPloit, select the **Default** one.

* From the **Integrations** dropdown list, select a specific repository where you want to get the scan reports.

5. In the <u>**Scan Targets** tab</u>, do the following:
* In the **Discovery Types** field, select one of the following ways your application attack surface should be mapped (depending on your subscription) – Crawler, Recording (HAR) or Open API: 
  * **Crawler** – This is the simplest option. Simply enter a URL (target host) to scan the whole or a part of the specified application. The crawler will map the entire application attack surface automatically.

  ![Crawler-settings](media/crawler.png ':size=45%')

   To scan only specific parts of your application, use the  ![plus-dark](media/plus-dark.png ':size=3%') button at the right side of the **Targets** section to add multiple URLs.<br> In this case, only the specified sections of the application and everything downstream from them will be scanned.

  * **Recording (HAR)** – Use a pre-recorded session of your application (HAR file), which has been created either manually or automatically (using QA tools, such as Selenium to scan your application). This discovery type enables you to define the scope of a scan and store login information in order to scan areas in your application that require authentication. See [Creating a HAR File](#creating-a-HAR-file) for more information.

  ![Recording](media/recording-har.png ':size=45%')

  >[!TIP|label:Pro Tip]
  To enjoy both full automation and deeper attack surface analysis, you can combine **Crawling** and **Recording (HAR)** in a single scan!

  * **Open API** – Use an `*.yml` file to scan APIs. See Scanning an API for more information.

    ![Recording](media/api-scan.png ':size=45%')

* In the **Coverage Exclusions** section, enter the URLs and parameters that NexPloit should ignore during scanning.

    ![Coverage-exclusions](media/coverage-exclusions.png ':size=45%')

* In the **Attack Surface Optimization** section, you can use the following options to optimize the scanning flow :

    ![attack-optimization](media/attack-optimization.png ':size=45%')

  **Smart scan** – Specify whether to use automatic smart decisions (such as parameter skipping, detection phases and so on) in order to minimize scan time. When this option is turned off, all tests are run on all the parameters, that increases coverage at the expense of scan time.<br>
  **Skip static parameters** – Specify whether to skip static parameters to minimize scan time.<br>
  **Target Parameter Locators** – Specify the URL scope to be scanned, as follows:
   - **URL Path** – The main part of the URL, after the hostname and before the query parameters is used to identify the specific resource in the host that the client wants to access. In some cases (such as API endpoints), it may contain dynamic parameters (for example, object id).
   - **URL Query** – The query parameters string (after the question mark (?) and, if relevant, before the hash sign (#)) is used to provide additional information from the client to the request, such as data to search for in the target resource.
   - **URL Fragment** – The last part of a URL, after the hash sign (#), is used as an internal page reference or by DOM elements such as JavaScript, only used on the client side.
   - **Headers** – Request Headers are used to provide additional information from the client to the server in each HTTP request, such as cookies, information formats, security settings and so on.
   - **Body** – A Request Body can contain anything. In many cases, it contains data bytes transmitted from the client to the server, such as files.
   - **Artificial URL Query** - A URL Query added artificially to check if it can be manipulated for attacks. 
   - **Artificial URL Fragment** -  A URL Fragment  added artificially to check if it can be manipulated for attacks. 

6. In the <u>**Network Settings**</u> tab, configure the following options:

    ![network-settings](media/network-settings.png ':size=45%')

* **Concurrent Requests** – Specify the maximum concurrent requests allowed to be sent by the scan in order to control the load on your server.
* **Custom Host Placeholders** – Defines host placeholders with specific addresses. For example, replacing `localhost` with a specific IP address.
* **Additional Headers** – Defines additional headers to append to each request. For example, authentication cookies.

7. In the <u>**Application Settings**</u> tab, select the type of authentication you want to apply for the scanned target:

    ![application-settings](media/application-settings.png ':size=45%')

* **None** - Select if the scan target does not include any authenticated resources.
* **Header authentication** - Specify additional headers that should be appended to each request to access the authenticated resources within the scan target. For example, authentication cookies.
* **Authentication object** - you can find a full description about how to use an authentication object in the [Managing Your Authentications section](guide/np-web-ui/scanning/managing-authentications/managing-your-authentications.md).

8. In the <u>**Scan Tests** tab</u>, do the following:
* In the **Modules** section, select one of the following scan types (depending on your subscription):

    ![modules](media/modules.png ':size=45%')

  * **DAST** – Scans your application for OWASP Top 10+ issues (vulnerabilities) and many different CVEs. This is the default option.
  * **Fuzzer** – Scans your application for OWASP Top 10+ issues (vulnerabilities), as well as business logic vulnerabilities, 0-Days and many unknown issues.

    >[!DANGER|label:Warning]
    This type of scan may harm your system and so must only be used on a testing environment.

* In the **Tests** section, select the tests to be performed during the scan by checking their checkboxes.

    ![tests](media/tests.png ':size=45%')

9. _(Optional)_ In the <u>**Scheduling** tab</u>, you can schedule a scan by selecting the **Enable scheduling** option and then defining the scan as follows:
* **Single scan** – Select date and time to schedule the scan to run once automatically.

    ![single-scan](media/single-scan.png ':size=45%')

* **Recurring scan** – Define the frequency and schedule of the scan to run repeatedly automatically.

    ![recurring-scan](media/recurring-scan.png ':size=45%')

10. Once you complete the setup, you can run the scan immediately or save it as a template. The template will be saved to the templates list in the **Templates** tab.  You can select any template when creating a new scan.

* Click the **Save as Template** button to save the scan template.
* Click the **Start Scan** button to run the preconfigured scan immediately.

You can also use the **Restore Default** button to reset the custom settings.


## Creating a HAR file
An HTTP Archive File (HAR file) is a recording of a user session with an application. Various methods can be used to collect this information, such as by using a QA tool (such as Selenium). Alternatively, you can collect it manually using your web browser's built-in DevTools, as described below.

### Gathering a HAR File Using DevTools
1. In a browser, open the DevTools. This can be done in most browsers using the F12 key on your keyboard. The following displays – \
![DevTools](media/devtools-1.png ':size=45%')
2. Select the Network tab.\
![DevTools-Network-Tab](media/devtools-2.png ':size=45%')
3. Make sure that the **Preserve log** and **Disable cache** checkboxes are checked.\
![DevTools-Checkboxes](media/devtools-3.png ':size=45%')
4. Leave the DevTools pane open and browse to your application. All the application’s requests are then displayed and recorded in the DevTools panel.
5. Interact with the application in the same way as a normal user would. Remember to use all the parts of the application that you want to be in the scope of the scan performed by NexPloit.
    > [!TIP|label:Pro Tip]
    If you are using both **Crawler** and a **HAR recording** There is no need to record using all the options in the application or to begin at the main page. It is important however to scan parts of the application that require authentication, meaning that you must log into the application so that it is included in the recording.
6. Right-click on any of the requests in the DevTools panel and select the Save all as HAR option.\
![Save-as-HAR](media/save-as-har.png ':size=45%')
7. Save the file in your desired location so that you can select it when [defining a new scan](#Creating-a-New-Scan).

## Handling Scans that Require Authentication 
In order to scan applications that require authentication, you can either [create a HAR file which includes the login process to your application](Creating-a-HAR-file) or add an authentication header to your scan, as described below.

### Adding an Authentication Header to Your Scans
To add an authentication header to your scan –
1. Log into the application that you want to scan.
2. Open the DevTools panel of your browser. In most browsers, this can be done by pressing the F12 key on your keyboard.
3. Select the Network tab.\
![Devtools-Network-Tab](media/devtools2-1.png ':size=45%')
4. Perform any action in the application in order to record a few requests in the Network pane.
5. Click the name of one of the recorded requests.\
![Devtools-Requests](media/devtools2-2.png ':size=45%')
6. Scroll down to the **Request Headers** category and find the authentication header. For example, as shown below –\
![Devtools-Auth-Header](media/devtools2-3.png ':size=45%')
7. Copy the value of the authentication header, as shown below –\
![Devtools-Copy-Auth-Header](media/devtools2-4.png ':size=45%')
8. To define a new scan open the [Scan Creation window](#Creating-a-New-Scan) and select the **Network settings** tab.
9. In the Additional headers field, click the ![Plus-Button](media\plus-dark.png ':size=3%') button to add the authentication header that you copied, as shown above. Make sure that the key and the value are exactly the same as they were in the request from which you copied them.

    ![New-Scan-Add-Auth](media/network-settings.png ':size=45%')