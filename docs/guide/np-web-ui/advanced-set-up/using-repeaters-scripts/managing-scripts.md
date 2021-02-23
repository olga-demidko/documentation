# Managing Repeater Scripts
The Repeater Scripts allow you to add, change or compute some part of a scan request before it is dispatched to the target. 

The [nexploit.app](https://nexploit.app/) enables you to manage the Repeater scripts in the **Repeaters** section of the Dashboard:
* [Creating a Script](#Creating-a-Script)
* [Displaying the Scripts List](#Displaying-the-Sripts-List) 
* [Editing a Script](#Editing-a-Script)
* [Deleting a Script](#Deleting-a-Script)
* [Loading a Script to a Repeater](#Loading-a-Script-to-a-Repeater)

## Creating a Script
To create a script, follow these steps:
1. In the **Repeaters** section, click **<> Repeater Scripts** in the upper right corner.

    ![Reapeaters-scripts](../media/repeaters-scripts/repeaters-scripts.png ':size=45%')

2. Click ![plus-button](../media/repeaters-scripts/plus-button.png ':size=2%') in the upper left corner.
3. On the script popup, do the following:
    * In the Name field, enter the name of your script.
    * _(Optional)_ In the **Description** field, enter some descriptive information about your script.
    * In the **Code** field, write the script code or paste it from your external editor. 
    >[!NOTE|label:Note]
    The code example given in this field shows how to write a script for calculating a hash message authentication code (HMAC) value.

  ![script-code](../media/repeaters-scripts/script-code.png ':size=45%')

## Displaying the Scripts List
All the created scripts are displayed in the **AVAILABLE SCRIPTS** section on the **Scripts** page.

   ![available-scripts](../media/repeaters-scripts/available-scripts.png ':size=45%')

In this section, you can use the following options:
* To quickly find a certain script, enter its name, description or ID in the search field in the upper right corner.
* To select the number of scripts that you want to view on one page, select it from the **Items per page** dropdown list at the bottom.
* To switch between the pages of the available scripts, use the navigation buttons in the lower right corner.

## Editing a Script
To edit a specific script, do the following:
1. In the **AVAILABLE SCRIPTS** section, select the script you want to change.
2. Click ![dots-icon](../media/repeaters-scripts/dots-icon.png ':size=2%') next to the selected script, and then select **Edit**.

 ![edit-script](../media/repeaters-scripts/edit-script.png ':size=45%')

3. On the script popup, add any changes you need, and then click **Update**.

## Deleting a Script
To delete a specific script, do the following:
1. In the **AVAILABLE SCRIPTS** section, select the script you want to delete.
2. Click ![dots-icon](../media/repeaters-scripts/dots-icon.png ':size=2%') next to the selected script, and then select **Delete**.

 ![script-delete](../media/repeaters-scripts/script-delete.png ':size=45%')

## Loading a Script to a Repeater 
To load a script to a specific Repeater, do the following:
1. Go to the **Repeaters** section.
2. From the list of available Repeaters, select the one you need.
3. Click ![dots-icon](../media/repeaters-scripts/dots-icon.png ':size=2%') next to the selected Repeater, and then select **Edit**.

 ![edit-script](../media/repeaters-scripts/edit-script.png ':size=45%')

  On the popup, do the following:<br>
  a) Select the type of the script coverage:
    * **Single global script** - applied for the requests that should cover all the target hosts. 
    * **Host-specific script** - applied for the requests that aim at only one specific host.
 
  ![scripts-type](../media/repeaters-scripts/scripts-type.png ':size=30%')

  b) From the dropdown list, select the script you want to connect, and then click Update.<br>
  The uploaded script will be then added to the scan request executed via the specified Repeater.

  ![select-script](../media/repeaters-scripts/select-script.png ':size=30%')
