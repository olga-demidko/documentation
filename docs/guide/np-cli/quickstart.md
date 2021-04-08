# 🚀 Quick Start
## Prerequisites
Before using the **NexPloit CLI Quick Start**, verify the following prerequisites:
* You are an active user on [nexploit.app](www.nexploit.app).
* You have a valid `AUTH_TOKEN` (API key) with the following scopes: `bot`, `files:write`, `scans:run`, `scans:read`. You can set up an[organization-level authentication token](guide/np-web-ui/advanced-set-up/managing-org#Managing-Organization-APICLI-Authentication-Tokens) or a [user-level authentication token](guide/np-web-ui/advanced-set-up/managing-personal-account#Managing-Your-Personal-API-Keys-Authentication-Tokens).
* You have an active `REPEATER_ID` See [Managing Repeaters](guide/np-web-ui/advanced-set-up/managing-repeaters) for more information about handling Repeaters.

## Using the NexPloit CLI
To use the NexPloit CLI, follow these steps:
1. To Install NexPloit CLI globally:
```bash
npm install @neuralegion/nexploit-cli -g
```
You can validate the installation by going to the directory of your project and running the following command:
```bash
nexploit-cli -h
```
This command displays a list of possible commands for the NexPloit CLI.
2. Activate the Repeater, as follows:
```bash
    nexploit-cli repeater               
    --token AUTH_TOKEN                  
    --id REPEATER_ID                    
    --bus amqps://amq.nexploit.app:5672
```
3. Start a new scan with a crawler, as follows:
```bash
    nexploit-cli scan:run                   
    --token AUTH_TOKEN                      
    --repeater REPEATER_ID                  
    --name "My First Scan"                  
    --crawler https://www.example.com       
    --host-filter https://www.example.com   
    --smart
```
This command initializes a new scan engine in the cloud, which begins scanning the target via the local **Repeater**.
4. View the scan results. You can follow the scan status at [nexploit.app/scans](https://nexploit.app/scans) or by using the NexPloit CLI polling command.
