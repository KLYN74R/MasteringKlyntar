---
description: >-
  What's inside anyway? Let's take a look at the chapters so you have a general
  idea of their content
cover: ../.gitbook/assets/pavel-blonde-girl-neon-light-iq.jpg
coverY: 468.55958549222805
---

# 👁 Overview

The encyclopedia includes many sections:

### <mark style="color:red;"></mark>[<mark style="color:red;">Cryptography</mark>](cryptography/)<mark style="color:red;"></mark>

Includes information about the crypto algorithms that will be used on Klyntar. Here you will learn about the reasons for the choice, about where and by whom it will be used and what their role is within the Klyntar processes

### <mark style="color:red;"></mark>[<mark style="color:red;">Architecture</mark>](architecture/)<mark style="color:red;"></mark>

Includes a description of the Klyntar architecture. Here we will talk about symbiotes, host chains, how sharding will be provided, cross-symbiote quantum swaps, workflows, thanks to which each symbiote will work according to its own scenario, and many other basic things

### <mark style="color:red;"></mark>[<mark style="color:red;">Services</mark>](services/)<mark style="color:red;"></mark>

Contains a description of the mechanisms of services: from what it is in general, why it is better than typical smart contracts and how it will affect the industry to creating it and making it part of the network!

### <mark style="color:red;"></mark>[<mark style="color:red;">Mutations</mark>](mutations.md)<mark style="color:red;"></mark>

Learn about the principle of mutations at Klyntar. Just as they work in nature, at Klyntar they bring constant improvement and positive change. For example, one symbiote could work using one set of asymmetric cryptography algorithms that is fast but takes up more memory, and another set of algorithms with a smaller signature but slower. But this is a simple example. In fact, the mutation mechanism is more complex, but at the same time an extremely useful thing that will be ahead of all other platforms precisely due to its multiplicity

### <mark style="color:red;"></mark>[<mark style="color:red;">Antivenom</mark>](antivenom-testnet/)<mark style="color:red;"></mark>

Here you will find a description of the Klyntar testnet, its capabilities and the widest possible functionality. Believe me, the usual testnets that you could meet in the framework of other crypto projects are not even close!

### <mark style="color:red;"></mark>[<mark style="color:red;">Code review</mark>](codereview/)<mark style="color:red;"></mark>

The section contains some descriptions of the individual parts of the Klyntar core. It should be especially useful for potential developers of various workflows, infrastructure operators and just inquisitive minds who are interested in what was on our minds when we "freaked something up again" and who would like to learn more about the kernel codebase. It is much more interesting to learn a detailed description from the developers themselves than to shovel thousands of lines of code yourself in an attempt to add 2 + 2. In addition, we fully admit that some of our logic could be wrong at some points, so with the help of the fact that you see our explanations, you will be able to more clearly understand what exactly we wanted to achieve and in case of our mistake, let us know and join active community!The section contains some descriptions of the individual parts of the Klyntar core. It should be especially useful for potential developers of various workflows, infrastructure operators and just inquisitive minds who are interested in what was on our minds when we <mark style="color:purple;">"freaked something up again"</mark> and who would like to learn more about the kernel codebase. It is much more interesting to learn a detailed description from the developers themselves than to shovel thousands of lines of code yourself in an attempt to add 2 + 2. In addition, we fully admit that some of our logic could be wrong at some points, so with the help of the fact that you see our explanations, you will be able to more clearly understand what exactly we wanted to achieve and in case of our mistake, let us know and join active community!

### [<mark style="color:red;">Unobtanium</mark>](unobtanium.md)<mark style="color:red;"></mark>

Let's start to tell what is unobtanium on Klyntar. It is important for us that hodlers of other cryptocurrencies, token holders of different projects, miners of PoW projects, stakers and other members of the crypto-loyal audience understand how they can use ALL their potential and resources on Klyntar!

### <mark style="color:red;"></mark>[<mark style="color:red;">Apollo</mark>](apollo.md)<mark style="color:red;"></mark>

Here we describe our CLI (_<mark style="color:purple;">Command Line Interface</mark>_) through which you can manage your entire infrastructure - nodes, clusters, services, and so on. I'm really proud of this tool, because the ecosystem of APIs, plugins, and so on maximizes the possibilities of an already flexible interface. All sorts of redefinitions, modularity, speed and versatility - you will learn about this

### <mark style="color:red;"></mark>[<mark style="color:red;">Runners</mark>](runners.md)<mark style="color:red;"></mark>

