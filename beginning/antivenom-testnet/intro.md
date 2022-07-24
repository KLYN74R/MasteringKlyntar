---
description: Initial launch and quick start
cover: ../../.gitbook/assets/d84c40e770fba3b613c372e4e2df5e48.gif
coverY: 142.28421970357454
---

# ✴ Intro

{% hint style="info" %}
This page is basically a copy of our testnet launch README. However, there are additional details here, so we advise you to go over this page even if you have already read
{% endhint %}

![](https://readme-typing-svg.herokuapp.com/?font=Major+Mono+Display\&size=100\&color=C20000\&center=true\&vCenter=true\&width=500\&height=200\&lines=Klyntar)

As you've seen, KLYNTAR is in symbiotic relationship with other blockchains. By running different nodes of other projects, working with tools required by them, the most auful & irritating problem was problem with initial setup - misconfigs, old docs, semver mistakes, nightly versions and so on. That's why, we've prepared docker images to allow you to be sure that you'll have 100% succesful setup. Recommended to be used to run KLY nodes & clusters, Apollo and so on.It's for better experience not to force you to waste time for finding misconfigs, dependencies problems and so on. Build & run quickly and let's start 🚀

{% hint style="warning" %}
We assume that you already have Docker installed on your machine. If not, you can install it for Linux & Windows & Mac [_<mark style="color:red;">**here**</mark>_](https://docs.docker.com/engine/install/)_<mark style="color:red;">****</mark>_
{% endhint %}

<mark style="color:yellow;">**Check if Docker is installed**</mark>

```
johndoe@klyntar:~$ docker -v
Docker version 20.10.14, build a224086
```

#### <mark style="color:yellow;">**Download the image**</mark>

We present you our initial image [_<mark style="color:red;">**klyntar/all\_in\_one**</mark>_](https://hub.docker.com/repository/docker/klyntar/all\_in\_one).

![](http://dockeri.co/image/klyntar/all\_in\_one)

This is the image with Node.js, Go , Python and some other tools like `pnpm` , `node-gyp` , `git` and so on preinstalled. This is the base layer for our other Dockerfiles (at least for the kernel and Apollo). Approximate compressed size 606 megabytes.

Also in the[ _<mark style="color:red;">**KlyntarBaseImages**</mark>_](https://github.com/KLYN74R/KlyntarBaseImages) repository you can find the sources of our images with their Dockerfile and build scripts. You can clone them and build the image locally, or you can browse through the bash build script and go through its commands to install everything you need on your host machine. But in any case, we would recommend using containers

![](<../../.gitbook/assets/image (3).png>)

```bash
docker pull klyntar/all_in_one@sha256:dff001a9cd3da6328c504b52ed8a5748c47d23219feae220930dac1c1981cfe7
```

<mark style="color:yellow;">**Running a container**</mark>

We recommend giving a container multiple ports

In general, you can choose any, but we recommend due to a certain "standard"

* **7331** - mainnet/kNULL default port for initial symbiote kNULL(Easter egg:It's reversed 1337 :smile:)
* **9691** -default Apollo UI server port(Easter egg:it's reversed 1969-the Apollo-11 mission and the first moon landing :full\_moon\_with\_face:)
* **11111** - local testnet(AntiVenom)

{% hint style="warning" %}
**⚠ ATTENTION:**

This setup is the most default & simple way. If you need,you can manually run container with more advanced steps e.g. by using volumes,set user and so on
{% endhint %}

Run the container

```bash
docker run -dtp 7331:7331 -p 9691:9691 -p 11111:11111 --name klyntar0 klyntar/all_in_one@sha256:dff001a9cd3da6328c504b52ed8a5748c47d23219feae220930dac1c1981cfe7
```

<mark style="color:yellow;">**The final**</mark>

Enter the container and go to the root directory

```bash
docker exec -ti klyntar0 bash

# Inside container

cd ~
```

Clone the KlyntarCore repository

```bash
git clone https://github.com/KLYN74R/KlyntarCore.git

cd KlyntarCore
```

And finally, run 1 build command

```bash
pnpm run build
```

### **Now take a rest and see the building process. It may take some minutes,but you're free from self-install tons of libs,dependencies and walking among dirs**

![](https://camo.githubusercontent.com/890365925b4390e67ce217443ecde4c3b550c33be04b3b69f8992a995840b188/68747470733a2f2f692e70696e696d672e636f6d2f6f726967696e616c732f64302f36332f30392f64303633303936626134653037373935633162646639383537326362373961382e676966)

{% hint style="warning" %}
**⚠ ATTENTION:**

As we said before,this setup is the most default way for quick start. In a nutshell, KLYNTAR go through the dirs and runs Typescript compiler, set access rights(700 by default for root user) for build scripts, build addons via Go compiler and run _<mark style="color:red;">**npm link**</mark>_ to make possible to run <mark style="color:purple;">**klyntar**</mark> as binary from <mark style="color:yellow;">**PATH**</mark> (by creating symlink to Node.js dir)
{% endhint %}

The signal that the build is successful will be such messages in the console

![](<../../.gitbook/assets/image (23) (1).png>)

#### ...and after building Go addons

![](<../../.gitbook/assets/image (17).png>)

#### **...One more thing**

Insofar as KLYNTAR has many chains( known as _<mark style="color:red;">**symbiotes**</mark>_) which symbiotically linked with the _<mark style="color:red;">**hostchains**</mark>_( Bitcoin,Ethereum,Avalanche,Solana,Dogecoin,XRP and other chains), we need <mark style="color:red;">**connectors**</mark> to allow symbiotes to interact with hostchains(e.g. reading contract state, getting blocks, write to hostchains and so on)

Here's the situation with symbiote connectors right now

*   #### **kNULL**

    Our initial symbiote runned by KlyntarTeam will use [**dev0** ](https://github.com/KLYN74R/KlyntarCore/tree/main/KLY\_Hostchains/connectors/dev0)pack with connectors. The initial set of hostchains will become public soon.
*   #### **AntiVenom**

    The alias for testnet by default configuration(**ANTIVENOM/CONFIGS/symbiotes.json**) have disabled connection with the hostchains(or their testnets) but anyway, as far you can enable it, you should have installed dependecies for packs with connectors

So, if you want to make connectors available, enable them in the configuration

```json
//Где-то внутри symbiotes.json
//Для активации смените на false

"STOP_HOSTCHAINS":{
        
        "ltc":true,
        "bsc":true,
        "eth":true
    
}
```

After activation, go to the directory with a set of connectors and start downloading dependencies

```bash
# In KlyntarCore directory

cd KLY_Hostchains/connectors/dev0

pnpm install
```

### &#x20;                        <mark style="color:red;">🚀 Great, now everything is ready 🚀</mark>



### ☄️ <mark style="color:red;">**Running AntiVenom(testnet)**</mark>

We assume that before to start some symbiote, you want to run at least local testnet to check how it works,to get used to the interface and so on. For this, you can instantly run AntiVenom locally. The testnet directory is **KlyntarCore/ANTIVENOM** and has the following structure:

```
KlyntarCore
│     
│   
└───ANTIVENOM (default testnet directory if you don't override it via env variable)
│   │   
│   │   
│   └───CHAINDATA(will be created after the daemon run in testnet mode)
│   │    │
│   │    └───Wvzv9zGXJL4FngTKACPPDpHgCjE2k22jB9EnjmZr81Bi 
│   │       │
│   │       │───CANDIDATES
│   │       │───CONTROLLER_BLOCKS
│   │       │───HOSTCHAINS_DATA
│   │       │───INSTANT_BLOCKS
│   │       │───METADATA
│   │       └───STATE
│   │        
│   └───CONFIGS
│   │    │
│   │    │───network.json
│   │    │───node.json
│   │    │───services.json
│   │    └───symbiotes.json
│   │
│   └───GENESIS
│   │ 
│   └───LOGS
│   │ 
│   └───SNAPSHOTS

```

This structure will be common to all symbiotes and is located at the top level of the selected directory.

Since we strive for maximum abstraction, such a structure will be independent of the mode of operation of the symbiote - regardless of the consensus, everyone has a genesis, everyone has chain data, logs, and so on.

**Recommendation**

To run any symbiote (including testnet) you need 2 directories - **CONFIGS** and **GENESIS**. You can find them on our website or on the resources of the company or community that launches the symbiote. Let's create a separate directory for our AntiVenom testnet with the default configuration.

```bash
# In ~/KlyntarCore

# Create directory for symbiote(testnet in this case)
mkdir -p ANTIVENOM_0

cd ANTIVENOM

cp -r CONFIGS GENESIS ../ANTIVENOM_0
```

Now, you can set some environment variables to set the path for this directory and other values. Find out more on our resources, but now we need only env for path

```bash
export SYMBIOTE_DIR=~/KlyntarCore/ANTIVENOM_0
```

Now set mode

```bash
export KLY_MODE=test
```

Finally run

```bash
klyntar
```

### You should see the following

![](<../../.gitbook/assets/image (16).png>)

Since you are using default configuration, there is default keypair, workflow and so on. To continue decrypt your private key with the password `qwerty`

#### **Tip**

Now you have locally runned symbiote AntiVenom. Your node is a single one and works as **Controller** for **dev\_controller** workflow. Soon we'll show who to make your network more advanced by adding **InstantGenerators**, changing workflows, make your network semi-public, join your symbiote to external AntiVenom testnets, make your AntiVenom network in TOR network(via hidden services) and other cool features!

### <mark style="color:red;">KLYNTAR - your provider to the world of new blockchains</mark>

**Advice**

Look for more information on our resources

### &#x20;          <mark style="color:red;">🔥Congratulations, you are now part of KLYNTAR🔥</mark>



### <mark style="color:red;">**⚙️ Outcome**</mark>

KLYNTAR can do literally everything. Described here is less than 0.001% of potential. Soon you'll get to know about another features like:

* Interactions with the hostchains, services, mutualism
* How to make your AntiVenom more advanced by making it semi-public, by adding tons of plugins and so on
* How to use Cryptoland with cool crypto features like VRF, multi & threshold & linkable ring signatures, post quantum cryptography and so on
* How to run clusters
* How to create workflows and this way-change the consensus
* How to take part in social consensus & voting
* How to use Unobtanium - your united resources from other blockchains e.g. bitcoin mined blocks, frozen stakes on Polygon, miner on Helium and so on

### <mark style="color:red;">🤓</mark> <mark style="color:red;"></mark><mark style="color:red;">**Advice**</mark>

Follow us to get the news & updates ASAP. Discuss, share ideas, advices, help newbies to make our community more powerful.We're happy to involve new members to KLY community 😊

[​​![](https://img.shields.io/badge/Reddit-FF4500?style=for-the-badge\&logo=reddit\&logoColor=white)](https://www.reddit.com/r/KLYN74R/)​[​​![](https://img.shields.io/badge/Twitter-1DA1F2?style=for-the-badge\&logo=twitter\&logoColor=white)](https://twitter.com/KLYN74R)​[​​![](https://img.shields.io/badge/Medium-12100E?style=for-the-badge\&logo=medium\&logoColor=white)](https://klyntar.medium.com/)​[​​![](https://img.shields.io/badge/TikTok-000000?style=for-the-badge\&logo=tiktok\&logoColor=white)​](https://www.tiktok.com/@klyn74r) [​​![](https://img.shields.io/badge/Instagram-E4405F?style=for-the-badge\&logo=instagram\&logoColor=white)](https://www.instagram.com/klyn74r/)​[​​![](https://img.shields.io/badge/Pinterest-%23E60023.svg?\&style=for-the-badge\&logo=Pinterest\&logoColor=white)](https://www.pinterest.com/klyn74r)​[​​![](https://img.shields.io/badge/dev.to-0A0A0A?style=for-the-badge\&logo=devdotto\&logoColor=white)](https://dev.to/klyntar)​[​​![](https://img.shields.io/badge/GitHub-100000?style=for-the-badge\&logo=github\&logoColor=white)​](https://github.com/KLYN74R) [​​![](https://img.shields.io/badge/Telegram-2CA5E0?style=for-the-badge\&logo=telegram\&logoColor=white)](https://t.me/KLYN74R)​[​​![](https://img.shields.io/badge/Discord-7289DA?style=for-the-badge\&logo=discord\&logoColor=white)](https://discord.gg/f7e7fCp97r)​[​​![](https://img.shields.io/badge/Tor%20site-330F63?style=for-the-badge\&logoColor=white)](http://klyntar66kjwhyirucco6sjgyp2f7lfznelzgpjcp6oha2olzb4rlead.onion/)​[​​![](https://img.shields.io/badge/YouTube-FF0000?style=for-the-badge\&logo=youtube\&logoColor=white)​](https://www.youtube.com/channel/UC3TiyK40an6rQlf3BarMDoQ) [​​![](https://img.shields.io/badge/Facebook-1877F2?style=for-the-badge\&logo=facebook\&logoColor=white)](https://www.facebook.com/KLYN74R/)​[​​![](https://img.shields.io/badge/GitLab-330F63?style=for-the-badge\&logo=gitlab\&logoColor=white)](https://gitlab.com/KLYNTAR)​[​​![](https://img.shields.io/badge/Tumblr-%2336465D.svg?\&style=for-the-badge\&logo=Tumblr\&logoColor=white)](https://klyn74r.tumblr.com/)​​![](https://img.shields.io/badge/Stack\_Overflow-FE7A16?style=for-the-badge\&logo=stack-overflow\&logoColor=white)\
