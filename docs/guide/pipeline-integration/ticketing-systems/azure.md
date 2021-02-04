<table id="integrations" >
  <tr>
    <td width="75%">
      <a href="#/guide/pipeline-integration/ticketing-systems/azure"> <h1>Azure Ticketing System</h1></a>
    </td>
    <td width="25%" style="text-align:right" rowspan="3">
      <img src="guide/pipeline-integration/ticketing-systems/media/azure/Integration_logo_example.png"></img>
    </td>
  </tr>
  <tr>
    <td style="text-align:left;vertical-align:text-top;padding:0px">
      The NexPloit integration into Azure lets you get the scan results in automatically created tickets on your selected Azure board. Each new ticket provides you with all the NexPloit information for solving issues, without having to leave their development environment.
    </td>
  </tr>
  <tr><td></td></tr>
</table>

## Connecting NexPloit to your Azure Account
To enable the integration, you need to connect NexPloit to your Azure account:
1. Go to [nexploit.app](https://nexploit.app).
2. In the left pane, select **Organization**. 
3. On the **Organization** page, scroll down to the **TICKET MANAGEMENT INTEGRATION** section. \
![azure-option](media/azure/azure-option.png ':size=45%')
4. Click ![dots-button](media/jira/dots-button.png ':size=1%') next to **Azure**, and then click **Settings**.\
![icon-settings](media/azure/icon-settings.png ':size=45%')
5. On the popup, click **Activate Azure Boards**.\
![activate-azure-boards](media/azure/activate-azure-boards.png ':size=45%')
6. On the popup, select your Azure account in the dropdown list, and then click **Save**.\
![select-azure-organization](media/azure/select-azure-rganization.png ':size=45%')\
The NexPloit integration into Azure is enabled. \
![enabled](media/azure/enabled.png ':size=45%')

## Adding Azure to a Scan
When [starting a new scan](guide/np-web-ui/scanning/creating-new-scan.md), you can select the Azure board on which to automatically open tickets with the detected issues . 

To select your Azure board for a new scan, follow these steps:
1. Go to the **Additional settings** option.\
![additional-settings](media/azure/additional-setttings.png ':size=45%')
2. In the **Integrations** dropdown list, select the Azure board for the scan.\
![selected-azure-board](media/azure/selected-azure-board.png ':size=45%')

Now, whenever you run this scan, all its detected issues automatically open the relevant tickets on the specified Azure board.
