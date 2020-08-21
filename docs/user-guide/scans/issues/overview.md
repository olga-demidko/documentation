# Discovered Issues (Results)
After clicking on a specific finding under **DISCOVERED ISSUES**, you will reach the issue page.

### 🌎 Section Map <!-- {docsify-ignore} -->
- [Issue Details](#issue-details)
- [Quick Navigation Between Issues](#quick-navigation-between-issues)
- [Download Issue Script](#download-issue-script)
- [Re-Test Issue](#re-test-issue)
- [Mark Issue as Resolved](#mark-issue-as-resolved)
- [Assign Users To Issue](#assign-users-to-issue)

<hr style="height:2px;background-color:#d1d3d4">

## Issue Details
Here you will see general useful information about the issue:
1. **Status** - Current status of this specific issue, can be [marked as resolved](#mark-as-resolved) at any point.
2. **Asignees** - Users that are assined to this specific issue, see [assign users to issue](#assign-users-to-issue) for more info.
3. **Details** - A short description of the specific issue, with information about what happened dynamically generated at the bottom of the explanation.
4. **Remedy Suggestions** - A short explanation about how this issue should be fixed.
5. **Possible Exposure** - A brief non-technical explanation about what kind of impact this specific issue might have on the application in case of a malicious breach.
6. **CVSS Scoring** - A summerized [Common Vulnerability Scoring System](https://en.wikipedia.org/wiki/Common_Vulnerability_Scoring_System ) score for this specific issue.
7. **Resources** - Additonal resources in case more detailed explantions are required.

![issue_details](media/issue-details-overview.png ':size=45%')

#### Additional Information <!-- {docsify-ignore} -->
Here you will see specific useful technical information about the issue:

8. **Additional Information** - When relevant, more technical inforamtion about the specific issue, which includes: database emumeration info, targeted DOM elemnet info, etc.
9. **Request** - All the request info, in a diff-like view to show what was changed in the request to execute this kind of attack.
10. **Screenshot** - When relevent, a screenshot demonstration of the attack execution.
11. **Response** - All the response info.

!> **Protip:** You can use the **Copy as cURL** button at the top right of the request display, in case you want to execute it manually.

![additiona_info](media/issue-details-additional-info.png ':size=45%')

## Quick Navigation Between Issues
You can quickly navigate between issues by clicking on the title, which will open a scrollable list of all the issues in this scan.

![quick_navigation_1](media/issue-details-quick-navigation-01.png ':size=45%')
&nbsp;&nbsp;&nbsp;&nbsp;
![quick_navigation_2](media/issue-details-quick-navigation-02.png ':size=45%')


## Download Issue Script
You can download a specific issues details as a `JSON` file, to be used later.

![download_script](media/issue-details-download-script-button.png ':size=45%')

Example script:
```js
{
  "method": "GET",
  "url": "http://34.207.67.27:8080/wavsep/active/LFI/LFI-Detection-Evaluation-GET-200Error/Case02-LFI-FileClass-FilenameContext-Unrestricted-FileDirective-DefaultFullInput-AnyPathReq-Read.jsp?target=file%3A%2F%2F..%5C..%5C..%5C..%5C..%5C..%5C..%5C..%5C..%5C..%5C..%5C..%5C..%5C..%5C..%5C%2Fetc%2Fpasswd%3Froot%2Fapache-tomcat-8.0.27%2Fwebapps%2Fwavsep%2Factive%2FLFI%2FLFI-Detection-Evaluation-GET-200Error%2Fcontent.ini",
  "headers": {
    "X-Scanner": "NexPloit",
    "Accept-Encoding": "identity",
    "User-Agent": "Mozilla/5.0 (X11; Linux x86_64; rv:68.0) Gecko/20100101 Firefox/68.0",
    "Cookie": "JSESSIONID=123; userinput=EmptyValue; parameter=\"http://M5BBaIfz2yls0KrjzzrN5Q?com\""
  }
}
```

## Re-Test Issue
You can modify and re-test a specific issue by using the **script editor** at the top toolbar.

![retest_script](media/issue-details-modify-script-button.png ':size=45%')

In the script editor, you can edit any of the specific request fields and send it again by clicking on **Execute**

![request_editor_script](media/issue-details-request-editor.png ':size=45%')

## Mark Issue as Resolved
You can mark an issue as resolved, by clicking on the **Mark As Resolved** button at the top toolbar.

![mark_resolved_button](media/issue-details-mark-resolved-button.png ':size=45%')

## Assign Users To Issue
You can assign a specific user to a specific issue, simply click on the **Assignee** field, select the relevant user, and clock on the **Plus** button to the right of the field. You can un-assign the user by clicking on the **Cross** button to the right of a user name.

![assign_user](media/issue-details-assign-user-01.png ':size=45%') 
&nbsp;&nbsp;&nbsp;&nbsp;
![assign_user](media/issue-details-assign-user-02.png ':size=45%')
