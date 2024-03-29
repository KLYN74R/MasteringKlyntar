---
description: >-
  What's inside anyway? Let's take a look at the chapters so you have a general
  idea of their content
cover: ../.gitbook/assets/pavel-blonde-girl-neon-light-iq.jpg
coverY: 213.55958549222805
---

# 👁 Overview

The encyclopedia includes many sections:\


### [<mark style="color:red;">Architecture</mark>](architecture/)

Includes a description of the KLYNTAR architecture. Here we will talk about the main components - about **symbiotes** and **hostchains**, about how sharding will be provided (the _<mark style="color:purple;">**multilevel sharding**</mark>_), cross-symbiote and cross-subchain interaction works, workflows, thanks to which each symbiote will work according to its own scenario, total parallelization(asynchronous flows of verification and block generation) and many other basic things

### [<mark style="color:red;">**Cryptography**</mark>](cryptography/)

Includes information about the crypto algorithms that will be used on KLYNTAR. Here you will learn about the reasons for the choice, about where and by whom it will be used and what its role is within the KLYNTAR processes. You will learn about the use cases of various kinds of cryptography primitives - from symmetric encryption to multi-signature aggregation, the use of ring signatures and post-quantum schemes (PKE in off-chain DApps 2.0 processes, NIST candidate signatures of different security levels, etc.), usage of Zero- Knowledge-Proofs mechanisms and much more. No wonder we combined it all under the name _<mark style="color:purple;">**Cryptoland**</mark>_

### [<mark style="color:red;">**Smart-contracts and virtual machines**</mark>](smart-contracts-and-virtual-machines/)

The section is devoted to the description of the work of smart contracts on KLYNTAR. You will learn how to write typical smart contracts, how to use advanced features for your contracts such as API calls and Internet access, cross-chain logic, off-chain computing, cross-VM interaction and more

### [<mark style="color:red;">DApps 2.0</mark>](dapps-2.0/)

It contains a description of the mechanisms of next-gen DApps: from what they are in general, why they are better than typical smart contracts and how their application will affect the industry, to how they can be created and made part of the network. You will also learn how to use the capabilities of different blockchains to create a new generation smart contracts. Also, we'll talk about mutations

### [<mark style="color:red;">Testnets</mark>](testnets/)

Here you will find a description of the KLY testnets - AntiVenom(public) and how to set up your private testnet

### [<mark style="color:red;">Code review</mark>](codereview/)

The section contains some descriptions of the individual parts of the KLYNTAR core. It should be especially useful for potential developers of various workflows, infrastructure operators and just inquisitive minds who are interested in what was on our minds when we <mark style="color:purple;">"freaked something up again"</mark> and who would like to learn more about the core codebase. It is much more interesting to learn a detailed description from the developers themselves than to shovel thousands of lines of code yourself in an attempt to add 2 + 2. In addition, we fully admit that some of our logic could be wrong at some points, so with the help of the fact that you see our explanations, you will be able to more clearly understand what exactly we wanted to achieve and in case of our mistake, let us know and join active community!

### [<mark style="color:red;">Multistaking and unobtanium</mark>](multistaking-and-unobtanium/)

Let's start by telling what is unobtanium on KLYNTAR. It is important for us that hodlers of other cryptocurrencies, token holders of different projects, miners of PoW projects, stakers and other members of the crypto-loyal audience understand how they can use ALL their potential and resources on KLYNTAR!

### [<mark style="color:red;">Apollo</mark>](apollo/)

Here we describe our CLI (_<mark style="color:purple;">Command Line Interface</mark>_) through which you can manage your entire infrastructure - nodes, clusters, services, and so on. For example, generating different addresses (for a threshold signature, multisig addresses, post-quantum key pairs), checking service software signatures, voting for something, and so on. I'm really proud of this tool, because the ecosystem of APIs, plugins, and so on maximizes the possibilities of an already flexible interface. All sorts of redefinitions, modularity, performance and versatility - you will learn about this

### [<mark style="color:red;">Runners</mark>](runners.md)

