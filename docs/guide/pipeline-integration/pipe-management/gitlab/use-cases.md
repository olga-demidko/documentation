<table id="integrations" >
  <tr>
    <td width="70%">
      <h1>GitLab</h1>
    </td>
    <td width="30%" style="text-align:center" rowspan="3">
      <img src="guide/pipeline-integration/pipe-management/media/gitlab/gitlab-logo.png" width="200" height="250"></img>
    </td>
  </tr>
  <tr>
    <td style="text-align:left;vertical-align:text-top;padding:0px">
    <p>If you are using the GitLab pipeline for development automation, you can integrate it with NexPloit to run security scans on every new build within your development environment.</p>
    Depending on the use case, you can apply multiple options for running scans from your CI pipeline.
    </td>
  </tr>
  </table>

## Use Cases<!-- {docsify-ignore} -->
### Scanning a Target in a Private Environment
You can run fast scans of the application which is currently under development within your pipeline. NexPloit allows you to follow the fail-fast principle by interrupting a scan automatically at the first detected vulnerability. Using this option, you are able to quickly and timely find and fix the security issues at the build level without delaying the whole development process.

As the scan target is closed within your pipeline, Nexploit engine cannot access it directly from the cloud. In this case, you can use the [Repeater](/guide/introduction/deployment-onprem.md) (NexPloit local agent) which serves as a request-proxy between NexPloit and the scan target inside your private environment.  You should first create a Repeater on the [nexploit.app](https://nexploit.app), and then connect it to your pipeline using the created Repeater ID. 

To run scans directly from your pipeline, you need to install the NexPloi CLI. It provides an easy-to-use interface and multiple [commands](guide/np-cli/command-list.md) you can use in your Travis flow. 

You can either run the NexPloit CLI with the Repeater using the NPM or by installing the existing Docker image inside your pipeline. The Docker image comprises the NexPloit CLI and Repeater. 

Find the examples here: 
  * [Scanning via a Repeater using the NPM](https://kb.neuralegion.com/#/guide/pipeline-integration/pipe-management/gitlab/examples?id=example-2-scanning-via-a-repeater-using-the-nexploit-cli-npm-installation)
  * [Scanning via a Repeater using the Docker image](https://kb.neuralegion.com/#/guide/pipeline-integration/pipe-management/gitlab/examples?id=example-3-scanning-via-a-repeater-using-the-nexploit-cli-docker-installation)


 ![gitlab-repeater](../media/gitlab/gitlab-repeater.png ':size=45%')

 ### Scanning a Target in a Public Environment
 Upon a release of a new build, you can run an overall complete scan of the target in the production or public pre-production environment. In this case, long scans will not interfere with the development process as compared to scanning in the private environment.  

 Depending on the access to the deployed target, you can run a scan using multiple options.
 * If the scan target is accessible from the Internet:<br>
  ![one](../media/travis/1.png ':size=3%') Directly from the [nexploit.app](https://nexploit.app)<br>
  ![two](../media/travis/2.png ':size=3%') From your pipeline using the NexPloit CLI (NPM). Find the example [here](https://kb.neuralegion.com/#/guide/pipeline-integration/pipe-management/gitlab/examples?id=example-1-direct-scanning-using-the-nexploit-cli-npm-installation). 


 ![gitlab-direct](../media/gitlab/gitlab-direct.png ':size=65%')

 * If the scan target has a private access (or if you want to scan specific local microservices), you can use the [Repeater](/guide/introduction/deployment-onprem.md) (NexPloit local agent) to ensure secure communication between NexPloit and the target. In this case, you can control scanning  only via the Nexploit CLI which can be installed using either ![three](../media/travis/3.png ':size=3%') the NPM or ![four](../media/travis/4.png ':size=3%') the Docker image.

   Find the examples here:
      * [Scanning via a Repeater using the NPM](https://kb.neuralegion.com/#/guide/pipeline-integration/pipe-management/gitlab/examples?id=example-2-scanning-via-a-repeater-using-the-nexploit-cli-npm-installation)
      * [Scanning via a Repeater using the Docker image](https://kb.neuralegion.com/#/guide/pipeline-integration/pipe-management/gitlab/examples?id=example-3-scanning-via-a-repeater-using-the-nexploit-cli-docker-installation)
 
 
  ![gitlab-repeater](../media/gitlab/gitlab-repeater.png ':size=45%')

