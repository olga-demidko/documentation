<table id="integrations" >
  <tr>
    <td width="75%">
      <a href="#/guide/pipeline-integration/ticketing-systems/azure"> <h1>Azure Boards</h1></a>
    </td>
    <td width="25%" style="text-align:right" rowspan="3">
      <img src="guide/pipeline-integration/ticketing-systems/media/azure/azure-boards-integration.png"></img>
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
      For each new scan, you can select any of multiple boards connected to your Azure account. 
    </td>
  </tr>
  <tr><td></td></tr>
</table>


## Prerequisites

* You are an active user on [nexploit.app](https://nexploit.app/). 

## Step-by-Step Guide

### Connect NexPloit to Your Azure Account

To enable the integration, you need to connect NexPloit to your Azure account:

1. Go to [nexploit.app](https://nexploit.app).

2. In the left pane, select **Organization**. 

3. On the **Organization** page, scroll down to the **TICKET MANAGEMENT INTEGRATION** section.

    ![ticketing-management-integration](media/azure/ticketing-management-integration.png ':size=45%')

4. Click ![dots-button](media/jira/dots-button.png ':size=1%') next to **Azure**, and then click **Settings**.

    ![azure-settings](media/azure/azure-settings.png ':size=45%')

5. On the popup, click **Activate Azure Boards**.

    ![activate-boards](media/azure/activate-boards.png ':size=45%')

6. On the popup, select your Azure account in the dropdown list, and then click **Save**.

    ![select-azure-organization](media/azure/select-azure-organization.png ':size=45%')

    The NexPloit integration into Azure is enabled.

    ![enabled](media/azure/enabled.png ':size=45%')

## Adding Your Azure Board to a New Scan
When [starting a new scan](guide/np-web-ui/scanning/creating-new-scan.md), you can select the Azure board on which to automatically open tickets with the detected issues. 

To select your Azure board for a new scan, follow these steps:
1. Go to the **Additional settings** option.

    ![additional-settings](media/azure/additional-setttings.png ':size=45%')

2. In the **Integrations** dropdown list, select the Azure board for the scan.

    ![selected-azure-board](media/azure/selected-azure-board.png ':size=45%')

Now, whenever you run this scan, all its detected issues automatically open the relevant tickets on the specified Azure board.
