# ℹ Command Language Syntax
Nexploit CLI accepts a wide variety of configuration options. You can run ```nexploit-cli --help``` command for comprehensive documentation. The configuration options and arguments in the command line must be passed after the program command that Nexploit CLI is executing.

```bash
 nexploit-cli <command> [option] [<argument>]
```
* Most commands and some options have aliases. Aliases are shown in the syntax statement for each command.
* The option names are prefixed with a double dash (--). The option aliases are prefixed with a single dash (-). Arguments are not prefixed. 
* Support is provided for an array of options of a specific command, separated by a space. For example:

```bash
  nexploit-cli scan:run                      \
  --token api-key                            \
  --name scan-name                           \
  --crawler target-url                       \
  --param path query body                    \
  --test default_login_location dom_xss sqli \
```
The Nexploit CLI provides the following global options that can affect the behavior of each command:


<table id="simple-table">
<tr>
<th width="25%"><strong>Option</strong></th>
<th><strong>Description</strong></th>
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
<td><code>--cluster</code></td>
<td>Nexploit cluster (domain name).<br><br><strong>Default:</strong><code>nexploit.app</code></td>
</tr>
<tr>
<td><code>--insecure</code></td>
<td>Allows the Nexploit CLI to proceed and operate even if the server connection is considered insecure.</td>
</tr>
<tr>
<td><code>--proxy=socksProxyUrl</code></td>
<td>SOCKS URL to proxy all traffic.</code><br><br> <strong><font color="blue">Note:</font></strong> SOCKS4, SOCKS5, SOCKS4a, SOCKS5h are currently supported. By default, if you specify <code>SOCKS://&lt;URL&gt;</code> , then SOCKS5h is applied.</td>
</tr>
<tr>
<td><code>--version, -v</code></td>
<td>Shows the Nexploit CLI version.</code></td>
</tr>
<tr>
<td><code>--help, -h</code></td>
<td>Shows the Nexploit CLI help documentation.</code></td>
</tr>
</table>
