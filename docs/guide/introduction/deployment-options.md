# Deployment Options
NeuraLegion offers the following deployment options for accessing the targets to be scanned –
* SaaS (Offering hosting on various hosting platforms)
* On-premises Agent (Repeater)
* Private Cloud

![deployment-options-chart](media/deployment-chart.png ':size=100%')

## SaaS
### Overview – No installation
Using NeuraLegion’s SaaS deployment option is simple. There is no need to install anything locally. 
Simply log in to the NeuraLegion platform and select the target application to be scanned. 

### How Does a SaaS Deployment Work?
NeuraLegion’s state-of-the art AIAST®-powered engines begin scanning the target for issues. Reports that show identified issues start displaying immediately, with zero false-positives.
The standard SaaS solution uses a multi-tenant architecture for the databases and static network configurations.

![saas-chart](media/saas-chart.png ':size=100%')

### Before You Begin
Before scanning, ensure that –
* The target application can be accessed from the Internet.
* NeuraLegion’s static IP (see below) is whitelisted by your WAF/firewall (recommended in order to avoid auto-blacklisting of NeuraLegion’s solutions).

> [!WARNING|label:Important]
NeuraLegion has two public static IPs:\
&nbsp;&nbsp;&nbsp;&nbsp;**U.S. –** 34.228.94.55\
&nbsp;&nbsp;&nbsp;&nbsp;**Europe –** 52.215.195.32

### Deployment Options
Currently, deployment is only possible on AWS. Deployment to other cloud vendors can be added, if needed, for specific scenarios. NeuraLegion fully manages the deployment process for you.

If you are interested in other deployment options, contact your sales representative.

### FAQs – SaaS Deployment
#### Why aren’t there any false positives?
NeuraLegion’s solutions do not simply scan, but rather interact with the target application. This means that every reported vulnerability is validated in real time. If a vulnerability cannot be validated, it is not reported, thereby saving you from unnecessary noise and hours of manual labor.

#### Will NeuraLegion have access to the vulnerabilities (issues) that it detects in my applications?
A NeuraLegion representative cannot access your scan results without your permission. If support is needed, then an organization’s owner can invite a NeuraLegion engineer to access your vulnerabilities in order to provide support.


## On-Premises Repeater (Agent)
### Overview
NeuraLegion’s Repeater is a local agent that provides a secure connection between NeuraLegion's cloud engine and a target on a local network. A Repeater enables you to securely scan targets on a local network, without having to whitelist NeuraLegion’s IP address in your firewall for incoming traffic.

A Repeater is intended for –
* Organizations that cannot open a port in the firewall for inbound traffic. The Repeater enables scans to run from either NeuraLegion’s SaaS or private cloud offerings.
* Users who must run a local scan on their machine without deploying the target application.

> [!WARNING|label:Important]
In order to function properly, the Repeater must have an outbound connection to **amq.nexploit.app** via the AMQ protocol (over TLS) using port 5672.

> [!WARNING|label:Important]
A Repeater is not required if you are able to whitelist a specific IP and port in your firewall.

