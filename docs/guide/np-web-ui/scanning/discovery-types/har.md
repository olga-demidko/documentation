# Scanning with a HAR

<iframe width="90%"  src="https://www.youtube.com/embed/7sEiHLeeMHI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

You can use a pre-recorded session of a user interaction with the target application (HAR file)  when running a scan.  Using the data contained in the HAR file, Nexploit defines the attack surface and ensures complete coverage of the scan scope.  To run a scan using a HAR file, you need to upload the file in the **Recording Session** section.

You can create a HAR file either manually or automatically (using QA tools, such as Selenium). See [Creating a HAR File](/guide/np-web-ui/scanning/discovery-types/create-har.md) to record an interaction session manually.  

![Recording](../media/recording-har.png ':size=45%')

>[!WARNING|label:Important]
 To ensure complete coverage of the scan, you should configure an authentication object so that the Nexploit engine can reach the authenticated parts of the target application. See [Managing Your Authentications](/guide/np-web-ui/scanning/managing-authentications/managing-your-authentications.md) for detailed information. 

 <table id="simple-table">
  <tr>
    <th width="50%"><b>Pros</b></td>
    <th width="50%"><b>Cons</b></td>
  </tr>
  <tr>
    <td width="50%"> <b>Deeper coverage</b>. You can enable Nexploit to switch between the microservers during scanning if the relative data is recorded in the HAR file. Nexploit uses all the recorded data to define the attack surface. Therefore, it can reach every part of your application covered by the HAR file.</td>
    <td width="50%"> <b>Less automation</b>. You have to create a HAR file on every new part of the application you want to scan. It may be a problem for large development teams where the engagement process is quite complicated.</td>
  </tr>
  <tr>
    <td width="50%"><b>Scope control</b>. The scan covers exactly the same scope of the target as recorded in the HAR file (determined by a user). Therefore, Nexploit can run a scan only for a new part, instead of scanning the whole application on every build. </td>  
     <td width="50%"></td>
  </tr>
  </table>

  >[!TIP|label:Pro Tip]
You can combine full automation with complete coverage by applying both the **Crawler** and **Recorded (HAR)** discovery types for a scan. 