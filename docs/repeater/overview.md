# NeuraLegion's Repeater
![repeater_image](https://d36jcksde1wxzq.cloudfront.net/be7833db9bddb4494d2a7c3dd659199a.png ':size=10%')

<!-- NeuraLegion’s **Repeater** is a local agent that provides a secure connection between NeuraLegion's cloud engine and a target on a local network. -->

### Quick Start {docsify-ignore}
- [Overview](#overview)
- [How the Repeater Works](#how-the-repeater-works)
- [Technical Requirements](#technical-requirements)
- [Benefits](#benefits)
- [Installation via Docker](#installation-via-docker)
- [Usage Examples](#usage-examples)
  - [Run a New Scan With NexPloit-CLI](#run-a-new-scan-with-nexploit-cli)
  - [Re-Run an Existing Scan](#re-run-an-existing-scan)
  - [Extra Headers](#extra-headers)
- [FAQ](#faq)

<hr style="height:2px;background-color:#d1d3d4">

## Overview
NeuraLegion’s **Repeater** is a local agent that provides a secure connection between NeuraLegion's cloud engine and a target on a local network.

It is intended for:
- Organizations that categorically cannot open a port in the firewall for inbound traffic to enable scans to run from either NeuraLegion’s SaaS, or private cloud offerings.
- Users who need to run a local scan on their machine without deploying the target application.

!> <font color="red" size="3"><b>IMPORTANT:</b> If you are able to whitelist a specific IP & port in your firewall, you do not need the Repeater</font>

Using NeuraLegion’s Repeater will enable you to securely scan targets sitting on a local network, without the need to whitelist our IP address in your firewall for incoming traffic.

!> <font color="red" size="3"><b>IMPORTANT:</b> In order to function, the repeater <b>REQUIRES</b> the ability to have an outbound connection to amq.nexploit.app via the AMQ protocol (over TLS) using port 5672</font>

This section explains the benefits and requirements of using a **Repeater** for scans.

## How the Repeater Works
NeuraLegion’s **Repeater** is an [Open Source](https://hub.docker.com/r/neuralegion/repeater) component. It is a lightweight local agent that securely connects to NeuraLegion’s cloud engines and mediates the traffic from the cloud to any local target.

After starting a scan with a configured Repeater, the communication works as follows:
1. The **Repeater** initiates a GET request to the cloud engine via AMQ server
2. The **Repeater** receives the request instructions of how to interact with the local target
3. The **Repeater** adds relevant headers to the request (locally), such as authentication headers and sends the request to the local target
4. The local target returns the response to the **Repeater**
5. The **Repeater** sends the response to the engine
6. Back to 1, until the scan is finished

![repeater-architecture](media/repeater-architecture.png ':size=45%')


## Technical Requirements
1. A local machine with:
  1. Access to relevant internal targets on the local network 
  2. The Repeater **ONLY** works when it has access to **amq.nexploit.app** at **port 5672**
  3. Docker compose installed OR NodeJS (v10+)
2. Installed Repeater on the relevant local machine (Docker or NexPloit-CLI)

## Benefits
- Secure access to local network applications
- Easy local control of the scan process with a CLI
- No WAF/Firewall/VPN configuration needed
- No exposure of internal IPs or authentication information to the cloud
- Complete transparency of the Repeater code

## Installation via Docker
To install the **Repeater**, you must have [Docker Compose](https://docs.docker.com/compose/install/) installed.

1. Pull the **Repeater Docker** using the command:
```
docker pull neuralegion/repeater
```
2. Create a new `API-KEY` with the scope `agents:write:repeater`
 - You can set up an [Organization level API Key](user-guide/organization-administration/details-and-policies.md#managing-organization-api-keys)
 - Or, a [User level API Key](user-guide/personal-account-administration/details-and-settings.md#managing-your-api-keys)

3. Set up a [New Agent](user-guide/agents/overview.md) to create a new `AGENT-ID`

4. Create a `docker-compose.yml` file with the following content:
```yaml
version: '3'
services:
  target.local:
    image: path/image-name
  repeater:
    image: neuralegion/repeater:latest
    restart: always
    environment:
      AGENT_KEY: API-KEY # from step 2
      AGENT_ID: AGENT-ID # from step 3
```

5. Install the **Repeater Docker** by running the command
```
docker-compose up
```

!> **Note**: If did not add a valid `API-KEY` and `AGENT-ID` you will get the following error: `repeater_1 | Unhandled exception in spawn: 403 - ACCESS_REFUSED - Login was refused using authentication mechanism PLAIN. For details see the broker logfile. (AMQP::Client::Connection::ClosedException)`

6. Now, when [Starting a New Scan](user-guide/scans/new-scan), you can connect the Repeater under [Addition Settings](user-guide/scans/new-scan#additional-settings)


More info on our **Docker Hub** page: https://hub.docker.com/r/neuralegion/repeater

## Usage Examples
### Run a New Scan With NexPloit-CLI
The Docker version of the Repeater comes with a built-in [NexPloit-CLI](nexploit-cli/overview.md)
```yaml
version: '3'
services:
  target.local:
    image: path/image-name
    ports:
      - "3000:3000"
  repeater:
    image: neuralegion/repeater:latest
    restart: always
    environment:
      AGENT_KEY: API-KEY
      AGENT_ID: AGENT-ID
      WEBDRIVERS: '[{"host": "xssdriver", "port": 2828}, {"host": "crawldriver", "port": 2829}]'
  nexploit:
    depends_on: 
    - repeater
    - target.local
    image: neuralegion/repeater:nexploit-cli
    environment:
      API_KEY: API-KEY
      AGENT_ID: AGENT-ID
    entrypoint:
    - bash
    - -c
    - >
      sleep 10;
      HARID=$$(nexploit-cli archive:upload --discovery oas --api-key=$$API_KEY /opt/repeater/swagger.yaml);
      echo Your HAR ID is $$HARID;
      SCANID=$$(nexploit-cli scan:run --name='My Scan' --agent=$$AGENT_ID --archive $$HARID --tests header_security --api-key $$API_KEY);
      echo Scan started $$SCAN_ID;
      echo Poll for scan results;
      RESULT=$$(nexploit-cli scan:polling --api-key $$API_KEY --failure-on=first-high-severity-issue \
        --interval=10000 --timeout=5min $$SCAN_ID);
      nexploit-cli scan:stop --api-key=$$API_KEY $$SCAN_ID;
      exit $$RESULT;
```

### Re-Run an Existing Scan
```yaml
version: '3'
services:
  target.local:
    image: path/image-name
    ports:
      - "3000:3000"
  repeater:
    image: neuralegion/repeater:latest
    restart: always
    environment:
      AGENT_KEY: API-KEY
      AGENT_ID: AGENT-ID
  nexploit:
    depends_on: 
    - repeater
    - target.local
    image: neuralegion/repeater:nexploit-cli
    environment:
      API_KEY: API-KEY
      SCAN_PROTOTYPE: 6WL3Gi74xzyc1Pvqz6qEdM # previous scan ID
    entrypoint:
    - bash
    - -c
    - >
      sleep 10;
      SCAN_ID=$$(nexploit-cli scan:retest --api-key=$$API_KEY $$SCAN_PROTOTYPE);
      echo Scan started $$SCAN_ID;
      echo Poll for scan results;
      RESULT=$$(nexploit-cli scan:polling --api-key $$API_KEY --failure-on=first-high-severity-issue \
        --interval=10000 --timeout=5min $$SCAN_ID);
      nexploit-cli scan:stop --api-key=$$API_KEY $$SCAN_ID;
      exit $$RESULT;
```

### Extra Headers
The Repeater allows a user to overload extra headers onto the Repeater's requests **LOCALLY**, without the need to set them up in NexPloit's cloud engine. This is done by setting the `EXTRA_HEADERS` environment variable.

For example:
```yaml
version: '3'
services:
  repeater:
    image: neuralegion/repeater:latest
    restart: always
    environment:
      AGENT_KEY: g5f1clg.lkfcjgnyyuzp34a1fnzmxn8lrxcjuwgu
      AGENT_ID: cdf07782-bc6c-486a-b459-e182808faa33
      EXTRA_HEADERS: {"my_header": "special token"}
```

Or as a command line configuration:
```
docker run neuralegion/repeater -e 'EXTRA_HEADERS={"my_header": "special token"}'
```

## FAQ
#### What is the maintenance / patching frequency? {docsify-ignore}
The engine requires no maintenance or patching from the client side, since it is in the cloud and gets the latest updates immediately.

The Repeater will require periodic updates, which can be performed manually by a simple CLI update command or automatically if the Repeater is installed during a build as part of the CI process.

#### Can I use a single machine with a Repeater to access multiple internal targets? {docsify-ignore}
Yes, as long as the local machine with the Repeater has access to the internal applications, multiple scans can be done via the same Repeater.

In addition, by installing the Repeater on a personal computer,  it is possible to create scans on local running applications, which is useful for developers that want to do quick tests without deploying code.

#### Do I need to change Firewall / Port settings for the Repeater? {docsify-ignore}
Not at all, using the Repeater does not require ANY changes to your network INBOUND traffic settings, because all the generated traffic is based on OUTBOUND requests from inside the network.

#### I have a Firewall between different internal applications, what do I need to do? {docsify-ignore}
In this case, you can either install a separate Repeater behind the relevant Firewalls to avoid any need for whitelisting, use open ports between the internal applications or configure new ports for the Repeater.

#### Will a Firewall affect the scan results or add False Positives? {docsify-ignore}
Not at all, the Repeater does not contain any complicated logic. All the decision making and False Positive removal by active validation are still performed by the engine in the cloud. This means that all the computation and advanced algorithms are available to scans that use a Repeater the same way as for regular scans.
