---
description: Turtles and elephants on which to hold symbiotes
cover: ../../.gitbook/assets/DeterminedEssentialHoki-size_restricted.gif
coverY: 0
---

# 👨👩👦 Hostchains

## <mark style="color:red;">What is considered a hostchain?</mark>

A **hostchain** is a chain (blockchain) whose security symbiotes rely on. It can be said that this is a carrier chain (host). Depending on the hostchain and its capabilities symbiotes enter into a variety of relationships with them - from simple commits of state to advance usage like protection from unavailability, transactions over hostchains(when you interact with Solana or Tron, for example, to call some contract on symbiotic chain) and so on

Hostchains in KLY will be various reliable networks such as Bitcoin, Ethereum, Solana, Near, TON, Cardano, BNB, XRP, and so on. It is on their general decentralization, fault tolerance and security that the symbiotes in the KLY ecosystem will rely

## <mark style="color:red;">Standard process for interacting with hostchains</mark>

This was originally planned - each of the symbiotic chains just makes a checkpoint of its state into the hostchains from time to time for the purpose of long-term security. The idea was to provide the only possible state of the symbiote in the long run.

{% hint style="info" %}
The maximum security threshold in the industry is the total resources that need to be spent on an attack on all blockchains such as PoW power to attack Bitcoin, Ethereum Classic, Monero, etc., the cost of stakes in order to become a validator on Ethereum, Solana or Avalanche, etc.
{% endhint %}

Therefore, if you make a checkpoint for example in 10 blockchains, then you can be sure that even if in the future one of them ceases to exist or undergoes a state rollback attack or ceases to be decentralized enough, the state of the symbiote will still remain safe. This is the perfect defense against long-range attacks, Sybil attacks (because you have many decentralized data sources in the form of nodes of other blockchains that have their own economic interest in maintaining the integrity of their hostchain) and so on.

<figure><img src="../../.gitbook/assets/HostchainsImage1.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (64).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/HostchainsImage2 (1).png" alt=""><figcaption></figcaption></figure>

In fact, imagine if you want to run a node to work on some of the symbiotes in the KLY ecosystem, but you can’t figure out which of the states A or B is valid. To do this, you can look into the blockchains of Bitcoin, Solana, Avalanche, Aptos and others where you will see that the state of a certain symbiote is still A, not B.

A little later, it was decided to implement **hivemind** - a mechanism for receiving checkpoints from other symbiotic chains in order to include it in your own checkpoint, and then in your set of hostchains. This allows you to pay less(after all, transactions on host chains cost money), but at the same time create a greater level of security.

<figure><img src="../../.gitbook/assets/HostchainsImage3 (1).png" alt=""><figcaption></figcaption></figure>

## <mark style="color:red;">Security budget and how hostchains will help us</mark>

TODO

## <mark style="color:red;">**PoW and PoS hostchains. Advantages and disadvantages**</mark>

We have moved on to an important topic. Since all hostchains are different, they all use different consensus algorithms. This is important for KLYNTAR, as it is about what is considered a finalization, whether this hostchain can be generally trusted, and so on. The dispute between PoS and PoW supporters has not faded away for a very long time, and each of them is right in its own way. But here we will rather not talk about classical PoW and PoS, but about two large groups of algorithms:

* Those who spend real resources (through mining, wasting memory, time)
* Those who rely on the intrinsic value of their coins (PoS and modifications, various BFTs, etc.)

