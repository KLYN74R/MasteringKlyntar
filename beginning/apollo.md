---
description: The detailed overview of our CLI & UI tool to control your KLY empire🪐
---

# 🌚 Apollo



![](https://user-images.githubusercontent.com/53381472/174458851-d6cbe7cd-3696-48ef-8839-975f061e393f.png)

![](https://readme-typing-svg.herokuapp.com/?font=Major+Mono+Display\&size=48\&duration=4000\&color=C20000\&center=true\&vCenter=true\&width=300\&height=80\&lines=Apollo)

### 📖 Content

* <mark style="color:red;"></mark>[<mark style="color:red;">Short intro</mark>](apollo.md#short-intro)<mark style="color:red;"></mark>
* <mark style="color:red;"></mark>[<mark style="color:red;">How to build</mark>](apollo.md#how-to-build)<mark style="color:red;"></mark>
* [<mark style="color:red;">Modularity</mark>](apollo.md#modularity)<mark style="color:red;"></mark>
* [<mark style="color:red;">Advice</mark>](apollo.md#advice)<mark style="color:red;"></mark>
* [<mark style="color:red;">Docs</mark>](apollo.md#docs)<mark style="color:red;"></mark>



### ⚡ Short intro

We're happy to present you Apollo - our powerful CLI & UI tool to control your KLYNTAR infrastructure. With this tool you can do everything - use it as wallet, interact with decentralized services, control your Unobtanium sources, deep dive into Cryptoland-our amazing collection of crypto algorithms available on KLYNTAR.

\


### 🏗️ How to build

As you've seen, KLYNTAR is in symbiotic relationship with other blockchains. By running different nodes of other projects, working with tools required by them, the most auful & irritating problem was problem with initial setup - misconfigs, old docs, semver mistakes, nightly versions and so on. That's why, we've prepared docker images to allow you to be sure that you'll have 100% succesful setup. So,let's start 🚀

#### **NOTE**

We assume that you have Docker on the board. You can install Docker for Linux & Windows & Mac [here](https://docs.docker.com/engine/install/)

```shell

klyntar@apollo:~# docker -v
Docker version 20.10.14, build a224086
```

#### **Download the image**

We present you our first image [klyntar/all\_in\_one](https://hub.docker.com/repository/docker/klyntar/all\_in\_one). This is universal image with preinstalled Node.js, Go , Python and some tools like `pnpm` , `node-gyp`, `git` and so on. We've created it to save your time and nervous system. This is the base layer for all our Dockerfiles(at least for core and Apollo). The aproximate compressed size is 606M. Also, in our repository [KlyntarBaseImages](https://github.com/KLYN74R/KlyntarBaseImage) you can find the sources of all base-layer Dockerfiles, so you can clone and build it yourself or find the bash build script and so through the process to install requirements to your host machine. But anyway,we recomend you to use containers.

![](https://user-images.githubusercontent.com/53381472/174490998-2041af0d-6cd5-4873-ad64-fa810cda02df.jpg)

```shell

docker pull klyntar/all_in_one@sha256:dff001a9cd3da6328c504b52ed8a5748c47d23219feae220930dac1c1981cfe7
```



#### **Run container**

We also recomend you to make port forwarding at least for default Apollo port 9691

#### **NOTE**

This is the most default & simple way. If you need,you can manually do this with more advanced steps e.g. using volumes,set user and so on

```shell
docker run -dtp 9691:9691 --name test_kly klyntar/all_in_one@sha256:dff001a9cd3da6328c504b52ed8a5748c47d23219feae220930dac1c1981cfe7
```

#### **Final**

Go into container to root dir

```shell
docker exec -ti test_kly bash

# Inside container

cd ~
```

Clone Apollo repository

```shell

git clone https://github.com/KLYN74R/Apollo.git

cd Apollo
```

Finally,run the only one command

```shell

pnpm run build
```

### **Now take a rest and see the building process. It may take some minutes,but you're free from self-install tons of libs,dependencies and walking among dirs**

\


![](https://i.pinimg.com/originals/d0/63/09/d063096ba4e07795c1bdf98572cb79a8.gif)

#### &#x20;The signs that build was succesful are messages to console like this

![](https://2131090630-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FphIHWZY173DpNXBbDjVg%2Fuploads%2FdewG1SQftz0ndvmG4fNa%2Fimage.png?alt=media\&token=ad2710a7-0fd1-43cb-ad80-62e78badb989)

#### ...and this

![](https://2131090630-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FphIHWZY173DpNXBbDjVg%2Fuploads%2FL3RavrjoA7nktQKFfV3i%2Fphoto\_2022-06-04\_11-55-04.jpg?alt=media\&token=6363785e-a243-4f98-80ca-5ee83b97da87)

#### Now try to run. You should see the following

![](https://user-images.githubusercontent.com/53381472/174460136-49cbf58b-fe08-4952-81b2-3b6e13d96444.jpg)



### ⚙️ Modularity

Working with different "hacking" tools,I've get the experience of so called 'best practises' of how to build real powerful tool. That's why, Apollo(as KLYNTAR) will be very modular. Just now,you have three ways to improve Apollo behaviour by loading modules to KLY\_Modules, KLY\_ServicesAPI and KLY\_WorkflowsAPI

\


#### **KLY\_Modules**

Directory for your external modules. This might be extra useful commands. Might be written by you or any other 3rd party. Must contain 2 directories **cli**(contains everything for commands in CLI) and **ui**(directory with everything for UI in browser). Soon we'll make a tutorial of HOWTO write modules for Apollo.

Each directory-is typically Git repository to allow you to easily update different modules independently if you need and swap versions. Moreover,soon you'll also have an amazing ability to verify authors cryptographically - via code signing. By having hash of repository you can verify authority and be sure that code is original using different crypto features like multisig or post-quantum cryptography,social staking and so on. We describe it in [Basic Security](https://mastering.klyntar.org/beginning/basic-security#additional-features) in our MasteringKlyntar book.



* CLI part

In CLI extra modules looks like ordinary commands. To allow your users to differ them, please, give them original prefix or make a single command with repository name and hide commands to subcommands

* UI part

If module also has a UI part(which is often the case), then you'll have ability to visit:

```shell

http(s)://<your_interface>:<port>/modules
```

to find there the entry point to your module.

\


**Summarizing this,your directories tree on these levels should look like this**

```
Apollo
│     
│   
└───KLY_Modules
│   │   
│   │
│   │   
│   └───init(default module,the entry point for the other)
│   │    │   
│   │    │───cli(directory for files to improve CLI)
│   │    │   │
│   │    │   └───init.js 
│   │    │
│   │    └───ui(directory for files to improve UI)
│   │        │
│   │        │───routes.js
│   │        │───templates(.ejs files)
│   │        │     └─...
│   │        │───configs.json
│   │        └───...
│   │   
│   │
│   └───your_custom_module
│        │   
│        │───cli(directory for files to improve CLI)
│        │    │   
│        │    └───init.js
│        │
│        └───ui(directory for files to improve UI)
│            │
│            │───routes.js
│            │───templates(.ejs files)
│            │     └─...
│            │───configs.json
│            └───...
│
│
└───KLY_ServicesAPI
    └───...
```

To update the repository with module go to appropriate directory **KLY\_Modules/\<your\_module>** and pull changes



#### **KLY\_ServicesAPI**

> **ServiceAPI** - directory with API repositories to interact with the scope of service runned on Klyntar. Imagine if all smart contracts on ETH will have a unique design in your wallet, separate page with all available features specific to contract. Since we have wider power, we also have so complicated way to improve abilities of your Apollo instance.

\


The same principle works for the services API. Each subdirectory - it's a repository. To check available services API go to

```shell

http(s)://<your_interface>:<port>/services
```

****

**KLY\_WorkflowsAPI**

> **WorkflowsAPI** - directory with API repositories to interact with symbiotes on Klyntar. Insofar as they can use different workflows(thanksfully to [Mutations principle](https://mastering.klyntar.org/beginning/mutations)),we need to make possible to use appropriate algorithms,build right events to send to symbiotes and use other specific features like traffic over TOR or threshold signatures. Imagine if you'll have ability to control your Bitcoin, Solana, Avalanche, Cosmos assets(native coins,tokens,etc.), execute smart contracts, make delegations using only one instrument. Yes,this is what Apollo do.

\


The same principle as for services API. Each subdirectory - it's a repository in this directory. To check your symbiotes and how to interact with them go to

```shell

http(s)://<your_interface>:<port>/symbiotes
```



### 🤓 Advice

Follow us to get the news & updates ASAP. Discuss, share ideas, advices, help newbies to make our community more powerful.We're happy to involve new members to KLY community 😊

\
[![](https://img.shields.io/badge/Reddit-FF4500?style=for-the-badge\&logo=reddit\&logoColor=white) ](https://www.reddit.com/r/KLYN74R/)[![](https://img.shields.io/badge/Twitter-1DA1F2?style=for-the-badge\&logo=twitter\&logoColor=white) ](https://twitter.com/KLYN74R)[![](https://img.shields.io/badge/Medium-12100E?style=for-the-badge\&logo=medium\&logoColor=white) ](https://klyntar.medium.com/)[![](https://img.shields.io/badge/TikTok-000000?style=for-the-badge\&logo=tiktok\&logoColor=white)](https://www.tiktok.com/@klyn74r)\
[![](https://img.shields.io/badge/Instagram-E4405F?style=for-the-badge\&logo=instagram\&logoColor=white) ](https://www.instagram.com/klyn74r/)[![](https://img.shields.io/badge/Pinterest-%23E60023.svg?\&style=for-the-badge\&logo=Pinterest\&logoColor=white) ](https://www.pinterest.com/klyn74r)[![](https://img.shields.io/badge/dev.to-0A0A0A?style=for-the-badge\&logo=devdotto\&logoColor=white) ](https://dev.to/klyntar)[![](https://img.shields.io/badge/GitHub-100000?style=for-the-badge\&logo=github\&logoColor=white)](https://github.com/KLYN74R)\
[![](https://img.shields.io/badge/Telegram-2CA5E0?style=for-the-badge\&logo=telegram\&logoColor=white) ](https://t.me/KLYN74R)[![](https://img.shields.io/badge/Discord-7289DA?style=for-the-badge\&logo=discord\&logoColor=white) ](https://discord.gg/f7e7fCp97r)[![](https://img.shields.io/badge/Tor%20site-330F63?style=for-the-badge\&logoColor=white) ](http://klyntar66kjwhyirucco6sjgyp2f7lfznelzgpjcp6oha2olzb4rlead.onion)[![](https://img.shields.io/badge/YouTube-FF0000?style=for-the-badge\&logo=youtube\&logoColor=white)](https://www.youtube.com/channel/UC3TiyK40an6rQlf3BarMDoQ)\
[![](https://img.shields.io/badge/Facebook-1877F2?style=for-the-badge\&logo=facebook\&logoColor=white) ](https://www.facebook.com/KLYN74R/)[![](https://img.shields.io/badge/GitLab-330F63?style=for-the-badge\&logo=gitlab\&logoColor=white) ](https://gitlab.com/KLYNTAR)[![](https://img.shields.io/badge/Tumblr-%2336465D.svg?\&style=for-the-badge\&logo=Tumblr\&logoColor=white) ](https://klyn74r.tumblr.com/)[![](https://img.shields.io/badge/Stack\_Overflow-FE7A16?style=for-the-badge\&logo=stack-overflow\&logoColor=white)](broken-reference)



### 📚Docs

Read the docs here to find out more\


:flag\_gb:: [![](https://img.shields.io/badge/Gitbook-000000?style=for-the-badge\&logo=gitbook\&logoColor=white)](https://mastering.klyntar.org)\
:flag\_ru:: [![](https://img.shields.io/badge/Gitbook-000000?style=for-the-badge\&logo=gitbook\&logoColor=white)](https://ru.mastering.klyntar.org)
