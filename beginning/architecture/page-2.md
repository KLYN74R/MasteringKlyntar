---
description: Bits in the world of blockchains
cover: >-
  ../../.gitbook/assets/tumblr_b800eb940c93611ad96334db121b1cf4_2323ada7_1280.webp
coverY: -249.75065387968615
---

# 👽 Symbiotes

### <mark style="color:red;">**Why Abstraction matters?**</mark>

We built KLYNTAR with the way the modern world works. Container shipping, USB standards, traffic routing - all this is interchangeable in the world and the same everywhere. When developing KLYNTAR, we did not try to "hardcode" a consensus there, which would then have to be changed for 8 years, we did not try to bind a fixed number of validators or impose any hard restrictions.

That is why the architecture is based on the principle of modularity when each individual symbiote can be built as a constructor, independently choosing a consensus (generally in KLYNTAR called _<mark style="color:yellow;">**workflows**</mark>_), a set of hostchains, the type of interaction with them, its own fees policy, and so on. That is why the architecture is based on the principle of modularity when each individual symbiote can be built as a constructor, independently choosing a consensus (generally in KLYNTAR called workflows), a set of hostchains, the type of interaction with them, its own fees policy, and so on.

In fact, KLYNTAR is also a framework for creating your own blockchains for your needs, and having KLYNTAR Services will help you run them in parallel with the main symbiotes and get the security and capabilities of KLYNTAR right out of the box - only now the game will be by your rules.

Despite this, there are a number of "standard" and "general" components of each symbiote. So, for example, the standard implementation of the KLYNTAR core written in Node.js includes some common elements for all symbiotes such as:

* Server implementation
* Boot file ([_<mark style="color:purple;">**klyn74r.js**</mark>_](https://github.com/KLYN74R/KlyntarCore/blob/main/klyn74r.js))
* Common files & directorites(usually confgs)
* Common global variables(for example, global configuration object or mapping with private keys)
* Running services & plugins
* ...and that's it😅
