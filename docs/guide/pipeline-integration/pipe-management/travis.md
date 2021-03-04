<table id="integrations" >
  <tr>
    <td width="70%">
      <h1>Travis CI</h1>
    </td>
    <td width="30%" style="text-align:center" rowspan="3">
      <img src="guide/pipeline-integration/pipe-management/media/travis/travis-logo.png" width="200" height="250"></img>
    </td>
  </tr>
  <tr>
    <td style="text-align:left;vertical-align:text-top;padding:0px">
    <p>If you are using the Travis CI pipeline for development automation, you can integrate it with NexPloit to run security scans on every new build within your development environment.</p>
    You can enable the integration using one of the following options based on the access permissions of the scan target:
   <ul>
    <li>Running scans using the <b>NexPloit CLI</b>. You should use this option if the scan target is an open-source application that can be reached from the Internet.</li>
    <li>Running scans using the <b>NexPloit CLI  with a pre-configured Repeater</b>. You should use this option if the scan target is hosted on your local network that cannot be reached directly from the Internet. In this case, the <a href="https://kb.neuralegion.com/#/guide/introduction/deployment-onprem">Repeater</a> serves as a proxy between NexPloit and your local target. </li>
    </td>
  </tr>
  </table>


## Running Scans Using NexPloit CLI
Using this approach, you need to install the NexPloit CLI on your Travis CI machine. The CLI provides an easy-to-use interface so that you can control the scans of the target application without leaving your development environment.

