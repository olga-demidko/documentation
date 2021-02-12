# GitHub Actions Pipe Management

![github-actions-logo](media/github-actions/github-actions-logo.png ':size=12%')

To enable full automation to your CI/CD pipeline, you can configure NexPloit to automatically run a scan with every build. Each new build with our GitHub Actions Integration performs security tests on the running application and provides developers with all the information from NexPloit they need to solve problems, without having to leave their development environment.

A full working example of a GitHub Actions pipeline with NexPloit can be found here: [github.com/NeuraLegion/example-actions](https://github.com/NeuraLegion/example-actions)

> [!INFO|label:Tip]
Although it is possible to configure a CI pipeline with our [REST API](https://kb.neuralegion.com/#/guide/np-rest-api/using), it is recommended to use our [NexPloit CLI](https://kb.neuralegion.com/#/guide/np-cli/overview) for an easier, more robust configuration of your pipeline.
<!-- 
More information about our GitHub Actions integration can be found here:
* [github.com/NeuraLegion/run-scan](https://github.com/NeuraLegion/run-scan)
* [github.com/NeuraLegion/stop-scan](https://github.com/NeuraLegion/stop-scan)
* [github.com/NeuraLegion/wait-for](https://github.com/NeuraLegion/wait-for) -->
