---
description: Separate blockchains in KLY ecosystem
cover: >-
  ../../.gitbook/assets/tumblr_b800eb940c93611ad96334db121b1cf4_2323ada7_1280.webp
coverY: -4.750653879686155
---

# 👽 Symbiotic chains

### <mark style="color:red;">**What is a symbiotic chain?**</mark>

{% hint style="info" %}
_<mark style="color:red;">**Symbiote(symbiotic chain)**</mark>_ is a separate chain in KLY ecosystem that has its own genesis, own history, state, works following its own workflows and interacts with its own set of hostchains
{% endhint %}



<figure><img src="../../.gitbook/assets/Symbiote_General.drawio.png" alt=""><figcaption></figcaption></figure>

In the image above, you can see an example of an ecosystem running 1 native blockchain (our KLY blockchain) and some other blockchains. Something like in Polkadot or Cosmos. Third party companies, organizations and teams will be able to host their blockchains in the KLY ecosystem and benefit from coexistence. This is similar to military or economic alliances in the real world and in such a scheme, often, the participating members are clearly in a better position than if they were a single separate entity.

## <mark style="color:red;">Symbiotic chain components</mark>

### <mark style="color:orange;">**Workflow**</mark>

The first and the main component of each symbiote is a workflow.

_<mark style="color:orange;">**Workflow**</mark>_ - a model of how some blockchain works. Here the consensus is determined, the set of essences is determined (different transactions), the set of routes for the server is determined (for communication between nodes) and much more. Let's figure it out.

Workflows that will be used by KLY core are located in the **KLY\_Workflows** directory. Other workflows can be created as a separate repository and to sign other devs about your work you can open a pull request to add the link to your custom workflow . You can see it on GitHub



## <mark style="color:red;">Modularity</mark>

As stated earlier (here), blockchains will be modular and highly customizable. That is why we try not to hardcode various kinds of parameters (if we talk about consensus), the implementation of individual crypto-algorithms, and so on.

For example, one blockchain (symbiote) in the KLY ecosystem can be a BFT blockchain with support for a WASM virtual machine, another blockchain will work on some kind of PoS modification and be private (permissioned). At the same time, each of them can take the KLY codebase and reuse virtual machines, code snippets, algorithm implementations, and so on.

We ourselves try to write different parts of the KLY core at a fairly high level in order to give other developers the opportunity to use it and improve their blockchain in the KLY ecosystem.



<figure><img src="https://media0.giphy.com/media/v1.Y2lkPTc5MGI3NjExcjV5YzRuYXRjb2ZjZDV4d2E5Ynk2aHBlZGN6cTNtcW13ZDBsMDh1NSZlcD12MV9naWZzX3NlYXJjaCZjdD1n/qgQUggAC3Pfv687qPC/giphy.gif" alt=""><figcaption></figcaption></figure>

By reading the documentation further or looking at the code on GitHub, you will notice that many of the directories contain subsections

For example, the directory with VMs looks like this:

<figure><img src="../../.gitbook/assets/image (59).png" alt=""><figcaption></figcaption></figure>

Directory with workflows

<figure><img src="../../.gitbook/assets/image (60).png" alt=""><figcaption></figcaption></figure>

As you can see, they all include several packs. This modular structure allows developers of other symbiotes to use some components in their codebase.

KLYNTAR will also be available for expansion with a wide ecosystem of plugins - from a websocket servers to custom logging mechanisms, from a reverse proxy server with filters to a Telegram bot. By the way, one more proof of modularity and independence (the directory with plugins contains separate repositories)

<figure><img src="../../.gitbook/assets/image (61).png" alt=""><figcaption></figcaption></figure>

Everything above is inbuilt in KLY core because it is in use. Native KLY symbiote use it. However, we create a separate repositories for VMs, plugins and so on.

For example, separate repository for KLY-EVM(improved EVM)

{% embed url="https://github.com/KLYN74R/KLY_EVM" %}

Or, KLY-WVM - WASM-based virtual machine by KLY with tons of features

{% embed url="https://github.com/KLYN74R/KLY_WVM" %}

Or, separate repository for Savitar plugin

{% embed url="https://github.com/KLYN74R/Savitar" %}



_<mark style="color:red;">**dev\_tachyon**</mark>_ will be lightning-fast, asynchronous, with multi-million TPS, maximally parallel BFT blockchain using staking (including staking with unobtanium), BLS multi-signatures and other interesting features

