# Jira Ticketing System

![jira-logo](media/jira/jira-logo.png ':size=25%')

To enable full automation to your CI/CD pipeline, you can configure NexPloit to automatically open tickets in your selected Jira repositories. Each new ticket provides developers with all the NexPloit information for solving problems, without having to leave their development environment.

## Connecting a Jira Account
To connect a Jira account –
1. Go to [nexploit.app](https://nexploit.app).
2. Select the Organization option in the left pane to display the Organization page.
3. Scroll down to the **TICKET MANAGEMENT INTEGRATION** section.\
![ticketing-panel](media/jira/ticketing-panel.png ':size=45%')
4. Click ![dots-button](media/jira/dots-button.png ':size=1%') next to **Jira** and then click **Settings**.\
![jira-settings](media/jira/jira-settings.png ':size=45%')
5. Fill in your Jira details\
![jira-integration-details](media/jira/jira-integration-details.png ':size=45%')
> [!WARNING|label:Important]
For security purposes, make sure to use the authentication token (API key) of a specific profile (not the Admin/Organization level API key).

## Adding a Jira Repository to a Scan
When [starting a new scan](guide/np-web-ui/scanning/creating-new-scan.md), you can select a Jira repository to which to automatically add the scan findings. Use one of the following methods –
* [Using the UI](#using-the-ui)
* [Using the NeuraLegion API](#using-the-neuralegion-api)

### Using the UI
To add a Jira repository to a scan using the UI –
1. Click **Additional settings**.\
![additional-settings](media/jira/additional-settings.png ':size=45%')
2. Under **Additional settings**, scroll down and click **Integrations**.\
![additional-settings-2](media/jira/additional-settings-2.png ':size=45%')
3. Select the relevant Jira repository and perform scans as needed.\
![additional-settings-3](media/jira/additional-settings-3.png ':size=45%')

### Using the NeuraLegion API
When creating a new scan from an API call, make sure to add the Jira repository details with the **trackingSpace** parameter. For example –
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