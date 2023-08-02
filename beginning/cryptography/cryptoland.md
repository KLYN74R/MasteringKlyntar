---
description: Disneyland?!
cover: >-
  https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FphIHWZY173DpNXBbDjVg%2Fuploads%2FyH3948zPachq9c7FNdyM%2FScZyDB.webp?alt=media&token=e81ba55b-4ea9-4ff9-820e-c7a8bb55c28d
coverY: -177.3838383838384
---

# 🎢 Cryptoland

## <mark style="color:red;">Importance for everyone</mark>

Since we are planning to develop numerous projects within our ecosystem, it becomes obvious that if all of them are somehow connected with KLYNTAR, then the use of various kinds of cryptographic primitives is expected.

In order to separate cryptographic capabilities from specific implementations of KLYNTAR modules (for example, for workflow symbiotes or as part of service workflows), we decided to create a separate convenient repository where we collected various kinds of algorithms - from ordinary signatures to ring and multi-signatures. From post-quantum key exchange algorithms to post-quantum signatures (mostly current NIST candidates 1-5 security levels). In short, you can explore the repository yourself.

It is also worth mentioning that the production version of the KLYNTAR core uses different languages ​​- from the main JS to individual components in WASM, Go, C and Rust. Thus, we seem to suggest to developers that they can publish various kinds of solutions in any language that they know and can offer some interesting and useful innovation for KLYNTAR or other projects. In any case, it will be possible to use them by compiling to WASM, using addons, libraries, and so on.

The purpose of creating this repository is also to give both KLYNTAR developers and just third-party developers for their projects the opportunity to quickly "join" the essence of the algorithm in order to come up with potential use cases. We also expect from developers a simple and understandable API for working with the algorithm and potential suggestions on how to embed them in the project.

It can also be added that during the development of KLYNTAR we ourselves encountered problems with the lack of intelligible formulations. For example, as mentioned earlier, many of the algorithms are taken from the repositories of well-known companies (such as Coinbase, Google, Cloudflare) which probably have cryptographers working at their headquarters, or at least people who understand the base well. But nevertheless, it was not always easy to port, for example, Go code to C or from C to Node.js addons - somewhere there were problems with serialization, somewhere with a bad description. It seems that there is a code, it seems to work, but there is no API for quick use - not everyone knows how to write a normal README.

Here, in _<mark style="color:purple;">**Cryptoland**</mark>_, we assume that the authors will fork the repository, add their directory inside the categories of algorithms and add there both files of their work and a clear description of how and where it can be used.



### <mark style="color:red;">**Examples**</mark>

<mark style="color:purple;">**You add some new signature algorithm**</mark>

First, build the right project structure, whether it's a JS ESM module, a Rust crate, or a Go library. Provide clear external interfaces so that a third-party developer can easily notice the typical "sign", "verify", "generateKeypair" and so on functions without even going deep. Please provide some usage examples in the README as in the example below

```javascript
import {sign,verify,generateKeys} from '@org/your-package'

//Generate keypair
//Note - use defualt keysizes. Supports 32 and 64 bytes
let keypair = generateKeys(32)


//Sign any data
let signature = sign(keypair.privateKey,"YOU DATA TO SIGN")


//Let's verify
let isVerified = verify(keypair.publicKey,"YOU DATA TO SIGN",signature)
```

This will speed up the work of other programmers who, based on these algorithms, will create new wallets or interfaces for Apollo, new services on KLYNTAR, and so on.

<mark style="color:purple;">**You add some new algorithm from the realm of**</mark>** **<mark style="color:red;">**Zero-Knowledge-Proofs**</mark>

Explain the cryptographic base, provide links and/or names to make it easier to look for alternatives. Again, provide something like a directory with examples where the process of use will be described in simple language to people. Also, in view of the fact that you are a developer and clearly understand what you are writing about, offer interesting use cases.

{% embed url="https://github.com/KLYN74R/Cryptoland" %}

### <mark style="color:red;">**Reference to ValarDohaeris**</mark>

Also, in addition to Cryptoland, we have another repository - ValarDohaeris

{% embed url="https://github.com/KLYN74R/ValarDohaeris" %}

The purpose of creating such a repository was to prepare for the release of _<mark style="color:purple;">**ValarDohaeris**</mark>_, within which we worked to ensure that the owners of private keys of other blockchain projects could easily interact with KLYNTAR. For example, in Apollo you can confirm ownership of your private keys so that KLYNTAR nodes recognize the amount of unobtanium in your wallets and can understand how many blocks you have generated in Filecoin or how many tokens you have in your BSC account. Looking at it, you can understand what we meant when we talked about usability - a good and understandable README and a structure of the same type, and now anyone can use it.

```javascript
//CRYPTO is klyntar,algorand,arweave,eos,eth_like,filecoin,harmony,helium,mina,polkadot,ripple,solana,stellar,zilliqa(unimplemented)
//TIP: Check the directories of package to get available formats or https://github.com/KLYN74R/ValarDohaeris

import VD from '@klyntar/valardohaeris/<CRYPTO>/vd.js'


//_______________________________ USE DEFAULT SETS OF FUNCTIONS _______________________________


let keys=await VD.generate()

console.log(keys)//Make sure format is OK

//Sign data in the string format
let data='SIGN ME',

    signature=await VD.sign(data,keys.privateKey)

console.log('Your signature in transportable format => ',signature)

console.log('Is ok => ',await VD.verify('ANOTHER DATA',signature,keys.address),` (should be ❌)`)

console.log('Is ok => ',await VD.verify(data,signature,keys.address),'(should be ✔️)')



//_______________________________ AND EXPLORE SPECIFIC FUNCTIONS _______________________________

console.log('Address in another format: ',VD.toPUB_K1(keys.address))
```

### <mark style="color:red;">Benefits for developers</mark>

Of course, the work for the benefit of KLYNTAR cannot go unnoticed. You can find out more in the [_<mark style="color:red;">**Contributions**</mark>_](../contributions.md) section, but now I will just briefly mention that within the framework of social consensus, right in the interface of Apollo (or other 3rd party tools), users will be able to vote for the most useful contributions to KLYNTAR. It does not matter if you are a plugin developer, created several packs with connectors or added many algorithms (as in this case we are talking about this) - all this will be taken into account at the level of metrics such as the number of clones, personal preferences of users and developers, the number of services and / or smart contracts using these algorithms (and their activity) and so on.

In view of this, we assume that the fund formed on the basis of commissions will be distributed among development teams or single developers.

What else is interesting is all sorts of features (well, where without them). For example, a developer who wins will be able to force certain addresses to exchange KLY for some tokens on top of KLYNTAR instead of a reward. However, you will learn about this in the specified link for contributors.
