# GitHub Issues Integration

![github_logo](media/github-logo.png ':size=40%')

## About
To enable full automation into your CI/CD pipeline, you can configure our solutions to automatically open tickets in your selected GitHub repositories. Each new ticket will provide all the information from NexPloit to give developers everything they need to solve the problems, without leaving the comfort of their development environment.

More info about NexPloit Integration to GitHub Issues here: https://github.com/apps/nexploit-app

## Connecting NexPloit to your GitHub repository

1. Login to NexPloit and navigate to the [organization page](https://nexploit.app/organization) by clicking on the **Organization** button on the sidebar.

![organization](media/go-to-organization.png ':size=100%')

2. Scroll down to the **TICKET MANAGEMENT INTEGRATION** panel.

![ticketing-panel](media/ticketing-panel.png ':size=100%')

3. Click on the ![dots](media/dots_button.png ':size=1%') button next to "GitHub" and then choose the "Settings" option.

![gh-settings](media/gh-ticketing-settings.png ':size=100%')

4. Click the ![activate](media/activate-github_button.png ':size=10%') button.

![gh-activate](media/gh-activate.png ':size=100%')

5. Select the GitHub organization to install the integration to.

![gh-select-org](media/github-select-org.png ':size=100%')

6. Click the "Install" button.

![gh-install](media/gh-install-app.png ':size=100%')

## Using GitHub Issues Integration

To have issues opened automatically, you'll need to select the GitHub repository for each scan.

1. When initiating a scan, go to the **ADDITIONAL SETTINGS** tab, and find the "Integrations" dropdown menu.

![additional-settings](media/additional-settings.png ':size=100%')

2. In the "Integrations" dropdown menu, select the GitHub repository for this scan.

![select-gh-repo](media/gh-repo-select.png ':size=100%')

Now when you'll run this scan, all it's issues will automatically open a ticket in the chosen GitHub repository.

<!-- ## Connect A Jira Account
1. To connect your account go to https://nexploit.app/organization

![organization](../../media/organization-from-scans.png ':size=80%')


2. Scroll down to the **TICKET MANAGEMENT OPTIONS** section.

![ticket_management_integration](../../media/ticket-management-integration.png ':size=80%')


3. Click on **⋮** and then on **Settings** next to **Jira**

![jira_settings](media/jira-settings.png ':size=80%')


3. Fill out your **Jira Integration Details** and click on **Connect**

!> **Make sure the API token you use is for a <u>specific profile</u> (not Admin/Organization level API key), this is done for security purposes.**

![jira_integration_details](media/jira-integration-details.png ':size=80%')


## Add a Jira Repository To a Scan
When starting a **new scan**, you can select a **Jira Repository** to automatically add the scan findings into.

### Using The UI
1.  Selecting the repository can be done by clicking on **Additional settings**

![new_scan_additional_settings](../../media/new-scan-additional-settings.png ':size=80%')


2. Under Additional settings, scroll down and click on **Integrations**.

![new_scan_integrations](../../media/new-scan-integrations.png ':size=80%')


3. Select the relevant **Jira Repository** and scan away!

![new_scan_jira_integration](media/new-scan-jira-integration.png ':size=80%')


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

### Using The CLI Tool
When starting a scan using our CLI tool **nexploit-cli**, you can select a **Jira Repository** to add the finding to automatically as they are discovered. Just add the Jira repository details with the **--tracking-space** parameter, for example:
```bash
nexploit-cli scan:run \
  --name scan-name \
  --archive received-archive-id \
  --api-key my-jwt-authentication-token \
  --tracking-space https://neuralegion-demo.atlassian.net/jira/software/projects/NEX/boards/1 
```

?> More info can be found here:  https://www.npmjs.com/package/@neuralegion/nexploit-cli
 -->
