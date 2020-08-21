# Private Cloud Solution
By using NeuraLegion’s **Private Cloud** offering, your organization will get a dedicated, isolated, NexPloit service environment.

### 🌎 Section Map <!-- {docsify-ignore} -->
- [Overview](#overview)
- [How it Works](#how-it-works)
- [Benefits Over the Standard SaaS Offering](#benefits-over-the-standard-saas-offering)
- [Deployment Options](#deployment-options)
- [FAQ](#faq)

<hr style="height:2px;background-color:#d1d3d4">

## Overview
Unlike the standard SaaS offering, which uses a multi-tenant architecture for the databases, and static network configurations, the **Private Cloud** offer provides you with a completely separate, configurable, cloud environment for your organization.

!> The **Private Cloud** instance is still hosted on the neuraLegion infrastructure.

## How it Works
All the relevant components that may include sensitive information, such as Databases, Engines, etc., are deployed in a separate cloud instance, which is managed by NeuraLegion.

Currently the **Private Cloud** offer is deployed on **AWS**, but deployment to other cloud vendors can be added as needed.

![cloud-architecture.png](media/cloud-architecture.svg ':size=45%')


## Benefits Over the Standard SaaS Offering
A completely separate environment (not multi-tenant), which includes:
- Separate Databases on the instance level, not just logical level on same Database like the standard SaaS offer
- Full control over network level configurations such as: 
  - Load handling
  - Network level access configurations (IP allow/deny)
  - Option for site2site VPN setup
- Improved security against lateral movement scenarios

## Deployment Options
Currently, deployment is possible on AWS, but deployment to other cloud vendors can be added if needed for specific scenarios. NeuraLegion fully manages the deployment process for you.

!> **If you are interested in other deployment options, please reach out to your sales contact.**

## FAQ
#### Will using a Private Cloud remove the need to use a Repeater? <!-- {docsify-ignore} -->
If the reason for using the Repeater is only to control network flow, and a site2site VPN tunnel can be created which will allow full access from the private cloud into the organization’s network, then the repeater is not needed. Otherwise, the Repeater is still needed for secure access to a local target from the cloud.

#### Do I still need to use whitelisting in my Firewall if I have a Private Cloud? <!-- {docsify-ignore} -->
Yes, unless a Site2Site VPN is configured and used.

#### Can I use a private data center instead of a private cloud? <!-- {docsify-ignore} -->
This is not an option we offer at this time.

#### Will NeuraLegion have access to my vulnerabilities that are found? <!-- {docsify-ignore} -->
Only if the owner of the organization will invite one of NeuraLegion’s engineers to the organization for support needs. A NeuraLegion representative will never be able to access your scan results without your permission.
