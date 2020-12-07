## Reviewing Scans
### Reviewing the Scan List
* To display the list of Scans select the Scans option in the left pane to display the Scans List. Each scan appears as a single row.

### Reviewing Scan History
#### What is Scan History?
Scan History shows the history of the runs of a specific scan.

This view enables you to see the status, results and settings of each run and the next scheduled run of the original scan. Each run may have a different status and different results. 

Reviewing the details of each run may provide insight into the trends of findings and results in your organization.

The settings of future scheduled scans can be modified, while still retaining the same Scan History view.

> [!NOTE|label:Note]
MY SCANS shows a single row showing the **latest** status of each scan. The Scan History shows a row for **each run** of a specific scan. 

#### Reviewing Scan History
##### Displaying Scan History
* To display Scan History –
1. Select the **Scans** option in the left pane to display the *Scans List*.\
Each scan appears as a single row. The Scan History ![Scan-History-Icon](media/scan-history-icon.png ':size=2%') icon on the right side indicates the quantity of runs of this scan.\
For example, 2 runs appear as follows ![Scan-History-Icon-2-Scans](media/scan-history-icon.png ':size=2%').
If a scan was not run multiple times, then this icon appears disabled ![Scan-History-Disabled](media/scan-history-disabled.png ':size=2%'), meaning that there is no Scan History. As always, the details of this scan can be viewed from the Scans List.
2. Click the ![Scan-History-Icon](media/scan-history-icon.png ':size=2%') icon on the right of a scan’s row to display its Scan History.\
![Scan-History](media/scan-history.png ':size=45%')
> [!NOTE|label:Note]
Most features of the Scan History page (such as filtering, sorting and selecting columns) are the same as in the Scans List.

##### Scan History List
The Scan History List shows a row for each run of the selected scan.\
![Scan-History](media/scan-history.png ':size=45%')
The next scheduled run (status **Scheduled**) or the most recent run appears at the top of the list.

The name of the selected scan and its start time appear at the top left of this page.\
![Name-and-Time-of-Scan](media/name-time-of-scan.png ':size=25%')

Each column in this page is the same as in the Scans page, except that in Scan History a row appears for **each run** of the scan, whereas in the Scans page a single row appears for each scan.
> [!NOTE|label:Note]
The **New Scan** button only appears in the Scans page.

> [!NOTE|label:Note]
The entire history of a scan’s runs is retained in the Scan History page unless you delete it.

##### Scan History Details 
The same scan results and settings as in the Scans List can be displayed for each scan run in the Scan History List.

* To display the details of a scan run Click on any run’s row to display the results and details of that run.
> [!NOTE|label:Note]
You can click anywhere on the row besides on a button. 

##### Scan History List Menu
* To display a menu of options for a scan run click ![dots-button](media/dots.png ':size=1%') in a scan run’s row.

Different options appear according to the *status* of the run. The following is a comprehensive list of menu options – 
* **Stop –** Stops a scan that is running. 
* **Delete –** Deletes all data about the selected scan run. You can delete multiple scan runs by ticking their checkboxes and then selecting this option. Deleting the next scheduled scan of a recurring scan, stops its recurrence.
* **Export –** Exports the scan results and details as a CSV or PDF.
* **Edit –** When a scan has **Scheduled** status, the **Edit** option enables you to modify the start time and *settings* of the next scan to be run. The settings options are the same way as in the *Scans* page. Modifying the scan settings in this manner retains the same Scan History.\
By default, a scan run is assigned the same name as the original scan. This **Edit** option always enables you to rename this run (regardless of the run’s status) in order to give it a more indicative name. For example, to indicate an important finding or event, such as the installation of a new product version.
* **Run Immediately –** Runs a scheduled scan immediately using its most recently defined settings.
* **Retest –** Creates separate scan entity that is a duplicate of the selected scan. Initially, the settings are identical, but can be modified by you without affecting the original scan settings. A separate Scan History is maintained for this retested scan. 
