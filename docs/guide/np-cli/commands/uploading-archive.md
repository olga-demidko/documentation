# 📤 Uploading an Archive
```nexploit-cli archive:upload [options] <file>``` uploads an HAR or OAS file to NeuraLegion storage.
>[!ATTENTION|label:WARNING]
If you plan to run a scan using an OAS file, you must specify a different discovery option by setting the `--discovery` to oas.

If an archive with that name already exists, the following error message displays – `The file with that name already exists or the HAR file is corrupted`.

# Arguments
| **Argument** | **Description** |
| :-- | :-- |
| ```<file>``` | A collection of your app http/websockets logs exported into a HAR file. Typically, you can use any browser's dev tools, NeuraLegion's browser extension or a Cypress plugin to generate them. In addition, you can use an OAS file that describes your public API. |

# Options
| **Option** | **Description** |
|:--|:--|
| ```--token my-jwt-authentication-token``` | The unique identifier used to authenticate a user, which can be issued in your organization's dashboard. |
| ```--type=har/openapi/postman``` | The specification type, which helps determine the best way to parse passed files.<br/><br/>**Default Value –** --type har |
| ```--discard=false/true```, ```-d=false/true``` | When true, removes an archive from the cloud storage after the scan finishes running.<br/><br/>**Default Value –** --discard true |
| ```--header=extraHeader```, ```-H=extraHeader``` | Extra headers to be passed with the OAS/Postman file. Also, it can be used to remove a header by providing a name without content. For example, -H "Host:".<br/><br/>**<font color="red">WARNING –</font>** Headers set with this option override the archive headers and are set in all requests. |
| ```--variable=envVariable```, ```-V=envVariable``` | Environment variables passed with the Postman file. |
| ```--api=ApiDomain``` | Set the API endpoint domain, for VPC, use: `--api https://private-domain.nexploit.app` <br/><br/>**Default Value:** `--api https://nexploit.app` |
