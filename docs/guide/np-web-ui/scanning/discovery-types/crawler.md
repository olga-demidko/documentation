# Scanning with a Crawler

<iframe width="560" height="315" src="https://www.youtube.com/embed/vCA0DwjLXyM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Nexploit can crawl your web application to define the attack surface. This option does not require any details that might get you tangled. To run a security scan using a crawler, you simply need to specify the target URL in the **Targets** field. 

You can scan either the whole application or its parts. To scan only specific parts of your application, click ![plus-dark](../media/plus-dark.png ':size=3%') at the right side of the **Targets** section to add multiple URLs. In this case, only the specified sections of the application and everything downstream from them will be scanned.

![Crawler-settings](../media/crawler.png ':size=45%')

>[!WARNING|label:Important]
 To ensure complete coverage of the scan, you should configure an authentication object so that the crawler can reach the authenticated parts of the target application. See [Managing Your Authentications](/guide/np-web-ui/scanning/managing-authentications/managing-your-authentications.md) for detailed information. 

 <table id="simple-table">
  <tr>
    <th width="50%"><b>Pros</b></td>
    <th width="50%"><b>Cons</b></td>
  </tr>
  <tr>
    <td width="50%"> <b>Simple usage</b>. You simply need to specify the target host. The crawler will define the attack surface (scan scope) automatically.</td>
    <td width="50%"> <b>Less coverage</b>. The crawler cannot get through some user-specific forms or provide the required input. It means that the attack surface may be defined incompletely, and Nexploit will not cover such parts of the application during scanning.</td>
  </tr>
  <tr>
    <td width="50%"><b>Full automation</b>. By default, the crawler automatically covers all the application parts that it can reach.</td>  
     <td width="50%"><b>Limited coverage level</b>. The crawler is applicable only to web pages of the target application and the microservices connected to the application directly. Crawling between the microservices is disabled.  </td>
  </tr>
  </table>

>[!TIP|label:Pro Tip]
You can combine full automation with complete coverage by applying both the **Crawler** and **Recorded (HAR)** discovery types for a scan. 
