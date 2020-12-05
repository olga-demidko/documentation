# Creating a New Scan
1. Select the **Scans** option in the left pane to display the Scans List. Each scan appears as a single row.\
![New-Scan](media/new-scan-1.png ':size=45%')
2. In the **Scans** page, click the **New Scan** ![New-Scan-Button](media/new-scan-button.png ':size=12%') button to create a new scan. The following displays –\
![New-Scan-Dialogue](media/new-scan-2.png ':size=45%')
3. In the **Scan name** field, enter any free-text name for this scan.
4. In the **Modules** field, select one of the following scan types (depending on your subscription) – 
    * **DAST –** Scans your application for OWASP Top 10+ issues (vulnerabilities) and many different CVEs. This is the default option.
    * **Fuzzer –** Scans your application for OWASP Top 10+ issues (vulnerabilities), as well as business logic vulnerabilities, 0-Days and many unknown issues.
    >[!ATTENTION|label:WARNING]
    <span style="color:#dc3545;">This type of scan may harm your system and so must only be used on a testing environment.</span>
5. In the **Discovery Types** field, select one of the following ways your applications attack surface is to be mapped (depending on your subscription) – **Crawler**, **Recording (HAR)** or **Open API**, as follows – 
    * **Crawler –** This is the simplest option. Simply enter a URL (target host) to scan all or part of the specified application. The crawler will map the entire application's basic attack surface automatically.\
    ![Crawler](media/crawler.png ':size=45%')\
    To scan only specific parts of your application, use the ![Plus-Button](media\plus-button.png ':size=3%') button at the right side of the **Targets** section to add multiple URLs. For example –
        * `www.example.com/home`
        * `www.example.com/news`
    
    In this case, only these two sections of the application and everything downstream from them will be scanned.
    * **Recording (HAR) –** Use a pre-recorded session of your application (HAR file) which was created either manually or automatically (using QA tools, such as Selenium to scan your application). This discovery type enables you to define the scope of a scan and store login information in order to scan areas in your application that require authentication. See [Creating a HAR File](#creating-a-HAR-file) for more information.
    * **Open API –** Use an `*.yml` file to scan APIs. See [Scanning an API](guide/np-web-ui/scanning/scanning-api.md) for more information.
6. *(Optional)* In order to make the scanning definition process quicker, in the **Scan Templates** field, you can select a predefined set of scan settings. NexPloit is provided with the following types of predefined scan settings –
    * **Fast Scan –** This is a preconfigured optimized scan, during which the engine automatically determines which tests to run, based on the data types that are detected. Some tests will be skipped in favor of speed.
    * **Comprehensive Scan –** All possible tests are performed during the scan. This is the most thorough scan, which takes the longest time to complete.
    * **API Scanning –** Predefined tests that are relevant for API targets.

  In addition, you can define your own scan templates. See [Managing Scan Templates](guide/np-web-ui/scanning/managing-scan-templates.md) for more information.

  > [!TIP|label:Pro Tip]
  To enjoy both full automation and deeper attack surface analysis, you can combine Crawling & Recoding (HAR) in a single scan! 
7. In the **Scan Tests** section, select the tests to be performed during the scan by checking their checkboxes.\
![Scan-Tests](media/scan-tests.png ':size=45%')
8. Select the file to scan, either –
    * Upload a file from your computer to the NeuraLegion cloud by clicking ![Clip-Button](media/clip-button.png ':size=4%') and then clicking the textbox to the left.\
    – OR – 
    * Import a file that is already in NeuraLegion's cloud by clicking ![Cloud-Button](media/cloud-button.png ':size=4%') and then choosing the file from the dropdown menu.\
    ![Select-File](media/select-file.png ':size=45%')
9. *(Optional)* In the **Scheduling** section, you can schedule a scan by selecting the **Enable scheduling** option and then defining the scan as follows –
    * **Single scan –** Choose a date and a time to schedule the scan to run once automatically.\
    ![Schedule-Single-Scan](media/sched-single-scan.png ':size=45%')
    * **Recurring scan –** Define the frequency and schedule of the scan to run repeatedly automatically.\
    ![Schedule-Recurring-Scan](media/sched-recurring-scan.png ':size=45%')
10. *(Optional)* In the **Additional Settings** section, you can configure the following options –\
    ![Additional-Settings](media/additional-settings.png ':size=45%')
    * **Concurrent Requests –** Specify the maximum concurrent requests allowed to be sent by the scan in order to control the load on your server. 
    * **Smart Scan –** Specify whether to use automatic smart decisions (such as parameter skipping, detection phases and so on) in order to minimize scan time. When this option is turned off, all tests are run on all parameters, which increases coverage at the expense of scan time.
    * **<div id="target-params-locations">Target Parameter Locations –</div>** Specify the URL scope to be scanned, as follows – 
        * **URL Path –** The main part of the URL, after the hostname and before the query parameters is used to identify the specific resource in the host that the client wants to access. In some cases (such as API endpoints), it may contain dynamic parameters (for example, object id).
        * **URL Query –** The query parameters string (after the question mark (?) and, if relevant, before the hash sign (#)) is used to provide additional information from the client to the request, such as data to search for in the target resource.
        * **URL Fragment –** The last part of a URL, after the hash sign (#), is used as an internal page reference or by DOM elements such as JavaScript, only used on the client side.
        * **Headers –** Request Headers are used to provide additional information from the client to the server in each HTTP request, such as cookies, information formats, security settings and so on.
        * **Body –** A Request Body can contain anything. In many cases, it contains data bytes transmitted from the client to the server, such as files.
    * **Additional Hosts –** Defines host placeholders with specific addresses. For example, replacing `localhost` with a specific IP address.
    * **Additional Headers –** Defines additional headers to append to each request. For example, authentication cookies.
    * **Integrations –** Connects the scan to a specific ticketing platform and repository, which will automatically add all the information about each found vulnerability to the repository.
    * **Repeater –** Connects the scan to a Repeater agent, which provides secure access to local networks.
11. Click the ![Run-Button](media/run-button.png ':size=4%') button after configuring the scan, as described above.

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
8. To define a new scan open the [Scan Creation window](#Creating-a-New-Scan) and expand the **Additional settings** section.
9. In the Additional headers field, click the ![Plus-Button](media\plus-button.png ':size=3%') button to add the authentication header that you copied, as shown above. Make sure that the key and the value are exactly the same as they were in the request from which you copied them.\
![New-Scan-Add-Auth](media/new-scan-auth-bearer.png ':size=45%')