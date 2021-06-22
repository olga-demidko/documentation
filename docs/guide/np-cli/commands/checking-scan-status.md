# 🚨 Checking Scan Status
```nexploit-cli scan:polling [options] <scan>``` configures ongoing polling of a scan status and helps you follow its progress during CI/CD flows.

After a scan launches, it frequently checks the scan status. If the scan finds at least of one issue of medium severity, Nexploit CLI finishes with exit code 50.

## Arguments

<table id="simple-table">
    <tr>
        <th width="34%"><strong>Argument</strong></th>
        <th><strong>Description</strong></th>
    </tr>
    <tr>
        <td><code>&#60scan&#62</code></td>
        <td>The ID of an existing scan that you want to check.</td>
    </tr>
</table>

## Options

<table id="simple-table">
<tr>
<th width="34%"><strong>Option</strong></th>
<th><strong>Description</strong></th>
</tr>
<tr>
<td><code>--token=apiKey</code>, <br><code>-t=apiKey</code></td>
<td>The unique identifier used to authenticate a user. The token (API key) can be issued in your organization’s dashboard.</td>
</tr>
<tr>
<td><code>--breakpoint=any/ medium_issue/high_issue</code>,<br><code>-b=any/medium_issue/high_issue</code></td>
<td>A conditional breakpoint that finishes the process with exit code 50 only after fulfilling the predefined condition. The breakpoint option allows you to follow the fail-fast principle when polling the scan results.<br><br> <strong>Default:</strong> <code>--breakpoint any</code></td>
</tr>
<tr>
<td><code>--interval=milliseconds</code></td>
<td>The period of time between the end of a timeout period or the completion of a scan status request, and the next request for status. For example, 60, 2min, 10h or 7d. A numeric value is interpreted in milliseconds.<br><br><strong>Default:</strong> --interval 5000</td>
</tr>
<tr>
<td><code>--timeout=milliseconds</code></td>
<td>The maximum time allowed for polling to end normally. For example, 60, 2min, 10h or 7d. A numeric value is interpreted in milliseconds.</td>
</tr>
<tr>
<td><code>--api=clusterUrl</code></td>
<td><b><i>(Deprecated)</i></b>. Set the API endpoint domain, for VPC, use: <code>--api https://private-domain.nexploit.app</code> <br><br><strong>Default:</strong> <code>--api https://nexploit.app</code></td>
</tr>
</table>