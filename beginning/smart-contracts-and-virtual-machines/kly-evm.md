---
description: Definitely, we should have the support of the most well-known VM
cover: https://wallpaperaccess.com/full/6223415.png
coverY: -79
---

# 🔮 KLY-EVM

<figure><img src="../../.gitbook/assets/KLY-EVM.gif" alt=""><figcaption></figcaption></figure>

## <mark style="color:red;">**KLYNTAR-EVM**</mark>

Well, yes, what did you think?!) KLYNTAR will allow symbiotes to use the EVM, write their own additional functions before running the EVM logic, make free calls (sandbox calls), make calls between virtual machines (cross-VM-calls), use free oracles from KLYNTAR and use heavy-duty functionality. In addition, thanks to the post-quantum capabilities of KLYNTAR, this functionality will also be extrapolated to the EVM!

## <mark style="color:red;">A separate repository for general updates and improvements</mark>

KLYNTAR EVM (KLY-EVM) will be available for everyone to use and improve. Here is a link to the repository we are working on

{% embed url="https://github.com/KLYN74R/KlyntarEVM" %}

Any symbiote or standalone project can use this repository as a dependency.

In addition, using some workarounds, you can write EVM functionality not only in Solidity, but also using other familiar languages - Rust, C, Python, Go, and more!

## <mark style="color:red;">What else is available?</mark>

Also, we have not forgotten about RPC. A JSON-RPC 2.0 implementation has already been written for KLY-EVM, which adds KLY-EVM compatibility with tools such as the web3 library, various wallets (Metamask) and other tools.

You can also use this repository as a dependency in your project

<figure><img src="../../.gitbook/assets/image (52).png" alt=""><figcaption></figcaption></figure>

{% embed url="https://www.npmjs.com/package/@klyntar/klyntarevmjsonrpc" %}

A flexible configuration tree is available here in which you can configure the chain ID, default gas price, set limits and more.

{% hint style="success" %}
<mark style="color:red;">**KLY-EVM**</mark> will be used in the original kNULL symbiote
{% endhint %}

## <mark style="color:red;">Additionally</mark>

We invite all projects that now exist in EVM-compatible chains to launch on KLYNTAR as well. Here you will get the fastest, safest and the most decentralized version of EVM with advanced functionality, lower (or even zero) gas prices and many other features!

If you are a DEX project, oracle network, NFT marketplace or any other project - welcome!

## <mark style="color:red;">Features</mark>

#### Sharded(low-level sharding implementation)

Since the native KLY chain (kNULL) is sharded, all shards will have the same chainID, despite the fact that individual accounts that are linked to a particular subchain are stored in the same database

#### Post-quantum secured

Leverage the power of post-quantum cryptography from the JavaScript environment using a magic address in the EVM(details [<mark style="color:red;">**here**</mark>](https://docs.klyntar.org/smart-contracts/kly-evm/magic-address))

#### Free EVM calls

KLY will allow you to call EVM for free - from WASM contracts or directly. It will be possible to build advanced schemes such as several free calls per day, free EVM calls depending on the target contract, free calls based on your role on KLY and so on.

#### Storage-by-subscription model

We plan to introduce a subscription system on the EVM storage so that only those who really benefit from it can use the decentralized benefits of KLY. Very interesting innovation

#### External storage

It will be possible to use external storage when working with smart contracts

#### WASM compatible

Call WASM from EVM and vice versa! Write EVM logic using WASM and benefit from hybrid smart contracts

{% hint style="info" %}
Follow the link to learn about using the KLY-EVM magic address to access KLY-WVM and the native environment (Node.js)
{% endhint %}

#### In-build powerful oracles

Call any internet API, use VRF and other powerful abilities of oracles. It will also be possible to modify existing oracles to suit your needs.

#### Interact with codeless smart-contracts by UVM

Powerful feature of KLY. Your EVM contract using oracles will be able to track RWX contracts whose work is being done in the real world

#### Pay fees in tokens

Advanced KLY-EVM will allow you to pay transaction fees not with native KLY coins, but with various stablecoins, NFTs, asset-wrapped coins, and so on!

#### Choose fee payer

The recipient, a third-party smart contract, and so on will be able to pay commissions for you!

## <mark style="color:red;">Links</mark>

{% embed url="https://klyntar.medium.com/klyntar-virtual-machines-part-0-kly-evm-shardable-low-level-managed-mutable-and-wasm-improved-5b5c653965d7" %}

{% embed url="https://docs.klyntar.org/smart-contracts/kly-evm" %}
