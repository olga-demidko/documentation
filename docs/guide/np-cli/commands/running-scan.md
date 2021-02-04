# 🏃 Running a Scan
```nexploit-cli scan:run [options]``` starts a new scan with the received configuration.
>[!NOTE|label:Note]
If you do not have enough available engines, the scan is placed in the queue. The new scan will start as soon as you manually stop another running scan or when the current scan has completed.

This command enables you to specify one or more discovery strategies. For example, using the `--crawler` option and/or the generated HAR files, separately or concurrently. This means that you can handle client-side dynamic content, javascript and so on.

## Options
| **Option** | **Description** |
|:--|:--|
| ```--token my-jwt-authentication-token``` | The unique identifier used to authenticate a user. It can be issued in your organization’s dashboard. |
| ```--name=extraHeader```,<br/>```-n=extraHeader``` | The name of the scan. |
| ```--archive=archiveID```,<br/>```-a=archiveID```  | The Archive ID, which can be received via the archive:upload command. |
| ```--crawler=url```,<br/>```-c=url``` | Specifies a list of specific URLs that should be included during crawler discovery. |
| ```--repeater=uuid``` | Specifies a list of Repeater UUIDs that should be connected with the scan. |
| ```--smart``` | Enables you to use automatic smart decisions, such as parameter skipping, detection phases and so on to minimize scan time. When turned off, all tests are run on all the parameters, which increases the coverage at the expense of scan time. |
| ```--param=path/query/fragment/header/body``` | Defines which part of the request to attack (see [here](guide/np-web-ui/scanning/creating-new-scan#target-params-locations) for more details).<br/><br/> **<font color="#0ba9b8">NOTE –</font>** This argument can be passed multiple times in the same command.<br/><br/>**Default Value –** `--parameter body query fragment`. |
| ```--module=dast/fuzzer``` | The DAST module tests for specific scenarios, such as OWASP top 10 and other common scenarios. The fuzzer module generates various new scenarios in order to test for unknown issues, providing automated AI-guided fuzz testing.<br/><br/>**Default Value –** `--module dast` |
| ```--host-filter=hostOrIp```,<br/>```-F=hostOrIp``` | The list of specific hosts to be included in the scan. |
| ```--header=extraHeader```,<br/>```-H=extraHeader``` | Extra headers to be passed with the archive file. It can also be used to remove a header by providing a name without content. For example, -H "Host:". <br/><br/>**<font color="red">WARNING –</font>** Headers set with this option override the archive headers and are set in all the requests. |
| ```--test=testName``` | Specifies a list of relevant tests to execute during a scan.<br/>For example, `--test default_login_location dom_xss`. |
| ```--api=ApiDomain``` | Set the API endpoint domain, for VPC, use: `--api https://private-domain.nexploit.app` <br/><br/>**Default Value:** `--api https://nexploit.app` |

