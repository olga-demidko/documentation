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


## Adding NexPloit to a Jenkins Pipeline

Here is a collection of steps, that creates a typical Jenkins flow. You can get an idea of how to use the NexPloit API and repeater.

### Prerequisites

You will first need to install the following on **your Jenkins machine**:
- [docker](https://docs.docker.com/engine/install/ubuntu/)
- [docker-compose](https://docs.docker.com/compose/install/)
- [npm](https://www.npmjs.com/)
- [NexPloit CLI package](/nexploit-cli/overview.md)

And you will need to set up the following on **www.nexploit.app**:
- A valid `API_KEY`
  - For this example these scopes are required: `agents:write:repeater`, `scans:run` and `scans:read`
  - More info about [setting up an API key](../user-guide/organization-administration/details-and-policies#managing-organization-api-keys)
- An active `REPEATER_ID`
  - More info about [Setting up a New Repeater](user-guide/agents/overview.md)

### Step-by-step Guide
Every step should be a separate `Execute Shell` script, for example:

![Run Docker](/media/pipeline-example-step-1.png ':size=30%')

Add the following `.sh` scripts to your Jenkins flow:

<!-- tabs:start -->

### **STEP 1 - Run Docker**

```bash
echo "Run docker image with target service and nexploit repeater image";

echo "
version: '3'
services:
  juiceshop.local:
    image: bkimminich/juice-shop
  repeater:
    image: neuralegion/repeater:latest
    restart: always
    environment:
      REPEATER_TOKEN: $API_KEY
      REPEATER_AGENT: $REPEATER_ID
      DEBUG: nexploit-cli" > docker-compose.yml;

docker-compose up -d;
```

### **STEP 2 - Wait for Setup**

```bash
echo "Waiting 10s for setup"

sleep 10s;
```

### **STEP 3 - Run a Scan (Re-Test)**

```bash
echo "Retest a scan"

# Retest scan with id gYJFr5vb6e6GkbJ4tinBms
SCAN_ID=$(nexploit-cli scan:retest --api-key=$API_KEY gYJFr5vb6e6GkbJ4tinBms);
echo "Scan started $SCAN_ID";

# Store a scan id
echo $SCAN_ID > env_scan_id.txt
```

### **STEP 4 - Poll Results**

```bash
echo "Poll for scan results";

# Pull Scan id from a file
SCAN_ID=`cat env_scan_id.txt`

# Poll the scan until it returns something, or its time runs out
RESULT=$(nexploit-cli scan:polling --api-key=$API_KEY --failure-on=first-issue --interval=10000 $SCAN_ID);

# After that - stop the scan
nexploit-cli scan:stop --api-key=$API_KEY $SCAN_ID;

# And put down the docker-compose
docker-compose down;

# Exit step with a code from nexploit-cli
exit $RESULT;
```

<!-- tabs:end -->

And that's it! Your Jenkins flow with NexPloit is configured!

!> See [NexPloit CLI Command List](/nexploit-cli/commands.md) for a full list of commands you can add to your Jenkins flow.

!> In case the build processes is faster than the scan you can use the jenkins wait for stage option, on which you can read more [here](http://cpitman.github.io/jenkins/cicd/2017/03/16/waiting-for-remote-systems-in-a-jenkins-pipeline.html#.XyA6Dp4zbLY).
