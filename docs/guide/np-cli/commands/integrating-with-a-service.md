# 🧩 Integrating with a Service
`nexploit-cli integration [options]` connects Nexploit with ticketing and management services deployed on local servers (currently only the On-Premise Jira is supported). The repositories of the connected services can then be integrated with the Nexploit projects and used as endpoints for the scan reports.

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

<table id="simple-table">
<tr>
<th><strong>Option</strong></th>
<th><strong>Description</strong></th>
</tr>
<tr>
<td><code>--cluster</code></td>
<td>Nexploit cluster (domain name).<br><br><strong>Default:</strong><code>nexploit.app</code></td>
</tr>
<tr>
<td><code>--access-key=integrationKey</code></td>
<td>The unique identifier generated on the <strong>JIRA INTEGRATION CONFIG</strong> popup of the <a href="https://nexploit.app/" target="_blank" rel="noopener">nexploit.app</a>.<br> Required to authorize Nexploit to the On-Premise Jira (local Jira Server).</td>
</tr>
<tr>
<td><code>--type=jira</code></td>
<td>Integration service type (currently only JIRA is supported).</td>
</tr>
<tr>
<td><code>--base-url=serviceUrl</code></td>
<td>The base URL to the Jira instance API.</td>
</tr>
<tr>
<td><code>--user=serviceUserName</code></td>
<td>Use a username for a local Jira Server or email for the Atlassian Jira Cloud.</td>
</tr>
<tr>
<td><code>--password=serviceUserPassword</code></td>
<td>Use a password for a local Jira Server or API token for the Atlassian Jira Cloud.</td>
</tr>
<tr>
<td><code>--token=apiKey</code>,<br><code>-t=apiKey</code></td>
<td>Nexploit <a href="https://kb.neuralegion.com/#/guide/np-web-ui/advanced-set-up/managing-org?id=managing-organization-apicli-authentication-tokens" target="_blank" rel="noopener">organization API key</a> or <a href="https://kb.neuralegion.com/#/guide/np-web-ui/advanced-set-up/managing-personal-account?id=managing-your-personal-api-keys-authentication-tokens" target="_blank" rel="noopener">personal API key</a> with the <code>bot</code> scope.<br> The <code>bot</code>scope enables connection between Nexploit and the Nexploit CLI.</td>
</tr>
<tr>
<td><code>--daemon</code>,<br> <code>-d</code></td>
<td>Runs the integration in a daemon mode.</td>
</tr>
<tr>
<td><code>--config=pathToConfig</code></td>
<td>Specifies the path to the configuration file. By default, the CLI tries to discover the config in <code>package.json</code> in the root directory of your application or a separate file by a specified name in the working directory. For details, see <a href="/#/guide/np-cli/configuration-files.md">Configuration Files</a> for more information.</td>
</tr>
<tr>
<td><code>--log-level<br>=0/1/2/3/4/silent/<br>error/warn/notice/verbose</code></td>
<td>Allows setting the level of logs to report. Any logs of a higher level than the one specified are shown. The options to select : 0, 1, 2, 3, 4, "silent", "error", "warn", "notice", "verbose".<br><br><strong>Default:</strong> 3</td>
</tr>
<tr>
<td><code>--insecure</code></td>
<td>Allows the Nexploit CLI to proceed and operate even if the server connection is considered insecure.</td>
</tr>
<tr>
<td><code>--proxy=socksProxyUrl</code></td>
<td>SOCKS URL to proxy all traffic.</code><br><br> <strong><font color="#1B49D4">Note:</font></strong> SOCKS4, SOCKS5, SOCKS4a, SOCKS5h are currently supported. By default, if you specify <code>SOCKS://&lt;URL&gt;</code> , then SOCKS5h is applied.</td>
</tr>
<tr>
<td><code>--bus=eventBusUrl</code></td>
<td><b><i>(Deprecated)</i></b>. Nexploit event bus URL.<br><br><strong>Default:</strong><code>--bus amqps://amq.nexploit.app:5672</code></td>
</tr>
</table>
