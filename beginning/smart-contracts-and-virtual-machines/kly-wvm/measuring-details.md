---
description: Some more interesting information about KLY-WVM
cover: >-
  https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FphIHWZY173DpNXBbDjVg%2Fuploads%2FW5NkohHP4l8QMUcsdKLt%2F4439981.jpg?alt=media&token=ce1c3747-342d-431d-938d-340f85842c1e
coverY: -179.34439283344392
---

# 💪 Measuring details

## <mark style="color:red;">Intro</mark>

The WVM uses a resource called _<mark style="color:red;">**gas**</mark>_. In general, the role of gas in VM - to provide a calculation of the cost of resources spent to perform a smart contract (its functions).

Through the principle of mutation, each symbiote individually assigns itself KLYNTAR VM capabilities and a spreadsheet. You can even make smart contracts run for free, build your own tree of who is allowed to run which smart contract for free, and so on.

## <mark style="color:red;">Measuring table</mark>

Earlier we showed you a simple function in the <mark style="color:purple;">**add.wat**</mark> file and there you could see that WebAssembly uses bytecodes. For the symbiote, it will be possible to configure the virtual machine in such a way as to independently adjust how much power each opcode will consume.

Here is an example **vmGasTable.json**.

```
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

## <mark style="color:red;">How KLYNTAR measure the gas to execute smart contracts</mark>

The execution of smart contracts should be controlled - after all, we do not need our processor to burn out and the node to stop. It is necessary to take into account the fact that inside the bytecode an attacker will try to hide an infinite loop or otherwise affect the normal flow of work in some other way.

In addition, it is necessary to control how many resources will be spent during the operation of the node. After all, running a function that simply returns the sum of a + b obviously requires less than a loop with 10,000 iterations.

In KLY-WVM, we will use the project from EWASM to measure the performance of smart contracts. Here is their GitHub

![](<../../../.gitbook/assets/image (8).png>)

{% embed url="https://github.com/ewasm" %}

We need the _<mark style="color:red;">**wasm-metering**</mark>_ repository which provides a function that needs to be injected into the bytecode to measure its execution

![](<../../../.gitbook/assets/image (21) (1).png>)

At the output, we will get a bytecode similar in functionality, but now the execution of operations is controlled and the calculation of the resources expended is underway. Let's do a little research

## <mark style="color:red;">We understand in more detail</mark>

For this, an example is provided in the README of the project:

```javascript
const fs = require('fs');
const metering = require('wasm-metering');

const wasm = fs.readFileSync('fac.wasm');
const meteredWasm = metering.meterWASM(wasm, {
  meterType: 'i32',
  fieldStr:'energyUse'
});

const limit = 90000000;
let gasBurned = 0;

const mod = WebAssembly.Module(meteredWasm.module);

const instance = WebAssembly.Instance(mod, {
  
    'metering': {

        'burnGas': gasAmount => {
    
            gasBurned += gasAmount;
          
            if (gasBurned > limit) throw new Error('No more gas for contract!');
        
        }
          
    }

});

const result = instance.exports.fac(6);
console.log(`Result:${result}, gas used ${gasUsed * 1e-4}`); // Result:720, gas used 0.4177
```

This defines the global variable _<mark style="color:purple;">**gasBurned**</mark>_ and the gas limit. As you can see from these lines, the module takes the bare bytecode and returns the modified bytecode where it injects a function reference from the outside (in this case, the _<mark style="color:purple;">**gasUse**</mark>_ function from the imported _<mark style="color:red;">**metering**</mark>_ object).

If the limit is exceeded, the work stops and we catch exceptions. Although the EWASM documentation describes the principle of operation, we will still not only hear, but also see how it works.

By the way, here is a detailed and good description on GitHub

![](<../../../.gitbook/assets/image (22) (1).png>)

{% embed url="https://github.com/ewasm/design/blob/master/metering.md" %}

## <mark style="color:red;">Check the modified WASM module</mark>

After changes are made to our module, let's write this set of bytes to a <mark style="color:purple;">**.wasm**</mark> file, and then decompile to <mark style="color:purple;">**.wat**</mark> from where we can look at the insides The original AssemblyScript module. Let's choose something more complex, for example a loop

```javascript
export function testAdding(a: i32, b: i32 ): i32 {

    let sum:i32 = 0;

    for(let i:i32=0;i<a;i++){

        sum+=b

    }

    return sum;
   
}
```

Although it could be done through multiplication, let's do it this way.

Get .wasm code

```
asc test.ts -o test.wasm -O3z
```

Write modified bytecode to file

```javascript
import metering from 'wasm-metering';
import fs from 'fs';

