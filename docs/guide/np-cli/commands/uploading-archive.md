# 📤 Uploading an Archive
```nexploit-cli archive:upload [options] <file>``` uploads an HAR or OAS file to NeuraLegion storage.
>[!ATTENTION|label:WARNING]
If you plan to run a scan using an OAS file, you must specify a different discovery option by setting the `--discovery` to oas.

If an archive with that name already exists, the following error message displays – `The file with that name already exists or the HAR file is corrupted`.

# Arguments

<table id="simple-table">
    <tr>
        <th width="30%"><strong>Argument</strong></th>
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
<th width="30%"><strong>Option</strong></th>
<th><strong>Description</strong></th>
</tr>
<tr>
<td><code>--token my-jwt-authentication-token</code></td>
<td>The unique identifier used to authenticate a user. The token (API key) can be issued in your organization's dashboard.</td>
</tr>
<tr>
<td><code>--type=har/openapi/postman</code></td>
<td>The specification type, which helps determine the best way to parse passed files.<br><br><strong>Default:</strong> <code>--type har</code></td>
</tr>
<tr>
<td><code>--discard=false/true</code>,<br> <code>-d=false/true</code></td>
<td>When true, removes an archive from the cloud storage after the scan finishes running.<br><br><strong>Default:</strong> <code>--discard true</code></td>
</tr>
<tr>
<td><code>--header=extraHeader</code>, <br><code>-H=extraHeader</code></td>
<td>Extra headers to be passed with the OAS/Postman file. Also, it can be used to remove a header by providing a name without content. For example, -H "Host:".<br><br><strong><font color="red">Warning:</font></strong> Headers set with this option override the archive headers and are set in all requests.</td>
</tr>
<tr>
<td><code>--variable=envVariable</code>,<br> <code>-V=envVariable</code></td>
<td>Environment variables passed with the Postman file.</td>
</tr>
<tr>
<td><code>--api=ApiDomain</code></td>
<td>Set the API endpoint domain. For VPC, use <code>--api https://private-domain.nexploit.app</code> <br><br><strong>Default:</strong> <code>--api https://nexploit.app</code></td>
</tr>
</table>
