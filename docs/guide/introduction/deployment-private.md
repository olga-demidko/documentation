# Private Cloud
## Overview
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

## How Does a Private Cloud Deployment Work?
All relevant components, which may include sensitive information, such as databases, engines and so on, are deployed in a separate cloud instance that is managed by NeuraLegion. Currently, the Private Cloud is deployed on AWS. Deployment to other cloud vendors can be added, as needed. NeuraLegion fully manages the deployment process for you.

> [!WARNING|label:Important]
If you are interested in other deployment options, contact your sales representative.

![private-cloud-chart](media/private-cloud-chart.png ':size=40%')

## FAQs – Private Cloud
### Will using a private cloud mean that I don’t need to use a Repeater?
If the only reason for using a Repeater is to control network flow, and if a site2site VPN tunnel can be created that enables full access from the private cloud to the organization’s network, then a Repeater is not needed. Otherwise, a Repeater is still needed in order to enable secure access to a local target from the cloud.

### Do I still need to use whitelisting in my firewall if I have a private cloud?
Yes, you must use whitelisting in your firewall with a private cloud, unless a site-to-site VPN is configured and used.

### Can I use a private data center instead of a private cloud?
You cannot use a private data center instead of a private cloud. This option is not supported at this time.

### Will NeuraLegion have access to my vulnerabilities that it detects?
A NeuraLegion representative cannot access your scan results without your permission. If support is needed, then an organization’s owner can invite a NeuraLegion engineer to access your vulnerabilities in order to provide support.
