---
description: The heart of any symbiote
cover: ../../../.gitbook/assets/951080b614db5517e5d24e55c46dca05.gif
coverY: 0
---

# 📄 Workflows

### <mark style="color:red;">Brief information</mark>

Every blockchain project you know works according to the scenario described by the programmers. Some use PoW consensus (Bitcoin, Monero, ETC), some rely on BFT modifications (Avalanche, Fantom) or PoS (Ethereum 2.0, Cardano).

In operation, some use VDF or multi-signatures, Pederson commitments, and zkSNARKs. All different. Everyone is good at something.

In order not to constrain developers and users, we allow each symbiote to work following its own rules, commission policy and so on.

This gives users the opportunity to use the symbiotes they need, depending on the necessary tasks, and allows developers to create real monsters in the world of blockchains.

### <mark style="color:red;">More about workflows</mark>

Earlier we talked about how symbiotes can create or use ready-made workflow templates on their own.

Flexibility allows you to set up all sorts of necessary interactions inside the workflow - communicating with the API, using connectors, communicating with other nodes, and so on. Also here you should solve other problems - caching, processing of system signals, data storage, generation of snapshots, selection of validators and other problems specific to blockchains.

Use whatever you can think of )

![](<../../../.gitbook/assets/image (5) (1) (1).png>)

### <mark style="color:red;">More about dev\_controller</mark>

Let's take the initial workflow [_<mark style="color:red;">**dev\_controller**</mark>_](https://github.com/KLYN74R/KlyntarCore/tree/main/KLY\_Workflows/dev\_controller) as an example. At the level of its code, it is determined that it has a main validator and at the same time, allows you to bet on other nodes that can also generate blocks. This workflow is presented in the image examples earlier. You may have seen it on the [_<mark style="color:red;">**Symbiotes**</mark>_](../page-2.md) page

![](<../../../.gitbook/assets/image (6) (1).png>)

Here, it is clear that he is the main one(big black server). Don't worry, this won't affect decentralization even for this workflow in any way, although we will have other variations(e.g. super decentralized _<mark style="color:red;">**dev\_tachyon**</mark>_ based on BFT).

In the code, you might notice two types of blocks. This is defined at the level of this workflow and is intended for the respective roles - the main validator Controller (and ControllerBlock) and nodes that can also generate InstantGenerators (for them - InstantBlocks).

![](<../../../.gitbook/assets/image (11) (1) (1) (1) (1).png>)

