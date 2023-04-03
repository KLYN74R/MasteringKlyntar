---
description: Where does it all start
cover: >-
  ../../.gitbook/assets/wallpapersden.com_cyberpunk-2077-digital-art-2020_3840x2160.jpg
coverY: 213.89119170984452
---

# ☕ General

### <mark style="color:red;">**Let's talk about the structure**</mark>

Working on KLYNTAR, we tried to make the project so powerful that it would surprise you, like when you were 8 years old when you found out that Santa Claus does not exist. We want to resurrect the time of useful projects by creating cool things for our industry, such as Unobtanium (so you can use your bitcoins, ethers, etc. to stake on KLYNTAR), KLYNTAR Services (so you write off-chain logic for KLYNTAR, other blockchains and the entire Internet and run them on millions of nodes at once relying on the security of KLYNTAR), Hivemind (to optimize the operation of symbiotes), SpookyAction (to launch contracts and execute transactions on any chain with the theoretically fastest speed in the industry), symbiotes and much more!

Symbiosis with other projects (chains) will give you the opportunity to use the best and much-loved features of other cryptocurrencies, as well as expand the capabilities of existing blockchains and your new ones that you will create on KLYNTAR. The point is to combine both new blockchains and old ones into one super organism and revolutionize the crypto industry! Shared resources, different consensuses, BTC miners, ETH token holders, Solana validators, maximum security based on the security of the entire crypto industry - this is all about KLYNTAR :)

![](<../../.gitbook/assets/image (1) (2).png>)

Above you see the general scheme taken from our whitepaper of the first version. Unlike other crypto projects, KLYNTAR does not have some kind of main chain, beacon chain or something like that that synchronizes and interleaves work in shards or coordinates blockchains (like Polkadot or Cosmos). We consider the entire blockchain space as a single reliable homogeneous environment and each blockchain is like a certain reliable container.

KLYNTAR consists of many parallel chains that we call _<mark style="color:yellow;">**symbiotes**</mark>_(they are represented in the diagram as parallel multi-colored rectangles). They got this name because they enter into a symbiotic relationship with other entities - _<mark style="color:yellow;">**hostchains**</mark>_(from the words host-carrier and chain-chain, shown at the top of the diagram). This connection is necessary for many reasons:

* _<mark style="color:orange;">**Maximum theoretical safety**</mark>_\
  \
  What could be safer than all crypto projects put together? By including its state commits in the host chains, KLYNTAR guarantees maximum security in terms of non-reverting and finalizing the updated state. To hack, the enemy now needs to buy back all the assets of PoS projects, cooperate the entire mining power of PoW projects, and get validator positions in different chains where delegation is practiced. We do not rely only on Bitcoin or only Ethereum. We do not rely on 21 validators and are not afraid of 5 mining pools. And also we are not tied to one chain, being completely dependent on it\

* _<mark style="color:orange;">**Movement flexibility**</mark>_\
  \
  If it becomes expensive to make commits on one chain or contact validators to execute a smart contract, then the mutation mechanism makes it easy to change the set of host chains or workflow\

*   _<mark style="color:orange;">**Rationality**</mark>_\
    \
    It would be illogical if we had a single KLYNTAR chain linearly and stupidly included its commits in all projects. It even sounds scary. After all, then you need to track all the other chains + it would be expensive and unprofitable.

    However, due to the fact that we have an infinite number of parallel symbiotes, you can choose to run a node or cluster with one, two or more symbiotes to track and work on it. Symbiotes interact with each other to include commits of their states in more networks.

    So one symbiote can commit to Bitcoin, Polygon, and Solana, and the other can commit to XRP, Litecoin, and Cardano. They include each other's commits in their set of host chains, and each of them pays a fee on only three networks, but in reality, there are now 6 host chains guarding their security. This was the simplest example\

* _<mark style="color:orange;">**Sharding-by-default**</mark>_\
  \
  A fundamental concept that allows symbiotes to work in parallel and independently of each other. Also, the default concept of sharding (with many symbiotes) allows you to share the load of interaction with other chains. Thus, one symbiote will be able to interact with your contracts on Cosmos, Solana and Polygon, and the other one will be able to read data from the Bitcoin chain and change the state, for example, on Ethereum contracts.

### <mark style="color:red;">**More about hostchains**</mark>

Why tie yourself to one circuit if you can immediately secure it to the maximum using various flexible circuits. With this thought, we sat when we planned the architecture and studied the documentation of other projects. We also know about the principle of operation of Polygon, various L2 projects on Ethereum, about RSK and even about Stacks, but KLYNTAR is about something else.&#x20;

By communicating with many chains, KLYNTAR brings security for them too due to the fact that KLYNTAR node and cluster operators can also run hostchain nodes and due to the fact that we rely on the security of hostchains( which means we are interested in their market value and development). We will talk about the trust market further and believe me, even if you now have a running infrastructure of other cryptocurrencies, you will already be useful on KLYNTAR and will be able to get what you need here.

### <mark style="color:red;">**More about symbiotes**</mark>

If you haven't figured it out yet, we've managed to build a project with the highest level of parallelism thanks to the symbiote architecture. The advantage here is that after the initial kNULL symbiote that our team launches, which will be the starting point for KLYNTAR, we will continue to launch other symbiotes. Thus, if the initial symbiote had a high load and completely clogged blocks, then the opening of a new parallel symbiote will transfer some of the transactions and load to the second chain. Due to the fact that the new chain will also require a security budget, it will be beneficial for the validators of the first symbiote to move there. As an analogy, you can imagine the discoverers of some continents - new lands, new opportunities. Also, it motivates some users to transfer their assets to a parallel chain.

This process will be repeated indefinitely, and along with it, opportunities, security and scalability will grow.

<mark style="color:purple;">**Security**</mark> - by increasing the number of host chains where the KLYNTAR state will be saved&#x20;

<mark style="color:purple;">**Scalability**</mark> - due to the parallel operation of symbiotes

<mark style="color:purple;">**Opportunities**</mark> - due to the fact that the new symbiote will attract new stakers, developers, and so on

Anyone can create their own new blockchain and attach it to the rest of the symbiotes. At the same time, your blockchain (symbiote) will immediately receive the security of KLYNTAR, will be supported by KLYNTAR nodes, and so on.

### <mark style="color:red;">Modularity</mark>

{% embed url="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FphIHWZY173DpNXBbDjVg%2Fuploads%2F2me78ElgBRbButusA65K%2Fthoughtworks-gif_dribbble.gif?alt=media&token=7516ff53-82b8-4683-9aea-0c1634767590" %}

By reading the documentation further or looking at the code on GitHub, you will notice that many of the directories contain subsections

For example, the directory for interacting with hostchains looks like this:

![](<../../.gitbook/assets/image (5) (1) (1) (1) (1).png>)

Directory with workflows:

![](<../../.gitbook/assets/image (1) (3).png>)

As you can see, they all include several packs. This modular structure allows one symbiote to work using some consensus script in controller mode, and another to follow the BFT consensus. Well, or, for example, choose a pack for working with hostchains.

KLYNTAR will also be available for expansion with a wide ecosystem of plugins - from a websocket servers to custom logging mechanisms, from a reverse proxy server with filters to a Telegram bot. By the way, one more proof of modularity and independence (the directory with plugins contains separate repositories)

![](<../../.gitbook/assets/image (6) (1) (1) (1).png>)

Learn more about plugins [_<mark style="color:red;">**here**</mark>_](../plugins.md)_<mark style="color:red;">****</mark>_
