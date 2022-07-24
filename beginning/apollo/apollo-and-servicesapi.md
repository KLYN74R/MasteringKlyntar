---
description: Custom interfaces for KLYNTAR Services in Apollo
---

# 🥶 Apollo and ServicesAPI

{% hint style="info" %}
Here we will tell you how to develop and add the functionality of services to use them in a single interface
{% endhint %}

### <mark style="color:red;">A little information</mark>

It would be cool if the wallets you used previously generated an interface and fields directly for each Dapp and / or smart contract with which you interact. In addition, wallet developers may make some mistakes and will not always keep up with all the latest in the industry.

In KLYNTAR, service developers can create their own interfaces and APIs to interact with them.

So, for example, if you go to a service that will represent a decentralized exchange, you will see the necessary input fields, useful information taken from the API of the website of the developers of this service.

If this is a Play-to-Earn service, then you can see your collection in a beautiful showcase, and through the Telegram API, publish ads for sale in the necessary Telegram channels.



In terms of directory tree - nothing new

```
Apollo
│     
│   
└───KLY_ServicesAPI
│   │   
│   │
│   │   
│   └───AMAZING_SERVICE_1
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

New APIs are connected using configuration settings

```json
"EXTRA_CLI": [
        "KLY_Modules/init/cli/init.js",
        "KLY_ServicesAPI/some_service/cli/init.js"
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

In <mark style="color:yellow;">**OPTIONS**</mark> you specify a prefix for your service. Thus, the full path to the main API service page will be **http(s)://localhost:9691/**<mark style="color:red;">**services**</mark>**/**<mark style="color:red;">**<**</mark><mark style="color:orange;">**YOUR\_PREFIX**</mark><mark style="color:red;">**>**</mark>

You can also choose an alias for the service (option ALIAS). It is recommended to choose something that is understandable to you.

Also specify <mark style="color:yellow;">**TYPE**</mark>=service as in the example above. This is necessary to distinguish services from other routes.

Finally, restart Apollo and go to the services section.

![](<../../.gitbook/assets/image (27) (1) (1).png>)

![](<../../.gitbook/assets/image (22) (1) (1) (1).png>)

Buttons will appear on the side that will lead you to the main API page of your service

### <mark style="color:red;">**Coming soon**</mark> 👻

More information to come in the future
