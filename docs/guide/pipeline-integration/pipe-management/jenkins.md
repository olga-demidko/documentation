<table id="integrations" >
  <tr>
    <td width="70%">
      <h1>Jenkins</h1>
    </td>
    <td width="30%" style="text-align:center" rowspan="3">
      <img src="guide/pipeline-integration/pipe-management/media/jenkins/jenkins-new-logo.png" width="200" height="250"></img>
    </td>
  </tr>
  <tr>
    <td style="text-align:left;vertical-align:text-top;padding:0px">
    If you are using Jenkins for automation in your development, this section will show you how easy it is to add NexPloit scans to your pipeline.
    </td>
  </tr>
  <tr>
  <td>
  <h2>Adding NexPloit to a Jenkins Pipeline</h2>
  </td>
  </tr>
  <tr>
  <td>
  There are many different approaches for building a Jenkins pipeline such as –
  </td>
  </td>
  </tr>
</table>

- [Using Only the NexPloit REST API](#using-only-the-nexploit-rest-api)
- [Using the NexPloit CLI](#using-the-nexploit-cli)
- [Using the NexPloit CLI with a Repeater](#using-the-nexploit-cli-with-a-repeater)

### Using Only the NexPloit REST API
Using this approach, there is no need to install anything on your Jenkins machine. Communication with NexPloit is done solely through the NexPloit REST API.

| **Pros**                                   | **Cons**                                                      |
|--------------------------------------------|---------------------------------------------------------------|
| There is nothing to install.               | API calls must be written manually.                           |
| Raw APIs are the most customizable option. | The target of the scan must be accessible from our static IP. |

#### Prerequisites
* The target of the scan is accessible from the Internet.
* A valid `AUTH_TOKEN` with the scope `scans:run`, `scans:read` and `scans:stop`. You can set up –
  * An [organization-level authentication token](guide/np-web-ui/advanced-set-up/managing-org#Managing-Organization-APICLI-Authentication-Tokens).\
  – OR – 
  * A [user-level authentication token](guide/np-web-ui/advanced-set-up/managing-personal-account#Managing-Your-Personal-API-Keys-Authentication-Tokens).


#### Step-by-step Guide
Every step must be a separate `Execute Shell` script. For example, as shown below –

![Run-Docker-Example](/media/jenkins/pipeline-example-step-1.png ':size=30%')

Add the following `.sh` scripts to your Jenkins flow:

<!-- tabs:start -->

##### **STEP 1 - Run a Scan (Re-Test)**

```bash
# Retest a scan with ID `SCAN_ID` and API key `AUTH_TOKEN`
SCAN_ID=$(curl -X POST https://nexploit.app/api/v1/scans/$SCAN_ID/retest -H "Authorization: Api-Key $AUTH_TOKEN" | jq -r '.id')
```

##### **STEP 2 - Wait For Issues**

```bash
# Check if there are any found issues
until [ $(curl https://nexploit.app/api/v1/scans/$SCAN_ID -H "Authorization: Api-Key $AUTH_TOKEN" | jq '.issuesBySeverity | length') -gt 0 ]
do
    sleep 10s;
done

echo "Found issues: "
curl https://nexploit.app/api/v1/scans/$SCAN_ID -H "Authorization: Api-Key $AUTH_TOKEN" | jq '.issuesBySeverity'

echo "Detailed scan status at: https://nexploit.app/scans/$SCAN_ID"
```

##### **STEP 3 - Stop the Scan**

```bash
# Stop the scan
curl https://nexploit.app/api/v1/scans/$SCAN_ID/stop -H "Authorization: Api-Key $AUTH_TOKEN"
```

<!-- tabs:end -->

And that's it! Your Jenkins flow with NexPloit is configured!

> [!TIP|label:Pro Tips]
> - See [NexPloit CLI Command List](/nexploit-cli/commands.md) for a full list of commands you can add to your Jenkins flow.\
> - If the build processes is faster than the scan you can use the Jenkins [wait for stage](http://cpitman.github.io/jenkins/cicd/2017/03/16/waiting-for-remote-systems-in-a-jenkins-pipeline.html#.XyA6Dp4zbLY) option.

### Using NexPloit CLI
Using this approach, you will need to install [NexPloit CLI](/nexploit-cli/overview.md) on your Jenkins machine. Which will provide an-easy-to use interface to control the scans, as well as other built-in capabilities such as: mock HAR file creation, Repeater and more.

| **Pros**                                                                                      | **Cons**                                                      |
|-----------------------------------------------------------------------------------------------|---------------------------------------------------------------|
| Better interface for commands, including pre-configured flows for CI/CD and usage automation. | Requires installation.                                        |
| Additional built-in capabilities, such as mock HAR generation, Repeaters and so on.           | The target of the scan must be accessible from our static IP. |

#### Prerequisites
* The target of the scan is accessible from the Internet.
* The NexPloit CLI package is installed on your Jenkins machine.
* A valid `AUTH_TOKEN` with the scope `scans:run`, `scans:read` and `scans:stop`. You can set up –
  * An [organization-level authentication token](guide/np-web-ui/advanced-set-up/managing-org#Managing-Organization-APICLI-Authentication-Tokens).\
  – OR – 
  * A [user-level authentication token](guide/np-web-ui/advanced-set-up/managing-personal-account#Managing-Your-Personal-API-Keys-Authentication-Tokens).

#### Step-by-step Guide
Every step must be a separate `Execute Shell` script. For example, as shown below –

![Run-Docker-Example](/media/jenkins/pipeline-example-step-1.png ':size=30%')

Add the following `.sh` scripts to your Jenkins flow:

<!-- tabs:start -->

##### **STEP 1 - Run a Scan (Re-Test)**

```bash
echo "Retest a scan"

# Retest a scan with ID `OLD_SCAN_ID` and API key `AUTH_TOKEN`
NEW_SCAN_ID=$(nexploit-cli scan:retest --token=$AUTH_TOKEN $OLD_SCAN_ID;
echo "Scan started $NEW_SCAN_ID";
```

##### **STEP 2 - Poll Results**

```bash
echo "Poll for scan results";

# Poll the scan until it returns something, or its time runs out
RESULT=$(nexploit-cli scan:polling --token=$AUTH_TOKEN --failure-on=first-issue --interval=10000 $NEW_SCAN_ID);

# After that - stop the scan
nexploit-cli scan:stop --token=$AUTH_TOKEN $NEW_SCAN_ID;

# Exit step with a code from nexploit-cli
exit $RESULT;
```

<!-- tabs:end -->

Your Jenkins flow with NexPloit is configured!

> [!TIP|label:Pro Tips]
> - See [NexPloit CLI Command List](guide/np-cli/command-list.md) for a full list of commands you can add to your Jenkins flow.
> - If the build processes is faster than the scan, you can use the Jenkins [wait for stage](http://cpitman.github.io/jenkins/cicd/2017/03/16/waiting-for-remote-systems-in-a-jenkins-pipeline.html#.XyA6Dp4zbLY) option.

### Using NexPloit CLI with a Repeater

When using this approach, you must [install the NexPloit CLI](guide/np-cli/installation.md) on your Jenkins machine. The CLI provides a simple interface for controlling the scans, as well as other built-in capabilities, such as mock HAR file creation, Repeaters and more.

| **Pros**                                                                                     | **Cons**               |
|----------------------------------------------------------------------------------------------|------------------------|
| Better interface for commands, including preconfigured flows for CI/CD and usage automation. | Requires installation. |
| Additional built-in capabilities, such as mock HAR generation, Repeaters and so on.          |                        |
| Able to scan local targets.                                                                  |                        |

#### Prerequisites
* The target of the scan is accessible from the Internet.
* A valid `AUTH_TOKEN` with the scope `scans:run`, `scans:read` and `scans:stop`. You can set up –
  * An [organization-level authentication token](guide/np-web-ui/advanced-set-up/managing-org#Managing-Organization-APICLI-Authentication-Tokens).\
  – OR – 
  * A [user-level authentication token](guide/np-web-ui/advanced-set-up/managing-personal-account#Managing-Your-Personal-API-Keys-Authentication-Tokens).

#### Step-by-step Guide
Every step should be a separate `Execute Shell` script. For example, as shown below –

![Run Docker Example](/media/jenkins/pipeline-example-step-1.png ':size=30%')

Add the following `.sh` scripts to your Jenkins flow:

<!-- tabs:start -->

##### **STEP 1 - Start a Repeater**

```bash
# Run the repeater
PID_REPEATER=$(nexploit-cli repeater --token=$AUTH_TOKEN --agent=$REPEATER_ID &> /dev/null & echo $!)
echo "Repeater PID: $PID_REPEATER"
```

##### **STEP 2 - Run a Scan (Re-Test)**

```bash
echo "Retest a scan"

# Retest a scan with ID `OLD_SCAN_ID` and API key `AUTH_TOKEN`
NEW_SCAN_ID=$(nexploit-cli scan:retest --token=$AUTH_TOKEN $OLD_SCAN_ID;
echo "Scan started $NEW_SCAN_ID";
```

##### **STEP 3 - Poll Results**

```bash
echo "Poll for scan results";

# Poll the scan until it returns something, or its time runs out
RESULT=$(nexploit-cli scan:polling --token=$AUTH_TOKEN --failure-on=first-issue --interval=10000 $NEW_SCAN_ID);

# After that - stop the scan
nexploit-cli scan:stop --token=$AUTH_TOKEN $NEW_SCAN_ID;

# Kill repeater process
kill -9 $PID_REPEATER

# Exit step with a code from nexploit-cli
exit $RESULT;
```
<!-- tabs:end -->

Your Jenkins flow with NexPloit is configured!

> [!TIP|label:Pro Tips]
> - See [NexPloit CLI Command List](guide/np-cli/command-list.md) for a full list of commands you can add to your Jenkins flow.
> - If the build processes is faster than the scan, you can use the Jenkins [wait for stage](http://cpitman.github.io/jenkins/cicd/2017/03/16/waiting-for-remote-systems-in-a-jenkins-pipeline.html#.XyA6Dp4zbLY) option.