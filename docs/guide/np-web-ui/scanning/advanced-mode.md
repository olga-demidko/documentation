# Advanced Mode
In the **NEW SCAN** dialog box, select the **Advanced** tab to create a scan with extended settings.

>[!NOTE|label:Note]
The required settings fields are marked with `*`. The tabs which include the required fields provide counters where the first digit is the number of completed required fields, and the second one is the total number of the required fields in this tab. Once you complete all the required fields in a tab, the counter next to the tab name turns green. Additionally, the number of missing or incorrect settings are shown as the **REMAINING ERRORS** at the bottom of the dialog box.

1. _(Optional)_ In order to make the scanning definition process quicker, in the <u>**Templates** tab</u>, you can select a predefined set of scan settings. Nexploit provides the following types of predefined scan settings:

    ![Templates](media/templates.png ':size=60%')

* **Deep Scan** – All possible tests are performed during the scan. This is the most thorough scan, which takes the longest time to complete.
* **Light Scan** – This is a preconfigured optimized scan, during which the engine automatically determines which tests to run, based on the data types that are detected. Some tests will be skipped in favor of speed.
* **Passive Scan** - The engine selects only host-based passive tests to be run.
* **API Scanning** – Predefined tests that are relevant for API targets.
* _(Optional)_ **Custom (own) templates** - The scans configured by a user manually and saved as templates. 


Once you select a template, you can view the predefined scan settings below the **Scan Templates** field.  To apply these settings for a new scan, click **Apply** next to the selected template. 

![apply-template](media/apply-template.png ':size=60%')


>[!TIP|label:Pro Tip]
In addition, you can define your own scan templates. See [Managing Scan Templates](guide/np-web-ui/scanning/managing-scan-templates.md) for more information.

2. In the <u> **Scan Details** tab</U>, do the following:

 ![Scan-details](media/scan-details.png ':size=60%')

* In the **Scan name** field, enter any free-text name for this scan.
* From the **Project** dropdown list, select the Nexploit project you want to use for the scan.

>[!NOTE|label:Note]
You can start a scan ONLY if a project is selected. If you do not have any projects in Nexploit, select the **Default** one.

* From the **Integrations** dropdown list, select a specific repository where you want to get the scan reports.

3. In the <u>**Scan Targets** tab</u>, do the following:
* In the **Discovery Types** field, select one of the following ways your application attack surface should be mapped (depending on your subscription) – Crawler, Recording (HAR) or Open API: <br>

__Crawler –__ This is the simplest option. Simply enter a URL (target host) to scan the whole or a part of the specified application. The crawler will map the entire application attack surface automatically.

To scan only specific parts of your application or add multiple hosts, click  ![plus-dark](media/plus-dark.png ':size=3%') at the right side of the **Targets** section .<br> In this case, only the specified sections of the application and everything downstream from them will be scanned. 
   
