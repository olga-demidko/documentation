# 🔓Testing Network Connectivity

If you are using a Repeater to scan targets on your local network, you are able to preliminary check if the Repeater can reach all the target applications. Such diagnostics allows you to reveal and fix the connectivity problems before you run a scan. 

`nexploi-cli configure --nogui` initializes the network testing wizard. Simply follow the wizard instructions to diagnose the communication between the Repeater and your local targets.

To run the testing, you will need a valid Repeater ID and an API token with the `bot` scope. You can get them on [nexploit.app](https://nexploit.app):
* To create a Repeater, see [Managing Repeaters](/guide/np-web-ui/advanced-set-up/managing-repeaters.md).
* To create an API key, see [organization API key](https://kb.neuralegion.com/#/guide/np-web-ui/advanced-set-up/managing-org?id=managing-organization-apicli-authentication-tokens) or [personal API key](https://kb.neuralegion.com/#/guide/np-web-ui/advanced-set-up/managing-personal-account?id=managing-your-personal-api-keys-authentication-tokens).

To find the connectivity test step-by-step guide, go to the [Troubleshooting](/guide/np-cli/troubleshooting.md) section.