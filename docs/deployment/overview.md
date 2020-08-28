# Deployment Options
**NeuraLegion offers 3 deployment configurations:**
- [SaaS offering hosted on a few different hosting platforms](deployment/saas.md)
- [On-prem agent (AKA Repeater)](deployment/repeater.md)
- [Private cloud offering](deployment/private-cloud.md)

![cloud-architecture](media/cloud-architecture.png ':size=45%')

## Data Security FAQ <!-- {docsify-ignore} -->
#### What kind of information does NeuraLegion access DURING a scan? <!-- {docsify-ignore} -->
During a scan, our solutions collect both application data and user data, which are used as part of the scan.
- **Application Data** - Refers to anything related to the application structure and functionality, for example parameter names and object strucure. This infomation is used to determine the application's attack surface.
- **User Data** - Referes to specific user information, for example values entered into parameters or authentication data. This information is used to improve the scan quality and results, such as identify parameter types and re-login automatically if needed.

#### What kind of information does NeuraLegion store AFTER a scan? <!-- {docsify-ignore} -->
Our cloud Machine Learning engine does not store the **User Data** of customers after the scan. Any user data of the scan is stored solely in memory, and is deleted as the scan ends. **Application Data** is being stored anonymously after the scan for the purpose of improving our Machine Learning engines.

In addition, NeuraLegion store the scan results after the scan, but we do not have access to it unless the customer shares it with us.

#### How does NeuraLegion ensure data security and privacy? <!-- {docsify-ignore} -->
We at NeuraLegion put the security and privacy of our customers at our top priority. 

We follow industry best-practices and standards in keeping data at rest as safe as possible. Our data storage protocols include: encryption, access control, data segregation (private separate instance for each scan per client) and more.

#### Will NeuraLegion share the finding reports with anyone else? <!-- {docsify-ignore} -->
No, only you have access to your reports. You can choose to download them or use them within our system, with full control of who has access to them. 

Keep in mind, if you choose to delete the scans from the system, they will be gone forever. NeuraLegion does not have access to them and therefore does not have the ability to restore the report information once deleted.
