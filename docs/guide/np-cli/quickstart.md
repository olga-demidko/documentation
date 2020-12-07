# 🚀 Quick Start
## Prerequisites
Before using the **NexPloit CLI Quick Start**, verify the following prerequisites –
* You are an active user on [nexploit.app](www.nexploit.app).
* You have a valid `REPEATER-TOKEN` with the scope `repeaters:write`, `files:write`, `scans:run`, `scans:read`. You can set up –
    * An [organization-level authentication token](guide/np-web-ui/advanced-set-up/managing-org#Managing-Organization-APICLI-Authentication-Tokens).\
  – OR – 
    * A [user-level authentication token](guide/np-web-ui/advanced-set-up/managing-personal-account#Managing-Your-Personal-API-Keys-Authentication-Tokens).
* You have an active `REPEATER-ID` See [Managing Repeaters](guide/np-web-ui/advanced-set-up/managing-repeaters) for more information about handling Repeaters.

## Using the NexPloit CLI
To use the NexPloit CLI –
1. To Install NexPloit CLI globally:
```bash
npm install @neuralegion/nexploit-cli -g
```
You can validate the installation by going to the directory of your project and running the following command –\
```bash
nexploit-cli -h
```
This command displays a list of possible commands for the NexPloit CLI.
2. Activate the Repeater, as follows –
```bash
    nexploit-cli repeater
    --token REPEATER-TOKEN
    --id REPEATER-ID
    --bus amqps://amq.nexploit.app:5672
```
3. Start a new scan with a crawler, as follows –\
```bash
    nexploit-cli scan:run
    --token REPEATER-TOKEN
    --repeater REPEATER-ID
    --name "My First Scan"
    --crawler https://www.example.com
    --host-filter https://www.example.com
    --smart
```
This command initializes a new scan engine in the cloud, which begins scanning the target via the local **Repeater**.
4. View the scan results. You can follow the scan status at [nexploit.app/scans](https://nexploit.app/scans) or by using the NexPloit CLI polling command.
