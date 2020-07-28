# Jenkins Integration

![jenkins_logo](media/jenkins-logo.png ':size=40%')

## Setup

To enable Jenkins integration go to the "Organization" tab from your dashboard.

![organization-tab](media/org-tab.png ':size=45%')

In order to configure jenkins find the "Pipeline Integration" widget and click the ![dots](media/dots_button.png ':size=1%') button next to "jenkins" and the click settings to configure integration.

![settings](media/jenkins-settings.png ':size=45%')

You'll be prompet to enter your Jenkins URL, username and access token. To find this information, in your Jenkins dashboard:
1. Click your name (upper-right corner).
2. Click Configure (left-side menu).
3. Use the "Add new Token" button to generate a new one and name it. Note that you must copy the token when you generate it as you cannot view the token afterwards.
After entering the information, click the ![connect](media/connect_button.png ':size=6%') button.

![jenkins-info](media/jenkins-info.png ':size=45%')

Now jenkins is fully configured for use.

## Use jenkins integration with NexPloit (CLI)

After configuring "jenkins" on NexPloit our API is able to access Jenkins API. You can start a scan during build and if NexPloit discovers an issue it will stop the current build process.

1. Create a new API key for your user ([instructions](user-guide/personal-account-administration/details-and-settings.md#managing-your-api-keys)), and enable required scopes (`files:read`, `files:write`, `scans:run`, `scans:read`).

2. Configure a build as you usually would in Jenkins.

3. Select discovery type.

  a. (If you are using a file) Upload your file.
    - To upload a pre-recorded HAR file use this curl command:
    ```bash
    $ curl -X POST "https://nexploit.app/api/v1/files?discard=true"     \
      -H "Content-Type: multipart/form-data"                          \
      -H "Authorization: Api-Key yufn0f6.yourapikeykuj069zopv0b1i"    \
      -F "har=@/path/to/the/file.har"
    ```
    The result of this request has the following structure:
    ```json
    {
        "ids": [ "6xkFraa5ecfmHhxTEnabZg" ]
    }
    ```
    - To upload an open-api specification use this curl command:
    ```bash
    $ curl -X POST "https://nexploit.app/api/v1/specs?discard=true"     \
      -H "Content-Type: multipart/form-data"                          \
      -H "Authorization: Api-Key yufn0f6.yourapikeykuj069zopv0b1i"    \
      -F "file=@/path/to/the/oas.json"
      -F "spec=OpenAPI" 
    ```
    
    - To use a url instead of file to scan an API use this curl command:  
    ```bash
    $ curl -X POST "https://nexploit.app/api/v1/specs?discard=true"     \
      -H "Content-Type: multipart/form-data"                          \
      -H "Authorization: Api-Key yufn0f6.yourapikeykuj069zopv0b1i"    \
      -F "url=https://site.swagger.io/v2/swagger.json"
      -F "spec=OpenAPI"
    ```
    The result of this request has the following structure:
    ```json
    {
      "id": "upcNrqjhujPfMysTzaNrMW"
    }
    ```
  Where `discard` - indicates the life circle of this archive. If you would like to use NexPloit within CI/CD flow, we recommend to set the `discard` option to `true` to remove the archive after running the scan.

  b. (If you want to use a crawler) To use a crawler instead of a HAR file, the crawler options are set as part of the scan creation process so there is no need to do anything before.
  The urls for the crawler are defined under the `crawlerUrls` property and they are an array of absolute urls.

  Note that you can only run a scan in combination of `archive + crawler` or `oas standalone`. To specify the discovery type use the proper values for `discoveryTypes` in the `create scan` request body.

  example:
  ```json
  {
      ...
       "discoveryTypes": [
          "archive",
          "crawler"
      ],
      ...
  }
  ```

  or 

  ```json
  {
      ...
      "discoveryTypes": [
          "oas"
      ],
      ...
  }
  ```

4. Add a step to run the scan with `sh: Shell Script` stage.

  ```bash
  $ curl --request POST \
      --url http://localhost:8000/api/v1/scans \
      --header 'accept: application/json, text/plain, */*' \
      --header "authorization: Api-Key yufn0f6.yourapikeykuj069zopv0b1i"    \
      --header 'content-type: application/json' \
      --data '{
          "name": "App scan",
          "discoveryTypes": [
              "archive",
              "crawler"
          ],
          "module": "core",
          "crawlerUrls": [
              "https://vulnerable-bank.com"
          ],
          "poolSize": 10,
          "fileId": "6xkFraa5ecfmHhxTEnabZg",
          "hostsFilter": [
              "vulnerable-bank.com"
          ],
          "schedule": null,
          "tests": [
              "angular_csti",
              "backup_locations",
              "jwt"
          ],
          "build": {
              "service": "jenkins",
              "project": "myapp",
              "buildNumber": 1
          }
      }'
  ```

  The result of this request has the following structure:

  ```json
  {
      "id": "6xkFraa5ecfmHhxTEnawZa" 
  }
  ```

5. Finish build configuration and run build.

### Additional Notes
In case the build processes faster than the scan you can use the jenkins wait for stage option, on which you can read more on this [link](http://cpitman.github.io/jenkins/cicd/2017/03/16/waiting-for-remote-systems-in-a-jenkins-pipeline.html#.XyA6Dp4zbLY).

Alternatively you can add a script to check for the scan status by calling 

```bash  
$ curl --request GET \
  --url https://nexploit.app/api/v1/scans/6xkFraa5ecfmHhxTEnawZa \
  --header 'authorization: Api-Key yufn0f6.yourapikeykuj069zopv0b1i'
```

The result of this request has the following structure:

```json
{
    "id": "5e74d7f9-e56a-40e5-a668-ba008de1a5cb",
	"nodeId": "cEvifiF6eNwoE281NhSNRH",
	"name": "App scan",
	"module": "core",
	"entryPoints": 0,
	"totalParams": 0,
	"startedBy": {
        ...
	},
	"organization": {
		...
	},
	"status": "pending", // done
	"elapsed": 0,
	"discoveryTypes": [
		"archive",
		"crawler"
	],
	"issuesLength": 0,
	"targets": [
		"vulnerable-bank.com"
	],
	"requests": 0,
	"parentId": null,
    "checks": {
        ...
    },
    "issuesBySeverity": [],
	"startTime": null,
	"requestStatuses": null,
	"techStack": []
}
```

This endpoint will return scan information with property `status`. The script can put the build on hold until NexPloit returns status `done`. To get the id of the scan use the return value of the create scan call.
