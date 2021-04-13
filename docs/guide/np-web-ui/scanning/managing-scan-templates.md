# Managing Scan Templates
## Scan Templates
A scan template enables you to save and reuse a set of scan settings so that you can start another scan more quickly. Nexploit provides the following default scan templates:

* **Deep Scan** – All possible tests are performed during the scan. This is the most thorough scan, which takes the longest time to complete.
* **Light Scan** – This is a preconfigured optimized scan during which the engine automatically determines which tests to run, based on the data types that are detected. Some tests will be skipped in favor of speed.
* **Passive Scan** - The engine selects only host-based passive tests to be run.
* **API Scanning** – Predefined tests that are relevant for API targets.


The following section provides guidelines for the following options:
* [Displaying Scan Templates](#Displaying-Scan-Templates)
* [Creating a New Template](#Creating-a-New-Template)
* [Editing a Template](#Editing-a-Template)
* [Deleting a Template](#Deleting-a-Template) 

## Displaying Scan Templates
To display scan templates, follow these steps:
1. In the left pane, select the **Scans** option. 
2. In the upper right corner, click **My Templates**.

    ![My-Templates](media/my-templates.png ':size=45%')

    The list of default and custom scan templates is displayed.

    ![Scan-Templates](media/templates-list.png ':size=45%')

3. To display the details of a specific template, select it from the list.<br> 
   On the popup, you can view all the information about this scan template, including:
   * Scan details
   * Scan targets
   * Network and application settings
   * Security tests to be run 

   ![Scan-Templates](media/templates-list.png ':size=45%')

## Creating a New Template
To create a new template, follow these steps:
1. At the top of the **Scan Templates** page,  click ![Plus-Button](media\plus-dark.png ':size=2%').

    ![New-Template](media\add-scan-template.png ':size=45%')

2. On the **CREATE SCAN TEMPLATE** popup, define the settings for a new scan template. These are the same [settings as for creating a new scan](guide/np-web-ui/scanning/creating-new-scan.md). 

    ![New-Template](media\new-template-popup.png ':size=45%')

3. Once you complete the setup, click **Create Template** to save the defined scan template.

## Editing a Template
To edit a template, follow these steps:
1. In the **Scan Templates** list, click ![Dots](media/dots-button.png ':size=2%') next to the template you want to edit.
2. Select the **Edit** option.

    ![Edit-Template](media/edit-template.png ':size=45%')

    > [!NOTE|label:Note]
The default templates cannot be edited.

3. On the popup, make changes to the setup of the selected scan template. These are the same [settings as for creating a new scan](guide/np-web-ui/scanning/creating-new-scan.md).
4. Once you complete editing the template, click **Update Template**.

## Deleting a Template
To delete a template, follow these steps:
1. In the **Scan Templates** list, click ![Dots](media/dots-button.png ':size=2%') next to the template you want to delete.
2. Select the **Delete** option.

    ![Delete-Template](media/delete-template.png ':size=45%')

    > [!NOTE|label:Note]
The default templates cannot be deleted.
