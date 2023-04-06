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

This gives users the opportunity to use the symbiotes they require, depending on the necessary tasks, and allows developers to create real monsters in the world of blockchains.

### <mark style="color:red;">More about workflows</mark>

Earlier we talked about how symbiotes can create or use ready-made workflow templates on their own.

Flexibility allows you to set up all sorts of necessary interactions inside the workflow - communicating with the API, using connectors, communicating with other nodes, and so on. Also here you should solve other problems - caching, processing of system signals, data storage, generation of snapshots, selection of validators and other problems specific to blockchains.

Use whatever you can think of )

![](<../../../.gitbook/assets/image (5) (1) (1).png>)

### <mark style="color:red;">**Create your own workflow**</mark>

Anyone on KLYNTAR will be able to create their own workflow if they have the necessary skills (programming, knowledge in the field of cryptography and understanding of the operation of blockchains).

Since within the workflow you actually describe how everything works (block generation, selection / change of validators, use of resources from other networks, interaction with hostchains), then the task of creating a really cool and necessary workflow falls on you - otherwise no one will use.

We assume the presence of several demanded workflows. Some workflow will be good for its speed, some security, the third will use zero-knowledge mechanisms, another one will use some of its own chips.

In this way, we allow new symbiotes to use the best available mechanisms for different needs. And users will be able to choose a symbiote for themselves, depending on what they require.

To make it easier for you to create your own workflow, there is dev\_helloworld. This is a workflow created as a template. It does nothing but print _<mark style="color:orange;">**Hello World from dev\_helloworld !!!**</mark>_ within a given period of time.

On GitHub in this repository is a README that includes the necessary hints to create your own workflow.

![](<../../../.gitbook/assets/image (2) (1).png>)

{% embed url="https://github.com/KLYN74R/KlyntarCore/tree/main/KLY_Workflows/dev_helloworld" %}

### <mark style="color:red;">Conclusion</mark>

Workflows amaze with their diversity and possibilities. We hope that the developers will appreciate our ideas and together we will create a lot of cool things for the industry
