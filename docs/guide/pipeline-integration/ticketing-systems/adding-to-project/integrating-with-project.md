# Using Ticketing Systems with Nexploit Projects 
You can add one or multiple repositories (projects, channels) of your ticketing systems to a specific Nexploit project. Therefore, you are able to create different sets of repositories that will be available for the relevant Nexploit projects of your organization.

The project integration configuration allows you to select any of the repositories associated with the specified Nexploit project when you start a new scan.  

## Prerequisites <!-- {docsify-ignore} -->
* You are an active user on [nexploit.app](https://nexploit.app/).
* The Nexploit is connected to your ticketing systems with the repositories you want to add to a certain project.

    ![repositories-enabled](media/repositories-enabled.png ':size=45%')

## Step-by-Step Guide <!-- {docsify-ignore} -->
### Configure the Nexploit Project Integration <!-- {docsify-ignore} -->
1. In the **TICKET MANAGEMENT INTEGRATION section**, click ![dots-button](media/icon-button.png ':size=2%') next to the ticketing system you need, and then select **Project Settings**.

    ![project-settings](media/project-settings.png ':size=45%')

2. On the **Projects Integration Config** popup, do the following:
    * In the **Project field**, enter or select the Nexploit project that you want to use for the scan.

     >[!NOTE|label:Note]
   You can start a scan ONLY if a project is selected. If you do not have any projects in Nexploit, select the **Default** one.

    *   From the **Associate repository…** dropdown list, select the repository (project, channel) that you want to use for the scan results within the specified project.
    The selected repository is automatically added to the **REPOSITORIES** list below. You can add multiple repositories (boards) to this list.
      *   To arrange the associated repositories in alphabetical order, hover-over **Name** and click ![down-arrow](media/down-arrow.png ':size=2%') next to it. 
      *   To make the repositories order free again, hover-over **Name** and click ![up-arrow](media/up-arrow.png ':size=2%') next to it. 
      *   To delete a repository from the list, click ![dots-button](media/icon-button.png ':size=2%') next to the repository and select **Disassociate**.
      *   To quickly select the required repository from the list, use the **Find a repository** search field. 
      *   To select the number of associated repositories that you can view on one **REPOSITORIES** page, use the **Items per page** dropdown list.
      *   To switch between the **REPOSITORIES** pages, use the navigation buttons above **Close**.  

 ![project-selection](media/project-selection.png ':size=45%')

3. Once you complete the projects integration configuration, click **Close** at the bottom of the popup.

### Select Repositories for a New Scan <!-- {docsify-ignore} -->

When [starting a new scan](guide/np-web-ui/scanning/creating-new-scan.md), you can select one or multiple integrated repositories (projects, channels) that you want to use as destinations for the scan reports within the specified Nexploit project.
1. Select the **Scan Details** tab.

    ![select-integrations](media/select-integrations.png ':size=45%')

2. From the **Integrations** dropdown list, select the integrated repositories that you want to use for the scan.