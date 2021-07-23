# Using Ticketing Systems with Nexploit Projects 
You can integrate one or multiple repositories (projects, channels) of your ticketing systems with a specific Nexploit project. Therefore, you are able to select any of the repositories available for the specified Nexploit project when you start a new scan.  

>[!Warning|label:Important] 
Only the users with the **Admin** and **Owner** roles have access to integrate a connected ticketing system with a specific project.


### Prerequisites <!-- {docsify-ignore} -->
* You are an active user on [nexploit.app](https://nexploit.app/).
* Nexploit is connected to your ticketing systems with the repositories you want to add to a certain project.

    ![ticketing-list](media/ticketing-list.png ':size=60%')

### Step-by-Step Guide <!-- {docsify-ignore} -->
#### Configure the Nexploit Project Integration <!-- {docsify-ignore} -->
1. In the **TICKET MANAGEMENT INTEGRATION section**, click ![dots-button](media/icon-button.png ':size=2%') next to the ticketing system you need, and then select **Project Settings**.

    ![project-settings](media/project-settings.png ':size=45%')

2. In the **Projects Integration Config** dialog box, do the following:
    * In the **Project field**, enter or select the Nexploit project that you want to use for the scan.

     >[!NOTE|label:Note]
   You can start a scan only if a project is selected. If you do not have any projects in Nexploit, select the **Default** one.

    *   From the **Associate repository…** dropdown list, select the repository (project, channel) that you want to use for the scan results within the specified project.
    The selected repository is automatically added to the **REPOSITORIES** list below. You can add multiple repositories (boards) to this list.
      *   To arrange the associated repositories in alphabetical order, hover-over **Name** and click ![down-arrow](media/down-arrow.png ':size=2%') next to it. 
      *   To make the repositories order free again, hover-over **Name** and click ![up-arrow](media/up-arrow.png ':size=2%') next to it. 
      *   To delete a repository from the list, click ![dots-button](media/icon-button.png ':size=2%') next to the repository and select **Disassociate**.
      *   To quickly select the required repository from the list, use the **Find a repository** search field. 
      *   To select the number of associated repositories that you can view on one **REPOSITORIES** page, use the **Items per page** dropdown list.
      *   To switch between the **REPOSITORIES** pages, use the navigation buttons above **Close**.  

 ![project-selection](media/project-selection.png ':size=45%')

3. Once you complete the projects integration configuration, click **Close** at the bottom of the dialog box.<br>
The associated repositories will be displayed in the **TICKETING SETTINGS** section on the **Project Settings** page.

#### Filter the Severity Level of Issues to be Opened in Integrated Services <!-- {docsify-ignore} -->

You can select a certain severity level of issues (findings) to be sent to a repository/channel associated with your Nexploit project. For example, if you set the high severity level for Monday integration, then only the detected issues of high severity will open tickets on your Monday board. 

>[!NOTE|label:Note]
The option to filter issue severity is only available to the users whose roles include the `integrations.repos:manage` access scope. For more information, see [Managing Access Scopes](/guide/np-web-ui/advanced-setup/managing-scopes/roles-management.md).

1. In the left pane, select **Projects**.
2. Click ![dots-button](media/icon-button.png ':size=2%') next to the project which is integrated with the required ticketing service, and then select **Settings**.
3. In the **TICKETING SETTINGS** section, use the **Issue severity** drop-down menu to filter the issues that will be sent to the associated repository.

    ![issue-severity](media/issue-severity.png ':size=60%')

#### Select Repositories for a New Scan <!-- {docsify-ignore} -->

When [starting a new scan](guide/np-web-ui/scanning/creating-new-scan.md), you can select one or multiple integrated repositories (projects, channels) that you want to use as destinations for the scan reports within the specified Nexploit project.
1. In the **Advanced** setup mode, select the **Scan Details** tab.

    ![select-integrations](media/select-integration.png ':size=45%')

2. From the **Integrations** dropdown list, select the integrated repositories that you want to use for the scan.