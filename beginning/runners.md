---
description: Let's look at where smart contracts of the new generation will start
cover: ../.gitbook/assets/Cyberpunk_final-uai-2880x1757.jpg
coverY: 355.6476683937824
---

# ⚙ Runners

### <mark style="color:red;">Where it all starts</mark>

After you have managed to get acquainted with the capabilities of the service, it is time to tell in more detail how they will be performed, what and where they will be launched, and how it works in general.

On KLYNTAR, all services will somehow go through the runner and its rules. A runner is like a middleware that receives a service from the network and, based on its settings, makes decisions like

* Is it worth running a service?
* How and how much memory to allocate to a service
* Whether to set any restrictions
* What is the security budget and how many security centers have checked this repository
* Is the address in the trust tree?
* How much can you potentially receive from this service Is it worth it to distribute and advertise the service further on the network?
* ...and other solutions

The runner decides whether to run the service on this node or send it to others, whether to give access to the network for the service, whether to run it in a separate container or in one of the existing ones, and so on.

Here's how you can schematically represent the runner

![](<../.gitbook/assets/image (8) (1).png>)

### <mark style="color:red;">In a nutshell</mark>

The nodes listen, distribute and download repositories (if a location is given) or compressed archives (if the service is distributed directly) and following the rules and settings of the runner decide how to run the service.

Due to the independence of runners from the network and its processes, as well as continuing the theme of modularity, we will allow users to use custom runners for their infrastructures, as well as provide the possibility of flexible configuration and customization for maximum efficiency.

Although you determine the functionality of the runner yourself, we still recommend that you focus on official solutions as the most effective ones.

### <mark style="color:red;">Runner at the code level</mark>

At the code level, the runner is a separate repository that lies in the _<mark style="color:red;">**KLY\_Runners**</mark>_ directory. You should already be familiar with the principle of how we store data, but we will still show the directory structure for clarity.

Here, for example, how it looks at the level of the code editor

![](<../.gitbook/assets/image (11) (1).png>)

You can update repositories independently. The KLYNTAR daemon, when it starts, looks at the _<mark style="color:orange;">**services.json**</mark>_ configuration file and the <mark style="color:orange;">**RUNNER**</mark> option where the path to the runner entry point is specified.

Here's what it looks like. Сonfiguration file services.json

```json
{
    "SERVICES":{
        
        //...define your services here to run in the same instance
    
    },

    "EXTERNAL_SERVICES":{

        //...define services of other
                
    },

    "RUNNER":"dev_andromeda/runner.js"
    
}
```

runner.js is the entry point of a runner that exports an unnamed function that receives an object of a standard structure as input and is taken to process it.

Here's what it looks like

