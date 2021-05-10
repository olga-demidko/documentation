## Reviewing Scans
### Reviewing Scans List
You can view the scanning log of your organization, including completed, pending and scheduled scans. To display the scans list, in the left pane, select the **Scans** option. Each scan appears as a single row.

### Reviewing Scan History
Scan history shows the history of the runs of a specific scan.

This view enables you to see the status, results and settings of each run and the next scheduled run of the original scan. Each run may have a different status and different results. 

Reviewing the details of each run may provide insight into the trends of findings and scanning results for your organization.

The settings of future scheduled scans can be modified, while retaining the same scan history view.

> [!NOTE|label:Note]
The **Scans** page shows a single row with the latest status for each scan. The **Scan History** page shows the list of all runs of a specific scan. 

##### Displaying Scan History
To display the scan history, follow these steps: 
1. From the scans list, select the scan the history of which you want to view. The scan history icon ![Scan-History-Icon](media/scan-history-icon.png ':size=3%') on the right side of the row indicates the quantity of runs of this scan.
If a scan has not been retested, then this icon is disabled ![Scan-History-Disabled](media/scan-history-disabled.png ':size=3%'), meaning that there is no scan history. The details of such scans can be viewed directly from the scans list.
2. To open the history of the selected scan, click  ![Scan-History-Icon](media/scan-history-icon.png ':size=3%') in the relative row.

    ![Scan-History](media/select-history.png ':size=45%')

    > [!NOTE|label:Note]
Most features of the **Scan history** page (such as filtering, sorting and selecting columns) are the same as on the **Scans** page. But the **New Scan** button only appears on the **Scans** page.

##### Scan History List
The scan history list shows all runs of the selected scan.

![Scan-History](media/scan-history.png ':size=45%')

The next scheduled run (with the **Scheduled** status) or the most recent run appears at the top of the list.

The name of the selected scan and its start time appear at the top left of this page.

![Name-and-Time-of-Scan](media/name-of-scan.png ':size=45%')

> [!NOTE|label:Note]
The entire history of the scan runs is retained on the **Scan History** page unless you delete it.

##### Scan History Details 
The same scan results and settings as for a single scan in the **MY SCANS** list can be displayed for each scan run in the **SCAN HISTORY** list.

To display the details of a scan run, click any place in the relative row except the button. 

##### Scan History Menu
To display the options menu for a scan run, click ![dots-button](media/dots-button.png ':size=2%') in the relative row.

Different options appear depending on the **Status** of the run. The following options are available: 
* **Stop –** Stops a scan that is running. 
* **Delete –** Deletes all data about the selected scan run, cancels the next scheduled run of a recurring scan, stops its recurrence. You can delete multiple scan runs by selecting their checkboxes and then selecting the **Delete** option. 
* **Export –** Exports the scan results and details as a CSV or PDF.
* **Edit –** When a scan has the **Scheduled** status, the **Edit** option enables you to modify the start time and settings of the next scan to be run. The settings options are the same as on the **Scans** page. Modifying the scan settings using this option retains the same scan history.
By default, a scan run is assigned the same name as the original scan. The **Edit** option always enables you to rename a specific run (regardless of its status) to give it a more indicative name. For example, this can be done to indicate an important finding or event, such as the installation of a new product version.
* **Run Immediately –** Runs a scheduled scan immediately using its most recently defined settings.
* **Retest –** Creates a separate scan entity that is a duplicate of the selected scan. Initially, the settings are identical, but you can modify them without affecting the original scan settings. A separate scan history is maintained for this retested scan. 
