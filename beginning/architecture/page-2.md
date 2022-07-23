---
description: Bits in the world of blockchains
cover: >-
  ../../.gitbook/assets/tumblr_b800eb940c93611ad96334db121b1cf4_2323ada7_1280.webp
coverY: -249.75065387968615
---

# 👽 Symbiotes

### <mark style="color:red;">**Why Abstraction matters?**</mark>

We built KLYNTAR with the way the modern world works. Container shipping, USB standards, traffic routing - all this is interchangeable in the world and the same everywhere. When developing KLYNTAR, we did not try to "hardcode" a consensus there, which would then have to be changed for 8 years, we did not try to bind a fixed number of validators or impose any hard restrictions.

That is why the architecture is based on the principle of modularity when each individual symbiote can be built as a constructor, independently choosing a consensus (generally in KLYNTAR called _<mark style="color:yellow;">**workflows**</mark>_), a set of hostchains, the type of interaction with them, its own fees policy, and so on. That is why the architecture is based on the principle of modularity when each individual symbiote can be built as a constructor, independently choosing a consensus (generally in KLYNTAR called workflows), a set of hostchains, the type of interaction with them, its own fees policy, and so on.

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

{% hint style="info" %}
_<mark style="color:red;">**Symbiote**</mark>_ is a separate chain that has its own genesis, its own history of events, its own state, works following its own workflows and interacts with its own set of hostchains
{% endhint %}

![](<../../.gitbook/assets/image (8).png>)

A similar structure resembles a chain-link grid

![](<../../.gitbook/assets/image (4).png>)

There are no weaknesses in such a structure, because everyone is connected to each other and all this with the participation of other networks.

We also talked about the growth of the state of the network and the redistribution of loads. Due to the fact that symbiotes are many independent chains, each of them "pulls" a part of transactions, users, and so on.

At the same time, the state of the network (actual data) and their history (actually the blockchain itself) do not add up to a large and heavy chain. In Bitcoin or other networks, you can usually only be sure of the validity of the state of the network and its security if you yourself become a full node, store the entire blockchain, and so on. In KLYNTAR, for example, if you have a 256 GB SSD, then you can support, for example, 1 symbiote, if you have more, you can support more, and so on. Requirements for you are not static, they say "you need storage for 1000 terabytes" and servers for 100 000 cores. You will be able to synchronize and start working faster, and this has a very positive effect on the decentralization of the network and ease of entry. The same principle applies to services (KLYNTAR Services) with which you will get acquainted in the following sections.

### <mark style="color:red;">What is a symbiote made of?</mark>

<mark style="color:orange;">**Workflow**</mark>

The first and the main component of each symbiote is a workflow.

_<mark style="color:orange;">**Workflow**</mark>_ - a model of how some blockchain works. Here the consensus is determined, the set of events is determined (different transactions, account freezes, execution of smart contracts, etc.), the set of routes for the server is determined (for communication between nodes) and much more. Let's figure it out.

Workflow will be located in the KLY\_Workflows directory. Each subdirectory will be a repository for version tracking. You can see it on GitHub

![](<../../.gitbook/assets/image (2).png>)

Here you can see 2 workflows - _<mark style="color:red;">**dev\_controller**</mark> _ and _ <mark style="color:red;">**dev**</mark>_<mark style="color:red;">**\_**</mark>_<mark style="color:red;">**symbiland**</mark>_

_<mark style="color:red;">**dev\_controller**</mark>_ is a centralized version of the workflow. There is 1 validator, however, blocks can be generated by anyone who has the corresponding rate(stake).

<mark style="color:yellow;">Don't be intimidated by the presence of 1 validator for several reasons:</mark>

* This is convenient for local testing and testnet launch.
* This is the fastest workflow due to the lack of multiple parties. Symbiotes with such a workflow can be launched by some "enough trusted person" (for example, an exchange or some organization) following something like the Proof-of-Authority model.
* The main validator still cannot reject transactions (thanks to mutualism and SpookyAction) or change the history of the chain (thanks to hostchains and the overall attack budget)

_<mark style="color:red;">**dev\_symbiland**</mark>_ will be a BFT blockchain using staking (including staking with unobtanium), BLS multisig and other interesting features

{% hint style="info" %}
Currently, we're working on both of them
{% endhint %}

{% hint style="warning" %}
Right now, we haven't inserted Git submodules here, so you don't see the icon. As mentioned earlier, everything may change by the release version, but we also assume that the most used workflows will be part of the core, and not distributed separately
{% endhint %}

We assume there will be several workflows, however, due to the concepts of "good and fast blockchains" there will be only a few main ones that everyone will use. In general, even our division into a workflow with a controller (dev\_controller) and a decentralized dev\_symbiland already looks sufficient.

<mark style="color:orange;">**Connectors**</mark>

The second important component of symbiotes are connectors - modules for working with host chains. You'll get to know them in more detail in the [_<mark style="color:yellow;">**Connectors**</mark>_](../connectors.md) section, but for now let's just say that they define how your symbiote interacts with host chains. Connector developers, for example, create an interface for you, providing functions for working with a certain type of smart contracts on the host chain that supports them, or other methods of interaction. Workflow developers then take these connectors and insert them into their code at the right places. For example, send a state commit to Ethereum and Tron where there will be a multi-signature of validators as a payload, or generate a zero-knowledge proof and send it to the EVM for some contract of your symbiote.
