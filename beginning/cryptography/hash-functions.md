---
description: BLAKE3,SHA-256 and some more explanations
cover: ../../.gitbook/assets/raijin-art-cyberpunk-girl-2-4khd.jpg
coverY: 267.6321243523316
---

# #⃣ Hash functions

The next important component is hash functions. For KLYNTAR we'll use a set of functions in our inner processes. Here's the list:

* BLAKE3 (256 bits with further potential extending to 512 bits)
* SHA-256
* SHA3

## <mark style="color:red;">BLAKE3</mark>

![Read more at https://github.com/BLAKE3-team/BLAKE3](<../../.gitbook/assets/image (2) (1) (1) (1) (1).png>)

BLAKE3 was chosen as the main candidate to be used as the lead hash function for getting block headers' hashes, hashes of workflows, services archives and so on. Superfast, supports **PRF**, **MAC**, **KDF**, and **XOF** modes, highly parallelizable and so on.

Since BLAKE3 supports XOF mode i.e. output length of a hash might be variable(like in SHAKE hashing scheme). This is important in case of using them as a quantum secure alternative to 128 or 256 bits schemes which can be abused by Grover or BHT algorithms in case of collision found(read more at [quantum-stuff.md](../quantum-stuff.md "mention")).

_<mark style="color:purple;">**Using on symbiotic chains**</mark>_

BLAKE3 will be used in workflows implementations. However, thanks to mutation mechanisms developers of other workflows,  operators of nodes in other symbiotes will have ability to use any function they want which will be presented in the official repository or developed/distributed by 3rd parties via alternative channels.

_<mark style="color:purple;">**Using to generate addresses**</mark>_

As for the application at the level of algorithms, we use BLAKE3 to generate addresses in post-quantum signature schemes due to the large size of the public key. Obviously, the address will be _<mark style="color:purple;">**BLAKE3(**</mark><mark style="color:red;">**PublicKe**</mark>_<mark style="color:red;">**y**</mark><mark style="color:purple;">**)**</mark>

This can be seen even in console

![This is what a key pair and address looks like for a post-quantum Dilithium](<../../.gitbook/assets/image (15) (1) (1) (1) (1).png>)

_<mark style="color:purple;">**Used to identify smart contracts**</mark>_

Unique IDs for unique contracts. For smart contracts, we are talking about the hash of the WASM module.

## <mark style="color:red;">**SHA-256**</mark>

Good and reliable, as well as a super popular hash function that has stood the test of time. In KLYNTAR, it is used selectively in certain places of the type to obtain seed when decrypting keys.

## <mark style="color:red;">**SHA3**</mark>

256-bit SHA-3 (also known as Keccak-256) based [_<mark style="color:purple;">**sponge function**</mark>_](https://en.wikipedia.org/wiki/Sponge\_function) is a NIST standard. It is used as the main one in Ethereum (although there is [_<mark style="color:purple;">**some confusion**</mark>_](https://ethereum.stackexchange.com/questions/550/which-cryptographic-hash-function-does-ethereum-use) between correspondences) and in other cryptocurrencies. Will be used by KLY-EVM.
