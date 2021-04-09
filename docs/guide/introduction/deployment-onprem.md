# On-Premises Repeater (Agent)
## Overview
NeuraLegion’s Repeater is a local agent that provides a secure connection between NeuraLegion's cloud engine and a target on a local network. A Repeater enables you to securely scan targets on a local network, without having to whitelist NeuraLegion’s IP address in your firewall for incoming traffic.

A Repeater is intended for –
* Organizations that cannot open a port in the firewall for inbound traffic. The Repeater enables scans to run from either NeuraLegion’s SaaS or private cloud offerings.
* Users who must run a local scan on their machine without deploying the target application.

> [!WARNING|label:Important]
In order to function properly, the Repeater must have an outbound connection to **amq.nexploit.app** via the AMQ protocol (over TLS) using port 5672.

> [!WARNING|label:Important]
A Repeater is not required if you are able to whitelist a specific IP and port in your firewall.

## How Does an On-Premises Repeater Deployment Work?
NeuraLegion’s Repeater is an [Open Source](https://www.npmjs.com/package/@neuralegion/nexploit-cli) component. It is a lightweight local agent that securely connects to NeuraLegion’s cloud engines and mediates the traffic from the cloud to any local target.

![repeater-chart](media/repeater-chart.png ':size=40%')

After starting a scan with a configured Repeater, communication works as follows –
1. The Repeater initiates a GET request to the cloud engine via the AMQ server.
2. The Repeater receives the request instructions describing how to interact with the local target.
3. The Repeater locally adds the relevant headers to the request, such as authentication headers and sends the request to the local target.
4. The local target returns the response to the Repeater.
5. The Repeater sends the response to the engine.
6. The Repeater returns to #1 until the scan completes.

## Technical Requirements
The On-Premises Repeater requires:
* A local machine with:
    * System:    Linux 4.4+ / Windows 8+ / Docker 20+
    * Processor: x86 or x64 1 core (minimum), 2 core (recommended)
    * RAM: 512 MB (minimum), 1 GB (recommended)
    * Hard disk: up to 512 MB of available space may be required
    * The Docker compose or NodeJS (v10+) installed
* Access to the relevant internal targets on the local network
* Access to the amq.nexploit.app on port 5672 or a provite cloud on the relevant port

## Installation
See the [Nexploit CLI Installation](/guide/np-cli/installation.md) section for installation instructions.

## Usage Examples
See the usage examples in the [Nexploit CLI Usage Examples](/guide/np-cli/usage-examples.md) section.

## FAQs – On-Premises Repeater
### What is the maintenance / patching frequency?
The Nexploit engine does not require any maintenance or patching from the client side. It is in the cloud and therefore is always updated automatically. 

The Repeater does require periodic updates. These can be performed either manually (using a simple CLI update command) or automatically (if the Repeater is installed during a build as part of the CI process).

### Can I use a single machine with a Repeater in order to access multiple internal targets?
Yes, on the condition that the local machine on which the Repeater is installed has access to the internal applications. In this case, multiple scans can be performed using the same Repeater.

In addition, by installing the Repeater on a personal computer, it is possible to scan locally running applications. This is useful for developers who want to perform quick tests without deploying code.

### Do I need to change firewall / port settings for the Repeater?
No. Using the Repeater does not require any changes to your network’s inbound traffic settings, because  all the generated traffic is based on outbound requests from inside the network.

### I have a Firewall between various internal applications. How do I handle this?
You have the following options, to – 
* Install a separate Repeater behind the relevant firewalls in order to avoid the need for whitelisting.
* Use open ports between the internal applications.
* Configure new ports for the Repeater.

### Will a Firewall affect the scan results or add false positives?
The Repeater does not contain any complicated logic. All decision making and removal of false-positives using active validation is performed by the engine in the cloud. This means that all the computational and advanced algorithms are available to scans that use a Repeater, in the same way as for scans that are deployed as a SaaS or in the private cloud.


