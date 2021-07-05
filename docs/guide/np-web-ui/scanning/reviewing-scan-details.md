# Reviewing Scan Details

Nexploit allows you to monitor the scan progress, check the setup and runtime parameters, as well as view the scan results. All these options are available for each scan selected on the **Scans** or **Scans History** page. 

The scan details are provided in the following sections:
* [Scan summary](#scan-summary)
* [Scan progress](#scan-progress)
* [Sitemap](#sitemap)
* [Entry points](#entry-points)
* [Discovered issues](#discovered-issues)
* [Response statuses](#response-statuses)
* [Technical stack](#technical-stack)
* [User comments](#user-comments)


### Scan summary
This section provides a summary of the runtime parameters of a scan, such as the module and discovery type of the scan, its lapse time, the number of discovered issues and total requests sent.

You can also check the initial settings of the scan in the Settings on create tab.

![Scan-Summary](media/scan-summary.png ':size=45%')

You can enter comments describing the scan at the **USER COMMENTS** section at the bottom of the page.

### Scan progress
This section shows the scan progress, how many tests have been completed and how many still remain.

You can view the notifications sent by the engine during the scan and download them. Nexploit also provides the option of downloading the engine log in the relative tab.

![Scan-Progress](media/scan-progress.png ':size=45%')

### Sitemap

This section shows a map representing the scope of the scan (attack surface). This sitemap shows all the parts of the application that Nexploit has identified and scanned.

![Sitemap](media/sitemap.png ':size=45%')

### Entry points

This section shows all entry points discovered and scanned by Nexploit. You can open an overview for each entry point by selecting it from the table. The overview provides the following details:

* Test run against the entrypoint
* Tested scenarios
* Parameters
* Statuses
* Request
* Response 

The tested scenarios represent the number of compromising requests sent to the application to reveal the vulnerability. The information on the tested scenarios is provided in the engine log that you can download from the **SCAN PROGRESS** section. 

![Entry-points](media/entry-points.png ':size=45%')

### Discovered issues

This section shows all the issues (vulnerabilities) detected during the scan. All the issues are grouped by issue type. To open the list of issues related to a certain issue type, select the relevant issue type in the **DISCOVERED ISSUES** table.  You can open the report on a specific issue by selecting it from the opened issue list. Each report provides detailed information about the detected issue and the guidelines on how to fix and prevent the issue.

To learn how to read and download the issue report, mark the issue as resolved, or assign the issues to another user, please see [Handling Discovered Issues](/guide/np-web-ui/scanning/discovered-issues.md).  

![Discovered-Issues](media/discovered-issues.png ':size=45%')

### Response statuses

This section shows the statuses of the responses received by Nexploit from the application during the scan, as well as the number of responses per each status. Check this section to determine whether there may be problems with the scan. For example, if the section shows that Nexploit receives mostly 404 responses, it may indicate that Nexploit is being blocked by a WAF, or that there is a problem with authentication (it may have expired).

![Response-Statuses](media/response-statuses.png ':size=45%')

### Technical stack 

This section shows the technical stack that the scan has detected is being used by the application. For example, which programming language is used, the type of database and/or web server, the front-end stack, and so on.

The discovery of the technical stack by Nexploit may demonstrate to you how easily an external entity can discover it. As a result, you may decide to improve the protection of the technical stack.

![technical-stack](media/tech-stack.png ':size=45%')

### User comments

The section at the bottom of the page enables you to enter comments and notes describing the scan, notes for yourself, or notes for other members of the organization. You can format the comment using markdown or using the provided formatting tools. To mention other users in your organization, use the @ symbol. 

After the comment is ready, click **Preview** to check the final view of the comment or **Comment** to post the comment immediately. After the comment has been posted, a new section called **TOTAL COMMENTS** appears at the bottom of the page. This section shows all comments posted previously.

![User-Comment](media/user-comments.png ':size=45%')

To include this comment in the scan report, select the **Include in report** checkbox under the comment.
