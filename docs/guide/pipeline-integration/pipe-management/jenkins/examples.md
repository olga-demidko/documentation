# Usage Examples
## Example 1. Direct scanning using the NexPloit CLI (NPM installation)
To apply this option, you only need to install the NexPloit CLI globally on your Jenkins machine using the relative NPM command. 

### Prerequisites<!-- {docsify-ignore} -->
* You are an active user on  [nexploit.app](https://nexploit.app). 
*  You have a valid [organization API key](https://kb.neuralegion.com/#/guide/np-web-ui/advanced-set-up/managing-org?id=managing-organization-apicli-authentication-tokens) or [personal API key](https://kb.neuralegion.com/#/guide/np-web-ui/advanced-set-up/managing-personal-account?id=managing-your-personal-api-keys-authentication-tokens) (`NEXPLOIT_TOKEN`) with the following scopes: `bot`,<br>`scans : run`,`scan : read`, and `scans : stop`.

### Step-by-Step Guide<!-- {docsify-ignore} -->

<!-- tabs:start -->

##### **STEP 1 - Install the CLI**

```bash
- npm install @neuralegion/nexploit-cli -g || true
```

##### **STEP 2 -  Run (Re-Test) a Scan**

```bash
echo "Retest a scan"

# Retest a previous scan with its ID `OLD_SCAN_ID` and API key `NEXPLOIT_TOKEN`
NEW_SCAN_ID=$(nexploit-cli scan:retest --token=$NEXPLOIT_TOKEN $OLD_SCAN_ID;
echo "Scan started $NEW_SCAN_ID";
```

##### **STEP 3 -  Poll the Results**

>[!NOTE|label:Note]
When polling the scan results, it is recommended to follow the fail-fast principle by using the `breakpoint` command.  See [NexPloit CLI Command List](guide/np-cli/command-list.md) for a full list of commands you can use in your Travis flow.

```bash
echo "Poll for scan results";

# Poll the scan until it returns some issue, or its time runs out
RESULT=$(nexploit-cli scan:polling --token=$NEXPLOIT_TOKEN --failure-on=first-issue --interval=10000 $NEW_SCAN_ID);

# After that - stop the scan
nexploit-cli scan:stop --token=$NEXPLOIT_TOKEN $NEW_SCAN_ID;

# Exit step with a code from nexploit-cli
exit $RESULT;
```

##### **STEP 4 -  View the  Results**
To view the reports on the detected issues, go to the [nexploit.app](https://nexploit.app).

<!-- tabs:end -->



## Example 2. Scanning via a Repeater using the NexPloit CLI (NPM installation)
To apply this option, you need to install the NexPloit CLI on your Jenkins machine and activate the Repeater using the Repeater ID and NexPloit API key. 

### Prerequisites<!-- {docsify-ignore} -->
* You are an active user on  [nexploit.app](https://nexploit.app). 
* You have a Repeater with a valid ID ‘REPEATER’. See [Managing Repeaters](/guide/np-web-ui/advanced-set-up/managing-repeaters.md) for the information about handling the Repeaters.
*  You have a valid [organization API key](https://kb.neuralegion.com/#/guide/np-web-ui/advanced-set-up/managing-org?id=managing-organization-apicli-authentication-tokens) or [personal API key](https://kb.neuralegion.com/#/guide/np-web-ui/advanced-set-up/managing-personal-account?id=managing-your-personal-api-keys-authentication-tokens) (`NEXPLOIT_TOKEN`) with the following scopes: `bot`,<br>`scans : run`,`scan : read`, and `scans : stop`.

### Step-by-Step Guide<!-- {docsify-ignore} -->

<!-- tabs:start -->

##### **STEP 1 - Install the CLI**

```bash
- npm install @neuralegion/nexploit-cli -g || true
```
##### **STEP 2 - Activate the Repeater**

```bash
PID_REPEATER=$(nexploit-cli repeater --token=$NEXPLOIT_TOKEN --agent=$REPEATER &> /dev/null & echo $!)
echo "Repeater PID: $PID_REPEATER"
```

>[!NOTE|label:Note]
If a valid API token `NEXPLOIT-TOKEN` and Repeater ID `REPEATER` were not added, then the **Unauthorized access** error appears. Please check your credentials.

>[!Warning|label:Important]
Make sure that the Repeater has an outbound connection to the NexPloit host depending on its deployment. The Repeater should be connected either to the default **amq.nexploit.app** via the AMQ protocol (over TLS) using port 5672 or to your private cloud using the relative port. 

##### **STEP 3 -  Run (Re-Test) a Scan**

```bash
echo "Retest a scan"

# Retest a previous scan with its ID `OLD_SCAN_ID` and API key `NEXPLOIT_TOKEN`
NEW_SCAN_ID=$(nexploit-cli scan:retest --token=$NEXPLOIT_TOKEN $OLD_SCAN_ID;
echo "Scan started $NEW_SCAN_ID";
```

##### **STEP 4 -  Poll the Results**

>[!NOTE|label:Note]
When polling the scan results, it is recommended to follow the fail-fast principle by using the `breakpoint` command.  See [NexPloit CLI Command List](guide/np-cli/command-list.md) for a full list of commands you can use in your Travis flow.

```bash
echo "Poll for scan results";

# Poll the scan until it returns some issue, or its time runs out
RESULT=$(nexploit-cli scan:polling --token=$NEXPLOIT_TOKEN --failure-on=first-issue --interval=10000 $NEW_SCAN_ID);

# After that - stop the scan
nexploit-cli scan:stop --token=$NEXPLOIT_TOKEN $NEW_SCAN_ID;

# Kill repeater process
kill -9 $PID_REPEATER

# Exit step with a code from nexploit-cli
exit $RESULT;
```

##### **STEP 5 -  View the  Results**
To view the reports on the detected issues, go to the [nexploit.app](https://nexploit.app).

<!-- tabs:end -->

## Example 3. Scanning via a Repeater using the NexPloit CLI (Docker installation)
To apply this option, you need to configure a Docker image inside your pipeline (for example,  by creating a docker-compose file). Once the Docker is configured, you can run the NexPloit CLI and activate the Repeater using the Repeater ID and NexPloit API key.   

### Prerequisites<!-- {docsify-ignore} -->
* You are an active user on  [nexploit.app](https://nexploit.app). 
* You have a Repeater with a valid ID ‘REPEATER’. See [Managing Repeaters](/guide/np-web-ui/advanced-set-up/managing-repeaters.md) for the information about handling the Repeaters.
*  You have a valid [organization API key](https://kb.neuralegion.com/#/guide/np-web-ui/advanced-set-up/managing-org?id=managing-organization-apicli-authentication-tokens) or [personal API key](https://kb.neuralegion.com/#/guide/np-web-ui/advanced-set-up/managing-personal-account?id=managing-your-personal-api-keys-authentication-tokens) (`NEXPLOIT_TOKEN`) with the following scopes: `bot`,<br>`scans : run`,`scan : read`, and `scans : stop`.

### Step-by-Step Guide<!-- {docsify-ignore} -->

<!-- tabs:start -->

##### **STEP 1 - Create the Docker compose `yml` file**
```bash
echo "Run docker image with target service and nexploit repeater image";

echo "
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
   DEBUG: nexploit-cli" > docker-compose.yml ;

   docker-compose up -d
```

##### **STEP 2 - Activate the Repeater**

```bash
PID_REPEATER=$(nexploit-cli repeater --token=$AUTH_TOKEN --agent=$REPEATER_ID &> /dev/null & echo $!)
echo "Repeater PID: $PID_REPEATER"
```

>[!NOTE|label:Note]
If a valid API token `NEXPLOIT-TOKEN` and Repeater ID `REPEATER` were not added, then the **Unauthorized access** error appears. Please check your credentials.

>[!Warning|label:Important]
Make sure that the Repeater has an outbound connection to the NexPloit host depending on its deployment. The Repeater should be connected either to the default **amq.nexploit.app** via the AMQ protocol (over TLS) using port 5672 or to your private cloud using the relative port. 

##### **STEP 3 -  Run (Re-Test) a Scan**

```bash
echo "Retest a scan"

# Retest a previous scan with its ID `OLD_SCAN_ID` and API key `NEXPLOIT_TOKEN`
NEW_SCAN_ID=$(nexploit-cli scan:retest --token=$NEXPLOIT_TOKEN $OLD_SCAN_ID;
echo "Scan started $NEW_SCAN_ID";
```

##### **STEP 4 -  Poll the Results**

>[!NOTE|label:Note]
When polling the scan results, it is recommended to follow the fail-fast principle by using the `breakpoint` command.  See [NexPloit CLI Command List](guide/np-cli/command-list.md) for a full list of commands you can use in your Travis flow.

```bash
echo "Poll for scan results";

# Poll the scan until it returns some issue, or its time runs out
RESULT=$(nexploit-cli scan:polling --token=$NEXPLOIT_TOKEN --failure-on=first-issue --interval=10000 $NEW_SCAN_ID);

# After that - stop the scan
nexploit-cli scan:stop --token=$NEXPLOIT_TOKEN $NEW_SCAN_ID;

# Kill repeater process
kill -9 $PID_REPEATER

# Exit step with a code from nexploit-cli
exit $RESULT;
```

##### **STEP 6 -  View the  Results**
To view the reports on the detected issues, go to the [nexploit.app](https://nexploit.app).

<!-- tabs:end -->





