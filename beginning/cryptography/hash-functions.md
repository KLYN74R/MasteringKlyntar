---
description: Blake3,SHA-256 and some more explanations
cover: ../../.gitbook/assets/raijin-art-cyberpunk-girl-2-4khd.jpg
coverY: 326.6321243523316
---

# #⃣ Hash functions

The next important component are hash functions. For Klyntar we'll use set of functions in our inner processes.Here's the list:

* BLAKE3 (256 bits with further potential extending to 512 bits)
* SHA-256
* SHA3

### BLAKE3

![Read more https://github.com/BLAKE3-team/BLAKE3](<../../.gitbook/assets/image (2) (1) (1) (1).png>)

BLAKE3 was choosen as main candidate to be used as lead hash function for getting block headers' hashes, hashes of workflows, services archives, quantum swaps(modification of atomic swaps) and so on. Superfast, supports **PRF**, **MAC**, **KDF**, and **XOF** modes,highly parallelizable and so on.

Insofar as BLAKE3 supports XOF mode i.e. output length of hash might be variable(like in SHAKE hashing scheme). This is important in case of using them as quantum secure alternative to 128 or 256 bits schemes which can be abused by Grover or BHT algorithms in case of collision found what will be dangerous to cross-symbiotes quantum swaps(read more at [quantum-stuff.md](../quantum-stuff.md "mention")).

_<mark style="color:yellow;">**Using on symbiotes**</mark>_

BLAKE3 will be used on kNULL symbiote by [_<mark style="color:red;">**dev\_controller**</mark>_](../architecture/workflows.md) workflow. However, thanksfully to mutation mechanisms <mark style="color:red;"></mark> developers of other workflows,operators of nodes in other symbiotes will have ability to use any function they want which will be presented in official repository or developed/distributed by 3rd parties via alternative channels.

_<mark style="color:yellow;">**Using to generate addresses**</mark>_

As for the application at the level of algorithms, we use BLAKE3 to generate addresses in post-quantum signature schemes due to the large size of the public key. Obviously the address will be _<mark style="color:purple;">**BLAKE3(**</mark><mark style="color:red;">**PublicKe**</mark>_<mark style="color:red;">**y**</mark><mark style="color:purple;">**)**</mark>

This can be seen even through Apollo

![This is what a key pair and address looks like for a post-quantum Dilithium](<../../.gitbook/assets/image (15).png>)

_<mark style="color:yellow;">**Usage for quantum swaps**</mark>_

To exchange resources in pairs of symbiote - symbiote or hostchain - symbiote, this function will also be necessary.

_<mark style="color:yellow;">**Use to identify services and smart contracts**</mark>_

Unique IDs for unique contracts and services. For smart contracts, we are talking about the hash of the WASM module, for the service - the hash of the archive.

### _<mark style="color:red;">**SHA-256**</mark>_

Good and reliable, as well as a super popular hash function that has stood the test of time. In KLYNTAR, it is used selectively in certain places of the type to obtain seed when decrypting keys or for reliability in service repositories (instead of the obsolete SHA-1).

### <mark style="color:red;">**SHA3**</mark>

256-bit SHA-3 (also known as Keccak-256) based __ [_<mark style="color:purple;">**sponge function**</mark>_](https://en.wikipedia.org/wiki/Sponge\_function) is a NIST standard. It is used as the main one in Ethereum (although there is [_<mark style="color:purple;">**some confusion**</mark>_](https://ethereum.stackexchange.com/questions/550/which-cryptographic-hash-function-does-ethereum-use) between correspondences) and in other cryptocurrencies. At KLYNTAR we use it for ring signatures and zkp Schnorr proofs.

### <mark style="color:red;">The quantum threat and the concept of RippedHashes</mark>

What is currently considered quantum-resistant tomorrow may fall into the category of vulnerable algorithms for quantum computers.

Since quantum algorithms are not a black magic box, but quite specific mathematical algorithms that simply rely on the physical properties of elementary particles (which can be called quantum and which exhibit the corresponding properties of wave-particle duality, indeterminacy, entanglement, and other effects), one must be prepared In addition, tomorrow an article will appear on the conditional _<mark style="color:purple;">**arxiv.org**</mark>_ about the next algorithm that will already threaten 256-bit secrets and this will require less quantum memory, fewer simultaneously entangled particles, or we will learn about a new record for decoherence time.

One way or another, we will face a very real problem that threatens all blockchains, algorithms based on hash functions, and so on. And we only mentioned the damage from attacks on hashes, but there are also other cryptographic schemes - key exchange, signatures, zero-knowledge proofs ...

However, since this section is dedicated specifically to hashes, they will be discussed.

<mark style="color:yellow;">**Hash sizes**</mark>

The mentioned BLAKE3 can be extended to 512 bytes or more. It will also be possible to consider the option of using other XOF functions.

<mark style="color:yellow;">**Signature Algorithms**</mark>

KLYNTAR also includes hash-based signature algorithms. These are Winternitz and HORS, both are used with a Merkle tree (because they are not stateless, but require storage of "used" expanded hashes). They can also be converted to 512 bit hashes if needed without significant cost. Currently they are included in the repository, but we do not plan to use them yet due to the availability of more efficient post-quantum signature algorithms - Dilithium (NIST candidate) and BLISS.

<mark style="color:yellow;">**RippedHashes**</mark>

Now we will talk about another method of protection. A cryptographically strong hash function is essentially needed so that we can be sure that <mark style="color:purple;">**hash**</mark>=<mark style="color:green;">**H**</mark>(<mark style="color:red;">**x**</mark>) corresponds to some <mark style="color:red;">**x**</mark> and at the same time the function is resistant to attacks of the first and second kind.

Having a field of values, it should be extremely difficult for an attacker to find the right <mark style="color:red;">**x**</mark> for <mark style="color:green;">**H**</mark>(<mark style="color:red;">**x**</mark>) and thus, for example, deceive light clients that do not store evidence in the form of a hash or new nodes that want to make sure that the state of some service is correct by comparing the hashes of the state in the symbiote with the received data .

Let's assume that there are two parties - proover and verifier. The verifier only stores the block hashes of some symbiote, and the prover sends those blocks to it. After that, the verifier calculates the hash of the block, makes sure that it is valid and that it belongs to the only possible chain of symbiote blocks, and accepts the state of the symbiote. This is, in a simplistic way, how mutualism works between symbiotes.

However, if the prover succeeds in replacing the blocks, but the hash is identical, then it goes without saying that the attack will be successful, because now it is not clear which of the blocks is part of the chain. Relatively speaking, it turns out that at some height of 500,000 different nodes offer us a block with the same index, but only with hashes <mark style="color:purple;">**aaaa...**</mark> and <mark style="color:purple;">**bbbb...**</mark>

And is it even possible to work somehow now? After all, even the presence of unobtanium rates obtained by PoW will not potentially save - having such an algorithm, an attacker will quickly find the necessary hashes and form false evidence even for PoW algorithms.

RippedHashes is based on the fact that in addition to the hash, the verifier will also need to store a certain part of the original data + adhere to certain logic (accept blocks of only the correct format). Thus, if, for example, the block size is limited to 4 megabytes, then in theory this is equivalent to a space from

$$
2^{4*1024*1024*8}=2 ^ {33 554 432}
$$

block variants (calculated based on bits). Given the format, as well as the values inside (for example, transaction amounts cannot be negative), this number is greatly reduced, although it is difficult to say according to what pattern. It is already more difficult for an attacker to find the right hash, because the value space is limited, and even if it is possible to find some alternative block with the same hash (in fact, a collision), but inside such a block there will be wrong address formats, incorrect data formats, etc. etc., then such a block can no longer be passed off as a real one.

However, although the value space has decreased, it still has not become zero. For greater minimization, the verifier had to initially store, in addition to the hash of the block, another part of the "clean data". For example, the address of the recipient in the transaction with index 10, the last 5 bytes of the commit address of some service, and so on. In this case, the attacker has even fewer options to generate a block that would break everything and at the same time match the hash and such additional conditions. So by increasing the stored data for the verifier, we thus reduce the attack surface of the proving attacker.

The algorithm is still raw and requires research + it is rather theoretical, but we must be ready for anything. It is also worth mentioning that RippedHashes are not suitable for cases where it is necessary to keep a secret. For example, for quantum swaps or zero-knowledge proofs. Although, again, you can try to unscrew something and do research.

It is also worth mentioning that RippedHashes are not suitable for cases where it is necessary to keep a secret. For example, for quantum swaps or zero-knowledge proofs. Although, again, you can try to unscrew something and do research.