### Prerequisites
* You are an active user on  [nexploit.app](https://nexploit.app). 
*  You have a valid [organization API key](https://kb.neuralegion.com/#/guide/np-web-ui/advanced-set-up/managing-org?id=managing-organization-apicli-authentication-tokens) or [personal API key](https://kb.neuralegion.com/#/guide/np-web-ui/advanced-set-up/managing-personal-account?id=managing-your-personal-api-keys-authentication-tokens) (`NEXPLOIT_TOKEN`) with the following scopes: `bot`,<br>`scans : run`,`scan : read`, and `scans : stop`.

### Step-by-Step Guide

<!-- tabs:start -->

##### **STEP 1 - Install the CLI**

```bash
- npm install @neuralegion/nexploit-cli -g || true
```

##### **STEP 2 -  Run (Re-Test) a Scan**

* If you need to run a new scan with a Crawler,  use the following script: 

```bash
-printf "Start Nexploit Scan 🏁"
- >
SCAN_ID=$(nexploit-cli scan:run 
--token $NEXPLOIT_TOKEN
--name "Test Travis Scan" 
--crawler www.example.com 
--smart 
- printf "Scan was started with ID https://nexploit.app/scans/$SCAN_ID\n"
```
* If you need to re-test a previous scan with its ID `OLD_SCAN_ID`, use the following script:

```bash
-printf "Retest a scan"
- >
NEW_SCAN_ID=$(nexploit-cli scan:retest 
--token=$NEXPLOIT_TOKEN 
$OLD_SCAN_ID
-printf "Scan was started with ID https://nexploit.app/scans/$NEW_SCAN_ID\n"
```

##### **STEP 3 -  Poll the Results**

>[!NOTE|label:Note]
When polling the scan results, it is recommended to follow the fail-fast principle by using the `breakpoint` command.  See [NexPloit CLI Command List](guide/np-cli/command-list.md) for a full list of commands you can use in your Travis flow.

```bash
- printf "Wait for issues ⏳\n"
 - >
# Poll the scan until it returns something, or its time runs out
nexploit-cli scan:polling 
--interval 30s 
--timeout 20m
--token $NEXPLOIT_TOKEN
--breakpoint medium_issue $SCAN_ID)
allow_failure: true

# After that - stop the scan
 - printf "Stop Scan 🛑"
 - nexploit-cli scan:stop --token $NEXPLOIT_TOKEN $SCAN_ID

```
##### **STEP 4 -  View the  Results**
To view the reports on the detected issues, go to the [nexploit.app](https://nexploit.app).

<!-- tabs:end -->

### Example

The following example shows how to run a new scan using the Crawler discovery type:

```bash
language: node_js
node_js:
 - 10
before_script:
 - npm install @neuralegion/nexploit-cli -g || true
script:
 - printf "Start Nexploit Scan 🏁"
 - >
  SCAN_ID=$(nexploit-cli scan:run
  --token $NEXPLOIT_TOKEN
  --name "Test Travis Scan"
  --crawler http://brokencrystals.com
  --smart)
 - printf "Scan was started with ID https://nexploit.app/scans/$SCAN_ID\n"
 - printf "Wait for issues ⏳\n"
 - >
   (nexploit-cli scan:polling
   --interval 30s
   --timeout 20m
   --token $NEXPLOIT_TOKEN
   --breakpoint medium_issue $SCAN_ID)
allow_failure: true
after_script:
 - printf "Stop Scan 🛑"
 - nexploit-cli scan:stop --token $NEXPLOIT_TOKEN $SCAN_ID
 ```

## Running Scans via a Repeater
When using this option, you need to install the Docker on your Travis machine. The Doker is a virtual server that will “host” the Repeater within your local network to reach the scan target. Once the Docker container is deployed, you can connect a certain Repeater created on the [nexploit.app](https://nexploit.app) to your local server using the Repeater ID and NexPloit API key. 


### Prerequisites
* You are an active user on  [nexploit.app](https://nexploit.app). 
* You have a Repeater with a valid ID ‘REPEATER’. See [Managing Repeaters](/guide/np-web-ui/advanced-set-up/managing-repeaters.md) for the information about handling the Repeaters.
* The Repeater can be reached from the Internet and has access to the relevant targets on your local network. 
*  You have a valid [organization API key](https://kb.neuralegion.com/#/guide/np-web-ui/advanced-set-up/managing-org?id=managing-organization-apicli-authentication-tokens) or [personal API key](https://kb.neuralegion.com/#/guide/np-web-ui/advanced-set-up/managing-personal-account?id=managing-your-personal-api-keys-authentication-tokens) (`NEXPLOIT_TOKEN`) with the following scopes: `bot`,<br>`scans : run`,`scan : read`, and `scans : stop`.

### Step-by-Step Guide

<!-- tabs:start -->

##### **STEP 1 - Install the Docker and CLI**

```bash
- sudo curl -L "https://github.com/docker/compose/releases/download/1.26.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
- sudo chmod +x /usr/local/bin/docker-compose
- npm install @neuralegion/nexploit-cli -g || true
```

##### **STEP 2 - Activate the Repeater**

```bash
- - printf "NEXPLOIT_TOKEN=$NEXPLOIT_TOKEN\nREPEATER=$REPEATER\n" > .env
- cat .env
- docker-compose --env-file=.env up -d
- docker-compose config
```

>[!NOTE|label:Note]
If a valid API token `NEXPLOIT-TOKEN` and Repeater ID `REPEATER` were not added, then the **Unauthorized access** error appears. Please check your credentials.

>[!Warning|label:Important]
Make sure that the Repeater has an outbound connection to the NexPloit host depending on its deployment. The Repeater should be connected either to the default **amq.nexploit.app** via the AMQ protocol (over TLS) using port 5672 or to your private cloud using the relative port. 

##### **STEP 3 -  Run (Re-Test) a Scan**

* If you need to run a new scan with a Crawler,  use the following script: 

```bash
-printf "Start Nexploit Scan 🏁"
- >
SCAN_ID=$(nexploit-cli scan:run 
--token $NEXPLOIT_TOKEN
--name "Test Travis Scan" 
--repeater $REPEATER
--crawler www.example.com 
--smart 
- printf "Scan was started with ID https://nexploit.app/scans/$SCAN_ID\n"
```
* If you need to re-test a previous scan with its ID `OLD_SCAN_ID`, use the following script:

```bash
-printf "Retest a scan"
- >
NEW_SCAN_ID=$(nexploit-cli scan:retest 
--token=$NEXPLOIT_TOKEN 
$OLD_SCAN_ID
-printf "Scan was started with ID https://nexploit.app/scans/$NEW_SCAN_ID\n""
```

##### **STEP 4 -  Poll the Results**

>[!NOTE|label:Note]
When polling the scan results, it is recommended to follow the fail-fast principle by using the `breakpoint` command.  See [NexPloit CLI Command List](guide/np-cli/command-list.md) for a full list of commands you can use in your Travis flow.

```bash
- printf "Wait for issues ⏳\n"
 - >
# Poll the scan until it returns something, or its time runs out
nexploit-cli scan:polling 
--interval 30s 
--timeout 20m
--token $NEXPLOIT_TOKEN
--breakpoint medium_issue $SCAN_ID)
allow_failure: true

# After that - stop the scan
 - printf "Stop Scan 🛑"
 - nexploit-cli scan:stop --token $NEXPLOIT_TOKEN $SCAN_ID

```
##### **STEP 5 -  View the  Results**
To view the reports on the detected issues, go to the [nexploit.app](https://nexploit.app).

<!-- tabs:end -->

### Example
The following example shows how to run a new scan using the Crawler discovery type:

```bash
language: node_js
node_js:
 - 10
before_script:
 - sudo curl -L "https://github.com/docker/compose/releases/download/1.26.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
 - sudo chmod +x /usr/local/bin/docker-compose
 - npm install @neuralegion/nexploit-cli -g || true
script:
 - printf "NEXPLOIT_TOKEN=$NEXPLOIT_TOKEN\nREPEATER=$REPEATER\n" > .env
 - cat .env
 - docker-compose --env-file=.env up -d
 - docker-compose config
 - printf "Start Nexploit Scan 🏁"
 - >
  SCAN_ID=$(nexploit-cli scan:run
  --token $NEXPLOIT_TOKEN
  --repeater $REPEATER
  --name "Test Travis Scan"
  --crawler http://brokencrystals.com
  --smart)
 - printf "Scan was started with ID https://nexploit.app/scans/$SCAN_ID\n"
 - printf "Wait for issues ⏳\n"
 - >
   (nexploit-cli scan:polling
   --interval 30s
   --timeout 20m
   --token $NEXPLOIT_TOKEN
   --breakpoint medium_issue $SCAN_ID)
allow_failure: true
after_script:
 - printf "Stop Scan 🛑"
 - nexploit-cli scan:stop --token $NEXPLOIT_TOKEN $SCAN_ID
 ```