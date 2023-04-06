---
description: Description of all constituent components
cover: >-
  https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FphIHWZY173DpNXBbDjVg%2Fuploads%2FM2MclBOlBzrks2Dyio4P%2Fphoto_2022-07-10_07-40-08.jpg?alt=media&token=b492d4f3-02ec-45fe-b487-6e18ddd85416
coverY: 137.9124579124579
---

# ⛓ Interactions with hostchains

### <mark style="color:red;">Short intro</mark>

KLYNTAR has a high degree of parallelization due to its architecture. In this regard, interaction with hostchains fits perfectly into this paradigm. We tried to divide the functionality into units, the separate existence of which would seem justified.

## <mark style="color:red;">Components</mark>

### <mark style="color:red;">Connectors</mark>

_<mark style="color:orange;">**Connectors**</mark>_ are the first and main component. Thanks to them, the symbiote interacts with the hostchains. A connector is essentially a module that exports the functions necessary to work with the hostchain.

For example, one connector allows you to commit a symbiote to some EVM chain using the smart contract's _<mark style="color:yellow;">**.makeCommit(symbiote\_hash,block\_index)**</mark>_ function and then check the inclusion using the _<mark style="color:yellow;">**.checkCommit(symbiote\_hash,block\_index)**</mark>_ function.

The other connector provides functions for working with Solana and an API for working with Solana programs. The third connector will work with Bitcoin and its forks for commits to Bitcoin-like chains using the features of the stack language.

### <mark style="color:red;">**Monitors**</mark>

Monitors are the second component. Monitors are your eyes in hostchains and symbiotes. Again, they work in parallel with the core (it can be a separate process, or you can even run the monitor on another machine or container) and monitor the events of other blockchains.

{% hint style="info" %}
Technically, no sense to split functionality. You can write a single module to interact with hostchain and it can be used by appropriate workflows
{% endhint %}
