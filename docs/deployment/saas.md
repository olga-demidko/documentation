# SaaS Solution
By using NeuraLegion’s **SaaS** offering, your organization will not need to worry about complicated deployments.

### 🌎 Section Map <!-- {docsify-ignore} -->
- [Overview](#overview)
- [How it Works](#how-it-works)
- [Requirements](#requirements)
- [Deployment Options](#deployment-options)
- [FAQ](#faq)

<hr style="height:2px;background-color:#d1d3d4">

## Overview
By using NeuraLegion’s **SaaS** offering, your organization will not need to worry about complicated deployments.

!> The standard **SaaS** solution uses a multi-tenant architecture for the databases, and static network configurations

## How it Works
By using our **SaaS** deployment option, you will not need to install anything locally!

Simply log in to our platform, point at the target application you would like to scan, and that’s it. Our state of the art AIAST® powered engines will start scanning the target for vulnerabilities. You will receive immediate reports on found issues, with no False-Positives!

![standard-saas-architecture](media/standard-saas-architecture.svg ':size=45%')

## Requirements
In order to start scanning, please make sure that the following applies:
- The target application can be accessed from the internet
- Our Static IP (see below) is whitelisted by your WAF / Firewall (recommended to avoid auto-blacklisting our solutions)

!> <font color="red" size="3"><b>IMPORTANT:</b> We have two public static IPs:
<br>
&emsp; American: <b>34.228.94.55</b>
<br>
&emsp; European: <b>52.215.195.32</b></font>

## Deployment Options
Currently, deployment is possible on AWS, but deployment to other cloud vendors can be added if needed for specific scenarios. NeuraLegion fully manages the deployment process for you.

!> **If you are interested in other deployment options, please reach out to your sales contact.**

## FAQ
#### No False Positives? How is that possible? <!-- {docsify-ignore} -->
It is quite simple, our solutions do not “just scan”, they **Interact** with the target application. Which means that every reported vulnerability is **validated in real time**. And if it cannot be validated, it will not be reported, saving you from unnecessary noise and many hours of manual results triage.

#### Will NeuraLegion have access to my vulnerabilities that are found? <!-- {docsify-ignore} -->
Only if the owner of the organization will invite one of NeuraLegion’s engineers to the organization for support needs. A NeuraLegion representative will never be able to access your scan results without your permission.
