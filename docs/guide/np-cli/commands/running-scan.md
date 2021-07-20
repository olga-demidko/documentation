# 🏃 Running a Scan
```nexploit-cli scan:run [options]``` starts a new scan with the received configuration.
>[!NOTE|label:Note]
If the maximum number of scans that can be run simultaneously is exceeded, the scan is placed in the queue. The concurrent scans limitation can be set either for the entire organization or for this particular project in the project settings. The new scan will start as soon as you manually stop another running scan or when the current scan is completed.

This command enables you to specify one or more discovery strategies. For example, using the `--crawler` option and/or the generated HAR files, separately or concurrently. This means that you can handle client-side dynamic content, javascript and so on.

## Options

<table id="simple-table">
<tr>
<th width=34%><strong>Option</strong></th>
<th><strong>Description</strong></th>
</tr>
<tr>
<td><code>--token=apiKey</code>,<br><code>-t=apiKey</code></td>
<td>The unique identifier used to authenticate a user. The token (API key) can be issued in your organization’s dashboard.</td>
</tr>
<tr>
<td><code>--name=scanName</code>, <br><code>-n=scanName</code></td>
<td>The name of the scan.</td>
</tr>
<tr>
<td><code>--archive=fileId</code>,<br> <code>-a=fileId</code></td>
<td>The Archive ID, which can be received via the&nbsp;archive:upload&nbsp;command.</td>
</tr>
<tr>
<td><code>--crawler=url</code>, <br><code>-c=url</code></td>
<td >Specifies a list of specific URLs that should be included during crawler discovery.</td>
</tr>
<tr>
<td><code>--repeater=repeaterId</code>, <br><code>--agent=repeaterId <b><i>(Deprecated)</i></b> </code>
</td>
<td> Specifies a list of Repeater UUIDs that should be connected with the scan.</td>
</tr>
<tr>
<td><code>--cluster</code></td>
<td>Nexploit cluster (domain name).<br><br><strong>Default:</strong><code>nexploit.app</code></td>
</tr>
<tr>
<tr>
<td><code>--project, -p</code></td>
<td>Allows specifying the Nexploit project for a scan using the project ID. You can find the project ID  in the <b>Projects</b> section on <a href="https://nexploit.app/scans">nexploit.app</a>.
</tr>
<tr>
<td><code>--integration, -i</code></td>
<td>Allows connecting a ticketing service with an associated repository for a scan. It enables you to get the reports on every detected vulnerability in automatically opened tickets/issues of the associated repository. <p>
<strong> <font color="blue">Note:</font></strong> You can only connect a ticketing service (system) that was previously integrated with Nexploit on <a href="https://nexploit.app/scans">nexploit.app</a>. Read more about integrating Nexpoloit with ticketing systems <a href="https://kb.neuralegion.com/#/guide/pipeline-integration/ticketing-systems/ticketing-overview">here</a>. <p> <i> Format:</i> <code> -i "service:repository"</code> <br> <i>Example:</i> <code> -i "github:example-app"</code> <br> If you want to connect several repositories for one scan, you can specify them one after another:<code> -i "github:example-app" -i "jira:example-app"</code><p> <strong> <font color="orange">Important:</font> </strong>    <ul>
    <li> To connect a ticketing service and a repository for a scan, the token (API key) that you use for the scan must include the <code>integration.repos:read</code> scope.</li> 
    <li>You cannot use the <code>--integration</code> option without specifying the <br> <code>--project</code> (see above). Make sure that you connect a repository associated with the specified project.</li>
</ul>
</tr>
<tr>
<td><code>--smart</code></td>
<td>Enables you to use automatic smart decisions, such as parameter skipping, detection phases and so on to minimize scan time. When turned off, all tests are run on all the parameters, which increases the coverage at the expense of scan time.</td>
</tr>
<tr>
<td><code>--param=path/query/fragment/<br>header/body/artifical-fragment/artifical-query</code></td>
<td>Defines which part of the request to attack (see <a href="#/guide/np-web-ui/scanning/creating-new-scan?id=target-params-locations">here</a> for more details).<br><br> <strong><font color="#0ba9b8">Note:</font></strong> This argument can be passed multiple times in the same command.<br><br><strong>Default:</strong>&nbsp;<code>--parameter body query fragment</code>.</td>
</tr>
<tr>
<td><code>--module=dast/fuzzer</code></td>
<td>The DAST module tests for specific scenarios, such as OWASP top 10 and other common scenarios. The fuzzer module generates various new scenarios in order to test for unknown issues, providing automated AI-guided fuzz testing.<br><br><strong>Default:</strong> <code>--module dast</code></td>
</tr>
<tr>
<td><code>--host-filter=hostOrIp</code>,<br> <code>-F=hostOrIp</code></td>
<td>The list of specific hosts to be included in the scan.</td>
</tr>
<tr>
<td><code>--header=headerName:headerValue</code>, <br><code>-H=headerName:headerValue</code></td>
<td>Extra headers to be passed with the archive file. It can also be used to remove a header by providing a name without content. For example, -H "Host:". <br><br><strong><font color="red">Warning:</font></strong> Headers set with this option override the archive headers and are set in all the requests.</td>
</tr>
<tr>
<td><code>--test=testName</code></td>
<td>Specifies a list of relevant tests to execute during a scan.<br>For example, <code>--test default_login_location dom_xss</code>.</td>
</tr>
<tr>
<td><code>--auth=authObjectID</code>, <br><code>-o=authObjectID</code></td>
<td>Specifies the ID of the authentication object to be connect to the scan. Find more info about using an authentication object at <a href="#/guide/np-web-ui/scanning/managing-authentications/managing-your-authentications">Manging Your Authentications</a>.</td>
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
<td>SOCKS URL to proxy all traffic.</code><br><br> <strong><font color="blue">Note:</font></strong> SOCKS4, SOCKS5, SOCKS4a, SOCKS5h are currently supported. By default, if you specify <code>SOCKS://&lt;URL&gt;</code> , then SOCKS5h is applied.</td>
</tr>
<tr>
<td><code>--api=clusterUrl</code></td>
<td><b><i>(Deprecated)</i></b>. Set the API endpoint domain, for VPC, use: <code>--api https://private-domain.nexploit.app</code> <br><br><strong>Default:</strong> <code>--api https://nexploit.app</code></td>
</tr>
</table>
