---
description: Why do services behave like symbiotes?
cover: ../../.gitbook/assets/3ce57b3f3bb818599a8259910fadd88e.gif
coverY: 0
---

# 💾 Milestones

### <mark style="color:red;">Service state commits</mark>

On the one hand, the services are independent of each other, and on the other hand, it is their interaction that amplifies the power of KLYNTAR Services. In order to add blockchain concepts to services, it is necessary that the latter have a single chain of their development - that is, everyone should be able to check the history of the service and be sure that throughout its existence it has worked as an honest blockchain.

Let me give an example, let's say we have some kind of service that acts as a decentralized off-chain oracle.

![](<../../.gitbook/assets/image (12).png>)

Without the history and evidence of the "work" of this service, potential users will not be able to be convinced of its honesty and reputation.

Let's imagine that other services use this oracle and the oracle decides to lie

![](<../../.gitbook/assets/image (14) (1).png>)

If there is no source where the oracle "attaches" its answers, then it will not be able to accumulate reputation and other services will not be able to know about its work.

### <mark style="color:red;">**Commits to symbiotes**</mark>

By storing part of the data or commits in symbiotes, it will be possible to track the lifetime and validity of the service. Returning to our example, if the oracle occasionally commits the hash of the root of the Merkle tree into a symbiote where the leaves of the tree would be the hashes of its predictions, then this second service could make sure that the oracle sacrifices its reputation, so trust in such there will be more data because the proof of a lie can be provided publicly (in the form of a path from the leaves to the root) and thus the reputation of the false oracle will be reset to zero, its token will depreciate and nothing good will happen.

### <mark style="color:red;">**Why commits to the symbiote**</mark>

Thanks to our architecture, you get a cheap and reliable source of storage. In addition, since other services will do the same, the value of the symbiote will increase according to Metclough's law of network utility.

{% embed url="https://en.wikipedia.org/wiki/Metcalfe's_law" %}

### <mark style="color:red;">Service autonomy</mark>

The service (more precisely, its developers) decide for themselves what to include in symbiotes, with what frequency, how everyone can verify their honesty, and more. We will publish more detailed information later.
