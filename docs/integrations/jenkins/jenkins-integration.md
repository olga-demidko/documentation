# Jenkins Integration

<a href="https://www.jenkins.io/" target="_blank">
  <img src="integrations/jenkins/media/jenkins-logo.png" alt="jenkins_logo"  width="35%")>
</a>

If you are using Jenkins for automation in your development, this section will show you how easy it is to add NexPloit scans to your pipeline.

## Adding NexPloit to a Jenkins Pipeline

There are many different methodologies for building a Jenkins pipeline, here are a few examples of different approaches:
- [Using Only our REST API](#using-only-our-rest-api)
- [Using NexPloit CLI](#using-nexploit-cli)
- [Using NexPloit CLI with a Repeater](#using-nexploit-cli-with-a-repeater)

<hr style="height:2px;background-color:#d1d3d4">

### Using Only Our REST API
Using this approach, you do not need to install anything on your Jenkins machine. The communication with NexPloit is done solely via our REST API.

<table style="width:100%">
  <th>Pros</th> <th>Cons</th>
  <tr>
    <td style="width:50%" valign="top">
      <li> No need to install anything </li>
    </td>
    <td style="width:50%" valign="top">
      <li> Need to write the <b>curl</b> commands manually </li>
      <li> The target of the scan must be accessible from our static IP </li>
      <li> Less control over the build (for example scan time) </li>
      </p>
    </td>
  <tr>
</table>

#### Prerequisites

- A valid `API_KEY`
  - For the example below you will need the following scopes: `scans:run`, `scans:read` and `scans:stop`
  - More info about [setting up an API key](../user-guide/organization-administration/details-and-policies#managing-organization-api-keys)
- The target of the scan is accessible from the internet

#### Step-by-step Guide
Every step should be a separate `Execute Shell` script, for example:

![Run Docker Example](/media/pipeline-example-step-1.png ':size=30%')

Add the following `.sh` scripts to your Jenkins flow:

<!-- tabs:start -->

##### **STEP 1 - Run a Scan (Re-Test)**

```bash
# Retest a scan with ID `SCAN_ID` and API key `API_KEY`
SCAN_ID=$(curl -X POST https://nexploit.app/api/v1/scans/$SCAN_ID/retest -H "Authorization: Api-Key $API_KEY" | jq -r '.id')
```

##### **STEP 2 - Wait For Issues**

```bash
# Check if there are any found issues
until [ $(curl https://nexploit.app/api/v1/scans/$SCAN_ID -H "Authorization: Api-Key $API_KEY" | jq '.issuesBySeverity | length') -gt 0 ]
do
    sleep 10s;
done

echo "Found issues: "
curl https://nexploit.app/api/v1/scans/$SCAN_ID -H "Authorization: Api-Key $API_KEY" | jq '.issuesBySeverity'

echo "Detailed scan status at: https://nexploit.app/scans/$SCAN_ID"
```

##### **STEP 3 - Stop the Scan**

```bash
# Stop the scan
curl https://nexploit.app/api/v1/scans/$SCAN_ID/stop -H "Authorization: Api-Key $API_KEY"
```

<!-- tabs:end -->

And that's it! Your Jenkins flow with NexPloit is configured!

!> See [NexPloit CLI Command List](/nexploit-cli/commands.md) for a full list of commands you can add to your Jenkins flow.

!> In case the build processes is faster than the scan you can use the jenkins wait for stage option, on which you can read more [here](http://cpitman.github.io/jenkins/cicd/2017/03/16/waiting-for-remote-systems-in-a-jenkins-pipeline.html#.XyA6Dp4zbLY).

<hr style="height:2px;background-color:#d1d3d4">

### Using NexPloit CLI
Using this approach, you will need to install [NexPloit CLI](/nexploit-cli/overview.md) on your Jenkins machine. Which will provide an-easy-to use interface to control the scans, as well as other built-in capabilities such as: mock HAR file creation, Repeater and more.

<table style="width:100%">
  <th>Pros</th>
  <th>Cons</th>
  <tr>
    <td style="width:50%" valign="top">
      <li> Better control over scans (for example scan time) </li>
      <li> Better interface for commands </li>
      <li> Additional capabilities with the CLI (mock HAR generation, Repeater, etc.) </li>
    </td>
    <td style="width:50%" valign="top">
      <li> Requires installation </li>
      <li> The target of the scan must be accessible from our static IP </li>
      </p>
    </td>
  <tr>
</table>

#### Prerequisites

- Installed [NexPloit CLI package](/nexploit-cli/overview.md) on **your Jenkins machine**
- A valid `API_KEY`
  - For the example below you will need the following scopes: `scans:run`, `scans:read` and `scans:stop`
  - More info about [setting up an API key](../user-guide/organization-administration/details-and-policies#managing-organization-api-keys)
- The target of the scan is accessible from the internet

#### Step-by-step Guide
Every step should be a separate `Execute Shell` script, for example:

![Run Docker Example](/media/pipeline-example-step-1.png ':size=30%')

Add the following `.sh` scripts to your Jenkins flow:

<!-- tabs:start -->

##### **STEP 1 - Run a Scan (Re-Test)**

```bash
echo "Retest a scan"

# Retest a scan with ID `OLD_SCAN_ID` and API key `API_KEY`
NEW_SCAN_ID=$(nexploit-cli scan:retest --api-key=$API_KEY $OLD_SCAN_ID;
echo "Scan started $NEW_SCAN_ID";
```

##### **STEP 2 - Poll Results**

```bash
echo "Poll for scan results";

# Poll the scan until it returns something, or its time runs out
RESULT=$(nexploit-cli scan:polling --api-key=$API_KEY --failure-on=first-issue --interval=10000 $NEW_SCAN_ID);

# After that - stop the scan
nexploit-cli scan:stop --api-key=$API_KEY $NEW_SCAN_ID;

# Exit step with a code from nexploit-cli
exit $RESULT;
```

<!-- tabs:end -->

And that's it! Your Jenkins flow with NexPloit is configured!

!> See [NexPloit CLI Command List](/nexploit-cli/commands.md) for a full list of commands you can add to your Jenkins flow.

!> In case the build processes is faster than the scan you can use the jenkins wait for stage option, on which you can read more [here](http://cpitman.github.io/jenkins/cicd/2017/03/16/waiting-for-remote-systems-in-a-jenkins-pipeline.html#.XyA6Dp4zbLY).

<hr style="height:2px;background-color:#d1d3d4">

### Using NexPloit CLI with a Repeater

Using this approach, you will need to install [NexPloit CLI](/nexploit-cli/overview.md) on your Jenkins machine. Which will provide an-easy-to use interface to control the scans, as well as other built-in capabilities such as: mock HAR file creation, Repeater and more.

<table style="width:100%">
  <th>Pros</th>
  <th>Cons</th>
  <tr>
    <td style="width:50%" valign="top">
      <li> Better control over scans (for example scan time) </li>
      <li> Better interface for commands </li>
      <li> Additional capabilities with the CLI (mock HAR generation, Repeater, etc.) </li>
      <li> Can scan local targets </li>
    </td>
    <td style="width:50%" valign="top">
      <li> Requires installation </li>
      </p>
    </td>
  <tr>
</table>

#### Prerequisites

- Installed [NexPloit CLI package](/nexploit-cli/overview.md) on **your Jenkins machine**
- A valid `API_KEY`
  - For the example below you will need the following scopes: `agents:write:repeater`, `scans:run`, `scans:read` and `scans:stop`
  - More info about [setting up an API key](../user-guide/organization-administration/details-and-policies#managing-organization-api-keys)
- An active `REPEATER_ID`
  - More info about [Setting up a New Repeater](user-guide/agents/overview.md)

#### Step-by-step Guide
Every step should be a separate `Execute Shell` script, for example:

![Run Docker Example](/media/pipeline-example-step-1.png ':size=30%')

Add the following `.sh` scripts to your Jenkins flow:

<!-- tabs:start -->

##### **STEP 1 - Start a Repeater**

```bash
# Run the repeater
PID_REPEATER=$(nexploit-cli repeater --token=plhzeup.nexp.0lhtc7ib5pogcibaqprz6gz994sltelu --agent=b5b03145-1f30-4002-bab1-8f1b58df4bf9 &> /dev/null & echo $!)
echo "Repeater PID: $PID_REPEATER"
```

##### **STEP 2 - Run a Scan (Re-Test)**

```bash
echo "Retest a scan"

# Retest a scan with ID `OLD_SCAN_ID` and API key `API_KEY`
NEW_SCAN_ID=$(nexploit-cli scan:retest --api-key=$API_KEY $OLD_SCAN_ID;
echo "Scan started $NEW_SCAN_ID";
```

##### **STEP 3 - Poll Results**

```bash
echo "Poll for scan results";

# Poll the scan until it returns something, or its time runs out
RESULT=$(nexploit-cli scan:polling --api-key=$API_KEY --failure-on=first-issue --interval=10000 $NEW_SCAN_ID);

# After that - stop the scan
nexploit-cli scan:stop --api-key=$API_KEY $NEW_SCAN_ID;

# Kill repeater process
kill -9 $PID_REPEATER

# Exit step with a code from nexploit-cli
exit $RESULT;
```
<!-- tabs:end -->

And that's it! Your Jenkins flow with NexPloit is configured!

!> See [NexPloit CLI Command List](/nexploit-cli/commands.md) for a full list of commands you can add to your Jenkins flow.

!> In case the build processes is faster than the scan you can use the jenkins wait for stage option, on which you can read more [here](http://cpitman.github.io/jenkins/cicd/2017/03/16/waiting-for-remote-systems-in-a-jenkins-pipeline.html#.XyA6Dp4zbLY).
