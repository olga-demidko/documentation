# Jenkins Integration

<a href="https://www.jenkins.io/" target="_blank">
  <img src="integrations/jenkins/media/jenkins-logo.png" alt="jenkins_logo"  width="35%")>
</a>

If you are using Jenkins for automation in your development, this section will show you how easy it is to add NexPloit scans to your pipeline.

## Adding NexPloit to a Jenkins Pipeline

There are many different methodologies for building a Jenkins pipeline, here are a few examples of different approaches:
- [Example: Using Only our REST API](#using-only-our-rest-api)
- [Example: Using NexPloit CLI](#using-nexploit-cli)
- [Example: Using NexPloit CLI with a Repeater](#using-nexploit-cli-with-a-repeater)

<hr style="height:2px;background-color:#d1d3d4">

### Using Only Our REST API
Using this approach, you do not need to install anything on your Jenkins machine. The communication with NexPloit is done solely via our REST API.

<table style="width:100%">
  <th>Pros</th> <th>Cons</th>
  <tr>
    <td style="width:50%" valign="top">
      <li> No need to install anything </li>
      <li> Raw APIs are the most customizable option </li>
    </td>
    <td style="width:50%" valign="top">
      <li> Need to write the <b>API calls</b> manually </li>
      <li> The target of the scan must be accessible from our static IP </li>
    </td>
  <tr>
</table>

> [!NOTE|label:Prerequisites]
> - The target of the scan is accessible from the internet
> - A valid `AUTH_TOKEN` with the scope: `scans:run`, `scans:read`, `scans:stop`
>   - You can set up an [Organization level Authentication Token](user-guide/organization-administration/details-and-policies.md#managing-organization-api-keys)
>   - Or, a [User level Authentication Token](user-guide/personal-account-administration/details-and-settings.md#managing-your-api-keys)

#### Step-by-step Guide
Every step should be a separate `Execute Shell` script, for example:

![Run Docker Example](/media/pipeline-example-step-1.png ':size=30%')

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

> [!TIP]
> - See [NexPloit CLI Command List](/nexploit-cli/commands.md) for a full list of commands you can add to your Jenkins flow
> - If the build processes is faster than the scan you can use the Jenkins [wait for stage](http://cpitman.github.io/jenkins/cicd/2017/03/16/waiting-for-remote-systems-in-a-jenkins-pipeline.html#.XyA6Dp4zbLY) option

<hr style="height:2px;background-color:#d1d3d4">

### Using NexPloit CLI
Using this approach, you will need to install [NexPloit CLI](/nexploit-cli/overview.md) on your Jenkins machine. Which will provide an-easy-to use interface to control the scans, as well as other built-in capabilities such as: mock HAR file creation, Repeater and more.

<table style="width:100%">
  <th>Pros</th>
  <th>Cons</th>
  <tr>
    <td style="width:50%" valign="top">
      <li> Better interface for commands, including pre-configured flows for CI/CD and usage automation </li>
      <li> Additional built-in capabilities such as: mock HAR generation, Repeater, etc. </li>
    </td>
    <td style="width:50%" valign="top">
      <li> Requires installation </li>
      <li> The target of the scan must be accessible from our static IP </li>
    </td>
  <tr>
</table>

#### Prerequisites

> [!NOTE|label:Prerequisites]
> - The target of the scan is accessible from the internet
> - Installed [NexPloit CLI package](/nexploit-cli/overview.md) on **your Jenkins machine**
> - A valid `AUTH_TOKEN` with the scope: `scans:run`, `scans:read`, `scans:stop`
>   - You can set up an [Organization level Authentication Token](user-guide/organization-administration/details-and-policies.md#managing-organization-api-keys)
>   - Or, a [User level Authentication Token](user-guide/personal-account-administration/details-and-settings.md#managing-your-api-keys)

#### Step-by-step Guide
Every step should be a separate `Execute Shell` script, for example:

![Run Docker Example](/media/pipeline-example-step-1.png ':size=30%')

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

And that's it! Your Jenkins flow with NexPloit is configured!

> [!TIP]
> - See [NexPloit CLI Command List](/nexploit-cli/commands.md) for a full list of commands you can add to your Jenkins flow
> - If the build processes is faster than the scan you can use the Jenkins [wait for stage](http://cpitman.github.io/jenkins/cicd/2017/03/16/waiting-for-remote-systems-in-a-jenkins-pipeline.html#.XyA6Dp4zbLY) option

<hr style="height:2px;background-color:#d1d3d4">

### Using NexPloit CLI with a Repeater

Using this approach, you will need to install [NexPloit CLI](/nexploit-cli/overview.md) on your Jenkins machine. Which will provide an-easy-to use interface to control the scans, as well as other built-in capabilities such as: mock HAR file creation, Repeater and more.

<table style="width:100%">
  <th>Pros</th>
  <th>Cons</th>
  <tr>
    <td style="width:50%" valign="top">
      <li> Better interface for commands, including pre-configured flows for CI/CD and usage automation </li>
      <li> Additional built-in capabilities such as: mock HAR generation, Repeater, etc. </li>
      <li> Can scan local targets </li>
    </td>
    <td style="width:50%" valign="top">
      <li> Requires installation </li>
    </td>
  <tr>
</table>

> [!NOTE|label:Prerequisites]
> - The target of the scan is accessible from the internet
> - A valid `AUTH_TOKEN` with the scope: `repeaters:write`, `scans:run`, `scans:read`, `scans:stop`
>   - You can set up an [Organization level Authentication Token](user-guide/organization-administration/details-and-policies.md#managing-organization-api-keys)
>   - Or, a [User level Authentication Token](user-guide/personal-account-administration/details-and-settings.md#managing-your-api-keys)
> - An active `REPEATER_ID`
>  - More info about [Setting up a New Repeater](user-guide/agents/overview.md)

#### Step-by-step Guide
Every step should be a separate `Execute Shell` script, for example:

![Run Docker Example](/media/pipeline-example-step-1.png ':size=30%')

Add the following `.sh` scripts to your Jenkins flow:

<!-- tabs:start -->

##### **STEP 1 - Start a Repeater**

```bash
# Run the repeater
PID_REPEATER=$(nexploit-cli repeater --token=$AUTH_TOKEN --repeater=$REPEATER_ID &> /dev/null & echo $!)
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

And that's it! Your Jenkins flow with NexPloit is configured!

> [!TIP]
> - See [NexPloit CLI Command List](/nexploit-cli/commands.md) for a full list of commands you can add to your Jenkins flow
> - If the build processes is faster than the scan you can use the Jenkins [wait for stage](http://cpitman.github.io/jenkins/cicd/2017/03/16/waiting-for-remote-systems-in-a-jenkins-pipeline.html#.XyA6Dp4zbLY) option
