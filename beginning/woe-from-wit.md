---
description: Some of our thoughts before we start
cover: ../.gitbook/assets/533240_cWTTOpjP0V_wrench.jpeg
coverY: 139.54231433506044
---

# 🧠 Woe from Wit

![](../.gitbook/assets/cb0586c52d9c39c873e43de91c59c39c.jpg)

### <mark style="color:red;">Crypto in 2k22, hustle culture and 1001 ideas</mark>

I'm sure if you're reading this, it means that you're probably interested in the latest in our field in one way or another. We do not care if you are a developer, an investor, a crypto enthusiast or an SEC agent. I think we will be able to convey to you the beauty of the decisions and developments made and the "gigantism" of thoughts.

Again, as mentioned earlier, due to close acquaintance with the technical characteristics of other projects, our head was spinning - after all, how can we surprise users, if it would seem that so much is already available - all sorts of DeFi, DEX, NFT marketplaces, cross-chains and other. Because of this, I had to spend a lot of time searching for tricky solutions that no one had thought of yet, choosing the best ones between different algorithms (for example, for generating key pairs, hashing, KEX mechanisms, etc.). What about by consensus? Your own solution or take a proven one? PoS or something based on real resources? What about scalability? Should we try to overtake Solana or focus on something else? How to solve the problems of PoS finalization, which has recently become more and more popular in conjunction with BFT mechanisms and (which is a pity for us) is replacing PoW with its "real resources"?

All this is just a part of the questions that arise in the minds of blockchain developers at the design stage. It becomes more difficult when it comes to implementation. Here one plan can replace another, then it turns out that the consensus you have chosen turns out to be absolutely not scalable in practice, and algorithms that yesterday still seemed good to you today already graze the backs of some new NIST "favorites".

With this text, we want to show that KLYNTAR was born in discussions, in the abyss of brainstorms and constantly changed to meet the necessary requirements. In the end, as a result, you are reading this document, which means that we still managed to create _<mark style="color:red;">**Frankenstein's monster**</mark>_, and now you will learn how.

### <mark style="color:red;">But in a nutshell, what do you mean?</mark>

I could answer here with the words of Newton from Silicon Valley, they say

> _<mark style="color:purple;">**You can't delve into smth quickly. To delve means to read carefully and scrupulously**</mark>_

However, before starting reading serious docks further, I will still clarify

![](https://readme-typing-svg.herokuapp.com/?font=Major+Mono+Display\&size=44\&color=C20000\&vCenter=true\&width=450\&lines=Klyntar+is+...)

* _<mark style="color:yellow;">**A project that relies on the security of the entire crypto industry**</mark>_\
  _<mark style="color:yellow;">****</mark>_\
  _<mark style="color:yellow;">****</mark>_KLYNTAR has a symbiotic architecture consisting of parallel and perpendicular blockchains, due to which it is not a single monochain, but many different micro chains (so-called _<mark style="color:red;">**symbiotes**</mark>_) that do not rely on some central "main" chain (commonly called a beacon chain (ETH 2.0 ), relay-chain (Polkadot), master chain, and so on), but rely on the overall security of other blockchains (the so-called _<mark style="color:red;">**hostchains**</mark>_) - on the PoW power of Bitcoin and forks, Ethereum (until they switched to PoS), Zilliqa, ZCash, Monero and many others, on the total value of all assets of the crypto industry, and therefore on stakes in Polkadot, Solana, Avalanche, Algorand and others, on storage volumes of Filecoin, Arweave, Chia, Spectrum and so on.\

* _<mark style="color:yellow;">**A project that has the maximum theoretically possible speed and relies on the speed of all blockchains (yes, more than Solana or TON)**</mark>_\
  \
  _<mark style="color:red;">**Sounds like an overstatement, but read please)**</mark>_\
  \
  Scaling is one of the key problems that many projects are trying to solve. Everyone's path is different, but the essence is the same. We decided to go further and reach the potential maximum computing capabilities of the industry. Imagine if ETH smart contracts could run on Solana. If Solana went down again (which happened several times over the past year), then its programs would be running on Polygon and Tron. Sounds strange, but theoretically achievable. How? Well, I had to use some loopholes and substitution of concepts, so I think you should read. In addition, you will learn about other methods of scaling at the consensus level (fast BFT), cryptography (using BLS multi-signature aggregation, separate chains for "heavy calculations"), learn about phantom blocks and much more).\