{% hint style="info" %}
Currently, we're working on all of them
{% endhint %}



<mark style="color:orange;">**Connectors**</mark>

The second important component of symbiotes are connectors - modules for working with hostchains. You'll get to know them in more detail in the [_<mark style="color:yellow;">**Connectors**</mark>_](../interactions-with-hostchains/connectors.md) section, but for now let's just say that they define how your symbiote interacts with hostchains.

Connector developers, for example, create an interface for you, providing functions for working with a certain type of smart contracts on the hostchain that supports them, or other methods of interaction.

Workflow developers then take these connectors and insert them into their code at the right places. For example, send a state commit to Ethereum and Tron where there will be a multi-signature of validators as a payload, or generate a zero-knowledge proof and send it to the EVM for some contract of your symbiote.

### <mark style="color:red;">So what's new you can create?</mark>

This is the power of modular workflows - you can come up with anything you want. For example, one symbiote will be launched by a group of enthusiasts where there will be BFT, and the conditional CoinBase will launch its own symbiote where it will represent the main validator.

It is possible to build a hybrid scheme where there will be both a centralizing factor and conditional "votes" of the group of validators of this symbiote. You can move part of the logic to the hostchain. So, for example, your symbiote can be verified through the contracts of some EVM blockchain - following the example of a Polygon-Ethereum pair or other L2 networks.

Build anything)

### <mark style="color:red;">Repository with workflows</mark>

Our GitHub has a corresponding repository where developers can publish their workflows

{% embed url="https://github.com/KLYN74R/Workflows" %}

Soon after the start of the project, we will publish instructions on writing a workflow and how to publish it to the repository

### <mark style="color:red;">Workflow entry point at the code level</mark>

For a better understanding of the inner workings, let's talk about how the work of the demon begins when you start it.

Let's go straight through the code so that you understand.

{% hint style="info" %}
By the way, this can be considered part of our analysis of the code. Although here we will consider superficially, there will be more and more detailed in the future. Demo version can also be viewed [<mark style="color:red;">**here**</mark>](../codereview/)
{% endhint %}

The first step is to determine the full path and work with environment variables. The kernel also determines in which mode the daemon is running (testnet / mainnet)

![](<../../.gitbook/assets/image (4) (1) (1) (1).png>)

Next comes the definition of the main directories and the paths to them

![](<../../.gitbook/assets/image (6) (1) (1).png>)

The core then loads the configuration into the global object and creates service links and directories

![](<../../.gitbook/assets/image (11) (1) (1) (1) (1) (1).png>)

Next, we skip the animations and move on to the important. Below you can see how the core imports 2 functions from the workflow module and calls them

![](<../../.gitbook/assets/image (10) (1) (1) (1) (1) (1).png>)

At the next stage, there is a definition of services that need to be launched at runtime. If there are none, nothing will happen

![](<../../.gitbook/assets/image (5) (1) (1) (1).png>)

![](<../../.gitbook/assets/image (3) (1) (1) (1) (1).png>)

Finally, the previously imported second symbiote workflow function is called. We saved a link to it in the previous step. Workflow developers themselves decide what to run in this function. The function is run in asynchronous mode

![](<../../.gitbook/assets/image (12) (1) (1) (1) (1) (1).png>)

The last point, a server is created that creates a global variable for access from under the workflow code. After that, import() is called which registers the routes that are described by your workflow

![](<../../.gitbook/assets/image (9) (1) (1) (1) (1) (1) (1) (1).png>)

### <mark style="color:red;">**Common components for symbiotes**</mark>

As mentioned earlier, there are a number of common elements for symbiotes

<mark style="color:yellow;">**Server**</mark>

![](<../../.gitbook/assets/image (7) (1) (1) (1) (1).png>)

{% embed url="https://github.com/uNetworking/uWebSockets.js" %}

We use this server implementation. This is a popular, low-level and fast server that has proven itself well in private projects and tests. You can do more research.

<mark style="color:yellow;">**Global variables**</mark>

Symbiotes can also use a number of global variables like CONFIG to get configuration data, PRIVATE\_KEYS mapping to access private keys, variables that point to directories, and so on.

{% hint style="info" %}
Full list will be available soon
{% endhint %}
