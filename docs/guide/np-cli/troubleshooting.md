# 👾 Troubleshooting

The purpose of this section is to help you solve common problems that you may encounter while using NexPloit CLI

### 🌎 Section Map <!-- {docsify-ignore} -->

- [Repeater](#repeater)
  - [Connectivity test](#connectivity-test)
 

<hr style="height:2px;background-color:#d1d3d4">

### Repeater

More info about how the Repeater works and when to use one can be found here [On-Premises Repeater (Agent)](/guide/introduction/deployment-onprem.md).

### Connectivity test

In order to user a Repeater from within a closed network, you must first make sure it has the proper access between all the components of the scan.
You can use the `nexploit-cli configure` command to run a simple connectivity testing process.

##### Prerequisites
- The machine on which the Repeater will run, must have the latest version of [NexPloit CLI installed](/guide/np-cli/installation.md).
- A valid `AUTH_TOKEN` with the following scopes: `bot`, `scans:run`, `scans:read`, `scans:stop`.
- You can set up an [organization Authentication Token](https://kb.neuralegion.com/#/guide/np-web-ui/advanced-set-up/managing-org?id=managing-organization-apicli-authentication-tokens) or a [personal Authentication Token](https://kb.neuralegion.com/#/guide/np-web-ui/advanced-set-up/managing-personal-account?id=managing-your-personal-api-keys-authentication-tokens).
- An active `REPEATER_ID`. More info about [Managing Repeaters](/guide/np-web-ui/advanced-set-up/managing-repeaters.md).

##### Step-by-Step Guide

1. Run the command `nexploit-cli configure` in your terminal, you should get the following output:

  ```bash
  Please browse to http://localhost:3000 to begin the configurations of the Repeater
  ```
  > [!NOTE|label:Note]
  If `http://localhost:3000` is already in use, a different port will be selected automatically.

  ![nexploit-cli-configure](media/nexploit-cli-configure.png ':size=40%')

2. Go to `http://localhost:3000` (or any other port that was used by the configure command), the configuration page will open in your local browser.

3. Fill out the `Auth Token` and `Repeater ID` details and click on **Next**.

  ![nexploit-cli-configure2](media/nexploit-cli-configure2.png ':size=40%')

4. The CLI will run the first stage of diagnostics:

  - **Connection to amq.nexploit.app at port 5672** is required for the Repeater to reach the scan engine
  - **Connection to nexploit.app at port 443** is required to reach our API endpoints
  - **Token and Repeater ID** are validated to be active

  If any of the validations fail, instructions on how to solve the problem will appear in the progress section below

  ![nexploit-cli-configure3](media/nexploit-cli-configure3.png ':size=40%')

5. After all the validations have passed, click on **Next**

  ![nexploit-cli-configure4](media/nexploit-cli-configure4.png ':size=40%')

6. Fill out the `Target URL` info and click on **Start Scan**, this step will validate the current machine has access to the target application.

    > [!NOTE|label:Note]
    This will create a new scan, but it will not perform any active attack scenarios, the only test that will run is a passive security header check on the target application

7. After the connection to the target application was validated successfully, click on **Next**

  ![nexploit-cli-configure5](media/nexploit-cli-configure5.png ':size=40%')

8. That's it, you have completed all the connectivity validations, you can see the demo scan in the UI by clicking on the link https://nexploit.app/scans

  ![nexploit-cli-configure6](media/nexploit-cli-configure6.png ':size=40%')
