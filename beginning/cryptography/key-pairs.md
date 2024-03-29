---
description: Perhaps the simplest
cover: ../../.gitbook/assets/3092916.jpg
coverY: -190
---

# 🔐 Key pairs

## <mark style="color:red;">Ed25519</mark>

Ed25519 was introduced in OpenSSH version 6.5. This is an implementation of EdDSA using the [<mark style="color:purple;">Twisted Edwards curve</mark>](https://en.wikipedia.org/wiki/Twisted\_Edwards\_curve). It uses elliptic curve cryptography which provides better security and higher performance compared to DSA or ECDSA.

For any type of interaction with KLYNTAR, you must have a pair of keys. You use the private key to sign the data, while the public key is used to verify the signature. In general, the principle is familiar to everyone.

KLYNTAR uses Ed25519 as the most default pair. Key sizes (both private and public) are 32 bytes. The public key in Base58 is your KLYNTAR address.

By the way, KLYNTAR addresses are compatible with Solana (given the fact that their default addresses are just a public key in Base58). Moreover, the commit transaction _<mark style="color:red;">**useful.txt**</mark>_ on the Solana mainnet (with a program Memo call) was made by the KLYNTAR keys

![You can view the transaction on the official Solana explorer](<../../.gitbook/assets/image (10) (1) (1) (1).png>)

![](<../../.gitbook/assets/image (8) (1) (1).png>)

{% embed url="https://explorer.solana.com/tx/36cs4bjKZJNcTsMA8N6Bz8mm2yBUX5WvcT74oT3Pn2sD6cMGprRQvmYVdPGQJmrnHPDrypJYkT9Zg6UHw4vuPssT" %}

Here is a typical example of a key pair generated via CLI or UI in Apollo

```
{
    publicKey: 'FmiD6J3EnJWce3M1UWwmbTSk4ss6HwX9Bq1ZGVJTq9Va',
    privateKey: 'MC4CAQAwBQYDK2VwBCIEIFBUTTsdsx2gq6XstzmhhU7AF0NExjJF3C15z8D4rHwJ'
}
```

![](<../../.gitbook/assets/image (14) (1) (1) (1) (1).png>)

<mark style="color:red;">**Node.js generates key pair in DER format**</mark>

1.Public SPKI type. So it looks like this right after generation\
\
`MCowBQYDK2VwAyEAsqv+zpsKO6vdklZ7wGcXzkpb27j+buojClSpqj78F3U=`\
\
All keys of this type have a common 12 bytes that there is no need to store publicly. We cut them off and convert the remaining 32 bytes to Base58. This process can be visualized as

![](<../../.gitbook/assets/image (9) (1) (1) (1) (1).png>)

2.Private PKCS8 type. Similarly, all privates share 16 bytes, but since they are not published, there is no need to change their size. We just apply Base64 to such a key, so it looks like this

`MC4CAQAwBQYDK2VwBCIEIKiJ1JIhmP4NelCCV5IAgQdOSfS/t3+9EjiL4zgG1HA0`

## <mark style="color:red;">Generation via OpenSSL</mark>

You can also repeat all this through OpenSSL

```bash
openssl genpkey -algorithm ed25519 -outform DER -out ed25519_private

cat ed25519_private | base64

//...something like MC4CAQAwBQYDK2VwBCIEIDNfdnUlKdo4fYCG+NzoEQRyanCphYKZUA9XX8uFI7nV
```

Generate public key

```bash
openssl pkey -outform DER -pubout -in ed25519_private -inform DER -out ed25519_pub

cat ed25519_pub | base64

//...MCowBQYDK2VwAyEA4PbMaYPMC+iTYtEfcNJmdoa4o8L0+yvQB2JEHLzRfi8=
```

It remains only to convert the public key to byte form, remove the first 12 bytes and convert to Base58.

## <mark style="color:red;">**Signature**</mark>

The signature is standard and takes 64 bytes. On KLYNTAR we use it in Base64.

## <mark style="color:red;">Why not to use the mnemonic phrase</mark>

{% hint style="success" %}
UPD: Starting from version _<mark style="color:red;">**v17.1.0**</mark>_ ValarDohaeris supports HD addresses in KLYNTAR and also generates 12 mnemo words for you. However, the functionality for generating key pair chains and importing a phrase will be implemented soon
{% endhint %}

![](<../../.gitbook/assets/image (16) (1) (1) (1) (1) (1).png>)

{% hint style="success" %}
Also, starting from _<mark style="color:red;">**v19.4.0**</mark>_, KLYNTAR received an implementation of the BIP-44 standard and currently included in the official BIP-44 list with an identifier of 7331 (1337 in the opposite direction). [_<mark style="color:red;">**Here**</mark>_](https://github.com/satoshilabs/slips/pull/1388) you can see the merge to the main branch of the register
{% endhint %}

{% hint style="info" %}
In future releases and updates, we will also create an implementation of BIP-44 for other types of keys that will be available on KLYNTAR - for multisig addresses and post-quantum key pairs
{% endhint %}

## <mark style="color:red;">**A couple more words**</mark>

We also decided not to follow the path of generating some checksums, certain prefixes, and so on. Also, we did not separate addresses into mainnet / testnet formats due to uselessness and inconvenience (considering the experience with Bitcoin and forks).

Ed25519 was selected as the best candidate available to be universal for symbiotes, services, smart contracts and other projects in the ecosystem.

## <mark style="color:red;">**Links**</mark>

{% embed url="https://docs.klyntar.org/web1337/send-transactions/default-ed25519-transactions" %}

{% embed url="https://ed25519.cr.yp.to/" %}

{% embed url="https://cryptobook.nakov.com/digital-signatures/eddsa-and-ed25519" %}
