---
description: What are services and how do they differ from smart contracts?
cover: ../../.gitbook/assets/3217b0f22fea29ad0496b2fac1a1da39.gif
coverY: 0
---

# 🤩 Intro

### <mark style="color:red;">Starting point</mark>

For a long time, crypto-industry projects allowed the execution of smart contracts in a limited environment using various kinds of restrictions, such as WASM modules that run in a secure sandbox, special languages ​​such as Solidity (EVM), Scilla (Zilliqa), Clarity (Stacks), Marlowe (Cardano) or third-party technologies like BPF(Solana). This is excellent, normal and, perhaps, it should have been so, but still - such restrictions do not contribute to the development of the industry in any way.

In addition, such applications use the chain itself to interact with each other - oracle calls, contract executions, etc. take place on-chain, which is often expensive and costly.

But it would be cool to transfer most of logic to offchain, make scaling personalized for each smart contract separately, work asynchronously and independently of each other, use different technologies without restrictions, limits, and so on. Smart contracts in this case could exchange data off-chain, various decentralized exchanges would request oracle data quickly and for free, individual contracts could decide who should be allowed to execute for free, at what time, and so on. Well, the time has come.

### <mark style="color:red;">KLYNTAR Services</mark>

We present you KLYNTAR Services - a new type of smart contracts on KLYNTAR. Unlike normal contracts, which are very limited, here you have no hands tied.

<mark style="color:yellow;">**I will give a couple of examples of services that can be implemented and launched by you on KLYNTAR**</mark>

For example, you can write an oracle service that will provide information to everyone in off-chain mode. Or, it could be a decentralized exchange that will use these oracles.

You can write a new, improved Filecoin that, for example, will listen to Avalanche and Solana to interact with their smart contracts and so on.

You can write your own token that will track your activity on social networks, write cross-chain and multi-chain applications, use cloud computing, and much more.

What can I say, even if the automatic launch of symbiotes can be built using KLYNTAR Services.&#x20;

These are just a few of the "instant" ideas that come to mind when talking about KLYNTAR Services.

### <mark style="color:red;">Introduction</mark>

Services are your separate projects that will run in parallel with symbiotes and will execute their own logic. This is a separate repository that you publish somewhere on GitHub or on your resources and which is supported by KLYNTAR nodes.

You build and deploy your service to the network following certain rules. For example, Apollo has a service command that provides functionality for building service metadata, searching for services over the network (to download them locally and also become a node that supports the service), for scanning services for malware (encryptors, loaders, stagers for exploits, etc. .d.)

![](<../../.gitbook/assets/image (7) (1) (1) (1).png>)

So, after you create your service, you can deploy it to the network. The nodes accept an archive or links, and then a _<mark style="color:red;">**runner**</mark>_ comes into play - a service handler that decides whether it is worth launching the service in principle, whether you trust the author or whether he is included in your trust tree, whether enough anti-virus centers have checked this repository, what is the subject of this service (maybe you want to support only services that are aimed at privacy) and much more.

{% hint style="info" %}
We'll get to know runners later in the [_<mark style="color:purple;">**Runners**</mark>_](../runners.md) chapter. However, for now, let it be for you some black box that simply accepts an archive with a service and performs certain actions with it.
{% endhint %}

### <mark style="color:red;">**Visualization**</mark>

Now we will present you with a picture-diagram that we stole from the page about runners, but here you can clearly see what's what

![](<../../.gitbook/assets/image (8) (1) (1) (1) (1).png>)

Here, the nodes that work in the KLYNTAR network are marked in blue(for simplicity, we will not divide them into symbiotes here), and purple is the newly launched service.

Consider step by step:

1. <mark style="color:red;">**Deploying the service to the network**</mark>\
   \
   Sending an archive in a special format - with signatures, hashes and additional metadata (signatures of antivirus services that checked the repository, signatures of some addresses trusted by the nodes in order for the service to launch as many nodes, your personal rate so that in case of violations you can deprive you of your share , the subject of the service, keywords, links in social networks - the Telegram channel of the service, TOR mirror, and so on.\

2. <mark style="color:red;">**Nodes take this special format and pass it to the runner for further processing**</mark>\
   \
   At this level, everything depends on the flexibility and configuration of the runner. At this stage, all checks take place - signatures, rates, the runner decides whether you are interested in the service to run it, checks multi-signatures from anti-virus services, and so on.\

3. <mark style="color:red;">**If the service passes the test, then the runner deploys the service based on its own rules**</mark>\
   \
   The runner can run in a separate Docker / LXC container, use an existing container, run on different machines, and more.\

4. <mark style="color:red;">**The rest of the nodes do the same and, as you have already noticed, a second network is being formed already for the service**</mark>\

5. <mark style="color:red;">**The service starts its activity using a large number of KLYNTAR nodes, their capabilities, works in parallel with other services and can interact with them**</mark>

### <mark style="color:red;">**Services capabilities**</mark>

Services can communicate with each other, work on other chains, be an independent network, and so on. For example, a service can be an oracle for KLYNTAR symbiotes, store EVM chain smart contract data, be a separate DEX, and so on. You can create anything!

### <mark style="color:red;">Service examples</mark>

Below are examples of services that we took from our WhitePaper. Here is the following situation:

Suppose you have some kind of smart contract on Polygon that should determine the authors of the best exploits (no matter for which platform or software - we will skip these details for simplicity) depending on the severity level of the exploited vulnerability according to CVSS metrics.

This is a very real situation - such events can be held by some organization or company + the results may be necessary for some other blockchain logic (for example, transfer 10 units of some token to the winners or something like that).

Since it is impossible to do this at Polygon, you can contact KLYNTAR Services. The image below just describes the mechanism of operation of such a service. The service makes money by analyzing samples and can be written by some cybersecurity company.

![](<../../.gitbook/assets/image (9) (1) (1) (1) (1) (1) (1).png>)

The following mechanism is described here:

1. You are preparing a smart contract if it has not yet been published on the Polygon network. Here you can specify time limits for the contest, specify the ETH address of the service that is allowed to write to your contract (for example, to record results), specify the condition for the severity level of the exploit (for example, issue higher rewards for more dangerous exploits) and the link that you get from the service so that exploit authors can upload their code there for analysis.
2. Then you find the right service. We will create a separate resource for you, or you can independently find the services you need through social networks or advertising. For example, you go to services.klyntar.org and get what you need by category or keyword.
3. Next, you need to conclude something like a public contract - you pay the cost of the service in KLY coins or following other terms of the service. For example, for greater flexibility, the service may allow you to pay for your services in Bitcoin, Monero, interact with you through a smart contract, and so on.\
   \
   In any case, we need this step for your own safety - after all, if the service does not behave as it should, it will lose trust, and hence the potential earnings and stakers (more on that later)\

4. After all the procedures, the service will give you a URL where exploit authors can upload their work. The service will process the samples and then publish the results in a Polygon contract where the corresponding logic will be executed (for example, for the first place, the author with the address 0xaaa... will receive 1 ETH, for the second place - 50 some tokens, and so on). , the author of the exploit can first publish the hash on the contract to prove his authorship in the future.
5. Since the results are public (the result of work in Polygon, the results of the service), anyone can check the authenticity of what is happening and the "honesty" of the service. Stakers for the service receive their share of the payment for the operation of the service, as they have tied their KLYNTAR coins or unobtanium (their resources) to the service.

Yes, services can support staking, have their own token, and so on. Unobtanium is used here as an example of staking. The bottom line is that if stakers link their unobtanium to the service, then when it is used by third-party users or smart contracts, part of the payments will go to the stakers.

At the same time, if the service does not have users or its malicious behavior is noticed, then the service will not earn anything and will lose users or trust, and stakers’ stakes will simply “idle” all this time instead of receiving a percentage if they were placed on the other-honest service.

<mark style="color:yellow;">**Next example**</mark>

Here is a second example of a service. Here again you can see the possibilities of KLYNTAR. So, for example, here the roles are divided between the nodes into:

* Solana nodes
* Avalanche nodes
* Nodes scouts
* Nodes coordinators

![](<../../.gitbook/assets/image (3) (1) (1) (1) (1).png>)

Here is an example of a service that allows you to transfer NFTs, tokens and other resources between networks and at the same time, scout nodes bring certain additional functions. For example, he can see that if someone tries to sell your service tokens on Avalanche (we just called them WKLY, but you can have your own name) to the contract address, which is also some kind of token, then the scout nodes will see this event , scan the contract, find out the information, and if, for example, this is some kind of scam project, then the tokens after your sale to the attacker’s contract will be blocked and the scammer will not receive anything.

![](<../../.gitbook/assets/image (4) (1) (1) (1).png>)

Since such events are publicly available, the scout nodes can provide proof to the rest of the token holders of this service - why did they suddenly decide to block the tokens of some address. The rest will be able to get acquainted with this evidence, and if it really turns out that the tokens were transferred to the contract of some scammer, then there is no reason to panic and sell your service token. On the contrary, it will be a signal that the scout nodes have done a good job.&#x20;

Thus, new and future holders will similarly be able to be convinced of the correctness of actions within the framework of the life of this service.

### <mark style="color:red;">As a conclusion</mark>

Here we have described in general terms the mechanism of operation of services. We have tried to give you an understanding of why it is better than regular smart contracts, what features are behind KLYNTAR Services and much more.

In the future, we will also publish various tutorials and practices on how to create your own service, how to correctly form service metadata for greater distribution, and so on.

Follow us on social networks in order to always be aware of news and updates!
