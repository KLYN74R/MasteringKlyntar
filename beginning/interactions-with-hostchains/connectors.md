---
description: Smth what links blockchains
cover: ../../.gitbook/assets/22b22287602523.5dbd29081561d.gif
coverY: -187.08477521327262
---

# 🖖 Connectors

### <mark style="color:red;">**Role on KLYNTAR**</mark>

Connectors are modules that encapsulate work with host chains. They export functions for a wide variety of interactions, from simply storing commits on host chains, to more advanced logic like using zkSNARKs and executing contracts. These functions are then used at the workflow level to interact with host chains. Connectors are usually distributed in packs for greater convenience and classification.

Since we have to adapt to the functionality of other chains, all you need to write your own connector is to study the API, SDK or documentation of the host chain for which the connector is intended (or groups of host chains if there is a common interface like that of EVM compatible blockchains.

Here's how to schematically label the connector so that you have a better understanding of what is happening

![](<../../.gitbook/assets/image (12) (1) (1).png>)

### <mark style="color:red;">Connector configuration and configurable parameters</mark>

The connectors also have a set of necessary configurable parameters - a pair of keys to work on the host chain, an endpoint URL (this can be your node, a node from your pool, or even a Node-as-a-Service decentralized service on KLYNTAR) and some more settings.

Flexibility and depth of settings are determined by the creator of the connector.

Within certain standards, workflow provides an <mark style="color:yellow;">**HC\_CONFIGS**</mark> object which contains the necessary configs for the connector. In order to show in practice, for example, here is how the configuration of one of the workflows that uses a set of symbiotes looks like.

![](<../../.gitbook/assets/image (15) (1) (1) (1).png>)

The set of custom parameters is defined in the connector. It all depends on how cool the connector is and how much it allows you to configure.

In this case, connectors for 3 host chains are used:

* Litecoin
* Ethereum
* BNB

They are all from the dev0 pack. Let's take a look inside

![](<../../.gitbook/assets/image (11) (1) (1) (1).png>)

{% hint style="warning" %}
It is also worth noting that this pack contains not too "cool" connectors. This group of connectors simply save the commit to the host chain and then check the commit asynchronously
{% endhint %}

Let's look at the code of the connectors to make it more clear to you. Here is the connector for Litecoin

![](<../../.gitbook/assets/image (16) (1) (1) (1) (1).png>)

Inside the function, you can see how the connector accesses its settings through the global <mark style="color:purple;">**CONFIG.SYMBIOTES\[**</mark><mark style="color:purple;"><mark style="color:yellow;">**\<symbiote>**<mark style="color:yellow;"></mark><mark style="color:purple;">**].HC\_CONFIGS**</mark> object. This is exactly the same object that we configured at the workflow configuration level.

Likewise with other functions. You can explore the repository yourself for a better understanding of how it works.

And here is an example of an EVM compatible connector. This is another proof of KLYNTAR's flexibility - because thanks to 1 connector, symbiotes can communicate with all EVM compatible blockchains.

![](<../../.gitbook/assets/image (3) (1).png>)

Here you can see how the connector uses standard parameters to work with EVM compatible blockchains. There are familiar terms like _<mark style="color:red;">**GAS\_LIMIT**</mark>_ and _<mark style="color:red;">**GAS\_PRICE**</mark>_, you can choose CHAIN\_ID according to this resource (to work with different networks) and much more.

Internally, this connector works by following the Web3 documentation and the JS toolkit for working with the EVM.

### <mark style="color:red;">Inside the connector</mark>

Connectors in general should be an exported object that contains all of the connector's functionality in its methods. Also, the connector may have some additional dependencies of its own (and therefore it will be necessary to load them) or require some operations on the code (compile something inside the module, etc.)

Here is what the general structure of the connector looks like

```javascript
//You can import anything you need
import something from 'somewhere'
import another from '../local/pack.js'


//Some local functions

let makeTransaction=(to,commitHash,blockID)=>{

    //...Here further logic

},


//Exportable object
export default {

    method1:()=>{
    
        let params = CONFIGS.SYMBIOTES[CURRENT_SYMBIOTE_ID].HC_CONFIGS
        
        ///...you can use params.PUB(pubkey/address), params.PRV and other options
    
    },
    
    method2:()=>{},
    
    ...
    
    someAnotherMethod:()=>{}

}
```

Imagine that there are EVM (Ethereum, Polygon, Avalanche) chains. In order to make sure that they ensure the safety of the KLYNTAR symbiote, you need to write some kind of connector. What can we think of? Well, the simplest option is to simply store state in a chain, as demonstrated above - without any two-way logic with smart contracts (especially when it comes to Bitcoin and the like, where they do not exist as such).

For such a simple connector, you probably need something like the functions setCommit (in order for some symbiote to save the commit) and checkCommit (in order to check the inclusion).

In this case, your connector might look like this:

```javascript
//You can import anything you need
import something from 'somewhere'
import another from '../local/pack.js'


//Some local functions

let makeTransaction=(to,commitHash,blockID)=>{

    //...Here further logic

},


//Exportable object
export default {

    method1:()=>{
    
        let params = CONFIGS.SYMBIOTES[CURRENT_SYMBIOTE_ID].HC_CONFIGS
        
        ///...you can use params.PUB(pubkey/address), params.PRV and other options
    
    },
    
    method2:()=>{},
    
    ...
    
    someAnotherMethod:()=>{}

}
```

### <mark style="color:red;">Mutual work of connectors and workflow</mark>

Since we want the maximum, both connector developers and workflow developers should make their modules following the practice of being as flexible as possible. This will allow the same connector to be used by completely different symbiotes and their workflow

### <mark style="color:red;">Using connectors at the workflow level</mark>

Again, the simplest workflow (dev\_controller) can be cited as an example. This is how he uses the connector in his code.

![https://github.com/KLYN74R/KlyntarCore/blob/0cd166e7790e9ddeac9d3d3b8ce069689bdba13b/KLY\_Workflows/dev\_controller/life.js#L247](<../../.gitbook/assets/image (14) (1) (1) (1).png>)

This is the block generation function. As part of the workflow, it is planned that a new commit cannot be added if the old one is not yet included in the host chain. In addition, the logic of periodic activation is defined at the connector level. So, for example, on Bitcoin and forks (due to the common API and similar data structures) you can set the CONFIRMATIONS parameter and thus the commits will be only at set intervals (due to the fact that on Bitcoin there is a difficulty correction and the network in any case mines a block approximately once in 10 minutes). But this is just an example, other connectors may be more functional and provide other cool features.

Function entry poin[\
<mark style="color:red;">**https://github.com/KLYN74R/KlyntarCore/blob/0cd166e7790e9ddeac9d3d3b8ce069689bdba13b/KLY\_Workflows/dev\_controller/life.js#L137**</mark>](https://github.com/KLYN74R/KlyntarCore/blob/0cd166e7790e9ddeac9d3d3b8ce069689bdba13b/KLY\_Workflows/dev\_controller/life.js#L137)

Here, just for flexibility, the workflow developer could come up with something for the workflow. For example, a block would be generated if it reached a certain multisig staking threshold, and so on.

{% hint style="info" %}
This page will still be updated as the topic of connectors is very large and exciting.
{% endhint %}
