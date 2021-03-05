<table id="integrations" >
  <tr>
    <td width="70%">
      <h1>Travis CI</h1>
    </td>
    <td width="30%" style="text-align:center" rowspan="3">
      <img src="guide/pipeline-integration/pipe-management/media/travis/travis-logo.png" width="200" height="250"></img>
    </td>
  </tr>
  <tr>
    <td style="text-align:left;vertical-align:text-top;padding:0px">
    <p>If you are using the Travis CI pipeline for development automation, you can integrate it with NexPloit to run security scans on every new build within your development environment.</p>
    Depending on the use case, you can apply multiple options for running scans from your CI pipeline.
    </td>
  </tr>
  </table>


## Use Cases
### Scanning a target at the development playground
You can run fast scans of the application which is currently under development within your pipeline. NexPloit allows you to follow the fail-fast principle by interrupting a scan automatically at the first detected vulnerability. Using this option, you are able to quickly and timely find and fix the security issues at the build level without delaying the whole development process.

As the scan target is closed within your pipeline, NexPlot engine cannot access it directly from the cloud. In this case, you can use the [Repeater](/guide/introduction/deployment-onprem.md) (NexPloit local agent) which serves as a proxy between NexPloit and the scan target inside your pipeline.  You should first create a Repeater on the [nexploit.app](https://nexploit.app), and then connect it to your pipeline using the predefined Repeater ID. 

To run scans directly from your pipeline, you need to install the NexPloi CLI. It provides an easy-to-use interface and multiple [commands](guide/np-cli/command-list.md) you can use in your Travis flow. 

You can either run the NexPloit CLI with the Repeater using the [NPM](guide/pipeline-integration/pipe-management/travis/examples.md) or by installing the [Docker](guide/pipeline-integration/pipe-management/travis/examples.md) inside your pipeline. The Docker is a container with the built-in NexPloit CLI and Repeater.

 ![travis-flow](../media/travis/travis-flow.png ':size=45%')

 ### Scanning a target at the production playground
 Upon a release of a new build, you can run an overall complete scan of the target at the production playground. In this case, long scans will not interfere with the development process as compared to scanning at the development playground. 

 Depending on the access to the deployed target, you can run a scan using multiple options.
 * If the scan target is accessible from the Internet:<br>
  ![one](../media/travis/1.png ':size=3%') Directly from the [nexploit.app](https://nexploit.app)<br>
  ![two](../media/travis/2.png ':size=3%') Directly from your development environment [using the NexPloit CLI (NPM)](guide/pipeline-integration/pipe-management/travis/examples.md) 

 ![repeater-npm](../media/travis/repeater-npm.png ':size=65%')

 * If the scan target has a limited access (for example, hosted on local microservers): you can use the [Repeater](/guide/introduction/deployment-onprem.md) (NexPloit local agent) to ensure secure communication between NexPloit and the target. In this case, you can control scanning  only via the Nexploit CLI which can be [installed](/guide/np/cli/installation) using either ![three](../media/travis/3.png ':size=3%') the [NPM](guide/pipeline-integration/pipe-management/travis/examples.md) or ![four](../media/travis/4.png ':size=3%')the [Docker](guide/pipeline-integration/pipe-management/travis/examples.md).

  ![docker-npm](../media/travis/docker-npm.png ':size=45%')








