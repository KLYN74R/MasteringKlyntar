---
description: >-
  How we'll keep our accounts & infrastructure & your quiet life and assets
  secured(on non chain level)
cover: >-
  ../.gitbook/assets/asus-rog-republic-of-gamers-cyberpunk-asus-zephyrus-wallpaper-2400x1350_50.jpg
coverY: 400
---

# 👮 Basic Security

This is some kind of report+maybe you can use this tips in your practise.But we think that users must know that our team care of your protection to prevent scam schemes & fake ICO's & phishing campaigns and so on.

### Commits signatures

Here's how it looks like

![](../.gitbook/assets/photo\_2022-05-18\_07-59-31.jpg) ![](../.gitbook/assets/photo\_2022-05-22\_11-06-00.jpg)

These are screenshots of the history of branches from GitHub and GitLab - there we will place all our code, projects, documents, and so on. All commits and any code posted by members of the Klyntar team will have a designation that will make it clear that no third party will be able to post anything even if they somehow gain access to the account. The same goes for the hosting platforms themselves. Although we have no reason to doubt GitHub (and its owner Microsoft in particular), node operators, users and all interested parties still need to be sure that the code is published by the Klyntar developers. You can locally import my public GPG key (and the keys of other team members) and verify each new pull via Apollo (_<mark style="color:purple;">checkrepo</mark>_ command in CLI) or _<mark style="color:purple;">git verify-commit</mark>_. The necessary links to set up the environment are also available below. Additionally, we also have a separate repository with other keys (Ed25519, post-quantum Dilithium, etc.) that you can also use for the necessary checks

{% file src="../.gitbook/assets/VladChernenko.pubgpg" %}
<mark style="color:red;">Go to</mark> [<mark style="color:purple;">https://github.com/KLYN74R/KlyntarTeamPubKeys</mark>](https://github.com/KLYN74R/KlyntarTeamPubKeys) <mark style="color:red;">to get more pubkeys</mark>
{% endfile %}

{% hint style="info" %}
Go to [https://www.gnupg.org/gph/en/manual/x56.html](https://www.gnupg.org/gph/en/manual/x56.html) to get the help if you need
{% endhint %}

### Additional features

We created a separate repository for a reason. GPG does not support such a large number of algorithms (we are currently using the most reliable RSA-4096 with a passphrase with high entropy), and the capabilities of GitHub come down only to SSH & GPG. Multisignatures or, for example, post-quantum algorithms are not available here. That is why we will create something like the second level of security for which we need this repository with keys and a separate command in Apollo.

Reading the previous section, you might have wondered: “Well, ok, what if one of you forgets your laptop somewhere, pushes a private key to some public repository, or, for example, one of your team members gets offended and releases a conditional wiper-commit that will steal my private keys and wipe my entire filesystem?". Again, thanks to such additional features of cryptography as multi-signatures, we will be able to avoid such incidents. Multiple signatures are also possible (signing the commit hash with several keys of different algorithms). For example, you will know that in addition to the fact that the commit was approved and signed by the required number of team members, the commit is additionally signed by some supported post-quantum algorithm.

### Git and hashes

Currently, Git uses SHA-1 hashes by default, but since version 2.29, [_<mark style="color:purple;">experimental support</mark>_](https://www.infoq.com/news/2020/10/git-2-29-sha-256/) for switching to SHA-256 has begun. This is very important because the same link contains implementation and PoC attacks when [_<mark style="color:purple;">two different files will generate the same hash</mark>_](https://shattered.it/).

&#x20;                                                 ![](<../.gitbook/assets/image (1) (1).png>)

Although this is not critically scary, as some publications shout about it, nevertheless, questions about the reliability of SHA-1 have been of interest to people in our industry for several years now. Therefore, although GitHub is still giving an error about accepting repositories with SHA-256 hashes, repositories of plugins, services, and so on that will be distributed outside hosting platforms (and therefore, regardless of whether this platform supports innovations or not) can use SHA- 256 as a hash function of the commits. We have already tested and no problems have arisen

![](<../.gitbook/assets/image (3) (1) (1).png>)

At the same time, you can still sign the repository hash with third-party keys and create your own acceptance rules. For example, a service repository can only be accepted by the nodes if it is signed by the Ed25519 key pair of the service creator and the largest service token hodler, or if the acceptance of the repository supports more than 2/3 of the service validator signatures and other rules that you can create yourself.

### Accounts

### Access to accounts for 3rd party apps & bots

### What about contributors?

### Self-sustaining security with symbiotes

### How the Continental release will help here?

###

###

###
