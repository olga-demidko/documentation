# 🔃 Retesting a Scan
```nexploit-cli scan:retest [options] <scan id>``` re-runs a scan by ID using the same configuration.

## Arguments

<table id="simple-table">
    <tr>
        <th width="30%"><strong>Argument</strong></th>
        <th><strong>Description</strong></th>
    </tr>
    <tr>
        <td><code>&#60scan id&#62</code></td>
        <td> The ID of an existing scan that you want to re-run.</td>
    </tr>
</table>

## Options

<table id="simple-table">
    <tr>
        <th width="30%"><strong>Option</strong></th>
        <th><strong>Description</strong></th>
    </tr>
    <tr>
        <td><code>--token my-jwt-authentication-token</code></td>
        <td>The unique identifier used to authenticate a user. The token (API key) can be issued in your organization’s dashboard.</td>
    </tr>
    <tr>
        <td><code>--api=ApiDomain</code></td>
        <td>Set the API endpoint domain. For VPC, use <code>--api https://private-domain.nexploit.app</code>.<p>
<b>Default:</b> <code>--api https://nexploit.app</code> </td>
    </tr>
</table>