Learn more about the processes from the moment your DApp 2.0 is deployed to the network to the moments of its practical use, off-chain interaction with other services, crypto projects, learn about amazing features, as well as how our future releases will change the concept of smart contracts and multichain interaction

### [<mark style="color:red;">Plugins</mark>](plugins.md)

Dive into the ecosystem of KLYNTAR plugins. We can say that the essence of plugins is one of the most useful and important components of the core. Start simple - for example, run custom event logging right at the runtime when your node is running. Then move on to something more complicated - let, for example, the bot catches the most interesting services from the network and, depending on your preferences, sends you a notification in Telegram (or your favorite messenger). And finally, high level - run a complex system of creating snapshots of the symbiotes you track in your cluster in such a way as to use memory as efficiently as possible. Interesting?) Then follow the link)

### [<mark style="color:red;">Best practices</mark>](best-practices.md)

Here you will learn how to properly use the repository with best practices when building your own infrastructure, configuring plugins, their combination, and so on

### [<mark style="color:red;">KLY ecosystem</mark>](kly-ecosystem-and-importance-for-the-world/)

Find out more about other upcoming projects and projects already in development

### [<mark style="color:red;">Pseudo ICO</mark>](pseudo-ico.md)

Learn more about how we decided to do the initial giveaway. No, this is not just a pre-sale in several stages. We guarantee a real decentralized distribution with the participation of other chains, Bitcoin & Ethereum miners, stakers of various projects, and so on, and the distribution itself will take place according to some quantum paradox - we will literally be able to influence the past. Recommended for reading at least for general acquaintance + understanding of who will become the first holders of our resources

### [<mark style="color:red;">Releases</mark>](broken-reference)

As part of the roadmap, of course, important updates are planned. We decided to give some information about the future releases & updates. Each of the releases represents a significant milestone in the development of the capabilities of KLYNTAR and the rest of the chains. Some of them will already be included in the first release of GammaBurst, some we have yet to implement

### [<mark style="color:red;">KIPs(KLY improvements proposals)</mark>](kips.md)

KLYNTAR is a completely open source and "controlled by community" story. Already at least from the descriptions of the previous chapters, we can conclude how we make sure that the community is maximally involved in the process of developing and improving KLY. At the same time, the country must know its heroes, which means that the contribution of each must be appreciated. Read more about it in this chapter

### [<mark style="color:red;">RWX contracts</mark>](rwx-contracts-real-world-execution-smart-contracts.md)

Learn about a new stage in the world of smart contracts. Codeless contracts for real world use and audited by KLY. Must have for **KLY Services**.

### [<mark style="color:red;">Quantum stuff</mark>](quantum-stuff.md)

One of my hobbies and passions is the wonderful world of quantum mechanics. In this section, the team will share their thoughts on the era of quantum computing and the role of cryptocurrencies in it

### [<mark style="color:red;">Info for contributors</mark>](contributions.md)

A little guidance and information for those who are going to become a KLY contributor

### [<mark style="color:red;">Basic security</mark>](basic-security.md)

Network security is one thing, quite another is when attacks occur through other channels. In the best case, the security guards find out about the oversight and promptly correct it, in the worst case, a post about the <mark style="color:purple;">**TOP DROP appears on the pages in social networks, SO SEND ME COINS, AND I WILL RESPOND TO YOU x2**</mark>. It seems ridiculous they say "who are the suckers who are being conducted", but that's just the accounts / sites of even large projects are amenable to attacks. As an example, the latest [_<mark style="color:red;">**attacks on Bored Ape accounts on Instagram**</mark>_](https://www.theverge.com/2022/4/25/23041415/bored-ape-yacht-club-nft-hack-instagram) are recalled, or, for example, the [_<mark style="color:red;">**case when the following appeared on the Twitter accounts of Gates, Musk and other famous people**</mark>_](https://www.nytimes.com/2020/07/15/technology/twitter-hack-bill-gates-elon-musk.html)

![](<../.gitbook/assets/image (3) (1) (1) (1) (1) (1) (1).png>)

Since we do not need this, we recommend that you read this chapter to understand how KlyntarTeam will deal with this

### [<mark style="color:red;">Social media</mark>](social-media.md)

Our social media links & other content
