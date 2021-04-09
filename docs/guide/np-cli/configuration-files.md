# ⚙️ Configuration Files
Any configuration option that can be set via the command line can also be specified in the `nexploit` section of your `package.json` or within a separate configuration file. A variety of configuration files can be used, as described in the following table. You can set your configurations in any of the files listed in the table or from the command line.

<table id="simple-table">
    <tr>
        <th width="20%"><strong>File Name</strong></th>
        <th <strong>File Type</strong></th>
    </tr>
    <tr>
        <td><code>.nexploit</code></td>
        <td> JSON </td>
    </tr>
    <tr>
        <td><code>.nexploit.json</code></td>
        <td> JSON </td>
    </tr>
    <tr>
        <td><code>.nexploit.yaml</code></td>
        <td> YAML </td>
    </tr>
    <tr>
        <td><code>.nexploit.yml</code></td>
        <td> YAML </td>
    </tr>
    <tr>
        <td><code>nexploit.config.js</code></td>
        <td> CommonJS export </td>
    </tr>
</table>

Specify a path to a configuration file using the `--config` option. By default, the CLI tries to discover a configuration `package.json` file in the root directory of your application, or one of the other specified file names in the working directory.

## Examples

### Uploading a Postman Collection
In some cases, you may want to upload a Postman collection that has many variables. In such cases, you can load variables from the configuration file, as shown in the following examples.

#### JSON Example
```JSON
{
  "discard": true,
  "type": "postman",
  "header": ["authorization: api-key my-api-key"],
  "variable": ["base-api-url: https://example.com/"]
}
```
#### YAML Example
```YAML
---
discard: true
type: postman
header:
  - 'authorization: api-key my-api-key'
variable:
  - 'base-api-url: https://example.com/'
  - 'some-secret: my-magic-number'
```
The code above enables you to issue the following command in your terminal –
```bash
  nexploit-cli archive:upload
  -t 75ngxdf.nexp.6kd4e9a6xcb2mbdfvnw76hnsqpyrf7wf
  /home/ubuntu/collection.json
```

### Crawler Scan
If you need to frequently scan multiple targets, you can specify them in a configuration file.

#### JSON Example
```JSON
{
  "crawler": [
    "https://example.com",
    "https://nova.example.com",
    "https://pbs.example.com",
    "https://google.com"
  ],
  "name": "scan-name",
  "token": "my-api-key"
}
```

#### YAML Example
```YAML
---
crawler:
  - https://example.com
  - https://nova.example.com
  - https://pbs.example.com
  - https://google.com
name: scan-name
token: my-api-key
```

### Predefined Pool of Tests
Nexploit CLI supports many different tests that can be executed. In some cases, it may be difficult to set them up using CLI options. In such cases, you can set them up using a configuration file.

#### JSON Example
```JSON
{
  "test": [
    "angular_csti",
    "jwt",
    "date_manipulation",
    "cookie_security",
    "csrf",
    "directory_listing",
    "dom_xss",
    "file_upload",
    "full_path_disclosure",
    "header_security",
    "http_method_fuzzing",
    "retire_js",
    "secret_tokens",
    "version_control_systems",
    "wordpress"
  ],
  "name": "scan-name",
  "token": "my-api-key"
}
```

#### YAML Example
```YAML
---
test:
- angular_csti
- jwt
- date_manipulation
- cookie_security
- csrf
- directory_listing
- dom_xss
- file_upload
- full_path_disclosure
- header_security
- http_method_fuzzing
- retire_js
- secret_tokens
- version_control_systems
- wordpress
name: scan-name
token: my-api-key
```

### Predefined Repeater Settings
The following are examples of Repeater settings to be used with the CLI.

#### JSON Example
```JSON
{
  "token": "my-jwt-authentication-token",
  "api": "https://nexploit.app",
  "bus": "amqps://amq.nexploit.app:5672",
  "proxy": "proxy-address"
}
```

#### YAML Example
```YAML
---
token: my-jwt-authentication-token
api: https://nexploit.app
bus: amqps://amq.nexploit.app:5672
proxy: proxy-address
```

### HAR Generation from NexMock
If you already have a prepared mock file, you can generate a HAR file using the following command –
```bash
nexploit-cli archive:generate \
  --output archive.har \
  --target url-tested-application \
  --header "Authorization: Bearer my-jwt-authentication-token" \
  .nexmockCopy to clipboardErrorCopied
```
Where –
* mockfile is the path to your mock file.
* archive is the path in which to save the HAR file.
The `archive:generate` command generates a new archive in the archive path –
```
Project
├── .nexploitrc       // CLI configuration
├── .nexmock          // your mock requests
└── archive.har       // generated HAR fileCopy to clipboardErrorCopied
```
You also can edit the configuration file and add your own options, as shown below –

#### JSON Example
```JSON
{
  "output": "archive.har",
  "token": "my-jwt-authentication-token",
  "target": "url-tested-application",
  "header": [
    "Authorization: Bearer my-jwt-authentication-token"
  ]
}
```

#### YAML Example
```YAML
---
output: archive.har
token: my-jwt-authentication-token
target: url-tested-application
header:
- 'Authorization: Bearer my-jwt-authentication-token'
```
To obtain the same output, simply issue the following CLI command –
```bash
nexploit-cli archive:generate .nexmock
```