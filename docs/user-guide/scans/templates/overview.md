# Scan Templates
Scan Templates make the process of initiating a scan quicker, they allow you to use predefined scan settings when creating a new scan.

### Quick Start {docsify-ignore}
- [Overview](#overview)
- [Creating a New Template](#creating-a-new-template)
- [Editing a Template](#editing-a-template)
- [Template Details](#template-details)
- [Deleting a Template](#deleting-a-template)

<hr style="height:2px;background-color:#d1d3d4">

## Overview
To see and edit your scan Templates, go to the "Scan Templates" tab from your dashboard.

![go-to-scan-profiles-tab](media/scan-profiles-01.png ':size=45%')

You'll be taken to your scan Templates management tab.

![scan-profiles-tab](media/scan-profiles-02.png ':size=45%')

There are 3 default templates:
- **Fast Scan** - Preconfigured optimized scan, the engine will determine automatically which tests to run, based on the data types that are detected. Some tests will be skipped in favour of speed.
- **Comprehensive Scan** - All the possible tests will be performed during the scan. This is the most thorough scan, which accordingly takes the longest time to finish
- **API Scanning** - Preconfigured tests that are relevant for API targets

## Creating a New Template

To create a new Template, simply click on the ![plus](media/plus_button.png ':size=2%') button at the top of the page.

![scan-profile-new](media/scan-profiles-05.png ':size=45%')

Now fill in the your desired settings:

1. Give the Template a name.
2. (optional) Give your Template a description.
3. Select the discovery type for the Template.
4. Depending on the discovery type you have selected, either add link(s) for the crawler, upload a HAR file or upload/add a link to an open API specification.
5. Select the tests to run with this Template.
6. Configure additional settings for the scans taht'll run with this Template.

Once done, just click the ![save-profile](media/save-profile_button.png ':size=8%') button.

![scan-profile-configure](media/scan-profiles-06.png ':size=45%')

## Editing a Template

To edit a Template, simply click on its name.

!> **Note:** You can't edit the default Templates.

![scan-profile-edit](media/scan-profiles-07.png ':size=45%')

Now make the changes you'd like to and click the ![update-profile](media/update-profile_button.PNG ':size=8%') button.

![scan-profile-update](media/scan-profiles-08.png ':size=45%')

## Template Details

To see details about a specific Template, simply click on its name.

![scan-profile-click](media/scan-profiles-03.png ':size=45%')

In the pop up window, you'll see all the information about the scan profile - its name, description, discovery types, which tests it's set to run and the additional settings it applies to the scan.

!> **Note:** If you are looking at one of the default Template, you won't be able to edit them.

![scan-profile-details](media/scan-profiles-04.png ':size=45%')

# Deleting a Template

To delete a Template, click the ![dots](media/dots_button.png ':size=1%') button next to the Template's name and then choose the "Delete" option.

![scan-profile-delete](media/scan-profiles-09.png ':size=45%')