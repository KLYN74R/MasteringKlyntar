---
description: Blake3,SHA-256 and some more explanations
cover: ../../.gitbook/assets/raijin-art-cyberpunk-girl-2-4khd.jpg
coverY: 326.6321243523316
---

# #⃣ Hash functions

The next important component are hash functions. For Klyntar we'll use set of functions in our inner processes.Here's the list:

* BLAKE3 (256 bits with further potential extending to 512 bits)
* SHA-256

### BLAKE3

![Read more https://github.com/BLAKE3-team/BLAKE3](<../../.gitbook/assets/image (2).png>)

BLAKE3 was choosen as main candidate to be used as lead hash function for getting block headers' hashes, hashes of workflows, services archives, quantum swaps(modification of atomic swaps) and so on. Superfast, supports **PRF**, **MAC**, **KDF**, and **XOF** modes,highly parallelizable and so on.

Insofar as BLAKE3 supports XOF mode e.g. output length of hash might be variable(like in SHAKE hashing scheme). This is important in case of using them as quantum secure alternative to 128 or 256 bits schemes which can be abused by Grover or BHT algorithms in case of collision found what will be dangerous to cross-symbiotes quantum swaps(read more at [quantum-stuff.md](../quantum-stuff.md "mention")).

BLAKE3 will be used on kNULL chain by [<mark style="color:red;">dev@controller</mark>](../architecture/workflows.md) workflow. However, thanksfully to [<mark style="color:red;">Mutation mechanisms</mark>](../mutations.md) <mark style="color:red;"></mark> developers of other workflows,operators of nodes in other symbiotes will have ability to use any function they want which will be presented in official repository or developed/distributed by 3rd parties via alternative channels.

### Ripped hashes concept
