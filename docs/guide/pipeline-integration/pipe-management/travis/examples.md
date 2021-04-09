# Usage Examples
## Example 1. Direct scanning using the Nexploit CLI (NPM installation)
To apply this option, you only need to install the Nexploit CLI globally on your Travis CI machine using the relative NPM command. 

### Prerequisites<!-- {docsify-ignore} -->
* You are an active user on  [nexploit.app](https://nexploit.app). 
*  You have a valid [organization API key](https://kb.neuralegion.com/#/guide/np-web-ui/advanced-set-up/managing-org?id=managing-organization-apicli-authentication-tokens) or [personal API key](https://kb.neuralegion.com/#/guide/np-web-ui/advanced-set-up/managing-personal-account?id=managing-your-personal-api-keys-authentication-tokens) (`NEXPLOIT_TOKEN`) with the following scopes: `bot`,<br>`scans : run`,`scan : read`, and `scans : stop`.
* You have created the `NEXPLOIT_TOKEN` variable on your Travis CI machine: more options > settings > add the environmental variable.

### Step-by-Step Guide<!-- {docsify-ignore} -->

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
 --smart)
- printf "Scan was started with ID https://nexploit.app/scans/$SCAN_ID\n"
```
* If you need to re-test a previous scan with its ID `OLD_SCAN_ID`, use the following script:

```bash
-printf "Retest a scan"
- >
NEW_SCAN_ID=$(nexploit-cli scan:retest 
 --token=$NEXPLOIT_TOKEN
 $OLD_SCAN_ID)
-printf "Scan was started with ID https://nexploit.app/scans/$NEW_SCAN_ID\n"
```

##### **STEP 3 -  Poll the Results**

>[!NOTE|label:Note]
When polling the scan results, it is recommended to follow the fail-fast principle by using the `breakpoint` command.  See [Nexploit CLI Command List](guide/np-cli/command-list.md) for a full list of commands you can use in your Travis flow.

```bash
- printf "Wait for issues ⏳\n"

 - >
  # Poll the scan until it returns something, or its time runs out
  nexploit-cli scan:polling 
   --interval 30s 
   --timeout 20m
   --token $NEXPLOIT_TOKEN
   --breakpoint medium_issue 
   $SCAN_ID

allow_failure: true

# After that - stop the scan
 - printf "Stop Scan 🛑"
 - nexploit-cli scan:stop --token $NEXPLOIT_TOKEN $SCAN_ID

```
##### **STEP 4 -  View the  Results**
To view the reports on the detected issues, go to the [nexploit.app](https://nexploit.app).

<!-- tabs:end -->

### Complete Example<!-- {docsify-ignore} -->

The following example is made up of the steps above and shows how to run a new scan using the Crawler discovery type:

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
   nexploit-cli scan:polling
   --interval 30s
   --timeout 20m
   --token $NEXPLOIT_TOKEN
   --breakpoint medium_issue $SCAN_ID
allow_failure: true
after_script:
 - printf "Stop Scan 🛑"
 - nexploit-cli scan:stop 
 --token $NEXPLOIT_TOKEN $SCAN_ID
 ```


## Example 2. Scanning via a Repeater using the Nexploit CLI (NPM installation)
To apply this option, you need to install the Nexploit CLI on your Travis CI machine and activate the Repeater using the Repeater ID and Nexploit API key. 

### Prerequisites<!-- {docsify-ignore} -->
* You are an active user on  [nexploit.app](https://nexploit.app). 
* You have a Repeater with a valid ID ‘REPEATER’. See [Managing Repeaters](/guide/np-web-ui/advanced-set-up/managing-repeaters.md) for the information about handling the Repeaters.
*  You have a valid [organization API key](https://kb.neuralegion.com/#/guide/np-web-ui/advanced-set-up/managing-org?id=managing-organization-apicli-authentication-tokens) or [personal API key](https://kb.neuralegion.com/#/guide/np-web-ui/advanced-set-up/managing-personal-account?id=managing-your-personal-api-keys-authentication-tokens) (`NEXPLOIT_TOKEN`) with the following scopes: `bot`,<br>`scans : run`,`scan : read`, and `scans : stop`.
* You have created the `NEXPLOIT_TOKEN` and `REPEATER` variables on your Travis CI machine: more options > settings > add the environmental variables.

### Step-by-Step Guide<!-- {docsify-ignore} -->

<!-- tabs:start -->

##### **STEP 1 - Install the CLI**

```bash
- npm install @neuralegion/nexploit-cli -g || true
```
##### **STEP 2 - Activate the Repeater**

```bash
nexploit-cli repeater 
--token $NEXPLOIT_TOKEN 
--id $REPEATER 
--bus amqps://amq.nexploit.app:5672 
```

>[!NOTE|label:Note]
If a valid API token `NEXPLOIT-TOKEN` and Repeater ID `REPEATER` were not added, then the **Unauthorized access** error appears. Please check your credentials.

>[!Warning|label:Important]
Make sure that the Repeater has an outbound connection to the Nexploit host depending on its deployment. The Repeater should be connected either to the default **amq.nexploit.app** via the AMQ protocol (over TLS) using port 5672 or to your private cloud using the relative port. 

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
--smart) 
- printf "Scan was started with ID https://nexploit.app/scans/$SCAN_ID\n"
```
* If you need to re-test a previous scan with its ID `OLD_SCAN_ID`, use the following script:

```bash
-printf "Retest a scan"
- >
NEW_SCAN_ID=$(nexploit-cli scan:retest 
--token=$NEXPLOIT_TOKEN 
$OLD_SCAN_ID)
-printf "Scan was started with ID https://nexploit.app/scans/$NEW_SCAN_ID\n"
```
##### **STEP 4 -  Poll the Results**

>[!NOTE|label:Note]
When polling the scan results, it is recommended to follow the fail-fast principle by using the `breakpoint` command.  See [Nexploit CLI Command List](guide/np-cli/command-list.md) for a full list of commands you can use in your Travis flow.

```bash
- printf "Wait for issues ⏳\n"
 - >
# Poll the scan until it returns something, or its time runs out
nexploit-cli scan:polling 
--interval 30s 
--timeout 20m
--token $NEXPLOIT_TOKEN
--breakpoint medium_issue $SCAN_ID
allow_failure: true

# After that - stop the scan
 - printf "Stop Scan 🛑"
 - nexploit-cli scan:stop 
 --token $NEXPLOIT_TOKEN $SCAN_ID

```
##### **STEP 5 -  View the  Results**
To view the reports on the detected issues, go to the [nexploit.app](https://nexploit.app).

<!-- tabs:end -->

### Complete Example<!-- {docsify-ignore} -->

The following example is made up of the steps above and shows how to run a new scan using the Crawler discovery type:

```bash
language: node_js
node_js:
 - 10
before_script:
 - npm install @neuralegion/nexploit-cli -g || true
script:
  nexploit-cli repeater 
  --token $NEXPLOIT_TOKEN
  --id $REPEATER 
  --bus amqps://amq.nexploit.app:5672 
 - printf "Start Nexploit Scan 🏁"
 - >
  SCAN_ID=$(nexploit-cli scan:run
  --token $NEXPLOIT_TOKEN
  --name "Test Travis Scan"
  --repeater $REPEATER
  --crawler http://brokencrystals.com
  --smart)
 - printf "Scan was started with ID https://nexploit.app/scans/$SCAN_ID\n"
 - printf "Wait for issues ⏳\n"
 - >
   nexploit-cli scan:polling
   --interval 30s
   --timeout 20m
   --token $NEXPLOIT_TOKEN
   --breakpoint medium_issue $SCAN_ID
allow_failure: true
after_script:
 - printf "Stop Scan 🛑"
 - nexploit-cli scan:stop 
 --token $NEXPLOIT_TOKEN $SCAN_ID
 ```


## Example 3. Scanning via a Repeater using the Nexploit CLI (Docker installation)
To apply this option, you need to configure a Docker image inside your pipeline (for example,  by creating a docker-compose file). Once the Docker is configured, you can run the Nexploit CLI and activate the Repeater using the Repeater ID and Nexploit API key.   

### Prerequisites<!-- {docsify-ignore} -->
* You are an active user on  [nexploit.app](https://nexploit.app). 
* You have a Repeater with a valid ID ‘REPEATER’. See [Managing Repeaters](/guide/np-web-ui/advanced-set-up/managing-repeaters.md) for the information about handling the Repeaters.
*  You have a valid [organization API key](https://kb.neuralegion.com/#/guide/np-web-ui/advanced-set-up/managing-org?id=managing-organization-apicli-authentication-tokens) or [personal API key](https://kb.neuralegion.com/#/guide/np-web-ui/advanced-set-up/managing-personal-account?id=managing-your-personal-api-keys-authentication-tokens) (`NEXPLOIT_TOKEN`) with the following scopes: `bot`,<br>`scans : run`,`scan : read`, and `scans : stop`.
You have created the `NEXPLOIT_TOKEN` and `REPEATER` variables on your Travis CI machine: more options > settings > add the environmental variables.

### Step-by-Step Guide<!-- {docsify-ignore} -->

<!-- tabs:start -->

##### **STEP 1 - Create the Docker compose `yml` file**
```bash
version:'3'
services:
 brokencrystals.local:
  image: neuralegion/brokencrystals
 repeater:
  image: neuralegion/repeater:latest
  restart: always
  environment:
   REPEATER_TOKEN: ${NEXPLOIT_TOKEN}
   REPEATER_AGENT: ${REPEATER}
   DEBUG: nexploit-cli
```

##### **STEP 2 - Deploy the Docker and run the CLI**

```bash
- sudo curl -L "https://github.com/docker/compose/releases/download/1.26.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
- sudo chmod +x /usr/local/bin/docker-compose
- npm install @neuralegion/nexploit-cli -g || true
```

##### **STEP 3 - Activate the Repeater**

```bash
- - printf "NEXPLOIT_TOKEN=$NEXPLOIT_TOKEN\nREPEATER=$REPEATER\n" > .env
- cat .env
- docker-compose --env-file=.env up -d
- docker-compose config
```

>[!NOTE|label:Note]
If a valid API token `NEXPLOIT-TOKEN` and Repeater ID `REPEATER` were not added, then the **Unauthorized access** error appears. Please check your credentials.

>[!Warning|label:Important]
Make sure that the Repeater has an outbound connection to the Nexploit host depending on its deployment. The Repeater should be connected either to the default **amq.nexploit.app** via the AMQ protocol (over TLS) using port 5672 or to your private cloud using the relative port. 

##### **STEP 4 -  Run (Re-Test) a Scan**

* If you need to run a new scan with a Crawler,  use the following script: 

```bash
-printf "Start Nexploit Scan 🏁"
- >
SCAN_ID=$(nexploit-cli scan:run 
--token $NEXPLOIT_TOKEN
--name "Test Travis Scan" 
--repeater $REPEATER
--crawler www.example.local 
--smart) 
- printf "Scan was started with ID https://nexploit.app/scans/$SCAN_ID\n"
```
* If you need to re-test a previous scan with its ID `OLD_SCAN_ID`, use the following script:

```bash
-printf "Retest a scan"
- >
NEW_SCAN_ID=$(nexploit-cli scan:retest 
--token=$NEXPLOIT_TOKEN 
$OLD_SCAN_ID)
-printf "Scan was started with ID https://nexploit.app/scans/$NEW_SCAN_ID\n"
```

##### **STEP 5 -  Poll the Results**

>[!NOTE|label:Note]
When polling the scan results, it is recommended to follow the fail-fast principle by using the `breakpoint` command.  See [Nexploit CLI Command List](guide/np-cli/command-list.md) for a full list of commands you can use in your Travis flow.

```bash
- printf "Wait for issues ⏳\n"
 - >
# Poll the scan until it returns something, or its time runs out
nexploit-cli scan:polling 
--interval 30s 
--timeout 20m
--token $NEXPLOIT_TOKEN
--breakpoint medium_issue $SCAN_ID
allow_failure: true

# After that - stop the scan
 - printf "Stop Scan 🛑"
 - nexploit-cli scan:stop 
 --token $NEXPLOIT_TOKEN $SCAN_ID

```
##### **STEP 6 -  View the  Results**
To view the reports on the detected issues, go to the [nexploit.app](https://nexploit.app).

<!-- tabs:end -->

### Complete Example<!-- {docsify-ignore} -->
The following example is made up of the steps above and shows how to run a new scan using the Crawler discovery type:

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
  --crawler http://brokencrystals.local
  --smart)
 - printf "Scan was started with ID https://nexploit.app/scans/$SCAN_ID\n"
 - printf "Wait for issues ⏳\n"
 - >
   (nexploit-cli scan:polling
   --interval 30s
   --timeout 20m
   --token $NEXPLOIT_TOKEN
   --breakpoint medium_issue $SCAN_ID
allow_failure: true
after_script:
 - printf "Stop Scan 🛑"
 - nexploit-cli scan:stop 
 --token $NEXPLOIT_TOKEN $SCAN_ID
 ```