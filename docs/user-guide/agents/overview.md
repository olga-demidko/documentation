# Agent (Repeater) Guide
![repeater_image](https://d36jcksde1wxzq.cloudfront.net/be7833db9bddb4494d2a7c3dd659199a.png)

## About
Repeater allows you to run NexPloit scans without exposing your ports outside. Also, it can be useful, if you want to run a local scan without deploying.

By design, repeater is just a docker image with a utility, that keeps connection with amq.nexploit.app:5672, performs requests on local target and sends responses to NexPloit backend.

More information about our GitHub Actions Integration can be found here: https://hub.docker.com/r/neuralegion/repeater
