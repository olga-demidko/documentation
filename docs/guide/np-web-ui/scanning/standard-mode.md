# Standard Mode
1. On the **NEW SCAN** popup, select the **Standard** tab to create a scan with minimal settings.
2. From the **Scan Targets** dropdown list, select one of the following:
    * _(Default)_ **Website via automatic crawling** - This is the simplest option. Simply enter a URL (target host) to scan the whole or a part of the specified application. To scan only specific parts of your application, click ![plus-dark](media/plus-dark.png ':size=3%') at the right side of the **Targets** section to add multiple URLs. See [Scanning with a Crawler](/guide/np-web-ui/scanning/discovery-types/crawler.md) for detailed information.

    ![standard-crawler](media/standard-crawler.png ':size=45%')

    * **Website via recorded session (HAR file)** - Use a pre-recorded session of your interaction with the application (HAR file), which has been created either manually or automatically (using QA tools, such as Selenium to scan your application). This discovery type enables you to define the scope of a scan and ensures complete coverage of the attack surface . See [Scanning with a HAR](/guide/np-web-ui/scanning/discovery-types/har.md) for detailed information.

    ![standard-har](media/standard-har.png ':size=45%')

  >[!TIP|label:Pro Tip]
  To enjoy both full automation and deeper attack surface analysis, you can combine **Crawling** and **Recording (HAR)** in a single scan.

    * **API endpoints via schema** - Use an *.yml file to scan APIs. See[Scanning an API](/guide/np-web-ui/scanning/discovery-types/open-api.md) for detailed information.

    ![standard-api](media/standard-api.png ':size=45%')

2. From the **Repeater** dropdown list, select a Repeater (local agent) to connect it to the scan. The Repeater is created in the **Repeaters** tab and serves as a request-proxy between NexPloit and the target hosted on a local network.  See [On-Premises Repeater (Agent)](/guide/introduction/deployment-onprem.md) for more information.

3. In the **Scan Name** field, enter a free-text scan name.
    If you have selected to scan a website using the crawler discovery tipe, the scan name is assigned automatically based on the specified hostname. You can change the created name if you want.

4. From the **Project** dropdown list, select the NexPloit project you want to use for the scan.
  >[!NOTE|label:Note]
    You can start a scan ONLY with a project selected. If you do not have any projects in NexPloit, select the Default one.

5. Once you complete the setup, click **Start Scan** to start scanning.




