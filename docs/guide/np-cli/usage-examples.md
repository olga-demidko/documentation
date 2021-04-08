# ✔ Usage Examples
NexPloit CLI provides many features in addition to scan control over our API. This section describes the following sample use cases –
* [NPM](#npm)
* [Docker](#docker)

## NPM
### New Scan from a Swagger Schema
This example describes how to scan an API endpoint directly. The scope of the scan, all the possible interactions and parameters are defined in an OpenAPI schema that is uploaded before starting the scan.

#### Prerequisites
* An active user on [nexploit.app](www.nexploit.app).
* A Swagger/OpenAPI schema `FILE_PATH`.
* A valid `AUTH_TOKEN` (API key) with the following scopes: `files:read`, `files:write`, `scans:run` and `scans:read`. You can set up an [organization-level authentication token](guide/np-web-ui/advanced-set-up/managing-org#Managing-Organization-APICLI-Authentication-Tokens) or a [user-level authentication token](guide/np-web-ui/advanced-set-up/managing-personal-account#Managing-Your-Personal-API-Keys-Authentication-Tokens).

#### Step-by-step Guide
**Step 1 – Upload a Schema**
```bash
  FILE_ID=$(nexploit-cli archive:upload
  --token $AUTH_TOKEN
  --type openapi
  --discard true
  	$FILE_PATH)
```
**Step 2 – Create a New Scan**
```bash
  SCAN_ID=$(nexploit-cli scan:run
  --token $AUTH_TOKEN
  --name "My First Scan"
  --archive $FILE_ID
  --smart)
```
**Step 3 – Poll Scan Status**
```bash
  nexploit-cli scan:polling
  --token $AUTH_TOKEN
  --breakpoint high_issue
  --interval 3000
  --timeout 1h
  $SCAN_ID
```

### Re-run a Previous Scan
This example describes how to re-run a previous scan using all the same scan settings and parameters.

#### Prerequisites
* An active user on [nexploit.app](www.nexploit.app).
* A previous `SCAN_ID`.
* A valid `AUTH_TOKEN` (API key) with the following scopes: `scans:run` and `scans:read`. You can set up an [organization-level authentication token](guide/np-web-ui/advanced-set-up/managing-org#Managing-Organization-APICLI-Authentication-Tokens) or a [user-level authentication token](guide/np-web-ui/advanced-set-up/managing-personal-account#Managing-Your-Personal-API-Keys-Authentication-Tokens).

#### Step-by-step Guide
**Step 1 – Re-run a Previous Scan**
```bash
  NEW_SCAN_ID=$(nexploit-cli scan:retest
  --token $AUTH_TOKEN
  $SCAN_ID)
```
**Step 2 – Poll Scan Status**
```bash
  nexploit-cli scan:polling
  --token $AUTH_TOKEN
  --breakpoint high_issue
  --interval 3000
  --timeout 1h
  $NEW_SCAN_ID
```

### New Scan with a Repeater
This example describes how to run a scan using a local Repeater.

#### Prerequisites
* An active user on the www.nexploit.app.
* A valid `AUTH_TOKEN` (API key) with the following scopes: `bot`, `scans:run` and `scans:read`. You can set up an [organization-level authentication token](guide/np-web-ui/advanced-set-up/managing-org#Managing-Organization-APICLI-Authentication-Tokens) or a [user-level authentication token](guide/np-web-ui/advanced-set-up/managing-personal-account#Managing-Your-Personal-API-Keys-Authentication-Tokens).
* An active `REPEATER_ID`. See [Managing Repeaters](guide/np-web-ui/advanced-set-up/managing-repeaters) for more information about handling Repeaters.

#### Step-by-step Guide
**Step 1 – Start a Repeater**
```bash
  PID_REPEATER=$(nexploit-cli repeater
  --token=plhzeup.nexp.0lhtc7ib5pogcibaqprz6gz994sltelu 
  --id=b5b03145-1f30-4002-bab1-8f1b58df4bf9 > /dev/null
  & echo $! )

  echo "Repeater PID: $PID_REPEATER"
```
**Step 2 – Run a New Scan with a Crawler**
```bash
  SCAN_ID=$(nexploit-cli scan:run
  --token $AUTH_TOKEN
  --name "My First Scan"
  --repeater $REPEATER_ID
  --crawler www.example.com
  --host-filter www.example.com
  --smart
  $SCAN_ID)
```
**Step 3 – Poll Scan Status**
```bash
  nexploit-cli scan:polling
  --token $AUTH_TOKEN
  --breakpoint high_issue
  --interval 3000
  --timeout 1h
  $SCAN_ID
```

## Docker
The Docker version of NexPloit CLI comes as a preconfigured Repeater container. As soon as the container is launched, the CLI activates the Repeater mode.

### Setup
#### Prerequisites
* An active user on [nexploit.app](www.nexploit.app).
* You must have Docker Compose installed.
* A valid `AUTH_TOKEN` (API key) with the `bot` scope . You can set up an [organization-level authentication token](guide/np-web-ui/advanced-set-up/managing-org#Managing-Organization-APICLI-Authentication-Tokens) or a [user-level authentication token](guide/np-web-ui/advanced-set-up/managing-personal-account#Managing-Your-Personal-API-Keys-Authentication-Tokens).
* An active `REPEATER_ID`. See [Managing Repeaters](guide/np-web-ui/advanced-set-up/managing-repeaters) for more information about handling Repeaters.

#### Step-by-step Guide
**STEP 1 – Create a `.yml` File**
```yml
version: '3'
services:
  target.local:
    image: path/image-name

  repeater:
    image: neuralegion/repeater:latest
    restart: always
    environment:
      REPEATER_TOKEN: AUTH_TOKEN
      REPEATER_ID: REPEATER_ID
```
**STEP 2 – Run the Docker**<br>
Run the **Repeater Docker** using the command:
```bash
docker-compose up
```
>[!NOTE|label:Note]
If a valid AUTH_TOKEN and REPEATER_ID was not added, then the **Unauthorized access** error appears. Please check your credentials.

Now, when Starting a New Scan, you can connect the Repeater under **Additional Settings** in the UI or use the CLI to start a scan.

### Run a New Scan with Docker Startup
The Docker version of the Repeater comes with a built-in **NexPloit-CLI**, so that additional functions can be added to the docker container to be executed after the Repeater mode is launched.

Here is an example of a `.yaml` configuration that will launch a new scan as soon as the Docker is running –

#### Prerequisites
* An active user on [nexploit.app](www.nexploit.app).
* You must have Docker Compose installed.
* A valid `AUTH_TOKEN` (API key) with the following scopes: `bot`, `scans:run`, `scans:read`. You can set up an [organization-level authentication token](guide/np-web-ui/advanced-set-up/managing-org#Managing-Organization-APICLI-Authentication-Tokens) or a [user-level authentication token](guide/np-web-ui/advanced-set-up/managing-personal-account#Managing-Your-Personal-API-Keys-Authentication-Tokens).
* An active `REPEATER_ID`. See [Managing Repeaters](guide/np-web-ui/advanced-set-up/managing-repeaters) for more information about handling Repeaters.

```yml
version: '3'
services:
  target.local:
    image: path/image-name
    ports:
      - '3000:3000'

  repeater:
    image: neuralegion/repeater:latest
    restart: always
    environment:
      REPEATER_TOKEN: AUTH_TOKEN
      REPEATER_ID: REPEATER_ID

  nexploit:
    depends_on:
      - repeater
      - target.local
    image: neuralegion/repeater:nexploit-cli
    environment:
      REPEATER_TOKEN: AUTH_TOKEN
      REPEATER_ID: REPEATER_ID
    entrypoint:
      - bash
      - -c
      - >
        sleep 10;
        HARID=$$(nexploit-cli archive:upload --type openapi --token=$$AUTH_TOKEN /opt/repeater/swagger.yaml);
        echo Your HAR ID is $$HARID;
        SCANID=$$(nexploit-cli scan:run --name='My Scan' --repeater=$$REPEATER_ID --archive $$HARID --tests header_security --token $$AUTH_TOKEN);
        echo Scan started $$SCAN_ID;
        echo Poll for scan results;
        RESULT=$$(nexploit-cli scan:polling --token $$AUTH_TOKEN --breakpoint=high_issue \
          --interval=10000 --timeout=5min $$SCAN_ID);
        nexploit-cli scan:stop --token=$$AUTH_TOKEN $$SCAN_ID;
        exit $$RESULT;
```

### Adding Extra Headers Locally
The Repeater enables a user to overload extra headers onto the Repeater's requests **LOCALLY**, without the need to set them up in NexPloit cloud engine. This is done by setting the `REPEATER_HEADERS` environment variable.
For example:
```yml
version: '3'
services:
  repeater:
    image: neuralegion/repeater:latest
    restart: always
    environment:
      REPEATER_TOKEN: AUTH_TOKEN
      REPEATER_ID: cdf07782-bc6c-486a-b459-e182808faa33
      REPEATER_HEADERS: '{ "my_header": "special token" }'
```
Or as a command line configuration:
```bash
docker run neuralegion/repeater -e 'REPEATER_HEADERS={"my_header": "special token"}'
```
 