Learn more about the processes from the moment your service is deployed to the network to the moments of its practical use, off-chain interaction with other services, crypto projects, learn about amazing features, as well as how our future releases will change the concept of smart contracts and multichain interaction

### <mark style="color:red;"></mark>[<mark style="color:red;">Plugins</mark>](plugins.md)<mark style="color:red;"></mark>

Dive into the ecosystem of Klyntar plugins. We can say that the essence of plugins is one of the most useful and important components of the core. Start simple - for example, run custom event logging right at the kernel runtime when your node is running. Then move on to something more complicated - let, for example, the bot catches the most interesting services from the network, their offers, and, depending on your preferences, sends you a notification in Telegram (or your favorite messenger). And finally, high level - run a complex system of creating snapshots of the symbiotes you track in your cluster in such a way as to use memory as efficiently as possible. Interesting?) Then follow the link)

### <mark style="color:red;"></mark>[<mark style="color:red;">Filters</mark>](filters.md)<mark style="color:red;"></mark>

Required to filter incoming data from transaction events to service events. Thanks to the filters, you can set limits on calls to your infrastructure depending on your preferences, filter by IP addresses (for example, do not accept transactions if the IP belongs to TOR exit nodes). Quite a powerful thing - we recommend that you familiarize yourself

### <mark style="color:red;"></mark>[<mark style="color:red;">Monitors</mark>](monitors.md)<mark style="color:red;"></mark>

Since we are working in a multi-space, it is necessary to monitor the situation in other symbiotes, host chains such as Ethereum, Solana, Tron, Bitcoin and so on. It's good that you will have the opportunity to visit the appropriate repository where community members and the main KlyntarTeam team will publish ready-made solutions that you will need for normal work

### <mark style="color:red;"></mark>[<mark style="color:red;">Adapters</mark>](adapters.md)<mark style="color:red;"></mark>

Since the data will come from different sources, it is advisable to convert them to the format necessary for the nodes of your cluster: somewhere you need to cache the data or get only the desired field - adapters will do just fine with this

### <mark style="color:red;"></mark>[<mark style="color:red;">Connectors</mark>](connectors.md)<mark style="color:red;"></mark>

As you can see, Klyntar is very flexible and modular in terms of architecture. As you will be able to find out further, symbiotes and hostchains are the basis, I would even say BASE

![](<../.gitbook/assets/image (3).png>)

Workflows typical for blockchain projects are based on them: transactions and their non-rollback are fixed, stakes are burned and frozen, and other on-chain events are held. Soon you will learn how it all works, but for now it is important to know that the interaction between these two components works thanks to connectors that determine the logic of the blockchain events - somewhere you have to wait for 2 Bitcoin blocks and finalization on Solana, somewhere one Litecoin block and several ledgers are enough on XRP. I hope you are interested, so run to read)

### <mark style="color:red;"></mark>[<mark style="color:red;">Best practices</mark>](best-practices.md)<mark style="color:red;"></mark>

Here you will learn how to properly use the repository with best practices when building your own infrastructure, configuring plugins, their combination, and so on

### <mark style="color:red;"></mark>[<mark style="color:red;">Other projects</mark>](other-amazing-projects-coming-soon.md)

Find out more about other upcoming projects and projects already in development

### <mark style="color:red;"></mark>[<mark style="color:red;">Pseudo ICO</mark>](pseudo-ico.md)<mark style="color:red;"></mark>



### <mark style="color:red;"></mark>[<mark style="color:red;">Releases</mark>](releases.md)<mark style="color:red;"></mark>

### <mark style="color:red;"></mark>[<mark style="color:red;">CIIPs(Crypto industry improvements proposals)</mark>](ciips.md)<mark style="color:red;"></mark>

### <mark style="color:red;"></mark>[<mark style="color:red;">Information for exchanges</mark>](information-for-exchanges.md)<mark style="color:red;"></mark>

### <mark style="color:red;"></mark>[<mark style="color:red;">Quantum stuff</mark>](quantum-stuff.md)<mark style="color:red;"></mark>

### <mark style="color:red;"></mark>[<mark style="color:red;">Info for contributors</mark>](contributions.md)<mark style="color:red;"></mark>

### <mark style="color:red;"></mark>[<mark style="color:red;">Basic security</mark>](basic-security.md)<mark style="color:red;"></mark>

### [<mark style="color:red;">Social media</mark>](social-media.md)<mark style="color:red;"></mark>