Some of them offer probabilistic finality, some guarantee instant finalization. In addition, often PoS proponents do not like to mention all sorts of long range attacks (when old validators create a fork from some earlier blockchain height and you now cannot know which one is valid. At the same time, slashing does not work, because old validators won't lose anything), although mining also has its own problems. Some (Zilliqa and others) are proposing a hybrid approach where PoW and PoS work together.

By having certain logic run on the symbiote workflow, you don't have to worry about communication with hostchains being expensive or under attack.

For example, in our workflow (workflows) it is planned to make sure that the validators hold the stake between commits to the hostchains. Thus, between two interactions with a hostchain, security and non-reversion is ensured by the rates of symbiote validators, and after the commit, security is already provided by the hostchains.

<mark style="color:yellow;">**Let's take an illustrative example**</mark>

![](<../../.gitbook/assets/image (13) (1) (1) (1) (1).png>)

From now on, this is a new non-returning point in the history of the symbiote. Both hostchains on PoW (Bitcoin) and on PoS / BFT (Solana and Avalanche) are used here. The state of the symbiote is protected both by the resources actually spent, and by the value of virtual assets and the value of networks.

However, to speed up + reduce the cost of such interactions, the symbiote interacts with hostchains at a selected frequency - once an hour, once a day, and so on. The longer the time between interactions, the longer validators and bidders cannot unlock their bids. Their coins are used as a security deposit.

So, in our example above, the interaction happens in a new block. Let these be blocks A, B and C for Solana, Avalanche and Bitcoin, respectively.

Suppose that all this happened for a block with an index of _<mark style="color:orange;">**100,000**</mark>_ and a hash _<mark style="color:orange;">**adcdef...**</mark>_. In this case, the nodes sign this data and publish their signatures.

![](<../../.gitbook/assets/image (7) (1) (1).png>)

We used multi-signatures here, which you will get acquainted with here, but for now let them be a kind of black box for you that will collect signatures and public keys of validators and aggregate them into a single proof.

As we can see above, the nodes have signed and now security and non-rollback are ensured by:

* Hostchains
* Signers on KLYNTAR

In this case, the signers' security budget is 60,000 KLY, but in general, you understand that it will be more. Moreover, workflow features are also the fact that not only direct validators can bet on the symbiote block. Third-party stakers don't even need to know what's inside - their job is to ensure the existence of a single valid chain.

<mark style="color:yellow;">**What's next?**</mark>

Since we are efficient, from block 100,000 until the next day (assuming the symbiote saves data to the hostchains once a day), security is provided by the symbiote's nodes and other signers.

They work extremely fast, generating many blocks per second (thanks to phantom blocks, which you will learn about in the next section) following the rules of their workflow.

Each block is signed in the same way as shown above, and the proof is also distributed over the network.

During the entire period between commits to the hostchains, the stakes of the signers are frozen. Thus, if necessary, they can be slashed and, if there is evidence that one of the validators signed a different version of the symbiote blocks, to deprive him of his bet.

In our example, it turns out that those who have frozen rates will not be able to unfreeze them for 1 day. As soon as the time for a new interaction session comes, the set of validators can be changed. You, if necessary, unfreeze your bet and leave with the interest earned, and other signers can be appointed in your place.

## <mark style="color:red;">Also an important appeal to the miners of current PoW projects</mark>

Do not rush to throw away the equipment. KLYNTAR will provide you with new opportunities️ 🧙‍♂️

![](<../../.gitbook/assets/image (9) (1) (1) (1) (1) (1).png>)

## <mark style="color:red;">Hivemind</mark>

Hivemind is the future of KLYNTAR's hostchain enhancements. In short, the symbiotes will exchange data with each other and ensure their safety and the safety of other symbiotes by measuring the block generation time in different hostchains (for the fastest possible finalization). Also, it will favorably affect the fact that interactions with hostchains will become cheaper and faster.

## <mark style="color:red;">Methods of interaction with hostchains</mark>

Symbiotes interact with hostchains using connectors or APIs. Such interaction occurs both at the workflow level and at the service level (KLYNTAR Services).

Maturing question

> Does this mean that I will need to run hostchain nodes???

No, don't worry, everything is cooler and more interesting here. Yes, in order to interact with hostchains within workflow and KLYNTAR Services, you will need to somehow communicate with other blockchains.

Here is an example connector for EVM chains

![](<../../.gitbook/assets/image (3) (1) (1) (2).png>)

{% embed url="https://github.com/KLYN74R/KlyntarCore/blob/main/KLY_Hostchains/connectors/dev0/evm.js" %}

It can be seen that here the Web3 module needs an endpoint address. Similar can be found in other connectors.

Here it is - if you have a node - use it, otherwise you have a whole range of possibilities:

* Use Node-as-a-Service Services
* Use public (but trusted) nodes
* Use nodes that can be rented out by those who have them

This way you can get started quickly without using your own resources. However, you should be careful - if you need to sign something on KLYNTAR after verification from the hostchain, then with false data from a malicious source, you risk losing your money.

{% hint style="info" %}
We will publish more detailed information later
{% endhint %}

{% hint style="info" %}
This page will be updated. Stay tuned so you don't miss anything important
{% endhint %}
