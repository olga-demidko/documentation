# Reviewing Scans
You can view the scanning log of your organization, including completed, pending and scheduled scans. To display the scans list, in the left pane, select the **Scans** option. Each scan appears as a single row.

![scans-list](media/scans-table.png ':size=60%')

### Managing Scans Table
You can set the information scope to display in the **MY SCANS** table. Nexploit allows you to change the order of the columns, select additional columns to be visible and adjust their width.

By default, the scans table includes the following columns:
* **Name** - custom name of the scan.
* **Issues** - number of detected vulnerabilities grouped by the severity level (red - high, yellow - medium, blue - low).
* **Requests** - total number of requests sent to the endpoints during the scan.
* **Elapsed** - total duration of the scan.
* **Start time** - date and time when the scan started.
* **End Time** - date and time when the scan ended.

### Sorting Scans 
The scans can be sorted by the column parameters, each either ascending or descending. For example, if you need to move the most recent scans up in the table, hover over the **Start Time** column name and click the appeared up-arrow. 

![sort-arrow](media/sort-arrow.png ':size=60%')

You can also search for a certain scan (for example, by its name or ID) across the table as well as filter the scans by projects and users using the relative options at the top of the table.

![sort-filter-scans](media/sort-filter-scans.png ':size=60%')

### Adjusting Scans Table 
To configure the scans table view, follow these steps:
1. Below the **+ New Scan button**, click ![settings-button](media/settings-button.png ':size=3%') to open the columns settings.
2. In the dialog box, select the check boxes next to the names of the columns you want to view in the table.

![columns-setup](media/columns-setup.png ':size=60%')

3. Drag the selected columns to put them in the desired order.
4. _(Optional)_. Adjust the width of the selected columns in the relative **Width** boxes.
5. _(Optional)_. To reset the column settings to default, click **Reset defaults** at the bottom of the dialog box.

### Scans List Menu
To display the options menu for a scan run, click ![dots-button](media/dots-button.png ':size=2%') in the relative row.

Different options appear depending on the **Status** of the run. The following options are available: 
* **Stop –** Stops a scan that is running. 
* **Delete –** Deletes all data about the selected scan run, cancels the next scheduled run of a recurring scan, stops its recurrence. You can delete multiple scan runs by selecting their checkboxes and then selecting the **Delete** option. 
* **Export –** Exports the scan results and details as a CSV or PDF.
* **Edit –** When a scan has the **Scheduled** status, the **Edit** option enables you to modify the start time and settings of the next scan to be run. The settings options are the same as on the **Scans** page. Modifying the scan settings using this option retains the same scan history.
By default, a scan run is assigned the same name as the original scan. The **Edit** option always enables you to rename a specific run (regardless of its status) to give it a more indicative name. For example, this can be done to indicate an important finding or event, such as the installation of a new product version.
* **Run Immediately –** Runs a scheduled scan immediately using its most recently defined settings.
* **Retest –** Creates a separate scan entity that is a duplicate of the selected scan. Initially, the settings are identical, but you can modify them without affecting the original scan settings. A separate scan history is maintained for this retested scan. 




