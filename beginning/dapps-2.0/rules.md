---
description: Some information for creating your services
cover: ../../.gitbook/assets/25e6e637824091.574db6cb0643d.gif
coverY: 87.09677419354838
---

# ⁉ Rules

### <mark style="color:red;">**Repositories**</mark>

We recommend that you write and maintain your service as a repository for ease of version tracking and for ease of global development. We recommend sticking to industry standards and formats. So, for example, if this is a Rust project, then it should have a Rust-specific structure, if it is a Node.js project, familiar files like package.json and others should be present. This is necessary so that there are no problems with the process of starting your services due to the absence of a file or because you incorrectly specified the path to the bash script.

### <mark style="color:red;">Runner mechanisms</mark>

Everything will be taken into account in the network. Cryptography makes it very easy to verify and publish evidence of malicious activity. Because of this, we recommend that you correctly specify the keywords of the service, be honest about the necessary resources for your service. For example, if the service requires a lot of memory, then specify it. In addition to alerting those who aren't ready or don't have much memory, you'll also help runners so they can run your service in the right container, allocate the right amount of memory, and so on.

### <mark style="color:red;">**Services and social consensus**</mark>

Due to the fact that everything is tracked and signed, it is possible to use it very flexibly with social consensus. For example, it will be easy to prove the malicious behavior of some oracle, dishonest changes in the state of the balances of some token, and so on.

With the development of the project, other Best Practices for writing services will appear. We recommend visiting the Best Practices page

{% embed url="https://mastering.klyntar.org/beginning/best-practices" %}
