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

![](<../../.gitbook/assets/image (7).png>)
