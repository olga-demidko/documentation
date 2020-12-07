# 🚨 Checking Scan Status
```nexploit-cli scan:polling [options] <scan>``` configures ongoing polling of a scan's status and helps you follow its progress during CI/CD flows.

After a scan’s launch, it frequently checks the scan's status. If the scan finds at least of one issue of medium severity, NexPloit CLI finishes with exit code 50.

## Arguments
| **Argument** | **Description**                                    |
|--------------|----------------------------------------------------|
| `<scan>`     | The ID of an existing scan that you want to check. |

## Options
| **Option**                                   | **Description**                                                                                                                                                                                                                                                    |
|------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `--token my-jwt-authentication-token`          | The unique identifier used to authenticate a user. It can be issued in your organization’s dashboard.                                                                                                                                                              |
| `--breakpoint=any / medium_issue / high_issue` | A conditional breakpoint that finishes the process with exit code 50 only after fulfilling the predefined condition.<br/><br/>**Default Value –** `--breakpoint any`                                                                                               |
| `--interval=milliseconds`                      | The period of time between the end of a timeout period or the completion of a scan status request, and the next request for status. For example, 60, 2min, 10h or 7d. A numeric value is interpreted in milliseconds.<br/><br/>**Default Value –** --interval 5000 |
| `--timeout=milliseconds`                       | The maximum time allowed for polling to end normally. For example, 60, 2min, 10h or 7d. A numeric value is interpreted in milliseconds.                                                                                                                            |


