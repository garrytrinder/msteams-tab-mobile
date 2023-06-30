Update `.vscode\tasks.json`, add "Start local tunnel" task after "Validate prerequisites" task

```json
{
    // Start the local tunnel service to forward public URL to local port and inspect traffic.
    // See https://aka.ms/teamsfx-tasks/local-tunnel for the detailed args definitions.
    "label": "Start local tunnel",
    "type": "teamsfx",
    "command": "debug-start-local-tunnel",
    "args": {
        "type": "dev-tunnel",
        "ports": [
            {
                "portNumber": 53000,
                "protocol": "https",
                "access": "public",
                "writeToEnvironmentFile": {
                    "endpoint": "TAB_ENDPOINT", // output tunnel endpoint as BOT_ENDPOINT
                    "domain": "TAB_DOMAIN" // output tunnel domain as BOT_DOMAIN
                }
            }
        ],
        "env": "local"
    },
    "isBackground": true,
    "problemMatcher": "$teamsfx-local-tunnel-watch"
},
```

Update `.vscode\tasks.json`, `dependsOn` array, include "Start local tunnel" task.

```json
"dependsOn": [
    "Validate prerequisites",
    "Start local tunnel",
    "Provision",
    "Deploy",
    "Start application"
],
```