During work, the controller collects all these blocks(which contains of txs, contract calls and so on) into a ControllerBlock and sends a commit to the hostchains or perform other logic via connectors(e.g. change some contract's state). This is what this stage looks like

![](<../../../.gitbook/assets/image (17) (1) (1) (1) (1) (1).png>)

At the connector level, a simple inclusion is defined (no additional logic). Also, the controller does not have the right to spend its stake between commits. A similar rule works for InstantGenerators - they can sign the only valid chain received from the controller and then check that it was included on the hostchain.

If not, then you can provide proof to other symbiotes and the controller will lose the bet. At the same time, if your transaction got into a non-rollback block (with a green frame), then everything is in order - now hostchains and other symbiotes are on guard against non-rollback.

Only after the next commit it will be possible to collect the bet and you can make sure that your transaction was non-rollback

### <mark style="color:red;">**Features**</mark>

<mark style="color:yellow;">**Phantom blocks**</mark>

{% hint style="info" %}
Phantom blocks will be present in other KLYNTAR workflows
{% endhint %}

An important feature of each workflow is its features. So for example workflow dev\_controller has parallel check and block generation flows.

In addition to being a very fast workflow, it has an important feature - _<mark style="color:red;">**phantom blocks**</mark>_.

Phantom blocks allow not to generate blocks of a certain size once for a period of time, but allow the controller or the current validator (if it is not a dev\_controller workflow) to release ALL transactions that it has into the world at once. Later, the asynchronous validation flow will reach these blocks and make state changes.

So, don't be surprised if there was just a 100,000 block, and 2 seconds later another 100 blocks appear.

Let's do a visualization. First, consider the verification and generation flows.

![](<../../../.gitbook/assets/image (15) (1) (1) (1) (1) (1).png>)

Green ones are blocks that the node has already checked, dotted ones are those that were generated at a time, a couple of seconds after the previous batch.

In this case, the validators and signers sign the block with the maximum height and its hash - in this case, block 119.

Due to this, the development of the symbiote chain is instantly formed. It does not matter that blocks have not been verified before, it is important to approve a single chain. From this moment on, even more interesting things begin.

<mark style="color:yellow;">**Confidence in validity**</mark>

Since we have not checked the blocks before (starting from 110th), we cannot know what are the current account balances and what are the states of smart contracts. This is because a potential attacker can send transactions to different nodes, so even if they kept some kind of local account, it is still impossible to verify the current state without a full check.

In this case, we use a certain pre-confidence. We trust our users and, as it were, say:

> We allow you to transact asynchronously and freaking fast, but be honest with the network. Otherwise, you will lose some of your coins

Let's imagine that in block 109, which is already validated, user X froze part of his bet and somehow said

> I bet my 100 KLY that in the next 1000 blocks I will not break anything and all my transactions will spend no more than I have, have the correct nonce and generally be valid

If during blocks 110 - 119 at least one incorrect transaction is noticed from the side of address X, then the network will deprive it of 100 KLY.

<mark style="color:yellow;">**Local Observations**</mark>

Through social interaction, the risk of invalid transactions can be minimized. So, for example, thanks to various plugins on KLYNTAR, you can set up the acceptance of transactions from the conditional Binance or CoinBase. You will assume that it is unlikely that such exchanges are profitable to carry out attacks against KLYNTAR and spam with invalid transactions, so accept their transaction and put it in a block.

Also, nodes can maintain their local lists of who spent how much (and thus reject invalid transactions even at the stage of accepting them on the server) and take advantage of other benefits of plugins and features of workflows

The final stage - checking on wallets

Another advantage is that your wallets (if they support this functionality) can process payments from other addresses instantly thanks to phantom blocks.

Let's look at our example - let's say you expect some customer Bob to pay for his order in your online store. you gave him your address

_<mark style="color:orange;">**FWZbuAkX6hAbpg5c9QixUxwjiWdSHMSLPBqHM1hoh8mc**</mark>_

for him to pay. At the same time, block 109 has already been checked and you know that Bob has 100 KLY coins there. Let your product cost 10 KLY.

After the network instantaneously produces 10 more blocks (110-119), your wallet (or a specialized API on the backend of your store) will load these blocks and quickly check for the necessary transaction. At the same time, you should not even check other transactions - you just take only those where Bob is the sender and check. At the same time, you already have a multi-signature of validators in your hands, they say

> 119 block with hash aaaaa.... - already part of the blockchain

If you find a valid transaction in this series of blocks from Bob in payment for your product, then everything is fine - you can send the product. Let's say you found her in block 116. Now you have confidence in your hands that Bob's transaction is valid and that block 119 with the required hash has entered the symbiote chain. And this despite the fact that you have not yet verified other transactions and blocks 110-119 on your node are still not verified. That's all the magic)

<mark style="color:yellow;">**Configuration**</mark>

Yes, the flexibility of this workflow can also be attributed to the configuration - you can find it here:

{% embed url="https://github.com/KLYN74R/KlyntarCore/blob/main/ANTIVENOM/CONFIGS/symbiotes.json" %}

Here you can flexibly configure the block generation time, stop and start block generation and verification flows, configure the polling time for new blocks, configure the TTL of the server, allocate separate endpoints for loading blocks from there (this can be some kind of CDN, for example, because blocks are static content) and much more. We recommend that workflow developers also make their configurations fairly detailed.

### <mark style="color:red;">**Create your own workflow**</mark>

Anyone on KLYNTAR will be able to create their own workflow if they have the necessary skills (programming, knowledge in the field of cryptography and understanding of the operation of blockchains).

Since within the workflow you actually describe how everything works (block generation, selection / change of validators, use of resources from other networks, interaction with hostchains), then the task of creating a really cool and necessary workflow falls on you - otherwise no one will use.

We assume the presence of several demanded workflows. Some workflow will be good for its speed, some security, the third will use zero-knowledge mechanisms, another one will use some of its own chips.

In this way, we allow new symbiotes to use the best available mechanisms for different needs. And users will be able to choose a symbiote for themselves, depending on what they need.

To make it easier for you to create your own workflow, there is dev\_helloworld. This is a workflow created as a template. It does nothing but print _<mark style="color:orange;">**Hello World from dev\_helloworld !!!**</mark>_ within a given period of time.

On GitHub in this repository is a README that includes the necessary hints to create your own workflow.

![](<../../../.gitbook/assets/image (2) (1).png>)

{% embed url="https://github.com/KLYN74R/KlyntarCore/tree/main/KLY_Workflows/dev_helloworld" %}

### <mark style="color:red;">Conclusion</mark>

Workflows amaze with their diversity and possibilities. We hope that the developers will appreciate our ideas and together we will create a lot of cool things for the industry
