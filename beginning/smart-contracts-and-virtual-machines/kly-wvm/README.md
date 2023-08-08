---
description: WASM-based amazing virtual machine by KLY
cover: ../../../.gitbook/assets/photo_2020-05-10_21-01-55.jpg
coverY: 97
---

# 💣 KLY-WVM

## <mark style="color:red;">Intro</mark>

<figure><img src="../../../.gitbook/assets/KLY-WVM preview.gif" alt=""><figcaption></figcaption></figure>

KLYNTAR WVM is based on WebAssembly which allows you to write in any language, then compile it into <mark style="color:purple;">**.wasm**</mark> bytecode and run it in a secure environment.

<figure><img src="../../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

WebAssembly is secure thanks to

* Lack of network access
* Lack of access to the file system
* Lack of access to the random number generator
* Other stuff

Thus, it is possible to locally (in your development environment, if you are a developer) create compressed and compiled .wasm files, and then publish them to the KLYNTAR network for execution.

You will be able to write in any language that you know well and compile into WASM modules, as well as use advanced features such as requests to the network or external storage of big data and much more.

## <mark style="color:red;">More about WebAssembly</mark>

Today, WebAssembly is becoming popular all over the world and in various areas - from small modules for working in the browser to cloud FaaS services and blockchains (Cosmos, Near, etc.).

Below is a list of languages that can already be used to compile to WASM and work safely on KLYNTAR symbiotes

<figure><img src="../../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

{% embed url="https://github.com/appcypher/awesome-wasm-langs" %}

{% hint style="info" %}
Not all langs will be supported by KLY
{% endhint %}

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

<figure><img src="../../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

We compile (with the help of flags **-O3z** we compress as much as possible and carry out optimization)

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

```sh
node test.js 11 33
```

```
11+33=44
```

This was a simple use case and you learned a little more about its format by looking at the code of the <mark style="color:purple;">**.wat**</mark> file.

Of course, it is difficult to write in pure WAT and therefore you will most likely use high-level languages such as AssemblyScript (an add-on on TypeScript), Rust, C ++, Go and others.

Since there are several tools for turning source code into WASM modules, we will try to use the most popular, documented and convenient ones in order to create the best working conditions for users and developers on KLY\


<figure><img src="../../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (5).png" alt=""><figcaption><p><mark style="color:red;"><strong>Build WASM modules with Rust</strong></mark></p></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (6).png" alt=""><figcaption><p><mark style="color:red;"><strong>Ofiicial WASM builder for Go</strong></mark></p></figcaption></figure>

## <mark style="color:red;">Links</mark>

{% embed url="https://wasmbook.com/" %}

{% embed url="https://www.rust-lang.org/fr/what/wasm" %}

{% embed url="https://docs.klyntar.org/smart-contracts/kly-wvm" %}
