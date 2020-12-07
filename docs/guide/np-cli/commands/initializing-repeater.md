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
| **Option**                                       | **Description**                                                                                                                                                                                                                                                                             |
|--------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ```--id=repeaterId```                            | The ID of an existing Repeater that you want to use.                                                                                                                                                                                                                                        |
| ```--token my-jwt-authentication-token```        | The unique identifier used to authenticate a user. It can be issued in your organization’s dashboard.                                                                                                                                                                                       |
| ```--bus=eventBus```                             | NexPloit Event Bus URL.<br/><br/>**Default Value –** `--bus amqps://amq.nexploit.app:5672`                                                                                                                                                                                                  |
| ```--header=extraHeader```, ```-H=extraHeader``` | Extra headers to be passed with each request. Also, it can be used to remove a header by providing a name without content. For example, -H "Host:".<br/><br/>**<font color="red">WARNING –</font>** Headers set with this option override the original headers and are set in all requests. |
| ```--headers=json```                             | JSON string that contains a header list, which is initially empty and consists of zero or more name and value pairs. <br/><br/>**<font color="red">WARNING –</font>** Headers set with this option override the original headers and are set in all requests.                               |
| ```--proxy=proxyUrl```                           | SOCKS4 or SOCKS5 URL to proxy all traffic.                                                                                                                                                                                                                                                  |
