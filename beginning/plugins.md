---
description: What makes KLYNTAR truly powerful
cover: ../.gitbook/assets/thumb-1920-1065736.jpg
coverY: 260.31088082901556
---

# 🔌 Plugins

![](<../.gitbook/assets/image (18).png>)

### <mark style="color:red;">What's this?</mark>

Earlier we wrote that modularity and extensions are one of the pillars of KLYNTAR. It is convenient when the system is not oak, it is easily supplemented with new features, useful APIs, and all this thanks to the many developers who will permanently improve it.

In the documentation, you have already noticed this at the level of symbiote workflows, at the Apollo level, and so on. Now let's talk about top-level plugins that are more general. Let's give a simple definition

{% hint style="info" %}
A _<mark style="color:red;">**KLYNTAR plugin**</mark>_ is a separately downloadable repository for your node / infrastructure that allows you to extend and / or improve the behavior of KLYNTAR
{% endhint %}

### <mark style="color:red;">**Usage**</mark>

Speaking about the importance of plugins, it is enough to simply list the potential number of use cases for which they are suitable. Here are "just" "a few" examples:

<mark style="color:yellow;">**For bots**</mark>

Launch a server for a bot (Telegram, Discord) that will inform you about events on the symbiotes on which your nodes work, which will allow you to make payments in Telegram without leaving your favorite messenger. Well, or at all - give your bot more privileges for maximum opportunities

<mark style="color:yellow;">**For custom logging mechanisms**</mark>

Getting detailed information about what is happening is an extremely important element. With the help of plugins, you can flexibly and dynamically change and receive logs that will be necessary for you

<mark style="color:yellow;">**To extend available APIs**</mark>

Of course, we will also constantly improve and supplement the existing set, but here you will also get great opportunities for control

<mark style="color:yellow;">**For dynamic removal of telemetry, launching your explorers, etc.**</mark>

Convenient when you get the actual explorer out of the box

<mark style="color:yellow;">**To run snapshot validation, compression, and transfer**</mark>

We previously wrote about betting on fortunes. It can also be used for faster snapshot loading, various checks using cryptographic magic and much more.

<mark style="color:yellow;">**To dynamically generate a list of connected nodes**</mark>

Blockchains usually work in a P2P environment and each node has a list of other nodes connected to it. Through plugins, it will be possible to add logic for adding or removing them from your list

<mark style="color:yellow;">**To set listeners for DB events**</mark>

The first implementation of the KLYNTAR core uses LevelDB which supports handling of interaction events with the database

<mark style="color:yellow;">**To install gateways in the**</mark>** **<mark style="color:red;">**TOR**</mark>** **<mark style="color:yellow;">**/**</mark>** **<mark style="color:red;">**I2P**</mark>** **<mark style="color:yellow;">**/**</mark>** **<mark style="color:red;">**ZeroNet**</mark>** **<mark style="color:yellow;">**network and others**</mark>

Yes Yes Yes. KLYNTAR will keep in touch with them. Here we have indicated only the most used and popular. Using such bridges, you will be able to run KLYNTAR nodes in TOR (as a hidden service) or I2P and at the same time interact with them as if they were in a normal network.

You can also use this gateway as a SOCKS proxy for Apollo to interact with KLYNTAR through the mentioned TOR

<mark style="color:yellow;">**For cache managers**</mark>

Delete, add, rotate. Get creative, create efficient managers for faster performance

### <mark style="color:red;">Directory level hierarchy</mark>&#x20;

Everything is pretty simple here. Plugins are located in the directory

<mark style="color:orange;">**<**</mark><mark style="color:red;">**YOUR\_KLYNTAR\_DIRECTORY**</mark><mark style="color:orange;">**>/KLY\_Plugins**</mark>

```
KlyntarCore
│     
└───KLY_Plugins
│  │
│  │───Bot
│  │───Logger
│  │───CacheManager
   └───...
```

Since you can run several daemons at the same time, it is convenient to have and update similar plugins in one place.

{% hint style="info" %}
When starting, do not forget to make sure that the plugins do not conflict for a port, some directory, and so on.
{% endhint %}

### <mark style="color:red;">Plugins from developers</mark>

All plugins from the KlyntarTeam developers will have the _<mark style="color:purple;">**dev\_**</mark>_ prefix. Thus, it will be easy to find them when parsing directories or using grep for example. Plugins from KlyntarTeam do not mean that they are somehow better or cooler than from third-party developers - we appreciate the work and contribution of everyone. However, it is worth emphasizing that such plugins have an advantage, because members of the KlyntarTeam clearly have a deeper understanding of the principles of KLYNTAR, core features, and so on. It is to be expected that such plugins will have better support, fewer bugs and be better studied by the community, which is good from a security point of view.

For example, we have already added the _<mark style="color:orange;">**dev\_nets\_gateway**</mark>_, _<mark style="color:orange;">**dev\_websocket**</mark>_, _<mark style="color:orange;">**dev\_proxy**</mark>_ and others plugins. All of them are currently in development.

Also, in addition to installing third-party plugins, some plugins will be built into the core repository itself that will be the most popular among the community.

### <mark style="color:red;">For developers + where to find plugins</mark>

For convenience, we have created a separate repository for plugins where developers can upload code, and those who want to improve their infrastructure can install whatever they like

{% embed url="https://github.com/KLYN74R/Plugins" %}

{% hint style="info" %}
Мы вскоре опубликуем инструкцию как и что заливать в этот репозиторий
{% endhint %}

### <mark style="color:red;">**Conclusion**</mark>

Plugins can also have compatibility levels - be universal or for a specific workflow. Soon we will tell you how to improve compatibility. Until then, keep creating!
