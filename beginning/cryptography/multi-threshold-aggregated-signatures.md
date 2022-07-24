---
cover: ../../.gitbook/assets/lizardcover.jpg
coverY: 50.40414507772021
---

# 🔏 Multi/Threshold/Aggregated signatures

![Know the difference](../../.gitbook/assets/1\_7QOBOIiZIQMK81Rt68FJ9g.png)

### <mark style="color:red;">BLS12-381</mark>

Let's move on to one of the most important concepts in KLYNTAR Cryptoland. We will talk about multi- and threshold signatures. We included this table for a reason. At first glance, it may seem that this is the same thing, and as we have already mentioned, due to work with the documentation of other projects, we often met that these concepts are confused. Separately, there are aggregated signatures, or rather, the aggregation mechanism as a whole (keys and signatures).

Since in KLYNTAR both multi-signatures and threshold signatures are built using the same curve (the aforementioned BLS12-381), you first need to get acquainted with it.

{% hint style="info" %}
If you haven’t heard anything about this curve and the presented mechanisms before, then don’t worry - BLS is also used in such eminent projects as ZCash, Algorand, Chia, Harmony, Filecoin, Dfinity (ICP) and is also planned to be used in Ethereum 2.0
{% endhint %}

_<mark style="color:purple;">**BLS(Barreto-Lynn-Scott)**</mark>_ curve which is great for so-called pairing in pair-based cryptography. The BLS12-381 curve was developed by Sean Bow in early 2017 as the basis for an update to the Zcash protocol. It is useful for digital signing and for creating zkSNARKS.

The Bonet-Lynn-Shaham (BLS) signature method is considered reliable for signature generation. It uses a bilinear pair with an elliptic curve group and provides some protection against index calculus attacks. The BLS also produces short signatures and has proven to be secure. While Schnorr signatures require random numbers to generate multiple signers, BLS does not rely on them.

### <mark style="color:red;">**Curve pairing**</mark>

We'll need a very special function that takes two points P and Q on a curve (or two different curves) and maps them to a number:

$$
е(Р, Q) → n
$$

We also require one important property from this function. If we have some secret number x and two points P and Q , we should get the same result no matter which point we multiply by this number:

$$
е(х×Р, Q) = е(Р, х×Q)
$$

Essentially, we need to be able to swap point factors between two arguments without changing the result. More generally, all of these swaps should produce the same result:

$$
e( a×P, b×Q) = e(P, ab×Q) = e(ab×P, Q) = e(P, Q)^{(ab)}
$$

If Alice wants to generate a BLS signature, she first generates a private key as a point on an elliptic curve

If Alice wants to generate a BLS signature, she first generates a private key as a point on an elliptic curve $$a$$ and calculates the public key using the publicly known base point $$G$$ using the formula

$$
P = aG
$$

It takes the hash of the message and then maps the hash value to a point on the elliptic curve. If we use SHA-256, we can convert the message to a 256-bit x-point. If we can't get a point on the curve, we add an incremental value.

We get the signature of message $$M$$ using the formula&#x20;

$$
S= a × H(M)
$$

Thanks to the pairing, we get

$$
e(G,S)=e(P,H(M))
$$

$$
e(G,S)=e(G,a×H(m))=e(a×G,H(m))=e(P,H(M))
$$

Visualisation

![/medium.com/cryptoadvance/bls-signatures-better-than-schnorr-5a7fe30ea716](<../../.gitbook/assets/image (36).png>)

Signature verification

![](<../../.gitbook/assets/image (13).png>)

<mark style="color:yellow;">**Aggregation**</mark>

Now let's combine all the signatures in the block! Imagine that we have 1000 validators and each of them must vote for the inclusion of some block in the blockchain. For each validator, a signature Si is obtained, a public key Pi and a message M (block metadata-hash, index, etc.) . Why store all signatures when they can be combined? In the end, we only care if all the signatures are valid. The aggregated signature will simply be the sum of all validator signatures:

$$
S = S1+S2+…+S1000
$$

To test the block, we need to check that the following equality holds:

$$
e(G, S) = e(P1, H(m))⋅e(P2, H(m))⋅…⋅e(P1000, H(m1000))
$$

Proof

$$
e(G, S) = e(G, (pk1+pk2+pk3)×H(m))
$$

$$
e((pk1+pk2+pk3)×G, H( m)) = e(P1+P2+P3, H(m)) = e(P, H(m))
$$

