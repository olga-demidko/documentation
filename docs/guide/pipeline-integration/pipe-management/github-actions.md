<table id="integrations" >
  <tr>
    <td width="70%">
      <h1>GitHub Actions</h1>
    </td>
    <td width="30%" style="text-align:center" rowspan="3">
      <img src="guide/pipeline-integration/pipe-management/media/github-actions/github-actions-new-logo.png" width="200" height="250"></img>
    </td>
  </tr>
  <tr>
    <td style="text-align:left;vertical-align:text-top;padding:0px">
    To enable full automation to your CI/CD pipeline, you can configure NexPloit to automatically run a scan with every build. Each new build with our GitHub Actions Integration performs security tests on the running application and provides developers with all the information from NexPloit they need to solve problems, without having to leave their development environment.
    </td>
  </tr>
  <tr>
  <td>
  A full working example of a GitHub Actions pipeline with NexPloit can be found here: <a href="https://github.com/NeuraLegion/example-actions">github.com/NeuraLegion/example-actions</a>.
  </td>
  </tr>
</table>

> [!INFO|label:Note]
Although it is possible to configure a CI pipeline with our [REST API](https://kb.neuralegion.com/#/guide/np-rest-api/using), it is recommended to use our [NexPloit CLI](https://kb.neuralegion.com/#/guide/np-cli/overview) for an easier, more robust configuration of your pipeline.
<!-- 
More information about our GitHub Actions integration can be found here:
* [github.com/NeuraLegion/run-scan](https://github.com/NeuraLegion/run-scan)
* [github.com/NeuraLegion/stop-scan](https://github.com/NeuraLegion/stop-scan)
* [github.com/NeuraLegion/wait-for](https://github.com/NeuraLegion/wait-for) -->
