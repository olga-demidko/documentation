# Managing Projects
If your organization has multiple groups that work on the development of several applications simultaneously, the best way to separate and manage the scanning flows is to create different Nexploit projects. You can manage which user groups get access to a project, and have full control over certain permissions and associated ticketing repositories.

In addition, you can limit the number of concurrent engines (scans) for each project so that each team has equal access to the organization engines. Let’s imagine that your organization has 10 engines and 2 projects, and there is no limitation on concurrent engines for these projects. It means that one project team can run all available engines at once and block the other team from scanning. To prevent such situations, you can, for example, set up the maximum number of concurrent engines to 5 per team, so that each team will be able to run 5 scans simultaneously without blocking each other. If a team decides to run more than 5 scans at once, the scans that exceed the limit will be queued. 

If you have integrated Nexploit with the ticketing tool a project team uses, the relative repositories (projects, channels) can be associated with a specific project. The integration configuration allows teams of different projects to select the repository associated with their project when creating a new scan. As a result, all the discovered issues will be opened as tickets or messages automatically in the selected repository.  

You can find more information about Nexploit integration with ticketing systems [here](/guide/pipeline-integration/ticketing-systems/ticketing-overview.md).

Please note that a project is required for the configuration of a new scan, so if you do not have any custom projects, you need to select the default one.   

The following options are available for managing projects:
* [Creating a project](#Creating-a-Project)
* [Viewing the project scans](#Viewing-the-project-scans)
* [Assigning a detected issue to a project user](#Assigning-a-Detected-Issue-to-a-Project-User)
* [Setting a maximum number of concurrent scans for a project](#Setting-a-Maximum-Number-of-Concurrent-Scans-for-a-Project)
* [Deleting a group from the project](#Deleting-a-Group-from-the-Project) 
* [Deleting a project](#Deleting-a-Project) 

### Creating a Project

To create a project, follow these steps:
1. In the left pane, select **Projects** and click **+ New Project**.

![new-project](media/new-project.png ':size=60%')

2. In the **NEW PROJECT** dialog box, enter a project name and select the groups that can access the project.

![save-project](media/project-popup.png ':size=30%')

3. Click **Save**.<br>
   A successfully created project appears in the **MY PROJECTS** table.

### Viewing the Project Scans

You can view the scans run within each particular project as well as retest, edit and delete them.  To view and manage project scans, click the raw with the project you need in the **MY PROJECTS** table. 

Most features of the scans, such as retesting, stopping, editing, exporting, and deleting, are the same as on the **Scans** page. Find more information [here](https://kb.neuralegion.com/#/guide/np-web-ui/scanning/reviewing-scans?id=scans-list-menu). 

### Assigning a Detected Issue to a Project User

You can view the information about all issues detected during the project scans and assign these issues to different members of the project team. To assign an issue to a user, follow these steps:
1. In the **MY PROJECTS** table, select the project you need.
2. On the **Project** page, scroll down to the **PROJECT ISSUES** table and select the issue you want to assign.

![project-issues](media/issues-table.png ':size=60%')

3. From the **Assignees** drop-down list, select the user(s) who should fix the issue. 

### Deleting a Group from the Project

To delete a group from a project, follow these steps:
1. In the **MY PROJECTS** table, click ![dots-button](media/dots-button.png ':size=2%') next to the project where you want to delete a group, and then select **Settings**.

![project-settings](media/project-settings.png ':size=60%')

2. In the **GROUP MANAGEMENT** table, click ![dots-button](media/dots-button.png ':size=2%') next to the group you want to delete, and then select **Delete**.

![delete-group](media/delete-group.png ':size=60%')

### Setting a Maximum Number of Concurrent Scans for a Project

To set a limit for scans that can be run simultaneously by one project team, do the following:
1. In the **MY PROJECTS** table, click ![dots-button](media/dots-button.png ':size=2%') next to the project where you want to set a limit to concurrent scans, and then select **Settings**.

![project-settings](media/project-settings.png ':size=60%')

2. In the **PROJECT SETTINGS** section, select the check box next to **Limit number of concurrent scans**.
3. In the **Max. concurrent scans** field, enter the number of engines that can be run concurrently for this project. 
   Please make sure that the number you set does not exceed the total  number of engines available for the entire organization.

![limit-number](media/limit-number.png ':size=60%')   

4. At the top right of the **Project Settings** page, click **Save**.

### Deleting a Project

To delete a  custom project, do the following:
1. In the **MY PROJECTS** table, click ![dots-button](media/dots-button.png ':size=2%') next to the project you want to delete, and then select **Delete**.

![delete-project](media/delete-project.png ':size=60%')

2. On the popup, click **Yes, delete**.
   By deleting a project, all the associated scans will be deleted along with their history and detected issues. This data cannot be restored after deletion.
 







