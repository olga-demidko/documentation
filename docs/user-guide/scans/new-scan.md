## Starting A New Scan

1. Once you are logged into the system, you’ll be taken to your dashboard. 
Here you can click the ![New Scan](media/new-scan-button.png ':size=8%') button to create a new scan.

![New_Scan_1](media/new-scan-01.png ':size=45%')


2. The scan creation form will pop up. Fill in a name for your scan.

![New_Scan_2](media/new-scan-02.png ':size=45%')


3. Select the **[Module](#modules)** you’d like to use in your scan (if applicable, depending on your subscription), 
the **[Discovery Type](#discovery-types)** that suits you and, optionally, a **[Scan Profile](#scan-profiles)**.

!> **Pro tip:** To enjoy both full automation and deeper attack surface analysis, you can combine **[Crawling](#using-a-crawler)** & **[Recoding (HAR)](#using-a-har-file)** in a single scan!


![New_Scan_3](media/new-scan-03.png ':size=45%')

4. Now select the tests you’d like to perform in the scan.

![New_Scan_7](media/new-scan-07.png ':size=45%')

5. Optionally, you can:
  - **[Set Up Scheduling](#scan-scheduling)** for your scan, such as scanning at a later date or recurring scan.
  - **[Configure Additional Settings](#additional-scan-settings)** for your scan, such as maximum concurrent requests for the scan, additional headers, integrations and/or agent.

6. Once you've configured your scan, click on the ![Upload_Clip](media/run_button.png ':size=5%') button.


## Modules
- **DAST** - scan your application for OWASP Top 10+ vulnerabilities and many different CVEs
- **Fuzzer** - scan your application for OWASP Top 10+ vulnerabilities, as well as business logic vulnerabilities, 0-Days and many unknown vulnerabilities. This module can be harmful to your system and so must be used only on a testing environment

![New_Scan_3](media/new-scan-03.png ':size=45%')

## Discovery Types
Discovery types are the way your applications attack surface is mapped, there are several options:
- **[Recording (HAR)](#using-a-har-file)** - use a pre-recorded session of your application (HAR file) which was created either manually or automatically with QA tools such as Selenium to scan your application. With this discovery type you can define the scope of the scan and store login information to scan areas in your application which require authentication
- **[Crawler](#using-a-crawler)** - use our Crawler to scan your application or parts of it automatically. All you need is a URL
- **[Open API](#scanning-an-api)** - NexPloit supports scanning APIs. You’ll need a *.yml file

![New Scan 3](media/new-scan-03.png ':size=45%')

### Using a HAR File
You can either use a new file or select a pre uploaded file (either a file you've used before or a file that was pre-uploaded using our browser extension, which you can read about here).
1. Upload your HAR file by clicking the ![Upload_Clip](media/clip_button.png ':size=4%') icon and then the textbox on its left. When you’ll click the textbox you’ll be asked to select your file to upload.

!> **Note:** HAR file names must be unique in the cloud storage, but you can use the **Delete after scan** option (below) when uploading the files in case of automation.

![New_Scan_4](media/new-scan-04.png ':size=45%')

2. If you want to use a HAR file that you have already uploaded before or that you have recorded via our web browser extension, click on the ![Cloud_button](media/cloud_button.png ':size=4%') button and then the textbox on its left. A drop down menu will open with a list of your uploaded files, choose the one that you’d like to use.

![New_Scan_5](media/new-scan-05.png ':size=45%')

3. Once you’ll choose a file, you will need to select the hosts that you’d like to scan. Make sure to only select hosts that you are allowed to scan.

![New_Scan_6](media/new-scan-06.png ':size=45%')

### Using a Crawler
Crawling is the simplest and fastest way to start a scan, by providing a target host(s) the crawler will map the entire application's basic attack surface automatically.
1. Select the "Crawler" option, then add the URL that you'd like to scan. If you'd like to add more than one URL use the ![Plus_button](media/plus_button.png ':size=2%') button to the right.

![New_Scan_11](media/new-scan-11.png ':size=45%')

### Scanning an API
To scan an API you’ll need either an Open API specification (Swagger) or a Postman collection (*.yml / *.yaml / *.json).

| Schema | Supported Versions |
| -- | -- |
| Swagger | 2+ |
| OpenAPI | 3+ |
| Postman | 2+ |

1. Select the "Open API" Discovery Type and then choose whether you'd like to scan an Open API specification or a Postman collection.

![New_Scan_13](media/new-scan-13.png ':size=45%')

2. Fill in the required extra headers for your scan (to add more than one use the ![plus](media/plus_button.png ':size=2%') button on the right). If you chose to scan a Postman collection you'll also have the option to add the relevant variables.

![New_Scan_14](media/new-scan-14.png ':size=45%')

3. Now choose the file to scan. You can either upload a file from your computer by clicking ![clip](media/clip_button.png ':size=3%') and then clicking the textbox to the left, or import a file from a link by clicking ![link](media/link_button.png ':size=3%') and then pasting a link in the textbox to the left.

![New Scan 15](media/new-scan-15.png ':size=45%')

## Scan Profiles
Scan profiles make the process of initiating a scan quicker, they allow you to use predefined scan settings when creating a new scan.
There are 3 default profiles:
- **Fast Scan** - Preconfigured optimized scan, the engine will determine automatically which tests to run, based on the data types that are detected. Some tests will be skipped in favour of speed.
- **Comprehensive Scan** - All the possible tests will be performed during the scan. This is the most thorough scan, which accordingly takes the longest time to finish
- **API Scanning** - Preconfigured tests that are relevant for API targets

## Scan Scheduling
You can set up a scan to start running at a later time, with two options:

### Schedule a Single Scan For Later
1. Click “Enable Scheduling” on the right, select the "Single Scan" option and then choose a date and a time for the scan to run.

![New Scan 8](media/new-scan-08.png ':size=45%')

### Schedule a Recurring Scan
1. Click “Enable Scheduling” on the right, then select the settings that suit you best.

![New Scan 9](media/new-scan-09.png ':size=45%')

## Additional Scan Settings
There are more additional settings you may want to use, such as setting the maximum concurrent scans for the scan to control the load on your server, adding additional headers to the scan (for example, you may want to add an authentication header to the scan to scan parts of your application that require authentication), select an integration to use and/or add an agent.

![New Scan 10](media/new-scan-10.png ':size=45%')