```javascript
export default async service=>{

    if(typeof service.title==='string' && service.desc.length<RUNNER_CONFIGS.DESC_MAX_LEN){

        LOG({data:`Received new service \x1b[31;1m${service.desc}\x1b[0m`,pid:process.pid},'CD')

        //...logic

    }
    
}
```

As for the worker processes, since they make up a set of route handlers and create routes to the server themselves, they must provide a handler for the runner to simply receive data from the network, pass it to the function, and then the runner will do its job.

For example, the _<mark style="color:red;">**dev\_controller**</mark>_ and _<mark style="color:red;">**dev\_bft**</mark>_ worker processes provide these handlers

```javascript
import {SAFE_ADD,PARSE_JSON} from '../../../KLY_Utils/utils.js'



//Get our runner
let SERVICE_RUNNER=await import(`../../../KLY_Runners/${CONFIG.RUNNER}`).then(m=>m.default).catch(e=>console.log(e))




export let SERVICES = {
    
    //Only this one function available for ordinary users(the others can be called by node owner)
    services:a=>{
        
        let total=0,buf=Buffer.alloc(0)
        
        a.writeHeader('Access-Control-Allow-Origin','*').onAborted(()=>{}).onData(async(chunk,last)=>{
         
            if(total+chunk.byteLength<=CONFIG.MAX_PAYLOAD_SIZE){
            
                buf=await SAFE_ADD(buf,chunk,a)//build full data from chunks
    
                total+=chunk.byteLength
                
                if(last){

                    let body=await PARSE_JSON(buf)

                    a.end(body?'OK':'ERR')

                    //Run further stage
                    SERVICE_RUNNER(body)

                }
  
            }
        
        })

    }

}



//Register route
UWS_SERVER

.post('/service',SERVICES.services)
```

As you can see, the server simply accepts some JSON service object and passes it to the runner for processing, while it simply sends a simple HTTP response.

### <mark style="color:red;">Runner configuration example</mark>

In order to further understand the principle of operation, you can look into the configuration

```json
{
    "DOCKER_CONFIGS":{
        
        "protocol":"http",
        "host":"localhost",
        "port":2375
    
    },

    "DESC_MAX_LEN":200,
    "REDIRECTION_DEPTH":3,

    "STATIC_NODES":[
        "https://someklyntarpool.io",
        "htts://api-klyntar.coinbase.com"
    ],

    "TRUSTED_HUBS":{
        "WoD3FV8ByzerAUUCZ5rF58aTLpz5kTNxHnyBS5vzuqeq":{},
        "7HHKSu9BNF7GuB3CX8BbUEzx9pp1SqLksigvfMZz9hopvWJJRSW4qrXTKWFq5ExSpm":{},
        "63dMQGT8u5BvsAE7UniDSbBDmK6igBvcwSVHotaQ6938eMRYPbZSHwAYTgQcACQ2KK":{}       
    },

    "PREFER_TOOLCHAIN":{
        
        "docker":["rust","node.js","c","c++"],

        "host":["rust","node.js","c","c++"]
        
    },

    "KEYWORDS":["web3","defi","bridge","tor","control","storage","api"],

    "NETCAP":{
 
    },

    "PREFER_SYMBIOTES":{
    
        "QfzhbWJsPa9NjqxepcXSbp1X58pkQNACS2ReyRo2SMCK":{
            "MIN_FREEZE":0
        },
        "NrHwU6YMS5VZatxo9Z188ptR7dbNyYexRKCYickQBJG4":{},
        "LvjcXxRbXbKnHSgaJrDWLx7vo8yR3BwpkBXApKukoaGX":{}
    },
    
    "PREFER_HOSTCHAINS":{
    
        "btc":{
            "MIN_FREEZE":0
        },
        "algo":{},
        "sol":{}
    },
    
    "DORMITORY":{
        
    },
    
    "ALLOWED_STORAGE":[
        "github.com",
        "gitlab.com",
        "pkg.go.dev",
        "crates.io",
        "npmjs.com",
        "rubygems.org",
        "getcomposer.org",
        "www.nuget.org",
        "hackage.haskell.org",
        "index.scala-lang.org"
    ],


    "REGISTRIES":{

        "NODE.JS":[
            
            "https://localhost:4873"
        
        ],
        "PYTHON":[


        ],
        "RUST":[


        ],
        "DOCKER":[
            
            "https://localhost:5000"
            
        ]

    },

    "CONTAINERS":[
        "group1-WoD3FV8ByzerAUUCZ5rF58aTLpz5kTNxHnyBS5vzuqeq-node",
        "group1-JeVZcdi8TQZaX6TKhtSKLCzMQMRCx5JjsQTiGbAaLPXW-rust.node.go.python"
    ]
    
}
```

Here the runner can determine from which resources it is allowed to download files, determine the containers with which it will work, set trusted centers - these can be multisig addresses that, for example, will send you a signature about the security of the service and you will make sure that if a certain number of addresses have already voted for the security of the service with a total balance of more than several million KLY and other options.

All this once again emphasizes the flexible possibilities of KLYNTAR and the possibilities of runners.

### <mark style="color:red;">Default runners</mark>

By default, the standard runner from the KLYNTAR developers will be available to you. We named it after our neighboring galaxy Andromeda. This is symbolic since we are comparing conventional smart contracts with our relatively well-known Milky Way galaxy. But the services in the form in which they will be on KLYNTAR are something new, some kind of new galaxy - not so distant, but still - opens up new opportunities for us

![](<../.gitbook/assets/image (19).png>)

{% hint style="info" %}
Currently, all runners are under development and will not be available for the first time for use on the network.
{% endhint %}
