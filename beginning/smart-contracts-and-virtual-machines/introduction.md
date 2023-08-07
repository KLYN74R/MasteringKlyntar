---
description: A few words about virtual machines available on KLY
cover: >-
  https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FphIHWZY173DpNXBbDjVg%2Fuploads%2FpFJEMjfSiciMrbEzPlyQ%2Fvaporwave_artwork_science_fiction_concept_art_original_4k_hd.jpg?alt=media&token=b163cdca-d00d-4867-8511-a171a14cc266
coverY: -39
---

# ℹ Introduction

## <mark style="color:red;">**Start**</mark>

<figure><img src="../../.gitbook/assets/KLY Virtual Machines.png" alt=""><figcaption></figcaption></figure>

Today, the need for smart contracts in blockchains is actually mandatory, because it allows you to write custom logic in the form of contracts that then live and executed in a decentralized environment.

At KLY we try to be as versatile as possible to allow you to quickly and easily start writing anything for KLYNTAR. That is why we provide developers with the opportunity to create smart contracts with amazing features that are available exclusively on KLY.

So, on KLY there will be such opportunities for creating decentralized logic:

* <mark style="color:red;">**KLY-WVM**</mark> - WASM-based virtual machine with wide support of several languages, tons of extensions, cross-VM calls to KLY-EVM, etc.
* <mark style="color:red;">**KLY-EVM**</mark> - EVM compatible VM with tons of features like sharding, storage-by-subscription model, fees in tokens, improved opcodes logic, cross-VM calls to KLY-WVM, etc.
* <mark style="color:red;">**UVM**</mark> - Universal Virtual Machine. Absctract VM which allow you to create DApps 2.0, interact with network, call inbuild oracles system, create & use Docker containers, create codeless smart-contracts with real-world execution and much more!

The KLYNTAR virtual machine is individual for each symbiote in terms of features and cost table. For its work, it uses a resource called _<mark style="color:red;">**energy**</mark>_. We decided to call the analogy with gas on Ethereum that way, but with the only difference that the concept of energy is more global.

As we know from physics

> Energy does not come from anywhere and does not go anywhere, but only passes from one state to another

With this in mind, we continue to work on KLYNTAR VM. You can run a virtual machine for tokens, for the level of utility of your service, for the amount of unobtanium, and much more.

However, in general, the essence of energy as a resource on KLYNTAR will be similar to the essence of gas in EVM machines - to provide a calculation of the cost of resources spent to perform a smart contract (its functions).

Through the principle of mutation, each symbiote individually assigns itself KLYNTAR VM capabilities and a spreadsheet. You can even make smart contracts run for free, build your own tree of who is allowed to run which smart contract for free, and so on.

### <mark style="color:red;">Measuring table</mark>

Earlier we showed you a simple function in the add.wat file and there you could see that WebAssembly uses bytecodes. For the symbiote, it will be possible to configure the virtual machine in such a way as to independently adjust how much power each opcode will consume.

Here is an example **vmEnergyTable.json**.

{% embed url="https://github.com/KLYN74R/KlyntarCore/blob/main/KLY_Workflows/dev_controller/vmEnergyTable.json" %}

```json
{
    "start": 0,
    "type": {
      "params": {
        "DEFAULT": 0
      },
      "return_type": {
        "DEFAULT": 0
      }
    },
    "import": 0,
    "code": {
      "locals": {
        "DEFAULT": 1
      },
      "code": {
        "get_local": 120,
        "set_local": 120,
        "tee_local": 120,
        "get_global": 120,
        "set_global": 120,
  
        "load8_s": 120,
        "load8_u": 120,
        "load16_s": 120,
        "load16_u": 120,
        "load32_s": 120,
        "load32_u": 120,
        "load": 120,
  
        "store8": 120,
        "store16": 120,
        "store32": 120,
        "store": 120,
  
        "grow_memory": 10000,
        "current_memory": 100,
  
        "nop": 1,
        "block": 1,
        "loop": 1,
        "if": 1,
        "then": 90,
        "else": 90,
        "br": 90,
        "br_if": 90,
        "br_table": 120,
        "return": 90,
  
        "call": 90,
        "call_indirect": 10000,
  
        "const": 1,
  
        "add": 90,
        "sub": 45,
        "mul": 45,
        "div_s": 36000,
        "div_u": 36000,
        "rem_s": 36000,
        "rem_u": 36000,
        "and": 45,
        "or": 45,
        "xor": 45,
        "shl": 67,
        "shr_u": 67,
        "shr_s": 67,
        "rotl": 90,
        "rotr": 90,
        "eq": 45,
        "eqz": 45,
        "ne": 45,
        "lt_s": 45,
        "lt_u": 45,
        "le_s": 45,
        "le_u": 45,
        "gt_s": 45,
        "gt_u": 45,
        "ge_s": 45,
        "ge_u": 45,
        "clz": 45,
        "ctz": 45,
        "popcnt": 45,
  
        "drop": 120,
        "select": 120,
  
        "unreachable": 1
      }
    },
    "data": 0
  }
```

{% hint style="info" %}
In more detail about the principles of measurement and such tables, we talk in the section Advanced features.
{% endhint %}

### <mark style="color:red;">Links</mark>

{% embed url="https://www.rust-lang.org/fr/what/wasm" %}

{% embed url="https://wasmbook.com/" %}

{% embed url="https://klyntar.medium.com/klyntar-virtual-machines-part-1-kly-vm-a-wasm-based-mutable-extendable-native-klyntar-vm-94aafe76ae0f" %}