* _<mark style="color:yellow;">**The project with the maximum level of parallelism**</mark>_\
  \
  Symbiotes work in parallel to each other, and KLYNTAR's dimensions increase not only vertically, but also horizontally. With this structure, you can reduce the weight of the circuit, which means that synchronization will be faster. _<mark style="color:red;">**Services**</mark>_ (this is how we call next-generation smart contracts that work off-chain (in addition to the usual WASM contracts that work on-chain), have access to advanced logic and features, such as choosing a database, opening ports and using network resources) are also parallel and, moreover, optional because they work "outside the chain". This gives amazing opportunities for all sorts of activities to speed up work and add new features (after all, parallelism according to Amdahl's law is maximum at 0% of dependent components. So instead of waiting for the mono-chain to vote for some changes, you can add something then new in one symbiote and start testing).\

* _<mark style="color:yellow;">**A project that has a "crypto" prefix for a reason**</mark>_\
  \
  _<mark style="color:red;">**Cryptography**</mark>_ is what Arthur Clarke's third law says

> ### **Any sufficiently advanced technology is indistinguishable from magic**

Many different crypto algorithms will be used in KLYNTAR workflows - from fast hash functions to post-quantum key exchange, from verifiable secret sharing schemes to threshold and ring signatures, from primitive zero-knowledge proofs to advanced mechanisms like zkSNARK / zkSTARK, blind signatures , VDF & VRF and much more that comes to mind.

In addition, through integration with other projects, paralleling the nature of KLYNTAR and mutualism (easy tracking and verification of other symbiotes), anyone will be able to run a bridge in [_<mark style="color:purple;">**StarkNet's**</mark>_](https://starkware.co/starknet/) zkSTARK rollup, for example, and use the power of Zero Knowledge Proofs.

*   _<mark style="color:yellow;">**A project that supports a multi-chain future and multi-chain logic**</mark>_\
    \
    Our strength is in unity! A deep understanding that the future of the crypto industry will be multi-chain in many ways and influenced many inventions, including unobtanium, services (new generation smart contracts), EVM and other virtual machines available on symbiotes (in the future).

    You will be useful on KLYNTAR if you are already a Bitcoin miner, own Cardano assets, have Brave tokens, have purchased storage space for Chia. If you play staking, then on a large scale) If decentralization is only maximum)\

* _<mark style="color:yellow;">**Benefit from any device**</mark>_\
  \
  Support for network state staking and snapshots, use of zero-knowledge proofs (in the future) will help you get up and running light nodes on phones, single board computers, etc. which will be able to work only on selective symbiotes, check only certain services and smart contracts and at the same time be confident in the provable validity of the chain, store the content of smart contracts and services in a more advanced way than IPFS, and much more\

*   _<mark style="color:yellow;">**Science and technologies is the foundation of KLYNTAR**</mark>_\
    \
    KLYNTAR will use not only cryptography. For example:\
    \
    _<mark style="color:red;">**Cybersecurity companies**</mark>_ will also be able to help KLYNTAR by monitoring the state of the network and analyzing service repositories for the presence of malware wipers, miners, C2 infrastructure beacons and preventing their launch by network nodes

    \
    _<mark style="color:red;">**AI software companies**</mark>_ will be able to offer their services as oracles for smart contracts

    \
    _<mark style="color:red;">**Mining pools**</mark>_ will be able to continue their work in Bitcoin or other crypto that their equipment is configured for and at the same time receive rewards and have "weight" on KLYNTAR to ensure the security of our network\


    And these are just a few examples ✨\

* _<mark style="color:yellow;">**Web3 took a wrong turn**</mark>_\
  \
  Our task is to improve the current Internet, and not to build some new and separate one. In KLYNTAR you will be able to use bots and use them in Telegram to get paid subscriptions, service payments and so on. You can redirect the commissions of your services or symbiotes (if there is a consensus on this matter) to fund Wikipedia or Telegram (an old dream of _<mark style="color:purple;">**@KlyntarTeam**</mark>_). You can store your articles from Medium, look for business partners, launch your own decentralized companies from people from all over the world, use staking and reputation, the influence of your social networks ... in short, the potential is limitless and you can continue indefinitely. KLYNTAR will definitely become an integral part of the global Internet.

### 👨‍🚀Well, let's move on, there is still a lot of interesting things ahead 🤖
