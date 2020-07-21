# Scan Details

- [Scan Summary](#scan-summary)
- [Scan Progress](#scan-progress)
- [Site Map](#site-map)
- [Discovered Issues](#discovered-issues)
- [Response Statuses](#response-statuses)
- [Technical Stack](#technical-stack)
- [User Comments](#user-comments)

<hr style="height:2px;background-color:#d1d3d4">

## Overview
To see details about a scan simply click on your desired scan in your dashboard.

![Scan Details 01](media/scan-details-01.png ':size=45%')


## Scan Summary
Now you'll be taken to the scan page. Here you can see information about the scan (is it done yet, number of vulnerabilities found, list of detected vulnerabilities, the response statuses the system was getting from your application and more).

![Groups 02](media/scan-details-02.png ':size=45%')

You can leave comments about the scan at the bottom of the page.

## Scan Progress
In this panel you can see how the scan is prgressing, how many tests have been completed and how many are still left.

![progress](media/scan-progress.png ':size=45%')

## Site Map
The sitemap shows the scope of the scan, here you can see all the parts of your application that NexPloit has identified and scanned.

![sitemap](media/sitemap.png ':size=45%')

## Discovered Issues
When the scanner finds a new issues, it will immediately appear under the **DISCOVERED ISSUES** panel, even if the scan is still running. Here you will see all the types of discovered issues and their quantitiy.

!> **Pro Tip:** You can use the filters at the top right to quickly find the issues you want.

![discovered_issues_closed](media/discovered-issues-closed.png ':size=45%')

To open a specific issue, click on the relevant group. A list of all the issues of that category will open, now click on the relevenat issue to see the all [issue details](user-guide/scans/issues/overview.md) about it.

![discovered_issues_open](media/discovered-issues-opened-category.png ':size=45%')

## Response Statuses
In the Response Statueses panel you'll be able to see all the kinds of responses NexPloit got from yout application during the scanning process, and their count. This can be used to indicate problems with the scan, for example if you'll notice that NexPloit gets almost only 404 responses, this could indicates that Nexploit is being blocked by a WAF, or that there is a problem with authentication (it could have expired).

![response_statuses](media/response_statuses.png ':size=45%')

## Technical Stack
At the "Technical Stack" panel you'll see what NexPloit has detected your application is using for its technical stack, for example - which programming language is used, what kind of database and/or web server, the front-end stack etc. This can be useful to see how easy it is to discover your technical stack so if you want to cover something up and NexPloit has detected it, it means you didn't cover it up properly.


## User Comments
At the bottom of the page there is a section for user comments, here you can leave notes about the scan for yourself or others in your organization. You can format the comment using markdown or with the formatting tools, and mention other users in your organization using "@". Once your comment is ready just clock the ![New Scan](media/comment_button.png ':size=7%') button.

![write_comment](media/write_comment.png ':size=45%')

When your comment is published you'll see it at the very bottom of the page. You'll also have the option to include it in the reoprts of the scan, simply tick the textbox under your comment.

![published_comment](media/published_comment.png ':size=45%')