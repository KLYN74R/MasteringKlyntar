---
description: Some of our thoughts before we start
cover: ../.gitbook/assets/533240_cWTTOpjP0V_wrench.jpeg
coverY: 138.54231433506044
---

# 🧠 Woe from Wit

![Thinking about a new feature](../.gitbook/assets/cb0586c52d9c39c873e43de91c59c39c.jpg)

## <mark style="color:red;">Crypto in 2k22, hustle culture and 1001 ideas</mark>

I'm sure if you're reading this, it means that you're probably interested in the latest in our field in one way or another. We do not care if you are a developer, an investor, a crypto enthusiast or an SEC agent. I think we will be able to convey to you the beauty of the decisions and developments made and the "gigantism" of thoughts.

Again, as mentioned earlier, due to close acquaintance with the technical characteristics of other projects, our heads were spinning - after all, how can we surprise users, if it would seem that so much is already available - all sorts of DeFi, DEX, NFT marketplaces, cross-chains and other. Because of this, I had to spend a lot of time searching for tricky solutions that no one had thought of yet, choosing the best ones between different algorithms (for example, for generating key pairs, hashing, KEX mechanisms, etc.). What about by consensus? Your own solution or take a proven one? PoS or something based on real resources? What about scalability? Should we try to overtake Solana or focus on something else? How to solve the problems of PoS finalization, which has recently become more and more popular in conjunction with BFT mechanisms and (which is a pity for us) is replacing PoW with its "real resources"?

All this is just a part of the questions that arise in the minds of blockchain developers at the design stage. It becomes more difficult when it comes to implementation. Here one plan can replace another, then it turns out that the consensus you have chosen turns out to be absolutely not scalable in practice, and algorithms that yesterday still seemed good to you today already graze the backs of some new NIST "favorites".

With this text, we want to show that KLYNTAR was born in discussions, in the abyss of brainstorms and constantly changed to meet the necessary requirements. In the end, as a result, you are reading this document, which means that we still managed to create _<mark style="color:red;">**Frankenstein's monster**</mark>_, and now you will learn how.

## <mark style="color:red;">But in a nutshell, what do you mean?</mark>

I could answer here with the words of Newton from _**Silicon Valley**_, they say

> _<mark style="color:purple;">**You can't delve into smth quickly. To delve means to read carefully and scrupulously**</mark>_

However, before starting reading serious docks further, I will still clarify

![](https://readme-typing-svg.herokuapp.com/?font=Major+Mono+Display\&size=44\&color=C20000\&vCenter=true\&width=450\&lines=Klyntar+is+...)

## <mark style="color:red;">**A project that relies on security of the entire crypto industry**</mark>&#x20;

KLYNTAR has a symbiotic architecture with multisharding consisting of parallel independent blockchains called _<mark style="color:red;">**symbiotes**</mark>_(1st level of sharding) which can be shardable too(2nd level of sharding), due to which it is not a single monochain, but many micro chains that do not rely on some central "main" chain (commonly called a beacon chain (ETH 2.0), relay-chain (Polkadot), master chain, and so on), but rely on the overall security of other blockchains (the so-called _<mark style="color:red;">**hostchains**</mark>_) - on the PoW power of Bitcoin and forks, Ethereum, Solana, Polkadot, BNB, Zilliqa, ZCash, Monero and many others, on the total value of all assets of the crypto industry, and therefore on stakes in Polkadot, Solana, Avalanche, Algorand and others, on storage volumes of Filecoin, Arweave, Chia, Spectrum and so on. The state of KLY is protected from rollbacks by common security of hostchains and regular checkpoints - now to rollback KLY you need to take control over Bitcoin, Ethereum, Solana and other blockchains.\
\
Moreover, the mechanism of multistaking allows you to become validator by providing your NFTs, tokens, bitcoins, ethers, etc. as a stake. The maximum security budget is for KLY.\


## <mark style="color:red;">A project that has the maximum theoretically possible speed(yes, more than Solana or TON)</mark>

_<mark style="color:purple;">**Sounds like an overstatement, but read please)**</mark>_\
\
Scaling is one of the key problems that many projects are trying to solve. We decided to go further and reach the potential maximum computing capabilities of the industry. That's why on the level of a single symbiote it's possible to create the second level of sharding to split a chain to _<mark style="color:red;">**subchains**</mark>_ where single authority creates new blocks lightning fast - with no extra communications, order agreements,etc.\
\
By the way, don't be scared - it's fault tolerant solution because of the existence of _**reassignment chains**_ - set of reserve pools which will create the blocks instead of primary pool in case of offline status or something else. These chains may contain 1000 reserve pools, separate networks like Bitcoin, Solana, Polygon, etc. Yes, even if all of the reserve pools on your subchain will stop - you can continue to work / share transactions via other blockchains. That is something what makes KLY "the most fault-tolerant network". \
\
The _**Tachyon**_ consensus creates conditions where you can be sure in finalization in several steps:

