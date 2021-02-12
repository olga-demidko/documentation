<table id="integrations" >
  <tr>
    <td width="70%">
      <h1>Azure Pipelines</h1>
    </td>
    <td width="30%" style="text-align:center" rowspan="3">
      <img src="guide/pipeline-integration/pipe-management/media/azure-pipelines/azure-pipeline-logo.png" width="200" height="250"></img>
    </td>
  </tr>
  <tr>
    <td style="text-align:left;vertical-align:text-top;padding:0px">
      If you are using Azure DevOps for development automation, you can integrate NexPloit with your Azure CI pipeline using the <a href="https://marketplace.visualstudio.com/items?itemName=Neuralegion.nexploit">NexPloit DevOps Integration extension</a>. The integration allows you to automate the security testing flow by running the NexPloit scans on every new build within your development environment.
    </td>
  </tr>
  <tr>
  <td width="65%">
    <h2>Prerequisites</h2>
    </td>
    </tr>
</table>

*   You are an active user on  [nexploit.app](https://nexploit.app). 
*   You have the [NexPloit DevOps Integration extension](https://marketplace.visualstudio.com/items?itemName=Neuralegion.nexploit)  installed on your Azure DevOps Server. 
*   The target of the scan is accessible from the Internet.
*   You have a valid [organization API key](http://localhost:3000/#/guide/np-web-ui/advanced-set-up/managing-org?id=managing-organization-apicli-authentication-tokens) or [personal API key](http://localhost:3000/#/guide/np-web-ui/advanced-set-up/managing-personal-account?id=managing-your-personal-api-keys-authentication-tokens) with the following scopes:
    - scans : run
    - scan : read
    - scans : stop

## Setup
### Using a Pre-recorded HAR File 
If you want to start a new scan with an added HAR file, first upload your HAR file to [nexploit.app](https://nexploit.app) using a simple curl command: 
```bash
$ curl -X POST "https://nexploit.app/api/v1/files?discard=true"  \
    -H "Content-Type: multipart/form/data"                       \
    -H "Authorization: Api-Key yufn0f6.yourapikeykuj069zopv0n1i" \
    -f 'har=@//path/to/the/file.har"   
```

The response **id** will then be used during setting a new scan in the pipeline, for example:
```bash
 {"ids":["6xkFraa5ecfmHhxTEnabZg"]}
```

## Step-by-Step Guide
### Opening the Integration Extension in Your Pipeline
1. In your pipeline, click the **Show assistant** button.

    ![show-assistant](media/azure-pipelines/show-assistant.png ':size=35%')

2. In the **Tasks** field, enter **nexploit scan**.

    ![nexploit-scan](media/azure-pipelines/nexploit-scan.png ':size=35%')

3. Do one of the following:
* To start a new scan, select the **NexPloit Scan** file.
* To re-run an existing scan, select the **NexPloit Re-run Scan** file. 

### Starting a New Scan in Your Pipeline
To initialize a new scan in your pipeline, follow these steps:
1. In the **NexPloit Scan** section, enter the scan details in the relevant fields and select the settings that you want to apply.

  ![new-scan](media/azure-pipelines/new-scan.png ':size=35%')

* For a scan with uploaded HAR file, additionally enter the response **id** in the **File ID** field.
>[!NOTE|label:Note]
The **File ID** value is required for the scans with uploaded HAR files. 

  Once you complete the setup, the scan is started automatically.

2. To manage the scanning process and view the results, go to your [nexploit.app](https://nexploit.app) account.

### Re-running an Existing Scan in Your Pipeline
You can restart a scan that you have already set up and run using [nexploit.app](https://nexploit.app). To do that, follow these steps: 
1. In the **NexPloit Re-run Scan** section, enter the scan details in the relevant fields.
2. Copy the ID of your scan in the address bar or the scan report window and paste it in the **Scan ID** field.

    ![scan-ID](media/azure-pipelines/scan-ID.png ':size=35%')

    Once you complete the setup, the scan is restarted automatically.

3.  To manage the scanning process and view the results, go to your [nexploit.app](https://nexploit.app) account.