### How Does an On-Premises Repeater Deployment Work?
NeuraLegion’s Repeater is an [Open Source](https://www.npmjs.com/package/@neuralegion/nexploit-cli) component. It is a lightweight local agent that securely connects to NeuraLegion’s cloud engines and mediates the traffic from the cloud to any local target.
![repeater-chart](media/repeater-chart.png ':size=100%')
After starting a scan with a configured Repeater, communication works as follows –
1. The Repeater initiates a GET request to the cloud engine via the AMQ server.
2. The Repeater receives the request instructions describing how to interact with the local target.
3. The Repeater locally adds the relevant headers to the request, such as authentication headers and sends the request to the local target.
4. The local target returns the response to the Repeater.
5. The Repeater sends the response to the engine.
6. The Repeater returns to #1 until the scan completes.

### Technical Requirements
The On-Premises Repeater requires – 
* A local machine with –
    * Access to relevant internal targets on the local network.
    * A Repeater only works when it has access to the amq.nexploit.app on port 5672.
    * The installation of Docker compose or NodeJS (v10+).
* An installed Repeater on the relevant local machine (Docker or NexPloit CLI).

### Installation
See the NexPloit CLI – Installation section for installation instructions.

### Usage Examples
See usage examples in the NexPloit CLI 🡺 Usage Examples section.

### FAQs – On-Premises Repeater
#### What is the maintenance / patching frequency?
The NexPloit engine does not require any maintenance or patching from the client side. It is in the cloud and therefore is always updated automatically. 

The Repeater does require periodic updates. These can be performed either manually (using a simple CLI update command) or automatically (if the Repeater is installed during a build as part of the CI process).

#### Can I use a single machine with a Repeater in order to access multiple internal targets?
Yes, on the condition that the local machine on which the Repeater is installed has access to the internal applications. In this case, multiple scans can be performed using the same Repeater.

In addition, by installing the Repeater on a personal computer, it is possible to scan locally running applications. This is useful for developers who want to perform quick tests without deploying code.

#### Do I need to change firewall / port settings for the Repeater?
No. Using the Repeater does not require any changes to your network’s inbound traffic settings, because  all the generated traffic is based on outbound requests from inside the network.

#### I have a Firewall between various internal applications. How do I handle this?
You have the following options, to – 
* Install a separate Repeater behind the relevant firewalls in order to avoid the need for whitelisting.
* Use open ports between the internal applications.
* Configure new ports for the Repeater.

#### Will a Firewall affect the scan results or add false positives?
The Repeater does not contain any complicated logic. All decision making and removal of false-positives using active validation is performed by the engine in the cloud. This means that all the computational and advanced algorithms are available to scans that use a Repeater, in the same way as for scans that are deployed as a SaaS or in the private cloud.


## Private Cloud
### Overview
Unlike the standard SaaS offering that uses a multi-tenant architecture for the databases and static network configurations, the Private Cloud provides a completely separate, configurable cloud environment for your organization.

> [!WARNING|label:Important]
The private cloud instance is hosted on the NeuraLegion infrastructure.

The Private Cloud’s separate, non-multi-tenant environment offers the following benefits over a standard SaaS environment –
* Separate databases at the instance level. Standard SaaS only accommodates some databases at a logical level.
* Full control over network level configurations, such as –
    * Load handling.
    * Network-level access configurations (IP allow/deny).
    * Options for site-to-site VPN setup.
* Improved security in lateral-movement scenarios.

### How Does a Private Cloud Deployment Work?
All relevant components, which may include sensitive information, such as databases, engines and so on, are deployed in a separate cloud instance that is managed by NeuraLegion. Currently, the Private Cloud is deployed on AWS. Deployment to other cloud vendors can be added, as needed. NeuraLegion fully manages the deployment process for you.

> [!WARNING|label:Important]
If you are interested in other deployment options, contact your sales representative.

![private-cloud-chart](media/private-cloud-chart.png ':size=100%')

### FAQs – Private Cloud
#### Will using a private cloud mean that I don’t need to use a Repeater?
If the only reason for using a Repeater is to control network flow, and if a site2site VPN tunnel can be created that enables full access from the private cloud to the organization’s network, then a Repeater is not needed. Otherwise, a Repeater is still needed in order to enable secure access to a local target from the cloud.

#### Do I still need to use whitelisting in my firewall if I have a private cloud?
Yes, you must use whitelisting in your firewall with a private cloud, unless a site-to-site VPN is configured and used.

#### Can I use a private data center instead of a private cloud?
You cannot use a private data center instead of a private cloud. This option is not supported at this time.

#### Will NeuraLegion have access to my vulnerabilities that it detects?
A NeuraLegion representative cannot access your scan results without your permission. If support is needed, then an organization’s owner can invite a NeuraLegion engineer to access your vulnerabilities in order to provide support.