Note that some hosts may be unreachable or unauthorized for a direct scan from the cloud. If a host cannot be reached by the engine, select a running Repeater for the scan in the **Network Settings** section. If a host is unauthorized for a direct scan from the cloud, either select a running Repeater for the scan or add a `.nex` file to the host root directory (read more information [here](https://kb.neuralegion.com/#/guide/np-web-ui/advanced-set-up/managing-org?id=defining-the-hosts-authorized-for-scanning)).<br> 
    
![Crawler-settings](media/crawler.png ':size=60%')
    
See [Scanning a website with a crawler](/guide/np-web-ui/scanning/discovery-types/crawler.md) for detailed information.


   **Recording (HAR) –** Use a pre-recorded session of your application (HAR file), which has been created either manually or automatically (using QA tools, such as Selenium to scan your application). This discovery type enables you to define the scope of a scan and store login information in order to scan areas in your application that require authentication. 
  
See [Creating a HAR File](/guide/np-web-ui/scanning/discovery-types/create-har.md) to learn how to create a HAR file.

Note that some hosts may be unreachable or unauthorized for a direct scan from the cloud. If a host cannot be reached by the engine, select a running Repeater for the scan in the **Network Settings** section. If a host is unauthorized for a direct scan from the cloud, either select a running Repeater for the scan or add a `.nex` file to the host root directory (read more information [here](https://kb.neuralegion.com/#/guide/np-web-ui/advanced-set-up/managing-org?id=defining-the-hosts-authorized-for-scanning)).

![Recording](media/recording-har.png ':size=60%')

 See [Scanning a website with a HAR file](/guide/np-web-ui/scanning/discovery-types/har.md) for detailed information.<br>


  >[!TIP|label:Pro Tip]
  To enjoy both full automation and deeper attack surface analysis, you can combine **Crawling** and **Recording (HAR)** in a single scan!

**Open API –** Use an `*.yml` file to scan APIs. See [Scanning API endpoints](/guide/np-web-ui/scanning/discovery-types/open-api.md) for detailed information.

 ![Recording](media/api-scan.png ':size=60%')

* In the **Coverage Exclusions** section, enter the URLs and parameters that Nexploit should ignore during scanning.

    ![Coverage-exclusions](media/coverage-exclusions.png ':size=60%')

* In the **Attack Surface Optimization** section, you can use the following options to optimize the scanning flow :

    ![attack-optimization](media/attack-optimization.png ':size=60%')

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

4. In the <u>**Network Settings**</u> tab, configure the following options:

    ![network-settings](media/network-settings.png ':size=60%')

* **Repeater** – Select a Repeater to connect it to the scan. The Repeater is created in the Repeaters tab and serves as a request-proxy between Nexploit and the target hosted on a local network.  See [On-Premises Repeater (Agent)](/guide/introduction/deployment-onprem.md) for more information.
* **Concurrent Requests** – Specify the maximum concurrent requests allowed to be sent by the scan in order to control the load on your server.
* **Custom Host Placeholders** – Defines host placeholders with specific addresses. For example, replacing `localhost` with a specific IP address.
* **Additional Headers** – Defines any custom headers to be appended to each request. If you need to add some authentication headers, see [Header Authentication](/guide/np-web-ui/scanning/managing-authentications/types/header-authentication).

5. In the <u>**Application Settings**</u> tab, select the type of authentication you want to apply for the scanned target:

    ![application-settings](media/application-settings.png ':size=60%')

* **None** - Select if the scan target does not include any authenticated resources.
* **Authentication object** - you can find a full description about how to use an authentication object in the [Managing Your Authentications section](guide/np-web-ui/scanning/managing-authentications/managing-your-authentications.md).

6. In the <u>**Scan Tests** tab</u>, do the following:
* In the **Modules** section, select one of the following scan types (depending on your subscription):

    ![modules](media/modules.png ':size=60%')

  * **DAST** – Scans your application for OWASP Top 10+ issues (vulnerabilities) and many different CVEs. This is the default option.
  * **Fuzzer** – Scans your application for OWASP Top 10+ issues (vulnerabilities), as well as business logic vulnerabilities, 0-Days and many unknown issues.

    >[!DANGER|label:Warning]
    This type of scan may harm your system and so must only be used on a testing environment.

* In the **Tests** section, select the tests to be performed during the scan by checking their checkboxes.

    ![tests](media/tests.png ':size=60%')

7. _(Optional)_ In the <u>**Scheduling** tab</u>, you can schedule a scan by selecting the **Enable scheduling** option and then defining the scan as follows:
* **Single scan** – Select date and time to schedule the scan to run once automatically.

    ![single-scan](media/single-scan.png ':size=60%')

* **Recurring scan** – Define the frequency and schedule of the scan to run repeatedly automatically.

    ![recurring-scan](media/recurring-scan.png ':size=60%')

8. Once you complete the setup, you can run the scan immediately or save it as a template. The template will be saved to the templates list in the **Templates** tab.  You can select any template when creating a new scan.

* Click **Save as Template** to save the scan template.
* Click **Start Scan** to run the preconfigured scan immediately.
>[!NOTE|label:Note]
If the maximum number of scans that can be run simultaneously is exceeded, the scan is placed in the queue. The concurrent scans limitation can be set either for the entire organization or for this particular project in the project settings. The new scan will start as soon as you manually stop another running scan or when the current scan is completed.

You can also use the **Restore Default** button to reset the custom settings.