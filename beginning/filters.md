---
description: Learn more about filters as part of symbiote workflows
cover: ../.gitbook/assets/GrfE.gif
coverY: 0
---

# 🛑 Filters

![](<../.gitbook/assets/image (14) (1).png>)

### <mark style="color:red;">Generally</mark>

The role of filters at first glance seems to be less significant than the role of connectors or plugins. However, they are also extremely important as they help you better filter the incoming data to your nodes.

As you have already read in the previous sections, block generation and block validation flows are asynchronous and independent of each other. Yes, in KLYNTAR blocks can be generated before they are checked. Thanks to the peculiarities of work and the stakes of users on their own honesty, we manage to achieve maximum performance and scalability.

Meanwhile, in general, to prevent all sorts of nastiness from entering the blockchain, we need filters.

A set of filters usually comes in one package along with the workflow repository, since it is assumed that the developer has already taken care of the minimum level of security - he has taken into account the available transactions on the workflow, better understands their pitfalls, and so on.

Meanwhile, you may notice that the filters are not fixed at the symbiote manifest level. This is because each node or group of nodes independently makes a decision regarding the reception of certain data.

### <mark style="color:red;">Where is or where to put your own filters</mark>

The filters are in the workflows package, that is, along this path

<mark style="color:orange;">**<**</mark><mark style="color:red;">**YOUR\_KLYNTAR\_DIRECTORY**</mark><mark style="color:orange;">**>/KLY\_Workflows/<**</mark><mark style="color:red;">**name of workflow**</mark><mark style="color:orange;">**>/filters.js**</mark>

{% hint style="info" %}
This is an optional path because the workflow developer can change the position of the filters in the hierarchy - for example, categorize, add a configuration file, and so on.
{% endhint %}

As for the developers of KlyntarTeam, for simplicity, we put the filters right away. Here's what it looks like

![Pretty simple hierarchy](<../.gitbook/assets/image (19) (1).png>)

### <mark style="color:red;">What are filters on the code level</mark>

Filters are a simple file with one object for export, which lists various kinds of triggers for events coming to you - transactions, locks, delegations, and so on.

Depending on their type, you already make decisions whether to accept them in the mempool or not

{% hint style="warning" %}
It is still recommended to use filters from the developers of the workflow pack. This will protect you from the fact that you forget to process some event or process it incorrectly.

Developers, in turn, are encouraged to enter some configuration file at the level of the workflow pack in which it will be possible to simply assign a minimum commission level, block incoming events from addresses from black lists, and so on.
{% endhint %}

![](<../.gitbook/assets/image (4) (1).png>)

### <mark style="color:red;">Repository with filters</mark>

We also created a repository with filters where different developers can publish their filters.

{% embed url="https://github.com/KLYN74R/Filters" %}
