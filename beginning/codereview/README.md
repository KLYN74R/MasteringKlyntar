---
description: What everyone expected from others
cover: ../../.gitbook/assets/223e6792880429.5e569ff84ebef.gif
coverY: -117.62176165803109
---

# 🧑💻 CodeReview

### <mark style="color:red;">**What is it?!**</mark>

The scope of crypto projects is often open source solutions. Since it is assumed that numerous developers will work on the kernel and its components, as well as other ecosystem projects, it would be good practice to make it clear what the kernel consists of, how the daemon is launched step by step, and explain the directory structure. Due to the fact that the project is large and complex, this will be extremely useful both for people who just want to learn more about the project, and for developers. Since we are just getting started right now, we will only provide something like a demo of what it will look like. Soon, we will create a separate book (documentation) that will be devoted to just this.

### <mark style="color:red;">Promised demo version</mark>

{% hint style="info" %}
Below will be a small "demo version" of the introduction to the code in order for you to imagine how we plan to provide information to developers. Also note that the following sections (_<mark style="color:red;">**Addons**</mark>_, <mark style="color:red;">**Blocks**</mark>...) have the _<mark style="color:purple;">**Coming soon**</mark>_ label. We will fill this in as interest in the project grows.
{% endhint %}

{% hint style="warning" %}
For development and code changes, we recommend cloning the repository again to a separate directory instead of changing to the one that runs the production version of the kernel.
{% endhint %}

### <mark style="color:red;">Preparing for parsing</mark>

For further reading and analysis, we recommend that you open the KLYNTAR kernel repository and, along with this guide, gradually figure out what's what

{% embed url="https://github.com/KLYN74R/KlyntarCore" %}

### <mark style="color:red;">**Directory tree**</mark>

Before starting to deal with the code, it is worth paying attention to the structure of the kernel directories. It has the following form

{% hint style="info" %}
Depth limit of 1 used
{% endhint %}

```
|-- KLY_Addons
|
|-- KLY_Hostchains
|
|-- KLY_Mutualism
|
|-- KLY_Plugins
|
|-- KLY_Runners
|
|-- KLY_Services
|
|-- KLY_Tests
|
|-- KLY_Utils
|
|-- KLY_VirtualMachines
|
|-- KLY_Workflows

```



<mark style="color:purple;">**KLY\_Addons**</mark>

A directory with various kinds of code in other languages. There are sources in Go, Rust and C ++ that require certain manipulations such as compiling into a library and converting to addons. So it will be enough to go to 1 directory and run the build. It is located at the top level of the kernel, as it contains mainly algorithms that will be common to different worker processes

<mark style="color:purple;">**KLY\_Hostchains**</mark>

A large and critical directory that used to interact with hostchains

<mark style="color:purple;">**KLY\_Mutualism**</mark>

Directory with functionality for cross-symbiotic interaction

<mark style="color:purple;">**KLY\_Plugins**</mark>

Contains plugins that are loaded separately by the node operator and serve to extend the capabilities of the kernel, workflows, and so on. More about plugins [_<mark style="color:red;">**here**</mark>_](../plugins.md)

<mark style="color:purple;">**KLY\_Runners**</mark>

Contains code for runners that listen for new services and run further logic based on the configuration - what to run and what not to run, in which container, which script to execute, and so on. There will also be a default runner from Andromeda developers. You can see this by looking at the repository

![](<../../.gitbook/assets/image (25) (1) (1) (1).png>)

{% hint style="warning" %}
Don't forget that the development process is ongoing
{% endhint %}

<mark style="color:purple;">**KLY\_Services**</mark>

Storage for services

<mark style="color:purple;">**KLY\_Tests**</mark>

Directory with individual units and other tests

<mark style="color:purple;">**KLY\_Utils**</mark>

Contains algorithms and data structures. Again, it is at the top level due to the fact that the algorithms and useful functions here are common to all symbiotes. We can even look at it visually

![](<../../.gitbook/assets/image (10) (1).png>)

<mark style="color:purple;">**KLY\_VirtualMachines**</mark>

Directory with virtual machines available to be used. Currently, it's WASM-based KLY-WVM and EVM-based KLY-EVM. Also, the abstract VM - UVM is a universal VM that allow interaction between EVM and WASM + other interesting and useful features like oracles, offchain abilities, etc.

<mark style="color:purple;">**KLY\_Workflows**</mark>

Contains workflows implementations for symbiotes

### <mark style="color:red;">Conclusion</mark>

This was an introductory explanation of the core. We started with the structure and will continue to disassemble in more detail and clearly. We believe that such a manual will be useful and give a deep understanding of KLYNTAR
