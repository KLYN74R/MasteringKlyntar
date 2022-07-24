---
description: What everyone expected from others
cover: ../../.gitbook/assets/223e6792880429.5e569ff84ebef.gif
coverY: -200.6217616580311
---

# 🧑💻 CodeReview

### <mark style="color:red;">**What is it?!**</mark>

The scope of crypto projects is often open source solutions. Since it is assumed that a large number of developers will work on the kernel and its components, as well as other ecosystem projects, it would be good practice to make it clear what the kernel consists of, how the daemon is launched step by step, and explain the directory structure. Due to the fact that the project is large and complex, this will be extremely useful both for people who just want to learn more about the project, and for developers. Since we are just getting started right now, we will only provide something like a demo of what it will look like. Soon, we will create a separate book (documentation) that will be devoted to just this.

### <mark style="color:red;">Promised demo version</mark>

{% hint style="info" %}
Below will be a small "demo version" of the introduction to the code in order for you to imagine how we plan to provide information to developers. Also note that the following sections (_<mark style="color:red;">**Addons**</mark>_, <mark style="color:red;">**Blocks**</mark>...) have the _<mark style="color:purple;">**Coming soon**</mark>_ label. We will fill this in as interest in the project grows.
{% endhint %}

{% hint style="warning" %}
For development and code changes, we recommend cloning the repository again to a separate directory instead of changing to the one that runs the production version of the kernel.
{% endhint %}

### <mark style="color:red;">Preparing for parsing</mark>

For further reading and analysis, we recommend that you open the KLYNTAR kernel repository and, along with this guide, gradually figure out what's what

{% embed url="https://github.com/KLYN74R/KlyntarCore" %}

### <mark style="color:yellow;">**Directory tree**</mark>

Before starting to deal with the code, it is worth paying attention to the structure of the kernel directories. It has the following form

{% hint style="info" %}
Depth limit of 1 used
{% endhint %}

```
|-- ANTIVENOM
|
|-- KLY_Addons
|
|-- KLY_Doppelgangers
|
|-- KLY_ExternalServices
|
|-- KLY_Hostchains
|
|-- KLY_Plugins
|
|-- KLY_Runners
|
|-- KLY_Services
|
|-- KLY_Tests
|
|-- KLY_Utils
|
|-- KLY_WASM
|
|-- KLY_Workflows
|
|-- MAINNET
```

<mark style="color:yellow;">**AntiVenom**</mark>

Default directory for testnet data. Used if the <mark style="color:red;">**SYMBIOTE\_DIR**</mark> environment variable is not specified and the testnet mode is set to <mark style="color:red;">**KLY\_MODE=test**</mark>. Has the following structure

```
ANTIVENOM
|
|-- CHAINDATA
|   `-- FASj1powx5qF1J6MRmx1PB7NQp5mENYEukhyfaWoqzL9
|       |-- CANDIDATES
|       |-- CONTROLLER_BLOCKS
|       |-- HOSTCHAINS_DATA
|       |-- INSTANT_BLOCKS
|       |-- METADATA
|       `-- STATE
|
|-- CONFIGS
|   |-- network.json
|   |-- node.json
|   |-- services.json
|   `-- symbiotes.json
|
|-- GENESIS
|   `-- FASj1powx5qF1J6MRmx1PB7NQp5mENYEukhyfaWoqzL9
|       `-- 0.json
|
|-- LOGS
|   `-- FASj1powx5qF1J6MRmx1PB7NQp5mENYEukhyfaWoqzL9.txt
|
`-- SNAPSHOTS
    `-- FASj1powx5qF1J6MRmx1PB7NQp5mENYEukhyfaWoqzL9
        |-- METADATA
        `-- STATE
