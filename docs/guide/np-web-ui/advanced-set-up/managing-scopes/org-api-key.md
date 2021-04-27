# Organization API Key Scopes

When creating an API key in the organization settings, you can predefine access permissions for this key by selecting the relative scopes. The following table describes the permissions each scope provides.  

<table id="simple-table">
  <tr>
    <th width="25%"><b>Scope</b></th>
    <th width="75%"><b>Description</b></th>
  </tr>
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
    <td width="25%"><code>scim </code></td>
    <td width="75%" >
       Enables user and group provisioning from ADFS to a NexPloit organization.   
    </td>
  </tr>
  <tr>
    <td width="25%"><code>bot</code></td>
    <td width="75%" >
       Enables communication between a Repeater and the NexPloit engine.   
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
  </table>