# Starting A New Scan
Here you will get all the information regarding how to start a new scan.

### Quick Start {docsify-ignore}
- [Overview](#overview)
- [Modules](#modules)
- [Discovery Types](#discovery-types)
  - [Using a HAR File](#using-a-har-file)
  - [Using a Crawler](#using-a-crawler)
  - [Scanning an API](#scanning-an-api)
- [Scan Templates](#scan-templates)
- [Scheduling](#scheduling)
  - [Schedule a Single Scan For Later](#schedule-a-single-scan-for-later)
  - [Schedule a Recurring Scan](#schedule-a-recurring-scan)
- [Additional Settings](#Additional-settings)
  - [Concurrent Requests](#concurrent-requests)
  - [Smart Scan](#smart-scan)
  - [Target Parameter Locations](#target-parameter-locations)
  - [Additional Hosts](#additional-hosts)
  - [Additional Headers](#additional-headers)
  - [Integrations](#integrations)
  - [Agents](#agents)

<hr style="height:2px;background-color:#d1d3d4">

## Overview
1. In the **Scans** page, click on the ![New Scan](media/new-scan-button.png ':size=8%') button to create a new scan.

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
  - **[Configure Additional Settings](#additional-settings)** for your scan, such as maximum concurrent requests for the scan, additional headers, integrations and/or agent.

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
To start a crawler scan simply select the "Crawler" option, then add the URL that you'd like to scan.

![New_Scan_11](media/new-scan-11.png ':size=45%')

#### Crawler Scoping
If you'd like to scan specific parts of your application, you can use the ![Plus_button](media/plus_button.png ':size=2%') button at the right side of the "hosts" section to add multiple URLs. 
For example:
- `kb.neuralegion.com/user-guide/`
- `kb.neuralegion.com/Integrations/`

In which case, only those 2 sections (and everything "downstream") will be scanned.

### Scanning an API
To scan an API you’ll need either an Open API specification (Swagger) or a Postman collection (*.yml / *.yaml / *.json).

| Schema  | Supported Versions |
| ------- | ------------------ |
| Swagger | 2+                 |
| OpenAPI | 3+                 |
| Postman | 2+                 |

1. Select the "Open API" Discovery Type and then choose whether you'd like to scan an Open API specification or a Postman collection.

![New_Scan_13](media/new-scan-13.png ':size=45%')

2. Fill in the required extra headers for your scan (to add more than one use the ![plus](media/plus_button.png ':size=2%') button on the right). If you chose to scan a Postman collection you'll also have the option to add the relevant variables.

![New_Scan_14](media/new-scan-14.png ':size=45%')

3. Now choose the file to scan. You can either upload a file from your computer by clicking ![clip](media/clip_button.png ':size=3%') and then clicking the textbox to the left, or import a file from a link by clicking ![link](media/link_button.png ':size=3%') and then pasting a link in the textbox to the left.

![New Scan 15](media/new-scan-15.png ':size=45%')

## Scan Templates
Scan Templates make the process of initiating a scan quicker, they allow you to use predefined scan settings when creating a new scan.
There are 3 default Template:
- **Fast Scan** - Preconfigured optimized scan, the engine will determine automatically which tests to run, based on the data types that are detected. Some tests will be skipped in favour of speed.
- **Comprehensive Scan** - All the possible tests will be performed during the scan. This is the most thorough scan, which accordingly takes the longest time to finish
- **API Scanning** - Preconfigured tests that are relevant for API targets

You can also create your own [Scan Templates](user-guide/scans/templates/overview.md)

## Scheduling
You can set up a scan to start running at a later time, with two options:

### Schedule a Single Scan For Later
1. Click “Enable Scheduling” on the right, select the "Single Scan" option and then choose a date and a time for the scan to run.

![New Scan 8](media/new-scan-08.png ':size=45%')

### Schedule a Recurring Scan
1. Click “Enable Scheduling” on the right, then select the settings that suit you best.

![New Scan 9](media/new-scan-09.png ':size=45%')

## Additional settings
At the bottom of the scan initiation panel, you will find the **Additional Settings** category. 

![additional-settings](media/additional-settings-open.png ':size=45%')

### Concurrent Requests
This setting allows your to set the maximum concurrent requests for the scan, to control the load on your server.

### Smart Scan
Use automatic smart decisions such as: parameter skipping, detection phases, etc. to minimize scan time. When turned off, all the tests will be run on all the parameters, which increases the coverage at the expense of scan time.

### Target Parameter Locations (URL Scoping)
- **URL Path** - Main part of the URL, after the hostname and before the query parameters. Used to identify the specific resource in the host that the client wants to access. In cases like API endpoints, may contain dynamic parameters (for example, object id).
- **URL Query** - Query parameters string, after the question mark (?) and, if relevant, before the hash sign (#). Used to provide additional information from the client to the request, such as data to search for in the target resource.
- **URL Fragment** - Last part of a URL, after the hash sign (#). Used as an internal page reference or by DOM elements such as JavaScript, only used on the client side.
- **Headers** - Request Headers, used to provide additional information from the client to the server in each HTTP request, such as cookies, information formats, security settings, etc.
- **Body** - Request Body, can contain anything, but in many cases contains data bytes transmitted from the client to the server, such as files.

### Additional Hosts
Defines host placeholders with specific addresses, for example, replacing `localhost` with a specific IP address.

### Additional Headers
Defines additional headers to append to each request, for example authentication cookies.

### Integrations
Connects the scan to a specific ticketing platform and repository, which will automatically add all the information about each found vulnerability to the repository.

### Agents
Connects the scan to a [Repeater](user-guide/agents/overview) agent, which provides secure access to local networks.
