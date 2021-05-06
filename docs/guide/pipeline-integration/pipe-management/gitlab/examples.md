# Usage Examples
## Example 1. Direct scanning using the Nexploit CLI (NPM installation)
To apply this option, you only need to install the NexPloit CLI globally on your GitLab machine using the relative NPM command. 

### Prerequisites<!-- {docsify-ignore} -->
* You are an active user on  [nexploit.app](https://nexploit.app). 
*  You have a valid [organization API key](https://kb.neuralegion.com/#/guide/np-web-ui/advanced-set-up/managing-org?id=managing-organization-apicli-authentication-tokens) or [personal API key](https://kb.neuralegion.com/#/guide/np-web-ui/advanced-set-up/managing-personal-account?id=managing-your-personal-api-keys-authentication-tokens) (`NEXPLOIT_TOKEN`) with the following scopes: `bot`,<br>`scans : run`,`scan : read`, and `scans : stop`.
* You have set the `NEXPLOIT_TOKEN` and `REPEATER` variables in your GitLab pipeline: Settings > CI/CD > Variables.

### Step-by-Step Guide<!-- {docsify-ignore} -->

<!-- tabs:start -->

##### **STEP 1 - Install the CLI**

```bash
- npm install @neuralegion/nexploit-cli -g --unsafe-perm || true
```

##### **STEP 2 -  Run (Re-Test) a Scan**

* If you need to run a new scan with a Crawler,  use the following script: 

```bash
- echo "Start Nexploit Scan 🏁"
  - >
    SCAN_ID=$(nexploit-cli scan:run --token $NEXPLOIT_TOKEN
    --name "Test Gitlab Scan"
    --crawler www.example.com 
    --smart)
  - echo "export SCAN_ID=$SCAN_ID" > $CI_PROJECT_DIR/variables
  - printf "Scan was started with ID https://nexploit.app/scans/$SCAN_ID\n"
```
* If you need to re-test a previous scan with its ID `OLD_SCAN_ID`, use the following script:

```bash
- echo "Retest a scan"
- >
  NEW_SCAN_ID=$(nexploit-cli scan:retest --token=$NEXPLOIT_TOKEN $OLD_SCAN_ID)
-printf "Scan was started with ID https://nexploit.app/scans/$NEW_SCAN_ID\n"
```

##### **STEP 3 -  Poll the Results**

>[!NOTE|label:Note]
When polling the scan results, it is recommended to follow the fail-fast principle by using the `breakpoint` command.  See [Nexploit CLI Command List](guide/np-cli/command-list.md) for a full list of commands you can use in your Travis flow.

```bash
- printf "Wait for issues ⏳\n"

 - >
  # Poll the scan until it returns something, or its time runs out
  (nexploit-cli scan:polling
    --interval 30s
    --timeout 20m
    --token $NEXPLOIT_TOKEN
    --breakpoint medium_issue $SCAN_ID)
  artifacts:
    paths:
    - variables
  allow_failure: true

# After that - stop the scan
 echo "Stop Scan 🛑"
      nexploit-cli scan:stop --token $NEXPLOIT_TOKEN $SCAN_ID
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
 --token $NEXPLOIT_TOKEN $SCAN_IDimage: ubuntu:20.04
cache:
  paths:
  - variables
test:
  before_script:
  - apt update -qq --fix-missing
  - apt install -y --no-install-recommends nodejs npm make g++
  - npm install @neuralegion/nexploit-cli -g --unsafe-perm || true
  script:
  - echo "Start Nexploit Scan 🏁"
  - >
    SCAN_ID=$(nexploit-cli scan:run --token $NEXPLOIT_TOKEN
    --name "Test Gitlab Scan"
    --crawler https://juice-shop.herokuapp.com/
    --smart)
  - echo "export SCAN_ID=$SCAN_ID" > $CI_PROJECT_DIR/variables
  - printf "Scan was started with ID https://nexploit.app/scans/$SCAN_ID\n"
  - printf "Wait for issues ⏳\n"
  - >
    (nexploit-cli scan:polling
    --interval 30s
    --timeout 20m
    --token $NEXPLOIT_TOKEN
    --breakpoint medium_issue $SCAN_ID)
  artifacts:
    paths:
    - variables
  allow_failure: true
  after_script:
  - source $CI_PROJECT_DIR/variables
  - >
    if [ -e $CI_PROJECT_DIR/variables ]; then
      echo "Stop Scan 🛑"
      nexploit-cli scan:stop --token $NEXPLOIT_TOKEN $SCAN_ID
    else
      echo "Failed to stop scan"
    fi
 ```


## Example 2. Scanning via a Repeater using the Nexploit CLI (NPM installation)
To apply this option, you need to install the NexPloit CLI on your GitLab machine and activate the Repeater using the Repeater ID and NexPloit API key. 

### Prerequisites<!-- {docsify-ignore} -->
* You are an active user on  [nexploit.app](https://nexploit.app). 
* You have a Repeater with a valid ID ‘REPEATER’. See [Managing Repeaters](/guide/np-web-ui/advanced-set-up/managing-repeaters.md) for the information about handling the Repeaters.
*  You have a valid [organization API key](https://kb.neuralegion.com/#/guide/np-web-ui/advanced-set-up/managing-org?id=managing-organization-apicli-authentication-tokens) or [personal API key](https://kb.neuralegion.com/#/guide/np-web-ui/advanced-set-up/managing-personal-account?id=managing-your-personal-api-keys-authentication-tokens) (`NEXPLOIT_TOKEN`) with the following scopes: `bot`,<br>`scans : run`,`scan : read`, and `scans : stop`.
* You have set the `NEXPLOIT_TOKEN` and `REPEATER` variables in your GitLab pipeline: Settings > CI/CD > Variables.

### Step-by-Step Guide<!-- {docsify-ignore} -->

<!-- tabs:start -->

##### **STEP 1 - Install the CLI**

```bash
- npm install @neuralegion/nexploit-cli -g --unsafe-perm || true
```
##### **STEP 2 - Activate the Repeater**

```bash
- echo "Run repeater 🔁"
  - echo $REPEATER
  - echo $NEXPLOIT_TOKEN
  - >
    nexploit-cli repeater
    --token $NEXPLOIT_TOKEN
    --id $REPEATER
```

>[!NOTE|label:Note]
If a valid API token `NEXPLOIT-TOKEN` and Repeater ID `REPEATER` were not added, then the **Unauthorized access** error appears. Please check your credentials.

>[!Warning|label:Important]
Make sure that the Repeater has an outbound connection to the Nexploit host depending on its deployment. The Repeater should be connected either to the default **amq.nexploit.app** via the AMQ protocol (over TLS) using port 5672 or to your private cloud using the relative port. 

##### **STEP 3 -  Run (Re-Test) a Scan**

* If you need to run a new scan with a Crawler,  use the following script: 

```bash
- echo "Start Nexploit Scan 🏁"
  - >
    SCAN_ID=$(nexploit-cli scan:run --token $NEXPLOIT_TOKEN
    --name "Test Gitlab Scan"
    --repeater $REPEATER
    --crawler www.example.com 
    --smart)
  - echo "export SCAN_ID=$SCAN_ID" > $CI_PROJECT_DIR/variables
  - printf "Scan was started with ID https://nexploit.app/scans/$SCAN_ID\n"
```
* If you need to re-test a previous scan with its ID `OLD_SCAN_ID`, use the following script:

```bash
- echo "Retest a scan"
- >
  NEW_SCAN_ID=$(nexploit-cli scan:retest --token=$NEXPLOIT_TOKEN $OLD_SCAN_ID)
-printf "Scan was started with ID https://nexploit.app/scans/$NEW_SCAN_ID\n"
```
##### **STEP 4 -  Poll the Results**

>[!NOTE|label:Note]
When polling the scan results, it is recommended to follow the fail-fast principle by using the `breakpoint` command.  See [Nexploit CLI Command List](guide/np-cli/command-list.md) for a full list of commands you can use in your Travis flow.

```bash
- printf "Wait for issues ⏳\n"

 - >
  # Poll the scan until it returns something, or its time runs out
  (nexploit-cli scan:polling
    --interval 30s
    --timeout 20m
    --token $NEXPLOIT_TOKEN
    --breakpoint medium_issue $SCAN_ID)
  artifacts:
    paths:
    - variables
  allow_failure: true

# After that - stop the scan
 echo "Stop Scan 🛑"
      nexploit-cli scan:stop --token $NEXPLOIT_TOKEN $SCAN_ID
```
##### **STEP 5 -  View the  Results**
To view the reports on the detected issues, go to the [nexploit.app](https://nexploit.app).

<!-- tabs:end -->

### Complete Example<!-- {docsify-ignore} -->

The following example is made up of the steps above and shows how to run a new scan using the Crawler discovery type:

```bash
image: ubuntu:20.04
cache:
  paths:
  - variables
test:
  before_script:
  - apt update -qq --fix-missing
  - apt install -y --no-install-recommends nodejs npm make g++
  - npm install @neuralegion/nexploit-cli -g --unsafe-perm || true
  script:
  - echo "Run repeater 🔁"
  - echo $REPEATER
  - echo $NEXPLOIT_TOKEN
  - >
    nexploit-cli repeater
    --token $NEXPLOIT_TOKEN
    --id $REPEATER
  - echo "Start Nexploit Scan 🏁"
  - >
    SCAN_ID=$(nexploit-cli scan:run --token $NEXPLOIT_TOKEN
    --repeater $REPEATER
    --name "Test Gitlab Scan"
    --crawler https://brokencrystals.com
    --smart)
  - echo "export SCAN_ID=$SCAN_ID" > $CI_PROJECT_DIR/variables
  - printf "Scan was started with ID https://nexploit.app/scans/$SCAN_ID\n"
  - printf "Wait for issues ⏳\n"
  - >
    (nexploit-cli scan:polling
    --interval 30s
    --timeout 20m
    --token $NEXPLOIT_TOKEN
    --breakpoint medium_issue $SCAN_ID)
  artifacts:
    paths:
    - variables
  allow_failure: true
  after_script:
  - source $CI_PROJECT_DIR/variables
  - >
    if [ -e $CI_PROJECT_DIR/variables ]; then
      echo "Stop Scan 🛑"
      nexploit-cli scan:stop --token $NEXPLOIT_TOKEN $SCAN_ID
    else
      echo "Failed to stop scan"
    fi
 ```


## Example 3. Scanning via a Repeater using the Nexploit CLI (Docker installation)
To apply this option, you need to configure a Docker image inside your pipeline (for example,  by creating a docker-compose file). Once the Docker is configured, you can run the NexPloit CLI and activate the Repeater using the Repeater ID and NexPloit API key.   

### Prerequisites<!-- {docsify-ignore} -->
* You are an active user on  [nexploit.app](https://nexploit.app). 
* You have a Repeater with a valid ID ‘REPEATER’. See [Managing Repeaters](/guide/np-web-ui/advanced-set-up/managing-repeaters.md) for the information about handling the Repeaters.
*  You have a valid [organization API key](https://kb.neuralegion.com/#/guide/np-web-ui/advanced-set-up/managing-org?id=managing-organization-apicli-authentication-tokens) or [personal API key](https://kb.neuralegion.com/#/guide/np-web-ui/advanced-set-up/managing-personal-account?id=managing-your-personal-api-keys-authentication-tokens) (`NEXPLOIT_TOKEN`) with the following scopes: `bot`,<br>`scans : run`,`scan : read`, and `scans : stop`.
* You have set the `NEXPLOIT_TOKEN` and `REPEATER` variables in your GitLab pipeline: Settings > CI/CD > Variables.

### Step-by-Step Guide<!-- {docsify-ignore} -->

<!-- tabs:start -->

##### **STEP 1 - Create the Docker compose `yml` file**
```bash
version: '3'
services:
  juiceshop.local:
    image: bkimminich/juice-shop
    ports:
          - "3000:3000"
  repeater:
    image: neuralegion/repeater:latest
    restart: always
    environment:
      REPEATER_TOKEN: $NEXPLOIT_TOKEN
      REPEATER_AGENT: $REPEATER
      DEBUG: nexploit-cli
```

##### **STEP 2 - Deploy the Docker and run the CLI**

```bash
before_script:
  - touch variables.txt
  - echo "****** INSTALL DEPENDECIES *********"
  - apt-get update
  - apt-get -y install curl
  - curl -L "https://github.com/docker/compose/releases/download/1.26.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
  - chmod +x /usr/local/bin/docker-compose
  - apt-get -y install apt-transport-https ca-certificates curl software-properties-common
  - curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
  - add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
  - apt update
  - apt-cache policy docker-ce
  - apt-get -y install docker-ce
  - docker-compose --version
  - service docker start
  - apt update -qq --fix-missing
  - apt install -y --no-install-recommends nodejs npm make g++
  - npm install @neuralegion/nexploit-cli -g --unsafe-perm || true
```

##### **STEP 3 -  Run (Re-Test) a Scan**

* If you need to run a new scan with a Crawler,  use the following script: 

```bash
- echo "Start Nexploit Scan 🏁"
  - >
    SCAN_ID=$(nexploit-cli scan:run --token $NEXPLOIT_TOKEN
    --name "Test Gitlab Scan"
    --repeater $REPEATER
    --crawler www.example.com 
    --smart)
  - echo "export SCAN_ID=$SCAN_ID" > $CI_PROJECT_DIR/variables
  - printf "Scan was started with ID https://nexploit.app/scans/$SCAN_ID\n"
```
* If you need to re-test a previous scan with its ID `OLD_SCAN_ID`, use the following script:

```bash
- echo "Retest a scan"
- >
  NEW_SCAN_ID=$(nexploit-cli scan:retest --token=$NEXPLOIT_TOKEN $OLD_SCAN_ID)
-printf "Scan was started with ID https://nexploit.app/scans/$NEW_SCAN_ID\n"
```

##### **STEP 4 -  Poll the Results**

>[!NOTE|label:Note]
When polling the scan results, it is recommended to follow the fail-fast principle by using the `breakpoint` command.  See [Nexploit CLI Command List](guide/np-cli/command-list.md) for a full list of commands you can use in your Travis flow.

```bash
- printf "Wait for issues ⏳\n"

 - >
  # Poll the scan until it returns something, or its time runs out
  (nexploit-cli scan:polling
    --interval 30s
    --timeout 20m
    --token $NEXPLOIT_TOKEN
    --breakpoint medium_issue $SCAN_ID)
  artifacts:
    paths:
    - variables
  allow_failure: true

# After that - stop the scan
 echo "Stop Scan 🛑"
      nexploit-cli scan:stop --token $NEXPLOIT_TOKEN $SCAN_ID
```
##### **STEP 5 -  View the  Results**
To view the reports on the detected issues, go to the [nexploit.app](https://nexploit.app).

<!-- tabs:end -->

### Complete Example<!-- {docsify-ignore} -->
The following example is made up of the steps above and shows how to run a new scan using the Crawler discovery type:

```bash
image: ubuntu:20.04
cache:
  paths:
  - variables
test:
  before_script:
  - touch variables.txt
  - echo "****** INSTALL DEPENDECIES *********"
  - apt-get update
  - apt-get -y install curl
  - curl -L "https://github.com/docker/compose/releases/download/1.26.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
  - chmod +x /usr/local/bin/docker-compose
  - apt-get -y install apt-transport-https ca-certificates curl software-properties-common
  - curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
  - add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
  - apt update
  - apt-cache policy docker-ce
  - apt-get -y install docker-ce
  - docker-compose --version
  - service docker start
  - apt update -qq --fix-missing
  - apt install -y --no-install-recommends nodejs npm make g++
  - npm install @neuralegion/nexploit-cli -g --unsafe-perm || true
  script:
  - echo "Start Nexploit Scan 🏁"
  - >
    SCAN_ID=$(nexploit-cli scan:run --token $NEXPLOIT_TOKEN
    --repeater $REPEATER
    --name "Test Gitlab Scan"
    --crawler http://juiceshop.local:3000
    --smart)
  - echo "export SCAN_ID=$SCAN_ID" > $CI_PROJECT_DIR/variables
  - printf "Scan was started with ID https://nexploit.app/scans/$SCAN_ID\n"
  - printf "Wait for issues ⏳\n"
  - >
    (nexploit-cli scan:polling
    --interval 30s
    --timeout 20m
    --token $NEXPLOIT_TOKEN
    --breakpoint medium_issue $SCAN_ID)
  artifacts:
    paths:
    - variables
  allow_failure: true
  after_script:
  - source $CI_PROJECT_DIR/variables
  - >
    if [ -e $CI_PROJECT_DIR/variables ]; then
      echo "Stop Scan 🛑"
      nexploit-cli scan:stop --token $NEXPLOIT_TOKEN $SCAN_ID
    else
      echo "Failed to stop scan"
    fi
 ```