# Reviewing Scan Details
* To view the details of a scan –
    1. Select the Scans option in the left pane to display the Scans List. Each scan appears as a single row.
    2. Click on the row of a scan to display its details.\
    ![Scans-List](media/scans-list.png ':size=45%')\
    The following sections of information are displayed about the selected scan –\
    ![Scan-Info](media/scan-info.png ':size=45%')
    * [SCAN SUMMARY](#SCAN-SUMMARY)
    * [SCAN PROGRESS](#SCAN-PROGRESS)
    * [SITE MAP](#SITE-MAP)
    * [DISCOVERED ISSUES](#DISCOVERED-ISSUES)
    * [RESPONSE STATUSES](#RESPONSE-STATUSES)
    * [TECHNICAL STACK](#TECHNICAL-STACK)
    * [USER COMMENTS](#USER-COMMENTS-For-a-Scan)

## SCAN SUMMARY
This section provides a summary of the runtime parameters of the scan, such as the **Modules** and **Discovery type** of the scan, its lapse time and the quantity of entry points, parameters and requests detected so far.\
![Scan-Summary](media/scan-summary.png ':size=45%')\
You can enter comments describing the scan at the **USER COMMENTS** section at the bottom of the page.

## SCAN PROGRESS
This section shows the progress of the scan, how many tests have been completed and how many still remain.\
![Scan-Progress](media/scan-progress.png ':size=45%')

## SITE MAP
This section shows a map representing the scope of the scan. This site map shows all the parts of the application that Nexploit has identified and scanned.\
![Site-Map](media/site-map.png ':size=45%')

## DISCOVERED ISSUES
See [Handling Discovered Issues](guide/np-web-ui/scanning/discovered-issues.md) for description of the discovered issues list, the details of each discovered issue and the options for viewing, downloading, retesting, marking and resolved and assigning an issue to another user.\
![Discovered-Issues](media/discovered-issues.png ':size=45%')
* To open a specific issue –
    1. Click on the relevant group. A list of all the issues of that category is displayed.
    2. Click on the relevant issue to see the all [issue’s details](guide/np-web-ui/scanning/discovered-issues.md#Reviewing-Discovered-Issue-Details).

## RESPONSE STATUSES
This section shows all the kinds of responses received by Nexploit got from the application during the scan and the quantity of each. Check this section to determine whether there may be problems with the scan. For example, if the section shows that Nexploit receives almost all 404 responses, it may indicate that Nexploit is being blocked by a WAF, or that there is a problem with authentication (it may have expired).\
![Response-Statuses](media/response-statuses.png ':size=45%')

## TECHNICAL STACK
This section shows the technical stack that the scan has detected is being used by the application. For example, which programming language is used, the type of database and/or web server, the front-end stack and so on. 

Discovery of the technical stack by Nexploit may demonstrate to you how easily an external entity can discover it. As a result, you may decide to place more protection around the technical stack.

## 	USER COMMENTS – For a Scan
The section at the bottom of the page enables you to enter comments and notes describing the scan, notes for yourself or notes for other people in the organization. You can format the comment using markdown or using the provided formatting tools. To mention other users in your organization use the @ symbol. 

After the comment is ready click the **Preview** button to display it or the **Comment** button to post the comment. After a comment has been entered a new section appears at the bottom called **ALL COMMENTS** showing all previously entered comments.\
![User-Comment](media/user-comment.png ':size=45%')\
To include this comment in the scans report, check the **Include in report** checkbox under the comment.\
![Include-Comment-in-Report](media/inc-comment-in-report.png ':size=45%')
