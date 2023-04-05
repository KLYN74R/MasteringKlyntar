---
cover: ../../.gitbook/assets/raijin-art-cyberpunk-girl-horn-vers (1).jpg
coverY: 555.440414507772
---

# 🛡 Symmetric ciphers

### <mark style="color:red;">AES-256</mark>

Yes, it was not without the use of symmetric encryption algorithms on KLYNTAR. Initially, the scope of their application was rather narrow (due to locality), but still there are many options for use, so now we will tell you in more detail.

Among symmetric algorithms, there is no more famous, stable and reliable than this one. Included in OpenSSL, GPG, used by ProtonMail, Google (for password encryption), malware developers, and other popular and widely used products and protocols. AES has been adopted as an official recommendation by the US government and no significant flaws or attacks have been found since.

Currently considered as [_<mark style="color:red;">**quantum-resistant**</mark>_](https://cryptobook.nakov.com/quantum-safe-cryptography#quantum-safe-and-quantum-broken-crypto-algorithms) (given a key size of 256 bits).

We use just the same 256 bit key which is the SHA-256 hash of your password. AES is used in CBC mode, although this is subject to change based on usage.

To set up the daemon, you will need to encrypt all your private keys - both KLYNTAR private keys and hostchain private keys to integrate with them (create transactions, interact with contracts, and so on).

When you start the KLYNTAR daemon, it will ask you to decrypt all your keys, as you can see in the image below

![Choose a strong password and make sure no one is watching you as you type. Do not disclose your password to anyone](<../../.gitbook/assets/image (12) (1) (1) (1).png>)

{% hint style="info" %}
Daemon startup visualization subject to change prior to release
{% endhint %}

<mark style="color:red;">**Behind the scenes, the following process takes place**</mark>

1. We get a 32 byte seed by hashing SHA-256\
   \
   HEXSEED = SHA256(<mark style="color:yellow;">**YOU\_PASSWORD**</mark>)
2. Next, we divide it into parts of 16 bytes. The first 16 bytes are the password, the second are the initialization vector
3. After that, your keys are placed in the memory of the process in which the KLYNTAR daemon is running.

### <mark style="color:red;">**Be careful**</mark>

Even though the private keys will be stored encrypted on the machine, they will still be available at the runtime of the running kernel. Thus, an attacker who has enough rights (for example, he is under root or exploited your old Apache) can dump the process memory and extract passwords from there.

For this reason, we recommend that you harden your system responsibly. Ideally, of course, the daemon should be a separate user and no one else would have access to its resources.

### <mark style="color:red;">Alternatives</mark>

Due to the fact that the scope is rather narrow, and private keys are not such large volumes to worry about speed, we are not yet considering other alternatives.

In services, you can use anything, even use custom algorithms in smart contracts.

As already mentioned, 256 bits is enough against Grover's attack to obtain a quadratic speedup in key selection (O(√N)) and against the BHT algorithm (O(N^1/3 complexity) however requires more entangled qubits). You can also visit the so-called _<mark style="color:yellow;">**Quantum Zoo**</mark>_ for more resources.

{% embed url="https://quantumalgorithmzoo.org/" %}

### <mark style="color:red;">**Some info for the future**</mark>

In the future, we also plan to implement Remote signing technology, thanks to which you will not have to store keys on "working machines". The nodes of your infrastructure will simply send you the necessary data for signature, and you will automatically produce valid signatures in a secure environment.
