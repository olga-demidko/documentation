# 🧩 Integrating with a Service
`nexploit-cli integration [options]` connects NexPloit with ticketing and management services deployed on local servers (currently only the On-Premise Jira is supported). The repositories of the connected services can then be integrated with the NexPloit projects and used as endpoints for the scan reports.

For more information about the integration capabilities, see [Ticketing Systems](/guide/pipeline-integration/ticketing-systems/ticketing-overview.md).

## Script Example
```bash
nexploit-cli integration                  \
--access-key INTEGRATION_ACCESS_KEY       \
--base-url https://acme.atlassian.net     \
--user username                           \
--password pa$$word                       \
--token API_TOKEN                         \
```
## Options
|  **Option** | **Description** |
|:--|:--|
| ```--access-key``` | The unique identifier generated on the **JIRA INTEGRATION CONFIG** popup of the [nexploit.app](https://nexploit.app/).<br> Required to authorize NexPloit to the On-Premise Jira (local Jira Server). |
| ```--type``` | Integration service type (currently only JIRA is supported). |
| ```--proxy``` | SOCKS4 or SOCKS5 URL to proxy all traffic. |
| ```--base-url``` | The base URL to the Jira instance API. |
| ```--user``` | Use a username for a local Jira Server or email for the Atlassian Jira Cloud. |
| ```--password``` | Use a password for a local Jira Server or API token for the Atlassian Jira Cloud. |
| ```--token``` | NexPloit [organization API key](https://kb.neuralegion.com/#/guide/np-web-ui/advanced-set-up/managing-org?id=managing-organization-apicli-authentication-tokens) or [personal API key](https://kb.neuralegion.com/#/guide/np-web-ui/advanced-set-up/managing-personal-account?id=managing-your-personal-api-keys-authentication-tokens) with the `bot` scope.<br> The `bot`scope enables connection between NexPloit and the NexPloit CLI. |
| ```--daemon``` | Runs the integration in a daemon mode. |


