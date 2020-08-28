# On-prem Agent (Repeater) Solution
### 🌎 Section Map <!-- {docsify-ignore} -->
- [Overview](#overview)
- [How the Repeater Works](#how-the-repeater-works)
- [Technical Requirements](#technical-requirements)
- [Benefits](#benefits)
- [Installation](#installation)
- [Usage Examples](#usage-examples)
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
NeuraLegion’s **Repeater** is an [Open Source](https://www.npmjs.com/package/@neuralegion/nexploit-cli) component. It is a lightweight local agent that securely connects to NeuraLegion’s cloud engines and mediates the traffic from the cloud to any local target.

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

## Installation
You can find full installation instructions in the [NexPloit CLI > Installation](/nexploit-cli/installation.md) section

## Usage examples
You can find usage examples in the [NexPloit CLI > Usage Examples](/nexploit-cli/usage-examples.md) section

## FAQ
#### What is the maintenance / patching frequency? <!-- {docsify-ignore} -->
The engine requires no maintenance or patching from the client side, since it is in the cloud and gets the latest updates immediately.

The Repeater will require periodic updates, which can be performed manually by a simple CLI update command or automatically if the Repeater is installed during a build as part of the CI process.

#### Can I use a single machine with a Repeater to access multiple internal targets? <!-- {docsify-ignore} -->
Yes, as long as the local machine with the Repeater has access to the internal applications, multiple scans can be done via the same Repeater.

In addition, by installing the Repeater on a personal computer,  it is possible to create scans on local running applications, which is useful for developers that want to do quick tests without deploying code.

#### Do I need to change Firewall / Port settings for the Repeater? <!-- {docsify-ignore} -->
Not at all, using the Repeater does not require ANY changes to your network INBOUND traffic settings, because all the generated traffic is based on OUTBOUND requests from inside the network.

#### I have a Firewall between different internal applications, what do I need to do? <!-- {docsify-ignore} -->
In this case, you can either install a separate Repeater behind the relevant Firewalls to avoid any need for whitelisting, use open ports between the internal applications or configure new ports for the Repeater.

#### Will a Firewall affect the scan results or add False Positives? <!-- {docsify-ignore} -->
Not at all, the Repeater does not contain any complicated logic. All the decision making and False Positive removal by active validation are still performed by the engine in the cloud. This means that all the computation and advanced algorithms are available to scans that use a Repeater the same way as for regular scans.