![https://asecuritysite.com/signatures/js\_bls](<../../.gitbook/assets/image (17).png>)

### <mark style="color:red;">Threshold Signatures (TBLS)</mark>

The next important component in KLYNTAR are threshold signatures (t of n or threshold signatures). Their importance and advantage over multi-signatures is that they serve a specific purpose - to ensure that T out of N participants who were established earlier and who own part of the group's private key can make a transaction.

Multi-signatures are versatile and can be useful in many places. For example, their advantage is that it is easy to achieve efficiency in generating _<mark style="color:red;">**N of N**</mark>_ signatures - for this you need _<mark style="color:red;">**N**</mark>_ members to sign the message _<mark style="color:yellow;">**M**</mark>_ with their private keys, and then aggregate public keys and signatures and get the master key of the group _<mark style="color:purple;">**PubN**</mark>_ and signature _<mark style="color:purple;">**SigN**</mark>_. Thanks to the properties of aggregation, it will not be necessary to store N signatures and N public keys in the blockchain (as happens in naive multi-signature implementations), and instead of N signatures, it will be enough to check only 1 aggregated one, which gives us super efficiency - you will learn more in the section below.

The problem arises when not all signers may agree with the signature decision, but it is enough just to reach a certain threshold T (that is, at least _<mark style="color:red;">**T of N**</mark>_ participants agree to sign the transaction). In this case, when using multi-signature, we need to create some additional execution rules, and the size of the proof also grows.

Let me give you an example - let's say we have 10 people who decided to generate a signature using BLS multi-signature (for a transaction, staking, fixing an unobtanium or something else). Let 6 of them agree, and 4 others - against. At the same time, you set a threshold on your public aggregated key at 6/10 in advance.

It's no problem for 6 people to sign something and then aggregate their 6 public keys into a 48 byte single public BLS. With a signature, it's the same - everything comes down to one thing.

![](<../../.gitbook/assets/image (35).png>)

However, to prove to the network that the 6/10 threshold is met, you must provide 4 separate 48-byte addresses of those who disagree. This is because there is no other way for the network to find out how many of the keys are included in MasterPub1-6. This leads us to difficulties because there may be not 10, but 200 signers.

It would be nice if all the "magic" was performed outside the blockchain - the nodes will not know about any thresholds, they will not disclose the public keys of dissenters, and so on. All the blockchain needs to know is the fact that the required threshold has been reached and that we have a valid signature.

This can be achieved with threshold signatures. In KLYNTAR we use the TBLS implementation using the above curve

![https://asecuritysite.com/shares/](<../../.gitbook/assets/image (18).png>)

For the secure DKG (distributed key generation) procedure, Feldman's verifiable secret sharing scheme is used. It allows splitting a shared private key based on the Benalo scheme and generating a shared public key based on the verification vectors. In this case, T out of N members of the group will be able to sign messages on behalf of the group.

{% embed url="https://en.wikipedia.org/wiki/Verifiable_secret_sharing" %}

{% embed url="https://crypto.stackexchange.com/questions/6637/understanding-feldmans-vss-with-a-simple-example" %}

### <mark style="color:red;">**Demonstration**</mark>

For a general understanding of the workflow, let's generate keys and test their capabilities. It will also be something of a helpful guide if you have any difficulty using them in the Apollo. Well, or if you didn’t understand much from the information above, now you will get a more visual explanation.

### <mark style="color:yellow;">Multisignatures</mark>

Go to Cryptoland

![](<../../.gitbook/assets/image (33).png>)

Select multisig from the drop-down menu and generate in the operations section. Now generate a pair

![](<../../.gitbook/assets/image (31).png>)

For the test, generate and save yourself a few pairs. Let's generate 3 pairs

![](<../../.gitbook/assets/image (37).png>)

{% hint style="info" %}
Don't forget to save your pairs. Autosave will be added in future versions of Apollo
{% endhint %}

Here's the pairs we have

```json
//1

{
   "privateKey":"caad28a7da57fb28879bfdd886714629e4152553a28540caed6f51531f5af61a",
   "pubKey":"7QMxLg6GJwQYjc8B2WBEvaQq3TfeBhgBqHGneFu43oLfwhovrPGykbkUGe94FacSuG"
 }

//2

{
   "privateKey":"c707f21257f4d0ff4edf4b7b79475049cd1e901b58bec6203d85b1a7552dcfa3",
   "pubKey":"6XFgbxpwngL7QTpui9S3JgAhnWmQqr2JswtKBVPM8dUKS1AZDpXtmyZNRmHfWRvTU6"
}

//3

{
   "privateKey":"9a495ccfc98a9417f45098db524a4eec318784dce7f42c3fce03a0ae075d22a6",
   "pubKey":"69pYH3EGQSQ6nP9qSXttj4nDkPFWRjsZt2kp11wpcpqEiXoT3Gg1SNKErgT3zAYnPd"
}
```

Now these 3 parties can sign some message. Let it be <mark style="color:purple;">**SEND 5 KLY TO BOB**</mark>

![](<../../.gitbook/assets/image (16).png>)

You should have 3 signatures

```
rXICCzA2OoKoZQ97kJNU9ghx7IZ4Y9dDHgdONRfKdzWgZxIxqRI217Gs9bAMGBnpFZ54bD/V1Ggr5nDwNwsUzkVpxx/xB6Zh2AaB5tHkYO8ny/JikY4ihcRAw20B16g8

lu29FIXc7hJjcvfA2muJTuHvr47il4VrAIaFzQl3OTLTprcGjTwabporzxg/VK4gCgzgoJ6fLL/MbmKkfFfmQEU5amwGRGfYisL6NJp1E9GpXOPKU+JZVmvQkf+XhseE

koPFh4Qyu3RNDCHAUK0Jj9gvYwMSGHNydcubZee3ESET3/kwufBAF0WSDJ3hnTO6DsECG9+Z+B02xD6MCGklRhk312Esl2vt3Zc9f7NwLfKiy+ZC+bEuYdDgGIl5Bl6v
```

You can take any of them and the corresponding public key and verify the signature

![Also, check the other pairs & signatures](<../../.gitbook/assets/image (23).png>)

And then the cryptographic magic begins. Aggregation. To do this, three parties or any other person can take public signatures and addresses and aggregate them together

<mark style="color:red;">**Public key aggregation**</mark>

![Split the keys with a colon](<../../.gitbook/assets/image (14).png>)

<mark style="color:red;">**Signatures aggregation**</mark>

![Split the signatures with a colon](<../../.gitbook/assets/image (39).png>)

Now we have a pair of master signature and master public key. Let's check

![](<../../.gitbook/assets/image (20).png>)

I think now the incredible properties have become more visible and obvious

### <mark style="color:yellow;">**Threshold signatures**</mark>

In Cryptoland now choose _<mark style="color:purple;">**thresholdsig**</mark>_

![](<../../.gitbook/assets/image (22).png>)

Let's simulate the situation - let you and 5 other friends want to create such an address, from which it will be possible to perform any action only by agreement of 4 friends. We have a 4/6 situation. Before you will be such fields

![](<../../.gitbook/assets/image (38).png>)

Let's enter our threshold 4, our ID (let it be 1) and the ID of other friends. You can choose anything as an ID, but it's easier to use numeric identifiers. Since the number of sides is 6, then there should be 6 identifiers (including yours)

![](<../../.gitbook/assets/image (9).png>)

You will get such a big output

![](<../../.gitbook/assets/image (26).png>)

<mark style="color:orange;">**The first is verification vector**</mark>

This is a necessary component for threshold signatures that will help make sure the parties (in this case, your other 5 friends) that the sharing of the secret was secure, that the part they received is valid and that each party received no more than necessary (that is, everything will be safe and threshold in 4/6 will not be violated)

_<mark style="color:red;">**Verification vector is public. Send it to other friends**</mark>_

<mark style="color:orange;">**Next is shares**</mark>

This is a component of the so-called _<mark style="color:purple;">**distributed key generation**</mark>_(DKG). They are sent one to each friend and do not have to be published anywhere. This is your safety first and foremost. You keep the share with your ID (where <mark style="color:purple;">**For user with id 1**</mark>, since you previously chose such an ID)

_<mark style="color:red;">**They are NOT public, but secretly sent to each friend**</mark>_

<mark style="color:orange;">**Last - your updated ID**</mark>

Save it as well. It will be necessary to verify the share and generate a partial signature

### <mark style="color:yellow;">What next?</mark>

Then your 5 friends repeat the same thing in their wallets. They only need to insert their ID and a similar set of IDs for your entire group (also 1,2,3,4,5,6 as generated by the first friend that you are in this example).

<mark style="color:yellow;">**Friend with ID=2**</mark>

![](<../../.gitbook/assets/image (12).png>)

<mark style="color:yellow;">**Friend with ID=3**</mark>

![](<../../.gitbook/assets/image (28).png>)

<mark style="color:yellow;">**Friend with ID=4**</mark>

![](<../../.gitbook/assets/image (15).png>)

<mark style="color:yellow;">**Friend with ID=5**</mark>

![](<../../.gitbook/assets/image (25).png>)

<mark style="color:yellow;">**Friend with ID=6**</mark>

![](<../../.gitbook/assets/image (11).png>)

### <mark style="color:yellow;">**Step 2**</mark>

You send all your friends the resulting verification vector and the balls to each of your friends. At the same time, you get a verification vector and your share from them.

Upon completion of the procedure, you, as a friend with ID=1, should have the following set:

* 5 verification vectors from each friend + your own (total 6)
* Your updated ID that you received in the first step
* 5 shares from each of your friends + your own which you generated at the first stage (where For user with id 1)

### <mark style="color:yellow;">Stage 3 - share verification</mark>

Now you need to make sure that none of your friends cheated and sent a false share. Otherwise, you run the risk of losing your vote, because violators will be able to solve everything without you by providing the function with a valid share that they will keep for themselves earlier

To do this, select the _<mark style="color:purple;">**verifyShare**</mark>_ mode

![](<../../.gitbook/assets/image (40).png>)