```

<mark style="color:purple;">**CHAINDATA**</mark> - stores state data, blocks and metadata (links to commits in host chains and other data)

<mark style="color:purple;">**CONFIGS**</mark> - directory with settings for this symbiote. We have divided into several files due to the large size of the configuration + for ease of editing

<mark style="color:purple;">**GENESIS**</mark> - directory with the genesis state for the symbiote. Can include multiple JSON files

<mark style="color:purple;">**LOGS**</mark> - directory with event logs

<mark style="color:purple;">**SNAPSHOTS**</mark> - contains METADATA and STATE subdirectories.METADATA stores pointers to the current snapshot block (height), its hash, canary, and other data. STATE is pure state data

{% hint style="info" %}
You may have noticed the intermediate directory

_<mark style="color:orange;">****</mark>_\
_<mark style="color:orange;">****</mark>_<mark style="color:orange;">**FASj1powx5qF1J6MRmx1PB7NQp5mENYEukhyfaWoqzL9**</mark>\
_<mark style="color:orange;">****</mark>_

This is the address that created this symbiote and the ID of the symbiote (similar to the address of a smart contract in EVM-compatible chains). When working with other chains, you will have different addresses. It is also an "unnecessary" directory due to the fact that a different design and placement of directories was originally planned. We will fix this in the future
{% endhint %}

<mark style="color:yellow;">**KLY\_Addons**</mark>

A directory with various kinds of code in other languages. There are sources in Go, Rust and C ++ that require certain manipulations such as compiling into a library and converting to addons. So it will be enough to go to 1 directory and run the build. It is located at the top level of the kernel, as it contains mainly algorithms that will be common to different worker processes.

<mark style="color:yellow;">**KLY\_Doppelgangers**</mark>

Designed for future releases

<mark style="color:yellow;">**KLY\_ExternalServices**</mark>

A directory that contains all the third party services that your runner loads. Is something like shared storage with the following structure

```
KLY_ExternalServices
|
|-- SomeOneService
|-- AnotherService
|-- Lokapala@1.3.37
|-- ...
`-- OneMoreService
```

Each directory here is a separate repository with a service that runs in your infrastructure.

<mark style="color:yellow;">**KLY\_Hostchains**</mark>

A large and critical directory that has this structure

```
KLY_Hostchains
│
│   
└───adapters
│   │   
│   │   README.md
│   │   
│   └───custom_MY_OWN_COLLECTION(kind of root directory for this pack)
│   │    │   
│   │    │───Solana(all files together)
│   │    │   └───configs.json
│   │    │   └───server.js
│   │    │   └───routes.js
│   │    │   └───...
│   │    │
│   │    │───XRP   
│   │    │   └───listener.rs(use different languages)
│   │    │   └───bot.js
│   │    │   └───Cargo.toml
│   │    │   └───...
│   │    │ 
│   │    │───RSK
│   │         └───...
│   │
│   └───dev0(developers' examples of adapters)
│        └───...
│
└───connectors
│   │ 
│   │  README.md
│   │   
│   └───dev0
│   │    │   
│   │    │───Solana(all files together)
│   │    │   └───configs.json
│   │    │   └───server.js
│   │    │   └───routes.js
│   │    │   └───...
│   │    │
│   │    │───XRP   
│   │    │   └───listener.rs(use different languages)
│   │    │   └───bot.js
│   │    │   └───Cargo.toml
│   │    │   └───...
│   │    │ 
│   │    │───RSK
│   │         └───...
│   │
│   └───dev0(developers' examples of adapters)
│        └───...
```

<mark style="color:yellow;">**KLY\_Plugins**</mark>

Contains plugins that are loaded separately by the node operator and serve to extend the capabilities of the kernel, workflows, and so on. More about plugins [_<mark style="color:red;">**here**</mark>_](../plugins.md)_<mark style="color:red;">****</mark>_

<mark style="color:yellow;">**KLY\_Runners**</mark>

Contains code for runners that listen for new services and run further logic based on the configuration - what to run and what not to run, in which container, which script to execute, and so on. There will also be a default runner from Andromeda developers. You can see this by looking at the repository

![](<../../.gitbook/assets/image (25) (1) (1).png>)

{% hint style="warning" %}
Don't forget that the development process is ongoing
{% endhint %}

<mark style="color:yellow;">**KLY\_Services**</mark>

Storage for your services. Structure similar KLY\_ExternalServices except that the services here are your own

<mark style="color:yellow;">**KLY\_Tests**</mark>

Directory with individual units and other tests

<mark style="color:yellow;">**KLY\_Utils**</mark>

Contains algorithms and data structures. Again, it is at the top level due to the fact that the algorithms and useful functions here are common to all symbiotes. We can even look at it visually

![](<../../.gitbook/assets/image (10).png>)

<mark style="color:yellow;">**KLY\_KVM**</mark>

Directory required for KLYNTAR VM(KLYNTAR VIRTUAL MACHINE) to work. It is also a storage for .wasm smart contracts

<mark style="color:yellow;">**KLY\_Workflows**</mark>

Contains symbiote workflow repositories

<mark style="color:yellow;">**MAINNET**</mark>

Absolutely the same structure as ANTIVENOM

### <mark style="color:red;">Conclusion</mark>

This was an introductory explanation of the kernel. We started with the structure and will continue to disassemble in more detail and clearly. We believe that such a manual will be useful and give a deep understanding of KLYNTAR
