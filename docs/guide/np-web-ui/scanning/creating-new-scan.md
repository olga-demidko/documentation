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

  * **Open API** – Use an `*.yml` file to scan APIs. See [Scanning an API](/guide/np-web-ui/scanning/scanning-api.md) for more information.

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
* **Additional Headers** – Defines any custom headers to be appended to each request. If you need to add some authentication headers, see [Header Authentication](/guide/np-web-ui/scanning/managing-authentications/types/header-authentication).

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
An HTTP Archive File (HAR file) is a recorded session of user interaction with an application. The HAR file keeps all the requests between the user and the application so that NexPloit can analyze them and adjust the selected security tests for each possible request. You can load a HAR file to a new scan to provide NexPloit with detailed information on how the application is built.

Based on the information recorded while navigating through the application, NexPloit can create sophisticated attacks to all the investigated resources. Therefore, the Recording (HAR) discovery type may provide larger coverage of the scan target than the Crawler reaches.  

>[!NOTE|label:Note]
The quality of the scan depends directly on the HAR file quality. The more detailed the HAR file, the larger the scan scope can be covered by NexPloit. 

You can use various methods to collect the application behavior information, for example by using a QA tool (such as Selenium). Alternatively, you can create a HAR file manually by using your web browser's built-in DevTools, as described below.

### Step-by-Step Guide
1. In your browser, open the DevTools pane. In most browsers, this can be done using the F12 key on your keyboard or by selecting the **Inspect** option from the browser menu. 

    ![DevTools](media/open-devtools.png ':size=45%')

2. Select the **Network** tab.

    ![Network-Tab](media/network-tab.png ':size=45%')

3. Make sure that the **Preserve log** and **Disable cache** checkboxes are selected. This will allow you to persist logs between page refreshes and see the page updates. 

    ![Checkboxes](media/preserve-log.png ':size=45%')

4. Leave the DevTools pane open and browse to your application. All the application requests are then displayed and recorded in the DevTools panel.

5. Interact with the application in the same way as a normal user would. Remember to use all the resources (parts, options) of the application that you want to be covered by the NexPloit scan.
    > [!TIP|label:Pro Tip]
    If you are using both **Crawler** and **Recording (HAR)** discovery types, there is no need to record all the options in the application or begin at the main page. It is important however to scan the application resources that require authentication. It means that you must log in to such resources so that these actions are included in the recording.

6. Once you complete the recording, right-click any of the requests in the DevTools panel and select the Save all as HAR option.

    ![Save-as-HAR](media/save-har.png ':size=45%')

7. Save the file in your desired location so that you can select it when [defining a new scan](#Creating-a-New-Scan). 



