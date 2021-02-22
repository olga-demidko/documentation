# 🔛 Initializing a Repeater
```nexploit-cli repeater [options]``` initializes a local Repeater process. When a scan is connected to such a Repeater, all the scan requests are pulled from the cloud through the Repeater to the local target of the scan.

A Repeater enables you to run NexPloit scans on a local compiled application, without exposing your ports externally. This means that you can scan an application without having to deploy the application or to generate external reports.

For details about how the Repeater works, see [On-Prem Agent Repeater (Agent) Deployment](guide/introduction/deployment-options.md#on-premises-repeater-agent).

## Additional Features
* Enables multiple scans to run through a single Repeater.
* Option to add headers to requests locally (authentication cookie and so on), without exposing them to the cloud.

> [!WARNING|label:Important]
The Repeater requires a working `AUTH_TOKEN` with the scope repeaters:write.

## Options
| **Option** | **Description** |
|:--|:--|
| ```--id=repeaterId``` | The ID of an existing Repeater that you want to use. |
| ```--token my-jwt-authentication-token``` | The unique identifier used to authenticate a user. It can be issued in your organization’s dashboard. |
| ```--bus=eventBus``` | NexPloit Event Bus URL.<br/><br/>**Default Value**: `--bus amqps://amq.nexploit.app:5672` |
| ```--header=extraHeader```,</br> ```-H=extraHeader``` | Extra headers to be passed with each request. Also, it can be used to remove a header by providing a name without content. For example, -H "Host:".<br/><br/>**<font color="red">Warning:</font>** Headers set with this option override the original headers and are set in all requests. |
| ```--headers=json``` | JSON string that contains a header list, which is initially empty and consists of zero or more name and value pairs. <br/><br/>**<font color="red">Warning:</font>** Headers set with this option override the original headers and are set in all requests. |
| ```--proxy=proxyUrl``` | SOCKS4 or SOCKS5 URL to proxy all traffic. |
| ```--daemon```, ```-d``` | Initializes the Repeater as a local daemon service </br></br> **<font color="blue">Note:</font>** If you run this command while a service is already running, it will first stop & delete the running service, and restarts it with the new repeater settings.</br></br> **<font color="blue">Note:</font>** Currently supported operating systems include windows (wscm) & Linux (systemd). |
| ```--remove-daemon```, ```--remove```, ```--rm``` | Stops & deletes the running repeater service. |
| ```--scripts``` | Loads scripts to the Repeater from a JSON of `{ "host": "filepath" }`<br><br><b><font color="blue">Note:</font></b> Wildcards are also supported, for example: `--scripts '{"*": "./hmac.js"}'` for a global script for all target hosts, or `--scripts '{"*.domain.com": "./hmac.js"}'` for all target hosts on sub-domains.<br><br>The loaded scripts are shown as 'read-only' with just a name on the [nexploit.app](https://nexploit.app/).<br><br>See [Repeater Scripts](docs/guide/np-web-ui/advanced-set-up/using-repeaters-scripts/scripts-overview.md) for more information about how the Repeater Scripts work. |
