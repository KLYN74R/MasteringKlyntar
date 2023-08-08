---
description: Separate blockchains in KLY ecosystem
cover: >-
  ../../.gitbook/assets/tumblr_b800eb940c93611ad96334db121b1cf4_2323ada7_1280.webp
coverY: -4.750653879686155
---

# 👽 Symbiotic chains

## <mark style="color:red;">**What is a symbiotic chain?**</mark>

{% hint style="info" %}
_<mark style="color:red;">**Symbiote(symbiotic chain)**</mark>_ is a separate chain in KLY ecosystem that has its own genesis, own history, state, works following its own workflows and interacts with its own set of hostchains
{% endhint %}



<figure><img src="../../.gitbook/assets/Symbiote_General.drawio.png" alt=""><figcaption></figcaption></figure>

In the image above, you can see an example of an ecosystem running 1 native blockchain (our KLY blockchain) and some other blockchains. Something like in Polkadot or Cosmos. Third party companies, organizations and teams will be able to host their blockchains in the KLY ecosystem and benefit from coexistence. This is similar to military or economic alliances in the real world and in such a scheme, often, the participating members are clearly in a better position than if they were a single separate entity.

## <mark style="color:red;">Symbiotic chain components</mark>

<figure><img src="../../.gitbook/assets/SingleSymbiote.png" alt=""><figcaption></figcaption></figure>

### <mark style="color:orange;">**Workflow**</mark>

The first and the main component of each symbiote is a workflow.

_**Workflow**_ - a model of how some blockchain works. Here the consensus is determined, the set of essences is determined (different transactions), the set of routes for the server is determined (for communication between nodes) and much more. Let's figure it out.

Workflows that will be used by KLY core are located in the **KLY\_Workflows** directory. Other workflows can be created as a separate repository and to sign other devs about your work you can open a pull request to add the link to your custom workflow . You can see it on GitHub

### <mark style="color:orange;">**Workflow**</mark>

<mark style="color:orange;">**TODO**</mark>

### <mark style="color:orange;">**Genesis**</mark>

<mark style="color:orange;">**TODO**</mark>

### <mark style="color:orange;">**Configuration**</mark>

<mark style="color:orange;">**TODO**</mark>

### <mark style="color:orange;">**Set of hostchains**</mark>



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