* Step 1 (fastest way:zap:) - O(1) lightning fast thanks to [_<mark style="color:red;">**Trust me bro**</mark>_](architecture/workflows/tachyon/trust-me-bro-a-o-1-instant-finalization-mechanism.md) mechanism. The block becomes finalized instantly, once it's generated. Say thanks to overstaking.
* Step 2 - default BFT finalization agreements generated by daily choosen quorum. Quorum vote for blocks on subchains and produce aggregated finalization proofs.
* Step 3 - checkpoints to hostchains. Once block with your tx was committed in 2/3N+1 of other blockchains like Bitcoin, Near, Avalanche, Solana, etc. you have a 1000000000% guarantee of finalization. KLY usually creates checkpoints to other blockchains once a day (just before the quorum change) with the maximum block height in subchains in a given era (today), but if necessary, you can independently make a checkpoint at any height of any symbiote subchain. If you see that your version of the subchain (roughly speaking, block index and hash) up to a given height got into more than 2/3 of other blockchains (hostchains) and at the same time, earlier commits of this subchain are also included in your subchain, then you can sleep peacefully.

**\[For step 2]**: Finally, our software [_**Savitar**_](https://github.com/KLYN74R/Savitar) was created to grab the range proofs for subchains - instead of voting per block, quorum votes for the ranges of blocks on subchain(for example, from 0-112, 778-1337, etc.).\


## <mark style="color:red;">The universal project which was created to be used and improved</mark>

As developers, we understand the needs of users and... other developers :relaxed:. That's why we propose various useful use-cases for our cryptography, libraries, network & genesis configurations, abilities of VMs(EVM & WASM & UVM) and so on. With KLY you can create EVM contract and use post-quantum cryptography in it, create WASM contract and call EVM from it, write extra-functionality for EVM on Rust, use built-in powerful oracles, create Docker container to implement your improvement proposal in a forkless way or even create your own blockchain and run it on KLY!\
\
With RWX smart-contracts you even don't need to know how to code. Moreover, you can create simple or advanced contracts with your business partner, delivery service, your employer and so on!\
\
Hope, in this and other docs we'll discover the whole potential of KLY :smirk:\


## <mark style="color:red;">A project that has a "crypto" prefix for a reason</mark>

_<mark style="color:purple;">**Cryptography**</mark>_ is what Arthur Clarke's third law says

> ### **Any sufficiently advanced technology is indistinguishable from magic**

Many crypto algorithms will be used in KLYNTAR workflows - from fast hash functions to post-quantum key exchange, from verifiable secret sharing schemes to threshold- and multisignatures, from primitive zero-knowledge proofs to advanced mechanisms like zkSNARK / zkSTARK, blind signatures, VDF & VRF and much more that comes to mind.\


## <mark style="color:red;">A project that supports multichain future and multichain logic</mark>

Our strength is in unity! A deep understanding that the future of the crypto industry will be multichain in many ways and influenced many inventions, including multistaking, Dapps 2.0( extended version of smart contracts), EVM and other virtual machines available on KLY(in the future).\


You will be useful on KLYNTAR if you are already a Bitcoin miner, own Cardano assets, have Brave tokens, have purchased storage space for Chia. If you play staking, then on a large scale). If decentralization is only maximum)\


## <mark style="color:red;">Benefit from any device</mark>

Support for network state staking and snapshots, use of zero-knowledge proofs (in the future) and removable blockchain will help you get up and running light nodes on phones, single board computers, etc. which will be able to work only on selective symbiotes, check only certain services and smart contracts and at the same time be confident in the provable validity of the chain, store the content of smart contracts and services in a more advanced way than IPFS, and much more\


## <mark style="color:red;">Science and technology are the foundation of KLYNTAR</mark>

KLYNTAR will use not only cryptography. For example:\
\
_<mark style="color:purple;">**Cybersecurity companies**</mark>_ will also be able to help KLYNTAR by monitoring the state of the network and analyzing Dapps 2.0 repositories for the presence of malware wipers, miners, C2 infrastructure beacons and preventing their launch by network nodes

\
_<mark style="color:purple;">**AI software companies**</mark>_ will be able to offer their services as oracles for smart contracts or will be useful for RWX(real-world execution) codeless smart-contracts

\
_<mark style="color:purple;">**Mining pools**</mark>_ will be able to continue their work in Bitcoin or other crypto that their equipment is configured for and at the same time receive rewards and have "weight" on KLYNTAR to ensure the security of our network\


And these are just a few examples ✨\


## <mark style="color:red;">Web3 took a wrong turn</mark>

Our task is to improve the current Internet, and not to build some new and separate one. In KLYNTAR you will be able to use KLY bots and use them in Telegram to get paid subscriptions, service payments and so on. You can redirect the fees of your services or symbiotes (if there is a consensus on this matter) to fund Wikipedia or Telegram (an old dream of _<mark style="color:purple;">**@KlyntarTeam**</mark>_). You can store your articles from Medium, look for business partners, launch your own decentralized companies from people from all over the world, use staking and reputation, the influence of your social networks... in short, the potential is limitless and you can continue indefinitely. KLYNTAR will definitely become an integral part of the global Internet.

### 👨‍🚀Well, let's move on, there are still a lot of interesting things ahead 🤖
