---
description: >-
  What is under the hood? Let's start with the basic of each crypto
  project-cryptography. Here you can read and find out more about cryptographic
  primitives used on Klyntar for the different cases
cover: ../../.gitbook/assets/cyberpunk-2077-grimes-1.png
coverY: 0
---

# 🔑 Cryptography

Klyntar has the most advanced & latest & reliable crypto algorithms for its workflows. It concerns signatures schemes,symmetric encryption,PQC(post quantum) schemes,multisignatures and so on!\
\
We especially present them step by step to substantiate their role on Klyntar. We're proud of this set because we've spent much time to find and include the best variants.\
\
Traditionally, all we know the most important postulate of cryptography:\
\
&#x20;                                                   _<mark style="color:purple;">**Don't use your custom algorithms**</mark>_\
_<mark style="color:purple;">****</mark>_\
_<mark style="color:purple;">****</mark>_All crypto algorithms on Klyntar are:

* Open source(obviously)
* Taken from official builds(e.g. native modules,libs and so on)
* Written by well known companies(e.g. this [_<mark style="color:red;">repo</mark>_](https://github.com/cloudflare/circl) by CloudFlare experts or [_<mark style="color:red;">this</mark>_](https://github.com/coinbase/kryptology) by Coinbase)
* Tested following Diverse Double-Compiling scheme(like placebo against Thompson attack**.**[_<mark style="color:red;">Read more</mark>_](https://www.awelm.com/posts/evil-compiler/)). We've found at least several implementations of the same algorithm and tested them to compare that results will be the same and different authors haven't bugs.&#x20;
