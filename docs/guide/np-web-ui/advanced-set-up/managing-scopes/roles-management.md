# Roles Management Scopes

When creating a custom role to be assigned to a new user, you can predefine access permissions for this role by selecting the relative scopes. The following table describes the permissions each scope provides.   

<table id="simple-table">
  <tr>
    <th width="25%"><b>Scope</b></th>
    <th width="75%"><b>Description</b></th>
  </tr>
  <tr>
    <td width="25%"><code>scans</code></td>
    <td width="75%" >
       Provides unrestricted access to scan management. 
    </td>
  <tr>
    <td width="25%"><code>scans:read </code></td>
    <td width="75%" >
       Allows viewing existing scans. 
    </td>
  </tr>
  <td width="25%"><code>scans:manage </code></td>
    <td width="75%" >
       Allows managing scans, for example editing scan settings or retesting a scan. 
    </td>
  </tr>
  <tr>
    <td width="25%"><code>scans:run </code></td>
    <td width="75%" >
       Allows running scans.   
    </td>
  </tr>
  <tr>
    <td width="25%"><code>scans:stop </code></td>
    <td width="75%" >
       Allows stopping scans. 
    </td>
  </tr>
  <tr>
    <td width="25%"><code>scans:delete </code></td>
    <td width="75%" >
       Allows deleting scans.   
    </td>
  </tr>
  <tr>
    <td width="25%"><code>issues:read</code></td>
    <td width="75%" >    
       Allows viewing detected issues.   
    </td>
  </tr>
  <tr>
    <td width="25%"><code>issues:manage </code></td>
    <td width="75%" >
      Allows managing detected issues, for example assigning a user to an issue, marking an issue as resolved, or retesting an issue.    
    </td>
  </tr>
   <tr>
    <td width="25%"><code>files:read </code></td>
    <td width="75%" >
       Allows reading files from the storage and verifying targets.   
    </td>
  </tr>
  <tr>
    <td width="25%"><code>files:write </code></td>
    <td width="75%" >
       Allows managing files in the storage, for example uploading or deleting them.   
    </td>
  </tr>
  <tr>
    <td width="25%"><code>integration.repos:read </code></td>
    <td width="75%" >
       Allows viewing associated repositories, for example GitHub repositories , Slack channels, or Jira boards.   
    </td>
    <tr>
    <td width="25%"><code>integration.repos:manage </code></td>
    <td width="75%" >
       Allows filtering the severity level of issues to be opened in integrated services.   
    </td>
  </tr>
  <tr>
    <td width="25%"><code>repeaters:read </code></td>
    <td width="75%" >
       Allows viewing organization’s repeaters.   
    </td>
  </tr>
  <tr>
    <td width="25%"><code>repeaters:write </code></td>
    <td width="75%" >
       Allows creating, editing, deleting a repeater, as well as testing repeater connection to a network.   
    </td>
  </tr>

  <tr>
    <td width="25%"><code>scripts:read</code></td>
    <td width="75%" >
      Allows viewing repeater’s scripts.   
    </td>
  </tr>
   <tr>
    <td width="25%"><code>scripts:write</code></td>
    <td width="75%" >
      Allows creating, editing and deleting scripts.   
    </td>
  </tr>
  <tr>
    <td width="25%"><code>org </code></td>
    <td width="75%" >
       Provides unrestricted access to organization management (including the permission to delete the organization).   
    </td>
  </tr>
  <tr>
    <td width="25%"><code>org:read</code></td>
    <td width="75%" >
      Allows viewing basic information about an organization.   
    </td>
  </tr>
  <tr>
    <td width="25%"><code>org:write</code></td>
    <td width="75%" >
      Allows editing basic information about an organization and managing its basic settings, for example, enforcing MFA.   
    </td>
  </tr>
  <tr>
    <td width="25%"><code>org.memberships:manage</code></td>
    <td width="75%" >
      Allows managing organization members, for example adding a member to an organization, deleting a member from an organization, or viewing a member’s profile.   
    </td>
  </tr>
  <tr>
    <td width="25%"><code>org.memberships:read</code></td>
    <td width="75%" >
     Allows viewing members of an organization.   
    </td>
  </tr>
  <tr>
    <td width="25%"><code>projects:admin</code></td>
    <td width="75%" >
     Allows to view information about projects.   
    </td>
  </tr>
  <tr>
    <td width="25%"><code>projects:manage</code></td>
    <td width="75%" >
     Allows managing projects, for example creating a new project or editing an existing one.   
    </td>
  </tr>
  <tr>
    <td width="25%"><code>projects:read</code></td>
    <td width="75%" >
     Allows displaying available projects.   
    </td>
  </tr>
  <tr>
    <td width="25%"><code>projects:delete</code></td>
    <td width="75%" >
     Allows to deleting projects.  
    </td>
  </tr>
  <tr>
    <td width="25%"><code>groups</code></td>
    <td width="75%" >
     Provides unrestricted access to group management. 
    </td>
  </tr>
  <tr>
    <td width="25%"><code>groups:manage</code></td>
    <td width="75%" >
     Allow managing groups, for example creating a new group or editing an existing group. 
    </td>
  </tr>
  <tr>
    <td width="25%"><code>groups:read</code></td>
    <td width="75%" >
     Allows viewing information about groups that a user has been added to. 
    </td>
  </tr>
   <tr>
    <td width="25%"><code>groups:admin</code></td>
    <td width="75%" >
     Allows viewing information about groups. 
    </td>
  </tr>
  <tr>
    <td width="25%"><code>groups:delete</code></td>
    <td width="75%" >
     Allows deleting groups. 
    </td>
  </tr>
  <tr>
    <td width="25%"><code>reports:read</code></td>
    <td width="75%" >
     Allows viewing scan reports. 
    </td>
  </tr>
  <tr>
    <td width="25%"><code>reports:write</code></td>
    <td width="75%" >
     Allows managing configuration of PDF reports. 
    </td>
  </tr>
  <tr>
    <td width="25%"><code>integrations:read</code></td>
    <td width="75%" >
     Allows viewing a list of available and enabled integrations.  
    </td>
  </tr>
  <tr>
    <td width="25%"><code>integrations:write</code></td>
    <td width="75%" >
     Allows enabling connection and associating other repositories to be used for a scan (ticketing systems).  
    </td>
  </tr>
  <tr>
    <td width="25%"><code>roles:read</code></td>
    <td width="75%" >
     Allows viewing a list of roles.  
    </td>
  </tr>
  <tr>
    <td width="25%"><code>roles:write</code></td>
    <td width="75%" >
     Allows creating and editing custom roles. The default roles (for example, “Admin”, “Owner”, etc.) are read-only.  
    </td>
  </tr>
  <tr>
    <td width="25%"><code>user</code></td>
    <td width="75%" >
     Selected by default for all roles.   
    </td>
  </tr>
  <tr>
    <td width="25%"><code>user:read</code></td>
    <td width="75%" >
     Allows viewing user’s personal details.   
    </td>
  </tr>
  <tr>
    <td width="25%"><code>user:write</code></td>
    <td width="75%" >
     Allows users to edit their personal details, for example change names, emails and passwords.   
    </td>
  </tr>
  <tr>
    <td width="25%"><code>scans-templates</code></td>
    <td width="75%" >
     Provides unrestricted access to scan templates management.  
    </td>
  </tr>
  <tr>
    <td width="25%"><code>scans-templates:read</code></td>
    <td width="75%" >
     Allows viewing existing scan templates.  
    </td>
  </tr>
  <tr>
    <td width="25%"><code>scans-templates:write</code></td>
    <td width="75%" >
     Allows creating, editing and deleting custom scan templates.  
    </td>
  </tr>
  <tr>
    <td width="25%"><code>auth-objects</code></td>
    <td width="75%" >
     Provides unrestricted access to authentication objects management.    
    </td>
  </tr>
  <tr>
    <td width="25%"><code>auth-objects:read</code></td>
    <td width="75%" >
     Allows to view basic configuration of authentication objects.    
    </td>
  </tr>
  <tr>
    <td width="25%"><code>auth-objects:write</code></td>
    <td width="75%" >
     Allows managing authentication objects that have been created by a user.    
    </td>
  </tr>
  <tr>
    <td width="25%"><code>auth-objects:test</code></td>
    <td width="75%" >
     Allows testing an authentication object during its configuration.    
    </td>
  </tr>
  <tr>
    <td width="25%"><code>logs</code></td>
    <td width="75%" >
     Allows viewing the activities log.    
    </td>
  </tr>
  <tr>
    <td width="25%"><code>comments</code></td>
    <td width="75%" >
     Allows viewing and managing comments in scans and issues that a user has access to.    
    </td>
  </tr>
   <tr>
    <td width="25%"><code>comments:read</code></td>
    <td width="75%" >
     Allows viewing comments in scans and issues that a user has access to.     
    </td>
  </tr>
   <tr>
    <td width="25%"><code>comments:write</code></td>
    <td width="75%" >
     Allows managing (editing, deleting) comments in scans and issues that a user has access to.     
    </td>
  </tr>
   <tr>
    <td width="25%"><code>plans</code></td>
    <td width="75%" >
     Allows viewing information about offered plans.   
    </td>
  </tr>
  <tr>
    <td width="25%"><code>products</code></td>
    <td width="75%" >
     Allows viewing information about offered products.   
    </td>
  </tr>
  <tr>
    <td width="25%"><code>payment-methods</code></td>
    <td width="75%" >
     Allows managing payment methods.   
    </td>
  </tr>
   <tr>
    <td width="25%"><code>subscriptions</code></td>
    <td width="75%" >
     Allows managing plan subscriptions for an organization.   
    </td>
  </tr>
   <tr>
    <td width="25%"><code>payments</code></td>
    <td width="75%" >
     Allows managing user’s payments.  
    </td>
  </tr>
  <tr>
    <td width="25%"><code>billing</code></td>
    <td width="75%" >
     Allows viewing billing summary.  
    </td>
  </tr>
  <tr>
    <td width="25%"><code>activities</code></td>
    <td width="75%" >
     Allows viewing notifications and managing the notification feed.  
    </td>
  </tr>
  <tr>
    <td width="25%"><code>api-keys</code></td>
    <td width="75%" >
     Allows creating personal API keys. 
    </td>
  </tr>
  <tr>
    <td width="25%"><code>org.api-keys</code></td>
    <td width="75%" >
     Allows creating organization API keys. 
    </td>
  </tr>
  <tr>
    <td width="25%"><code>auth-providers</code></td>
    <td width="75%" >
     Allows configuring SSO providers (okta, Google, ADFS). 
    </td>
  </tr>
  </table>