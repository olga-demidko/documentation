# Jira Integration

![jira_logo](media/jira-software-blue.svg ':size=50%')

## About
To enable full automation into your CI/CD pipeline, you can configure our solutions to automatically open tickets in your selected Jira repositories. Each new ticket will provide all the information from NexPloit to give developers everything they need to solve the problems, without leaving the comfort of their development environment.

## Connect A Jira Account
1. To connect your account go to https://nexploit.app/organization

![organization](../../media/organization-from-scans.png ':size=45%')


2. Scroll down to the **TICKET MANAGEMENT OPTIONS** section.

![ticket_management_integration](../../media/ticket-management-integration.png ':size=45%')


3. Click on **⋮** and then on **Settings** next to **Jira**

![jira_settings](media/jira-settings.png ':size=45%')


3. Fill out your **Jira Integration Details** and click on **Connect**

!> **Make sure the API token you use is for a <u>specific profile</u> (not Admin/Organization level API key), this is done for security purposes.**

![jira_integration_details](media/jira-integration-details.png ':size=45%')


## Add a Jira Repository To a Scan
When starting a **new scan**, you can select a **Jira Repository** to automatically add the scan findings into.

### Using The UI
1.  Selecting the repository can be done by clicking on **Additional settings**

![new_scan_additional_settings](../../media/new-scan-additional-settings.png ':size=45%')


2. Under Additional settings, scroll down and click on **Integrations**.

![new_scan_integrations](../../media/new-scan-integrations.png ':size=45%')


3. Select the relevant **Jira Repository** and scan away!

![new_scan_jira_integration](media/new-scan-jira-integration.png ':size=45%')


### Using The NeuraLegion API
When creating a new scan from an **API call**, make sure to add the Jira repository details with the **trackingSpace**  parameter, for example:
```bash
curl 'https://nexploit.app/api/v1/scans' \
-H 'Authorization: Api-Key YOUR_API_KEY' \
-H 'Content-Type: application/json' \
--data '{
  "name": "test",
  "discoveryTypes": [
    "crawler"
  ],
  "crawlerUrls": [
    "https://nexploit.app/login"
  ],
  "tests": [
    "jwt",
    "angular_csti"
  ],
  "trackingSpace":{
    "uri":"https://neuralegion-demo.atlassian.net/jira/software/projects/NEX/boards/1",
    "service":"jira",
    "id":"NEX",
    "name":"NexPloit"
  }
}'
```
?> More info can be found here: https://nexploit.app/api/v1/docs/#/Scans/ScanController.createScan