const wasm = fs.readFileSync('test.wasm');

const meteredWasm = metering.meterWASM(wasm,{
    meterType: 'i32',
    fieldStr:'burnGas'
})

fs.writeFileSync('metered.wasm',meteredWasm)

console.log('Default module => ',wasm)
console.log('After injection => ',meteredWasm)
```

We'll get this output

```
Default module =>  <Buffer 00 61 73 6d 01 00 00 00 01 07 01 60 02 7f 7f 01 7f 03 02 01 00 05 03 01 00 00 07 17 02 0a 74 65 73 74 41 64 64 69 6e 67 00 00 06 6d 65 6d 6f 72 79 02 ... 38 more bytes>
After injection =>  <Buffer 00 61 73 6d 01 00 00 00 01 0b 02 60 02 7f 7f 01 7f 60 01 7f 00 02 13 01 08 6d 65 74 65 72 69 6e 67 06 75 73 65 67 61 73 00 01 03 02 01 00 05 03 01 00 ... 83 more bytes>
```

It can be seen that the size has increased and now it will be seen why. First, let's test the work

```javascript
import loader from '@assemblyscript/loader';
import metering from 'wasm-metering';
import fs from 'fs';

const wasm = fs.readFileSync('test.wasm');

const meteredWasm = metering.meterWASM(wasm,{
    meterType: 'i32',
    fieldStr:'burnGas'
});

const gasLimit = 2000000;
let gasBurned = 0;

let wasmMetered = await loader.instantiate(meteredWasm,{
    
    'metering': {

        'burnGas': gasAmount => {
    
            gasBurned += gas;
          
            if (gasBurned > gasLimit) throw new Error('No more gas for contract!')
        
        }
          
    }
    
});

const result = wasmMetered.exports.testAdding(8,20);

console.log(`Result:${result}, gas used ${gasBurned * 1e-4}`);
```

```
Result:160, gas used 1.0672000000000001
```

Decompile to <mark style="color:purple;">**.wat**</mark> format

```
wasm2wat metered.wasm
```

And check the file

```wasm
(module
 (type $i32_=>_none (func (param i32)))
 (type $i32_i32_=>_i32 (func (param i32 i32) (result i32)))
 (import "metering" "burnGas" (func $fimport$0 (param i32)))
 (memory $0 0)
 (export "testAdding" (func $0))
 (export "memory" (memory $0))
 (func $0 (param $0 i32) (param $1 i32) (result i32)
  (local $2 i32)
  (local $3 i32)
  (call $fimport$0
   (i32.const 92)
  )
  (loop $label$1
   (call $fimport$0
    (i32.const 377)
   )
   (if
    (i32.gt_s
     (local.get $0)
     (local.get $2)
    )
    (block
     (call $fimport$0
      (i32.const 872)
     )
     (local.set $3
      (i32.add
       (local.get $1)
       (local.get $3)
      )
     )
     (local.set $2
      (i32.add
       (local.get $2)
       (i32.const 1)
      )
     )
     (br $label$1)
    )
   )
  )
  (call $fimport$0
   (i32.const 211)
  )
  (local.get $3)
 )
)
```

We can see our function for measuring

```wasm
 (import "metering" "burnGas" (func $fimport$0 (param i32)))
```

Thus, everywhere in the code where this function will be called, we will understand that there is an gas count. So you can see that the function is called when entering the main _<mark style="color:purple;">**testAdding**</mark>_ function, at the beginning of the loop, when returning from the function, and so on.

With the help of these tools you can play and test the mechanics of work yourself

{% hint style="info" %}
Stay tuned to this page so you don't miss anything important
{% endhint %}

## <mark style="color:red;">**Links**</mark>

{% embed url="https://ewasm.readthedocs.io/en/mkdocs/" %}
