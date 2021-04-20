<table id="integrations" >
  <tr>
    <td width="70%">
      <h1>JFrog</h1>
    </td>
    <td width="30%" style="text-align:center" rowspan="3">
      <img src="guide/pipeline-integration/pipe-management/media/jfrog/jfrog-logo.png" width="200" height="250"></img>
    </td>
  </tr>
  <tr>
    <td style="text-align:left;vertical-align:text-top;padding:0px">
    If you are using JFrog  Pipelines for development automation, you can integrate it with NexPloit to run security scans on every new build as part of your SDLC.
    <p>For this example, we use a sample vulnerable application in a public <a href="https://github.com/neuralegion/jfrog-example">GitHub repository</a>. The repository also contains the corresponding JFrog Pipeline YAML file. You can use this application for a test project.
    </td>
  </tr>
  <tr>
  <td width="65%">
    <h3>Prerequisites</h3>
    </td>
    </tr>
</table>

* You are an active user on  [nexploit.app](https://nexploit.app). 
*  You have a valid [organization API key](https://kb.neuralegion.com/#/guide/np-web-ui/advanced-set-up/managing-org?id=managing-organization-apicli-authentication-tokens) or [personal API key](https://kb.neuralegion.com/#/guide/np-web-ui/advanced-set-up/managing-personal-account?id=managing-your-personal-api-keys-authentication-tokens) (`NEXPLOIT_TOKEN`) with the following scopes: `bot`,<br>`scans : run`,`scan : read`, and `scans : stop`.

### YAML File Breakdown
<!-- tabs:start -->

##### **Resources and pipelines configuration**
The YAML file contains configuration for security scanning and the pipeline itself (called nexploit), with details of the repository and execution steps.

```bash
resources:
  - name: jfrognexploit
    type: GitRepo
    configuration:
      gitProvider: GH
      path: NeuraLegion/jfrog-example

pipelines:
  - name: nexploit
    steps:
      - name: nexploit
        type: Bash
        configuration:
          integrations:
            - name: Nexploit
          inputResources:
            - name: jfrognexploit
```
A Git repository is given as a JFrog resource, so you can use this repository for any events, such as pushing a new commit or as a trigger to run a security scan.

##### **Execution steps**
The execution steps are the following:
1. Setting up the environment (NodeJS).
2. Installing the [NexPloit CLI](https://kb.neuralegion.com/#/guide/np-cli/overview) utility. Using the Nexploit CLI commands, you can run, poll status and stop scans directly from your pipeline.

```bash
execution:
          onExecute:
            - sudo apt update
            - sudo chmod 1777 /tmp
            - sudo apt update
            - sudo apt install nodejs npm
            - sudo apt install --fix-broken
            - sudo npm install -g @neuralegion/nexploit-cli --unsafe-perm=true
            - |
```

##### **Scan setup**

The scan setup includes the following details:
1. A crawler will be used on the target to define the attack surface and optimize the security tests.
2. NEXPLOIT_TOKEN  (API key) required to use the NexPloit CLI.
3. Interval of pollins the scan results (detected issues).
4. The length of the scan (timeout).
5. When polling the scan results, it is recommended to follow the fail-fast principle by using the `breakpoint` command. The scan stops automatically once a high severity issue is detected.  See [NexPloit CLI Command](https://kb.neuralegion.com/#/guide/np-cli/command-list) List for a full list of commands you can use for a scan.

```bash
 SCAN_ID=$(nexploit-cli scan:run                                                \
                  --name "💎 Broken Crystals for a #${res_jfrognexploit_commitSha} #${run_id}" \
                  --crawler https://brokencrystals.com                                         \
                  --token $int_Nexploit_NEXPLOIT_TOKEN)
            - printf "Scan was started with ID https://nexploit.app/scans/$SCAN_ID"
            - |
              nexploit-cli scan:polling               \
                --interval 30s                        \
                --timeout 12m                         \
                --token $int_Nexploit_NEXPLOIT_TOKEN  \
                --breakpoint high_issue $SCAN_ID
          onComplete:
            - nexploit-cli scan:stop --token $int_Nexploit_NEXPLOIT_TOKEN $SCAN_ID
```

<!-- tabs:end -->

### Step-by-Step Guide
#### Step 1 : Set up an Automatic Scan in JGrog 
On the **Node Pools** page, click **Add Node Pool** and configure.

![add-node-pool](./media/jfrog/add-node-pool.png ':size=45%')

#### Step 2: Integrate GitHub with JFrog

1. Get a GitHub token.  In GitHub, select **Settings** > **Developer Settings** > **Personal Access Tokens** > **Generate New Token**.
2. Copy the generated token.
3. In JFrog, select **Integrations** > **Add an integration**.

    ![add-integration](./media/jfrog/add-integration.png ':size=50%')

4. Give the integration a name, select the type and paste the token.

    ![add-new-integration](./media/jfrog/add-new-integration.png ':size=35%')

#### Step 3: Integrate NexPloit with JFrog 

1. Generate an API key (`NEXPLOIT_TOKEN`) on [nexploit.app](https://nexploit.app). Go to **User Settings** > **Create New API Key** > **Select All** > create and copy the token. 
2. In JFrog, select **Integrations** > **Add an integration**.
3. Give the integration a name, select the type and paste the token.

    ![integrate-with-nexploit](./media/jfrog/integrate-with-nexploit.png ':size=45%')

#### Step 4: Add YAML Pipeline Source  

1. In JFrog, select **Pipeline Sources** > **Add Pipeline Source** > **From YAML**.
2. Select your GitHub integration for SCM provider integration, enter the repository name with JFrog configuration and the branch.
3. Select **Create Source**.

    ![add-source](./media/jfrog/add-source.png ':size=35%')

You are now ready to build and run a new scan!

#### Step 5: Run a new scan

In JFrog, select **Pipelines** > **nexploit** > **nexploit** > **Trigger this step**.

![trigger-this-step](./media/jfrog/trigger-this-step.png ':size=45%')

You will then get a view of your current CI process.

![polling-results](./media/jfrog/polling-results.png ':size=40%')

In the image above, you can see the security scan has started and the results are being polled.

You can now view the security scan status and results in the dashboard on [nexploit.app](https://nexploit.app).

On detection of a high severity issue, the build is failed and the scan is stopped automatically.

![breakpoint](./media/jfrog/breakpoint.png ':size=45%')

The scanner is set to automatically scan every time there is a change committed in the repository, enabling developers to run an automated, comprehensive and accurate security scan on every commit.

![automatic-scan](./media/jfrog/automatic-scan.png ':size=45%')






