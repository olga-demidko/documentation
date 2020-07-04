## Starting A New Scan

1. Once you are logged into the system, you’ll be taken to your dashboard. 
Here you can click the ![New Scan](media/new-scan-button.png ':size=8%') button to create a new scan.

    ![New Scan 1](media/new-scan-01.png ':size=100%')


2. The scan creation form will pop up. Fill in a name for your scan.

    ![New Scan 2](media/new-scan-02.png ':size=100%')


3. Select the module you’d like to use in your scan (if applicable, depending on your subscription), 
the discovery type that suits you and, optionally, a scan profile.

    ![New Scan 3](media/new-scan-03.png ':size=100%')

    Modules:
    <ol type="A"; style="margin-top:-18px;">
    <li>DAST - scan your application for OWASP Top 10 + vulnerabilities and many different CVEs.</li>
    <li>Fuzzer - scan your application for OWASP Top 10 + vulnerabilities, as well as business logic vulnerabilities, 0-Days and many unknown vulnerabilities. This module can be harmful to your system and so must be used only on a testing environment.</li>
    </ol>

    <p id="Discovery_Types">Discovery Types</p>
    <ol type="A"; style="margin-top:-18px;">
    <li>Recording - use a pre-recorded session of your application (a HAR or WSAR file) which was created either manually or automatically with QA tools such as Selenium to scan your application. With this discovery type you can define the scope of the scan and store login information to scan areas in your application which require authentication.</li>
    <li>Crawler - use our Crawler to scan your application or parts of it automatically. All you need is a URL.</li>
    <li>Open API - NexPloit supports scanning APIs. You’ll need a *.yml file.</li>
    </ol>

    Scan Profiles:
    <ul type=""; style="margin-top:-18px">
    <li>Scan profiles make the process of initiating a scan quicker, they allow you to use predefined scan settings when creating a new scan.</li>
    </ul>

4. Proceed according to your choice of Discovery Types (notice that you can combine <a href="#/user-guide/scans/new-scan?id=Discovery_Types" style="text-decoration: inherit; color: inherit; font: inherit">options A. and B.</a> in a single scan):

    #### Use a HAR/WSAR file
    You can either use a new file or select a pre uploaded file (either a file you've used before or a file that was pre-uploaded using our browser extension, which you can read about here).
    <ol type="A"; style="margin-top:-18px;">
    <li>Upload your HAR/WSAR file by clicking the <img src="user-guide/scans/media/clip_button.png" width="3.2%" style="margin-bottom:-5px;"> icon and then the textbox on its left. When you’ll click the textbox you’ll be asked to select your file to upload.

    ![New Scan 4](media/new-scan-04.png ':size=100%')</li>

    <li>If you want to use a HAR/WSAR file that you have already uploaded before or that you have recorded via our web browser extension, click the <img src="user-guide/scans/media/cloud_button.png" width="3.2%" style="margin-bottom:-5px;"> button and then the textbox on its left. A drop down menu will open with a list of your uploaded files, choose the one that you’d like to use.

    ![New Scan 5](media/new-scan-05.png ':size=100%')</li>
    </ol>
    Once you’ll choose a file, you will need to select the hosts that you’d like to scan. Make sure to only select hosts that you are allowed to scan.

    ![New Scan 6](media/new-scan-06.png ':size=100%')

    Now select the tests you’d like to perform in the scan.

    ![New Scan 7](media/new-scan-07.png ':size=100%')

    Optionally, you can schedule your scan for later. You have two options to schedule a scan:
    <ol type="A"; style="margin-top:-18px;">
    <li>Schedule a single scan for later. Click “Enable Scheduling” on the right, select the "Single Scan" option and then choose a date and a time for the scan to run.

    ![New Scan 8](media/new-scan-08.png ':size=100%')</li>
    <li>Schedule a recurring scan. Click “Enable Scheduling” on the right, then select the settings that suit you best.

    ![New Scan 9](media/new-scan-09.png ':size=100%')</li>
    </ol>

    There are more additional settings you may want to use, such as setting the maximum concurrent scans for the scan to control the load on your server, adding additional headers to the scan (for example, you may want to add an authentication header to the scan to scan parts of your application that require authentication), select an integration to use and/or add an agent.

    ![New Scan 10](media/new-scan-10.png ':size=100%')
    
    #### Use a Crawler
    
    #### Use an API Specification