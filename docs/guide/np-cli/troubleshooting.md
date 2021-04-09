# 👾 Troubleshooting

The purpose of this section is to help you solve common problems that you may encounter while using NexPloit CLI

### 🌎 Section Map <!-- {docsify-ignore} -->

- [Repeater](#repeater)
  - [Connectivity test](#connectivity-test)
 

<hr style="height:2px;background-color:#d1d3d4">

### Repeater

More info about how the Repeater works and when to use one can be found here [On-Premises Repeater (Agent)](/guide/introduction/deployment-onprem.md).

### Connectivity Test

In order to use a Repeater from within a local network, you must first make sure it has a proper access to all the target applications.
You can use the `nexploit-cli configure --nogui` command to run a simple connectivity testing process.

##### Prerequisites
- The machine on which the Repeater will be run, must have the latest version of the [Nexploit CLI](/guide/np-cli/installation.md).
- A valid API key (`API token`) with the following scopes: `bot`, `scans:run`, `scans:read`, `scans:stop`.<br>
  You can create an [organization API key](https://kb.neuralegion.com/#/guide/np-web-ui/advanced-set-up/managing-org?id=managing-organization-apicli-authentication-tokens) or a [personal API key](https://kb.neuralegion.com/#/guide/np-web-ui/advanced-set-up/managing-personal-account?id=managing-your-personal-api-keys-authentication-tokens).
- A valid `REPEATER_ID`. To create a Repeater, see [Managing Repeaters](/guide/np-web-ui/advanced-set-up/managing-repeaters.md).

##### Step-by-Step Guide

1. Run the command `nexploit-cli configure --nogui` in your terminal.<br> 
  The Nexploit Network Testing wizard is launched.
  
2. Enter the `API Token` and `Repeater ID` in the relative fields.

  ![credentials](media/test-credentials.png ':size=40%')

3. The CLI runs the first stage of the external communication diagnostics:

    * **Validating that the connection to amq.nexploit.app:5672 at port 5672 is open** is required for the Repeater to reach the scan engine.
    * **Validating that the connection to nexploit.app at port  is open** is required to reach the Nexploit API endpoints.
    * **Verifying provided Token and Repeater ID** is required to validate the credentials.

  The diagnostics results are provided next to the validation parameters. 

  ![external](media/external-diagnostics.png ':size=40%')
  
  After the external communication diagnostics has passed, the CLI switches to the validation of the Repeater communication with local target application(s).

4. Enter the target URL(s) to test if the Repeater can reach them.

  ![internal](media/internal-testing.png ':size=40%')

  The internal communication diagnostics starts, and the Repeater tries to reach the specified applications. 

  ![reach-url](media/trying-to-reach.png ':size=40%')
5. Once the diagnostics is completed, you can see how many targets cannot be reached by the Repeater.<br>
  To exit the wizard, close the terminal.

