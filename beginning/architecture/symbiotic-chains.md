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

We built KLYNTAR with the way the modern world works. Container shipping, USB standards, traffic routing - all this is interchangeable in the world and the same everywhere. When developing KLYNTAR, we did not try to "hardcode" a consensus there, which would then have to be changed for 8 years, we did not try to bind a fixed number of validators or impose any hard restrictions.

That is why the architecture is based on the principle of modularity when each individual symbiote can be built as a constructor, independently choosing a consensus (generally in KLYNTAR called _**workflows**_), a set of hostchains, the type of interaction with them, its own fees policy, and so on.

In fact, KLYNTAR is also a framework for creating your own blockchains for your needs, and having KLYNTAR Services will help you run them in parallel with the main symbiotes and get the security and capabilities of KLYNTAR right out of the box - only now the game will be by your rules.

Despite this, there are a number of "standard" and "general" components of each symbiote. So, for example, the standard implementation of the KLYNTAR core written in Node.js includes some common elements for all symbiotes such as:

* Server implementation
* Boot file ([_<mark style="color:purple;">**klyn74r.js**</mark>_](https://github.com/KLYN74R/KlyntarCore/blob/main/klyn74r.js))
* Common files & directorites(usually confgs)
* Common global variables(for example, global configuration object or mapping with private keys)
* Running services & plugins
* ...and that's it😅

Everything else is modular and symbiote dependent. We will talk about this in more detail later on this page.

What is a symbiote?

![](<../../.gitbook/assets/image (8) (1) (1) (1) (1) (1).png>)

A similar structure resembles a chain-link grid

![](<../../.gitbook/assets/image (4) (1) (1) (1) (1).png>)

There are no weaknesses in such a structure, because everyone is connected to each other and all this with the participation of other networks.

We also talked about the growth of the state of the network and the redistribution of loads. Due to the fact that symbiotes are many independent chains, each of them "pulls" a part of transactions, users, and so on.

At the same time, the state of the network (actual data) and their history (actually the blockchain itself) do not add up to a large and heavy chain. In Bitcoin or other networks, you can usually only be sure of the validity of the state of the network and its security if you yourself become a full node, store the entire blockchain, and so on. In KLYNTAR, for example, if you have a 256 GB SSD, then you can support, for example, 1 symbiote, if you have more, you can support more, and so on. Requirements for you are not static, they say "you need storage for 1000 terabytes" and servers for 100 000 cores. You will be able to synchronize and start working faster, and this has a very positive effect on the decentralization of the network and ease of entry. The same principle applies to services (KLYNTAR Services) with which you will get acquainted in the following sections.

Also, KLY will store only a state, but not the full blockchain(due to the high speed of blocks generation). Nodes will store it for a period of time to allow everyone to verify the changes from state S1 to state S2.

Anyway state changes should be accepted by millions of validators(stakers) and commited on many hostchains, so you can be sure of the state validity.

### <mark style="color:red;">What is a symbiote made of?</mark>

<mark style="color:orange;">**Workflow**</mark>

The first and the main component of each symbiote is a workflow.

_<mark style="color:orange;">**Workflow**</mark>_ - a model of how some blockchain works. Here the consensus is determined, the set of events is determined (different transactions, account freezes, execution of smart contracts, etc.), the set of routes for the server is determined (for communication between nodes) and much more. Let's figure it out.

Workflow will be located in the KLY\_Workflows directory. Each subdirectory will be a repository for version tracking. You can see it on GitHub

![](<../../.gitbook/assets/image (12).png>)

Here you can see 3 workflows - _<mark style="color:red;">**dev\_controller,dev\_tachyon**</mark>_ and _<mark style="color:red;">**dev\_helloworld**</mark>_(template to allow developers to write custom workflows)&#x20;

_<mark style="color:red;">**dev\_controller**</mark>_ is a centralized version of the workflow. There is 1 validator, however, blocks can be generated by anyone who has the corresponding rate(stake).

<mark style="color:yellow;">Don't be intimidated by the presence of 1 validator for several reasons:</mark>

* This is convenient for local testing and testnet launch.
* This is the fastest workflow due to the lack of multiple parties. Symbiotes with such a workflow can be launched by some "enough trusted person" (for example, an exchange or some organization) following something like the Proof-of-Authority model.
* The main validator still cannot reject transactions (thanks to mutualism and SpookyAction) or change the history of the chain (thanks to hostchains and the overall attack budget)

_<mark style="color:red;">**dev\_tachyon**</mark>_ will be lightning-fast, asynchronous, with multi-million TPS, maximally parallel BFT blockchain using staking (including staking with unobtanium), BLS multi-signatures and other interesting features

{% hint style="info" %}
Currently, we're working on all of them
{% endhint %}

{% hint style="warning" %}
Right now, we haven't inserted Git submodules here, so you don't see the icon. As mentioned earlier, everything may change by the release version, but we also assume that the most used workflows will be part of the core, and not distributed separately
{% endhint %}

We assume there will be several workflows, however, due to the concepts of "good and fast blockchains" there will be only a few main ones that everyone will use. In general, even our division into a workflow with a controller (dev\_controller) and a decentralized dev\_tachyon already looks sufficient.

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