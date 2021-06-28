# 📤 Uploading an Archive
```nexploit-cli archive:upload [options] <file>``` uploads an HAR or OAS file to the Nexploit storage.
>[!ATTENTION|label:WARNING]
If you plan to run a scan using an OAS file, you must specify a different discovery option by setting the `--discovery` to OAS.

If an archive with that name already exists, the following error message displays – `The file with that name already exists or the HAR file is corrupted`.

# Arguments

<table id="simple-table">
    <tr>
        <th width="39%"><strong>Argument</strong></th>
        <th><strong>Description</strong></th>
    </tr>
    <tr>
        <td><code>&#60file&#62</code></td>
        <td> A collection of your app http/websockets logs exported into a HAR file. Typically, you can use any browser's dev tools, NeuraLegion's browser extension or a Cypress plugin to generate them. In addition, you can use an OAS file that describes your public API.</td>
    </tr>
</table>

# Options

<table id="simple-table">
    <tr>
        <th width="39%"><strong>Option</strong></th>
        <th><strong>Description</strong></th>
    </tr>
    <tr>
        <td><code>--token=apiKey</code>,<br><code>-t=apiKey</code></td>
        <td>The unique identifier used to authenticate a user. The token (API key) can be issued in your organization's dashboard.</td>
    </tr>
    <tr>
        <td><code>--type=har/openapi/postman</code>,<br> <code>-t=har/openapi/postman</code></td>
        <td>The specification type, which helps determine the best way to parse passed files.<br><br><strong>Default:</strong> <code>--type har</code></td>
    </tr>
    <tr>
        <td><code>--discard</code>,<br> <code>-d</code></td>
        <td>When true, removes an archive from the cloud storage after the scan finishes running.<br><br><strong>Default:</strong> <code>--discard true</code></td>
    </tr>
    <tr>
        <td><code>--header=headerName:headerValue</code>,<br><code>-H=headerName:headerValue</code></td>
        <td>Extra headers to be passed with the OAS/Postman file. Also, it can be used to remove a header by providing a name without content. For example, -H "Host:".<br><br><strong><font color="red">Warning:</font></strong> Headers set with this option override the archive headers and are set in all requests.</td>
    </tr>
    <tr>
        <td><code>--variable=variableName:variableValue</code>,<br><code>-V=variableName:variableValue</code></td>
        <td>Environment variables passed with the Postman file.</td>
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
        <td><code>--api=clusterUrl</code></td>
        <td><b><i>(Deprecated)</i></b>. Set the API endpoint domain. For VPC, use <code>--api https://private-domain.nexploit.app</code> <br><br><strong>Default:</strong> <code>--api https://nexploit.app</code></td>
    </tr>
</table>
