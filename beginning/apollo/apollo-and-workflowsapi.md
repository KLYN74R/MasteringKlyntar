# 🥵 Apollo and WorkflowsAPI

Since different symbiotes work following different functionality, have their own set of on-chain events, their own smart contracts and their own connections with host chains, it is necessary to provide the appropriate functionality for interacting with the symbiote.

That's what WorkflowsAPIs are for. They are located in the KLY\_Workflows directory and have a similar structure to the _<mark style="color:red;">**cli**</mark>_ and _<mark style="color:red;">**ui**</mark>_ directories.

```
Apollo
│     
│   
└───KLY_Workflows
│   │   
│   │
│   │   
│   └───dev_controller
│   │    │   
│   │    │───cli(directory for files to improve CLI)
│   │    │   │
│   │    │   └───init.js 
│   │    │
│   │    └───ui(directory for files to improve UI)
│   │        │
│   │        │───routes.js
│   │        │───templates(.ejs files)
│   │        │     └─...
│   │        │───configs.json
│   │        └───...
```

To activate, make changes to the Apollo configuration

```json
 "EXTRA_CLI": [
        "KLY_Modules/init/cli/init.js",
        "KLY_"
    ],

    "EXTRA_UI": [
        
        {

            "TYPE":"service",
            
            "ALIAS":"Service 0",

            "PATH":"KLY_ServicesAPI/some_service/ui/route0.js",
            
            "OPTIONS":{
             
                "prefix":"/service0"
            
            }

        },

        {

            "PATH":"KLY_Modules/init/ui/routes.js",

            "OPTIONS":{
             
                "prefix":"/"
            
            }

        }
        
    ]
```

In Apollo, you will see them in the SYMBIOTES section after connecting the module in the configuration file and restarting the server

![](<../../.gitbook/assets/image (24).png>)

{% hint style="info" %}
This page will be updated over time.
{% endhint %}
