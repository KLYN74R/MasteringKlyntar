---
description: A few words about KLYNTAR VM
cover: >-
  https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FphIHWZY173DpNXBbDjVg%2Fuploads%2FpFJEMjfSiciMrbEzPlyQ%2Fvaporwave_artwork_science_fiction_concept_art_original_4k_hd.jpg?alt=media&token=b163cdca-d00d-4867-8511-a171a14cc266
coverY: -39
---

# ℹ Introduction

### <mark style="color:red;">**Start**</mark>

![](<../../.gitbook/assets/image (15) (1).png>)

Today, the need for smart contracts in blockchains is actually mandatory, because it allows you to write custom logic in the form of contracts that then live and execute in a decentralized environment.

At KLYNTAR we tried to be as versatile as possible in order to allow you to quickly and easily start writing anything for KLYNTAR. You will be able to write in any language that you know well and that compiles into WASM modules, as well as use advanced features such as requests to the network or storage of big data "off the block" symbiote that can be requested to perform some function and much more.

KLYNTAR VM is based on WebAssembly which allows you to write in any language, then compile it into .wasm bytecode and run it in a secure environment.

WebAssembly is secure thanks to

* Lack of network access
* Lack of access to the file system
* Lack of access to the random number generator
* Other stuff

Thus, it is possible to locally (in your development environment, if you are a developer) create compressed and compiled .wasm files, and then publish them to the KLYNTAR network for execution

![](<../../.gitbook/assets/image (7).png>)

### <mark style="color:red;">More about WebAssembly</mark>

Today, WebAssembly is becoming popular all over the world and in various areas - from small modules for working in the browser to cloud FaaS services and blockchains (Cosmos, Near, etc.).

Below is a list of languages that can already be used to compile to WASM and work safely on KLYNTAR symbiotes

![](<../../.gitbook/assets/image (25) (1) (1).png>)

{% embed url="https://github.com/appcypher/awesome-wasm-langs" %}

WebAssembly is not exactly a language, it's more of a low-level bytecode that executes quickly and safely. For an illustrative example, we can consider the .wat file format - these are the files of the so-called WebAssemblyText. It can also be compiled to wasm and vice versa. So for example you can repeat this procedure using the tools wat2wasm (obviously <mark style="color:purple;">**.wat**</mark> => <mark style="color:purple;">**.wasm**</mark>) and wasm2wat (vice versa). Just the same, .wat files allow us to see WASM opcodes, understand that there is work with the stack like low-level languages, and so on. For example, here is the implementation of a simple function that takes 2 parameters and returns their sum

File _<mark style="color:red;">**add.wat**</mark>_

```wasm
(module
 (func (export "calculate")
 (param $value_1 i32) (param $value_2 i32)
 (result i32)
    local.get $value_1
    local.get $value_2
    i32.add
    )
 )
```

Next, we use the _<mark style="color:purple;">**wat2wasm**</mark>_ tool that comes with the _<mark style="color:red;">**wat-wasm**</mark>_ package.

![](<../../.gitbook/assets/image (23) (1) (1).png>)

We compile (with the help of flags -O3z we compress as much as possible and carry out optimization)

```
wat2wasm add.wat -o add.wasm -O3z
```

And use in Node.js

```javascript
import fs from 'fs';
const bytes = fs.readFileSync (__dirname+'/add.wasm');

let value_1 = parseInt (process.argv[2]);
let value_2 = parseInt (process.argv[3]);

let obj = await WebAssembly.instantiate(new Uint8Array(bytes));

let add_value = obj.instance.exports.calculate(value_1,value_2);

console.log(`${value_1}+${value_2}=${add_value}`);
```

```bash
node test.js 11 33
```

```bash
11+33=44
```

This was a simple use case and you learned a little more about its format by looking at the code of the .wat file.

Of course, it is difficult to write in pure WAT and therefore you will most likely use high-level languages such as AssemblyScript (an add-on on TypeScript), Rust, C ++, Python and others.

We will just start using AssemblyScript as the first entry point for .wasm smart contracts on KLYNTAR.

![](<../../.gitbook/assets/image (9) (1).png>)

{% embed url="https://github.com/AssemblyScript/assemblyscript" %}

More will be added later. Here are some related repositories

![](<../../.gitbook/assets/image (26) (1) (1).png>)

![](<../../.gitbook/assets/image (18) (1).png>)

![](<../../.gitbook/assets/image (22) (1) (1).png>)

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
