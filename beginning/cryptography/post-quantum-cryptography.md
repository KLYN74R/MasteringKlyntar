---
description: A large section dedicated to post quantum algorithms on KLYNTAR
cover: ../../.gitbook/assets/1608636809_1.jpg
coverY: -28.739205526770295
---

# ⚡ Post quantum cryptography

### <mark style="color:red;">**Introduction**</mark>

Thanks to cryptography, we live in a secure world. This, at first glance, invisible to the layman, component of the Internet allows us to safely surf the sites, use cryptocurrency, conduct transactions, sign various kinds of agreements, and so on. Behind all this is the reliability of various mathematical schemes, elliptic curves, discrete logarithm, modular arithmetic, key exchange protocols, hashing algorithms, and much more. Yes, yes - not just beautiful buttons and smooth menus.

Generally speaking, the most popular and used algorithms can be counted on the fingers literally in every category

* Hashes - SHA families, old MD, BLAKE hashes
* Signatures - RSA, ECDSA, EdDSA, Ed25519
* Symmetric encryption - AES, CAST, ChaCha20
* Key exchange - ECDH, DH, X25519

They have worked well for a long time, are open source (consistency with the [_**Kerckhoffs principle**_](https://www.techtarget.com/whatis/definition/Kerckhoffs-principle)), and have been subjected to research and attacks for many years. However, nothing lasts forever and gradually the security of these algorithms will fall due to the advent of quantum computers.

As mentioned earlier, quantum computers are not some magical black box that "calculates something quickly". These are very specific mathematical algorithms, but their difference from the standard mathematical hacking paths is that they use another fundamental science - physics.

In mathematics, it can't happen that zero suddenly becomes one if you don't like the answer. In quantum mechanics, it is possible.

If earlier, within the framework of classical attacks on algorithms, a mathematical approach was used (not taking into account attacks through third-party channels such as signal interception, van Eyck interception, etc.), now physics and the nature of fundamental particles of the Standard Model come into play

![](<../../.gitbook/assets/image (41).png>)

{% embed url="https://en.wikipedia.org/wiki/Standard_Model" %}

Taking advantage of such benefits of quantum mechanical properties as interference, wave-particle duality, entanglement, nondeterminism, we eventually get the opportunity to build schemes that allow us to perform fast factorization (and thus threaten RSA and similar algorithms), search with quadratic acceleration (threatening symmetric algorithms and hashes) and much more.

### <mark style="color:red;">Problems of quantum algorithms</mark>

Mathematical attacks on algorithms were previously limited to mathematics. These are various meet-in-the-middle attacks, hijacking and oracle attacks (CPA/CCA), reuse, rainbow tables and other ways.

Since the quantum threat relies on both mathematics and physics, then the problems here are both mathematical (create an algorithm, build gates and select matrices) and physical (difficulty of maintaining entanglement, environmental influences, natural restrictions through energy loss).

These two types of problems do not allow for the time being to create a wunderwaffe in the world of cryptography. However, one should not treat this negligently - one must be prepared for anything.

### <mark style="color:red;">KLYNTAR and that's all of the above. Types of Algorithms</mark>

Therefore, we have a very specific need for the use of post-quantum security mechanisms at KLYNTAR. We need to secure everything from signatures to architectural concepts due to the fact that we rely on the security of other chains, so if they are vulnerable, then this could threaten us (it could, because it does not threaten now).

We have identified several areas that need to be secured

### <mark style="color:red;">**Key Pairs / Signatures**</mark>

![Groups of post-quantum algorithms](<../../.gitbook/assets/image (10).png>)

At the initial stages, we decided to use Dilithium and BLISS signatures. Among other algorithms, their ratio of security and sizes of public keys + signatures seemed to be optimal. They show good speed and can take part in various events on KLYNTAR. We recommend using them as an advanced security address. For example, you can store large amounts on them and use them infrequently or even through a cold wallet.

_<mark style="color:purple;">**Dilithium**</mark>_

![](<../../.gitbook/assets/image (38).png>)

This algorithm is a NIST candidate and provides the ability to generate key pairs and signatures. Widely popular, studied at the highest levels. It is included in the post-quantum implementation of _<mark style="color:yellow;">**OpenSSL**</mark>_, is being studied by CloudFlare, and is included in their CIRCL repository.

![](<../../.gitbook/assets/image (36).png>)

{% embed url="https://github.com/cloudflare/circl" %}

We just use this implementation from CloudFlare by providing a standard set of functions like generate, sign and verify.

There are several implementations depending on the NIST security levels. Here are their characteristics

![](<../../.gitbook/assets/image (34).png>)

The creators themselves recommend using the Dilithium3 parameter set, but we use Dilithium5 due to greater security. However, to change the security level, it is enough to simply change one line so that such changes can be made if necessary. Here is a comparison table of security levels according to NIST



| NIST security level |  Hack is so difficult as...  |
| :-----------------: | :--------------------------: |
|          1          |   Bruteforcing AES-128 key   |
|          2          | Find a collision for SHA-256 |
|          3          |   Bruteforcing AES-192 key   |
|          4          | Find a collision for SHA-384 |
|          5          |   Bruteforcing AES-256 key   |

We also leave you a link to the implementation of the API for Node.js in the Cryptoland repository

{% embed url="https://github.com/KLYN74R/Cryptoland/blob/main/dilithium.go" %}

Link to official research website

{% embed url="https://pq-crystals.org/dilithium/index.shtml" %}

_<mark style="color:purple;">**BLISS**</mark>_

The second and priority post-quantum signature algorithm will be BLISS. It is also based on lattice cryptography, more specifically RLWE (Ring Learning With Errors). Although it creates a small signature and has good security, it has not been listed as a candidate for standardization by NIST. It uses the Fiat-Shamir trellis signature scheme and its improved sample selection method for parameters. It also uses Huffman encoding to compress the signature.

You can already generate a BLISS key pair and an address. The address is the BLAKE3 hash of the public key

![](<../../.gitbook/assets/image (44).png>)

{% embed url="https://bliss.di.ens.fr/" %}

{% embed url="https://asecuritysite.com/signatures/go_bliss" %}

### <mark style="color:red;">**Comparison**</mark>

Some of our algorithms are missing from the table

![](<../../.gitbook/assets/image (21).png>)

It would seem strange - well, where in the blockchain can this be needed? Everything falls into place when it comes to off-chain interaction of nodes - as part of the exchange of data between services or communication with the outside world.

Due to the fact that symmetric encryption is faster than asymmetric encryption, in the ordinary world, for example, in TLS or SSH protocols, a symmetric key is negotiated. This provides a secure communication channel.

Since we are talking about post-quantum mechanisms, here we have chosen several candidates. So, Kyber, SIKE, SIDH and CSIDH will be available on KLYNTAR.

Each of them is either a current NIST candidate (Kyber) or alternatives (super isogeny algorithms).

We use the CloufFlare CIRCL implementation as addons from Go to Node.js. Also, since the full path is <mark style="color:purple;">**Go**</mark>** => **<mark style="color:purple;">**C**</mark>** => **<mark style="color:purple;">**Node.js**</mark>, you can use our repository with a simple API in any language

{% embed url="https://github.com/KLYN74R/Cryptoland" %}

{% embed url="https://github.com/cloudflare/circl" %}

Here are some comparison tables

![s://blog.cloudflare.com/nist-post-quantum-surprise/](<../../.gitbook/assets/image (28).png>)

![](<../../.gitbook/assets/image (23).png>)

{% embed url="https://pq-crystals.org/kyber/index.shtml" %}

### <mark style="color:red;">Assymetric encryption</mark>

We will also provide you with asymmetric encryption. Asymmetric encryption allows one party to have a pair of keys $$(PubKey,PrivateKey)$$ and receive messages encrypted with a public key from other parties and decrypt them using private ones.

In this regard, we decided not to add much and limited ourselves to Kyber PKE. KLYNTAR provides CloudFlare's implementation of Kyber1024 PKE, although again this is variant and is solved by changing one line of code.

{% embed url="https://github.com/KLYN74R/Cryptoland/blob/main/kyber_pke.go" %}

### <mark style="color:red;">Alternatives</mark>

In view of the principle of mutations, we allow the use of alternative methods of post-quantum cryptography. Such for example can be used on services. You are free to choose different kinds of algorithms, but in any case, test and do not use untested implementations

Additional links

### <mark style="color:red;">Links</mark>

{% embed url="https://www.nist.gov/news-events/news/2022/07/nist-announces-first-four-quantum-resistant-cryptographic-algorithms" %}

{% embed url="https://blog.cloudflare.com/nist-post-quantum-surprise/" %}

{% embed url="https://asecuritysite.com/pqc/" %}
