# SaaS
## Overview – No installation
Using NeuraLegion’s SaaS deployment option is simple. There is no need to install anything locally. 
Simply log in to the NeuraLegion platform and select the target application to be scanned. 

## How Does a SaaS Deployment Work?
NeuraLegion’s state-of-the art AIAST®-powered engines begin scanning the target for issues. Reports that show identified issues start displaying immediately, with zero false-positives.
The standard SaaS solution uses a multi-tenant architecture for the databases and static network configurations.

![saas-chart](media/saas-chart.png ':size=40%')

## Before You Begin
Before scanning, ensure that –
* The target application can be accessed from the Internet.
* NeuraLegion’s static IP (see below) is whitelisted by your WAF/firewall (recommended in order to avoid auto-blacklisting of NeuraLegion’s solutions).

> [!WARNING|label:Important]
NeuraLegion has the following public static IPs:\
&nbsp;&nbsp;&nbsp;&nbsp;**U.S.** – **54.205.119.224** <br>
&nbsp;&nbsp;&nbsp;&nbsp;**Europe** – **54.75.37.42**

## Deployment Options
Currently, deployment is only possible on AWS. Deployment to other cloud vendors can be added, if needed, for specific scenarios. NeuraLegion fully manages the deployment process for you.

If you are interested in other deployment options, contact your sales representative.

## FAQs – SaaS Deployment
### Why aren’t there any false positives?
NeuraLegion’s solutions do not simply scan, but rather interact with the target application. This means that every reported vulnerability is validated in real time. If a vulnerability cannot be validated, it is not reported, thereby saving you from unnecessary noise and hours of manual labor.

### Will NeuraLegion have access to the vulnerabilities (issues) that it detects in my applications?
A NeuraLegion representative cannot access your scan results without your permission. If support is needed, then an organization’s owner can invite a NeuraLegion engineer to access your vulnerabilities in order to provide support.
