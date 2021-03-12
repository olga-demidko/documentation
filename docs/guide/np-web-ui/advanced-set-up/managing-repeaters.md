# Managing Repeaters
NeuraLegion’s Repeater is a local agent that provides a secure connection between NeuraLegion's cloud engine and a target on a local network. A Repeater enables you to securely scan targets on a local network, without having to whitelist NeuraLegion’s IP address in your firewall for incoming traffic. See [On-Premises Repeater (Agent)](guide/introduction/deployment-options.md#On-Premises-Repeater-Agent) for a description of how an on-premise Repeater works in a NexPloit solution.

The following options are provided for managing Repeaters –
* [Displaying the Repeaters List](#Displaying-the-Repeaters-List)
* [Adding a New Repeater](#Adding-a-New-Repeater)
* [Editing the Repeater Details](#Editing-the-Repeater-Details)
* [Deactivating and Activating a Repeater](#Deactivating-and-Activating-a-Repeater)
* [Diagnosing the Connection to Network Tartgets](#Diagnosing-the-Network-Connection)
* [Deleting a Repeater](#Deleting-a-Repeater)


## Displaying the Repeaters List
To display the Repeater list, select the **Repeaters** option in the left pane to display the list of Repeaters. Each Repeater appears as a single row.

 ![Reapeaters](media/repeaters-list.png ':size=45%')

## Adding a New Repeater
To add a new Repeater, follow these steps:
1. Select the **Repeaters** option in the left pane to display the list of Repeaters. 
2. Click ![plus-icon](media/plus-icon.png ':size=2%') at the top-left. 

    ![new-repeater](media/add-repeater.png ':size=30%')

3. Enter the Repeter details and click **Add**. 

## Editing the Repeater Details
To edit Repeater details, follow these steps:
1. Click the ![dots](media/dots-button.png ':size=2%') button next to a Repeater name and then select the **Edit** option.

    ![edit-repeater](media/edit.png ':size=45%')

2. Modify the Repeater details as you need, and then click **Update**.

    ![edit-repeater](media/update-popup.png ':size=30%')

## Deactivating and Activating a Repeater
### Deactivating a Repeater
To deactivate a Repeater click the ![dots](media/dots-button.png ':size=2%') button next to the Repeater name, and then select the **Deactivate** option.

 ![deactivate-repeater](media/deactivate.png ':size=45%')

### Activating a Repeater
To activate a Repeater click the ![dots](media/dots-button.png ':size=2%') button next to the Repeater name, and then select the **Activate** option.

 ![activate-repeater](media/activate.png ':size=45%')

## Diagnosing the Network Connection
You can check if the on-premise Repeater can successfully connect to all the target hosts on your local network. The Repeater diagnostics allow you to reveal and fix the connection problems before you run a scan.

**Prerequisites**
* You have created a Repeater on [nexploit.app](https://nexploit.app/scans).
* You have activated the Repeater inside your local network using the [NexPloit CLI](/guide/np-cli/commands/initializing-repeater.md).

To run the connection diagnostics, follow these **steps**:
1. Click ![dots](media/dots-button.png ':size=2%') next to the Repeater connected to your network, and then select **Diagnose**.

    ![repeater-diagnose](media/repeater-diagnose.png ':size=45%')

2. In the **Targets** field, specify the URLs of thel targets that must be reached by the Repeater.<br>
You can add up to 1000 target hosts separated with a newline, semicolon or comma.   

    ![run-diagnostics](media/run-diagnostics.png ':size=45%')

3. Click **Run Tests**.<br>
    The results of the diagnostics will be displayed in the **Results** field.

## Deleting a Repeater
To delete a Repeater, follow these steps:
1. Click ![dots](media/dots-button.png ':size=2%') to left of the Repeater name.

    ![delete-repeater](media/delete.png ':size=45%')

2. Select the **Delete** option. 

    ![delete-repeater](media/delete-yes.png ':size=45%')

3. Click **Yes**.
