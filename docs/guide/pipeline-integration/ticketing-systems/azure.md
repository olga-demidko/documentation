<table id="integrations" >
  <tr>
    <td width="70%">
      <h1>Azure Boards</h1>
    </td>
    <td width="30%" style="text-align:center" rowspan="3">
      <img src="guide/pipeline-integration/ticketing-systems/media/azure/azure-boards-logo.png" width="200" height="250"></img>
    </td>
  </tr>
  <tr>
    <td style="text-align:left;vertical-align:text-top;padding:0px">
      You can connect your Azure board to a Nexploit scan to get all the discovered issues on automatically created Azure tickets. NexPloit opens each new ticket for one specific issue and provides the following information:
      <ul>
        <li>Issue severity level</li>
        <li>Details of discovery</li>
        <li>Possible exposure</li>
        <li>Remediation suggestions </li>
      </ul>
      For each new scan, you can select any of multiple boards connected to the account of your Azure DevOps organization.
    </td>
  </tr>
  <tr><td></td></tr>
</table>


## Prerequisites

* You are an active user on [nexploit.app](https://nexploit.app/). 

## Step-by-Step Guide

### Connect NexPloit to Your Azure DevOps Organization 

To enable the integration, you need to connect NexPloit to the account of your Azure DevOps organization:

1. Go to [nexploit.app](https://nexploit.app).

2. In the left pane, select **Organization**. 

3. On the **Organization** page, scroll down to the **TICKET MANAGEMENT INTEGRATION** section.

    ![ticketing-management-integration](media/azure/ticketing-management-integration.png ':size=45%')

4. Click ![dots-button](media/azure/icon-button.png ':size=2%') next to **Azure**, and then select **Settings**.

    ![azure-settings](media/azure/azure-settings.png ':size=45%')

5. On the popup, click **Activate Azure Boards**.

    ![activate-boards](media/azure/activate-boards.png ':size=45%')

6. On the popup, select your your Azure DevOps organization from the dropdown list, and then click **Save**.

    ![select-azure-organization](media/azure/select-azure-organization.png ':size=45%')

    The NexPloit integration with Azure is enabled.

    ![enabled](media/azure/enabled.png ':size=45%')

### Configure NexPloit Integration with Azure projects 
You can connect your NexPloit project to the projects of your Azure DevOps organization. The connection allows NexPloit to automatically provide the scan reports on the associated Azure boards of specific projects. 

To associate your NexPloit project with the Azure boards, follow these steps:

1. In the **TICKET MANAGEMENT INTEGRATION** section, click ![dots-button](media/azure/icon-button.png ':size=2%') next to **Azure**, and then select **Project Settings**.

    ![project-settings](media/azure/project-settings.png ':size=45%')

2. On the **Azure Projects Integration Configuration** popup, do the following:
  *   In the **Project** field, enter or select the NexPloit project that you want to use for the scan. 

  >[!NOTE|label:Note]
You can start a scan ONLY if a project is selected. If you do not have any projects in NexPloit, select the **Default** one.

  *   From the **Associate repository…** dropdown list, select your Azure board.\
      The selected board is automatically added to the **REPOSITORIES** list below. You can add multiple repositories (boards) to this list.

    *   To arrange the associated repositories in alphabetical order, hover-over **Name** and click ![down-arrow](media/azure/down-arrow.png ':size=2%') next to it. 
    *   To make the repositories order free again, hover-over **Name** and click ![up-arrow](media/azure/up-arrow.png ':size=2%') next to it. 
    *   To delete a board from the list, click ![dots-button](media/azure/icon-button.png ':size=2%') next to the board and select **Disassociate**.
    *   To quickly select the required repository from the list, use the **Find a repository** search field. 
    *   To select the number of associated repositories that you can view on one **REPOSITORIES** page, use the **Items per page** dropdown list.
    *   To switch between the **REPOSITORIES** pages, use the navigation buttons above **Close**.  

  ![project-selection](media/azure/project-selection.png ':size=45%')

3. Once you complete the projects configuration, click **Close** at the bottom of the popup.

### Select Your Azure Board for a New Scan
When [starting a new scan](docs/guide/np-web-ui/scanning/creating-new-scan.md), you can select one or multiple associated Azure boards (repositories) that you want to use as destinations for the scan reports.

1. On the **New Scan** popup, go to the **Additional settings** section.

  ![integrations](media/azure/integrations.png ':size=45%')

2. From the **Integrations** dropdown list, select the connected Azure boards that you want to use for the scan.\
All the issues detected during the scan will automatically open the relevant tickets on the specified Azure boards.
