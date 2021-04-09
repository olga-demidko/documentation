# Handling Discovered Issues

## Reviewing the Discovered Issues List
1. Select the **Scans** option in the left pane to display the Scans List. Each scan appears as a single row.
2. Click on the row of a scan to display its details.
3. Scroll down to the **DISCOVERED ISSUES** section, which shows a row representing each type of issue (vulnerability) discovered by the scan and the quantity of each. 

> [!TIP|label:Pro Tip]
The top of this section provides various options for filtering the discovered issues that are displayed.

![Discovered-Issues](media/discovered-issues-fullscreen.png ':size=45%')

## Reviewing Discovered Issue Details
To display the detailed results of each discovered issue –
1. Select the **Scans** option in the left pane to display the Scans List. Each scan appears as a single row.
2. Click on the row of the scan to display its details page.
3. Scroll down to the **DISCOVERED ISSUES** section, which shows a row representing each type of issue (vulnerability) discovered by the scan and the quantity of each. 
4. Click on the issue type row **<span style="color:#FF0000;">(1)</span>** to display a row for each discovered issue of that type.
5. To display details about a specific issue, click on its row **<span style="color:#FF0000;">(2)</span>**.

![Discovered-Issue-Details](media/discovered-issue-details.png ':size=45%')

The following sections of information are displayed about a selected issue –
* [ISSUE OVERVIEW](#ISSUE-OVERVIEW)
* [ADDITIONAL INFORMATION](#ADDITIONAL-INFORMATION)
* [REQUEST](#REQUEST)
* [RESPONSE](#RESPONSE)
* [SCREENSHOT](#SCREENSHOT)
* [USER COMMENTS](#USER-COMMENTS-For-a-Discovered-Issue)

### ISSUE OVERVIEW
This section provides general useful information about the issue –\
![Issue-Overview](media/issue-overview.png ':size=45%')
1. **Status –** Specifies the current status of this specific issue. The status of this issue is **Unresolved** until it is [marked as **Resolved**](#Marking-an-Issue-as-Resolved).
2. **Assignees –** Specifies the users that are assigned to this specific issue. See [Assign Users To an Issue](#Assign-a-User-to-an-Issue) for more information.
3. **Details –** Provides a short description of this issue. It also displays dynamically generated information about what happened at the bottom of the explanation. 
4. **Remedy Suggestions –** Provides a short explanation about how this issue should be fixed.
5. **Possible Exposure –** Provides a brief non-technical explanation about what kind of impact this specific issue might have on the application in case of a malicious breach.
6. **CVSS Scoring –** Provides a [Common Vulnerability Scoring System](https://en.wikipedia.org/wiki/Common_Vulnerability_Scoring_System) score (CVSS) summarizing this specific issue.
7. **Resources –** Provides references to resources in case more detailed explanations are required.

### ADDITIONAL INFORMATION
When relevant, this section provides additional technical information about the specific issue, which includes – database enumeration information, targeted DOM element information and so on.

![Additional-Information](media/additional-info.png ':size=45%')

### REQUEST
Displays the request info in a diff-like view that shows what was changed in the request in order to execute this type of attack.
> [!TIP|label:Pro Tip]
You can use the Copy as CURL button at the top right of the request display in order to execute it manually.

### RESPONSE
Provides all the response information.

### SCREENSHOT
When relevant, shows a screenshot demonstrating the attack execution.

### USER COMMENTS – For a Discovered Issue
The section at the bottom of the page enables you to enter comments and notes describing the discovered issue for yourself or notes for other people in the organization. You can format the comment using markdown or using the provided formatting tools. To mention other users in your organization use the @ symbol. 

After you enter the comment, click the **Preview** button to display it. Click the **Comment** button to post the comment. After a comment has been posted, a new section appears at the bottom called **ALL COMMENTS** showing all previously posted comments.

![Comment](media/user-comment.png ':size=45%')\
To include this comment in the scans report, check the **Include in report** checkbox under the comment.

## Navigating Quickly Between Issues
To quickly navigate between issues click the title of an issue to open a scrollable list of all the issues in this scan.

![Navigating-Issues](media/navigating-issues.png ':size=45%')

## Downloading an Issue’s Script
To download a specific issue’s details as a `JSON` file to be used later click the **Download script** ![Download-Script](media/download-button.png ':size=1%') button.

![Download-Script](media/download-script.png ':size=45%')

Example script:

```JSON
{
  "method": "GET",
  "url": "http://34.207.67.27:8080/wavsep/active/LFI/LFI-Detection-Evaluation-GET-200Error/Case02-LFI-FileClass-FilenameContext-Unrestricted-FileDirective-DefaultFullInput-AnyPathReq-Read.jsp?target=file%3A%2F%2F..%5C..%5C..%5C..%5C..%5C..%5C..%5C..%5C..%5C..%5C..%5C..%5C..%5C..%5C..%5C%2Fetc%2Fpasswd%3Froot%2Fapache-tomcat-8.0.27%2Fwebapps%2Fwavsep%2Factive%2FLFI%2FLFI-Detection-Evaluation-GET-200Error%2Fcontent.ini",
  "headers": {
    "X-Scanner": "Nexploit",
    "Accept-Encoding": "identity",
    "User-Agent": "Mozilla/5.0 (X11; Linux x86_64; rv:68.0) Gecko/20100101 Firefox/68.0",
    "Cookie": "JSESSIONID=123; userinput=EmptyValue; parameter=\"http://M5BBaIfz2yls0KrjzzrN5Q?com\""
  }
}
```

## Retesting an Issue
Retesting at issue creates a separate scan entity that is a duplicate of the selected scan. Initially, the settings are identical, but can be modified by you without affecting the original scan settings.

To modify and re-test a specific issue by using the script editor –
1. Click the **Modify script** ![Modify-Script-Button](media/modify-button.png ':size=3%') button.\
![Modify-Script](media/modify-script.png ':size=45%')
2. In the script editor, you can edit any request field and retest it (scan it again) by clicking on the **Execute** button.\
![Execute-Script](media/execute-script.png ':size=45%')

## Marking an Issue as Resolved
To mark an issue as resolved click the **Mark As Resolved** ![Mark-As-Resolved-Button](media/resolved-button.png ':size=3%') button at the top toolbar.

![Mark-As-Resolved](media/mark-as-resolved.png ':size=45%')

## Assign a User to an Issue
To assign a specific user to a specific issue –
1. Click on the Assignees field, as shown below –\
![Assignees-Field](media/assignees-field.png ':size=45%')
2. Select the relevant user.
3. Click the **<span style="color:#FF0000;">+</span>** button to the right of the field.\
> [!NOTE|label:Note]
You can unassign the user by clicking on the X button to the right of a user’s name, as shown below –\
![Unassign-User](media/unassign-user.png ':size=45%')