---
description: Some more interesting information about KLYNTAR VM
cover: >-
  https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FphIHWZY173DpNXBbDjVg%2Fuploads%2FW5NkohHP4l8QMUcsdKLt%2F4439981.jpg?alt=media&token=ce1c3747-342d-431d-938d-340f85842c1e
coverY: -243.34439283344392
---

# 💪 Advanced features

### <mark style="color:red;">How KLYNTAR measure the energy to execute smart contracts</mark>

The execution of smart contracts should be controlled - after all, we do not need our processor to burn out and the node to stop. It is necessary to take into account the fact that inside the bytecode an attacker will try to hide an infinite loop or otherwise affect the normal flow of work in some other way.

In addition, it is necessary to control how many resources will be spent during the operation of the node. After all, running a function that simply returns the sum of a + b obviously requires less than a loop with 10,000 iterations.

In KLYNTAR VM, we will use the project from EWASM to measure the performance of smart contracts. Here is their GitHub

![](<../../.gitbook/assets/image (8).png>)

{% embed url="https://github.com/ewasm" %}

We need the _<mark style="color:red;">**wasm-metering**</mark>_ repository which provides a function that needs to be injected into the bytecode to measure its execution

![](<../../.gitbook/assets/image (21) (1).png>)

At the output, we will get a bytecode similar in functionality, but now the execution of operations is controlled and the calculation of the resources expended is underway. Let's do a little research

### <mark style="color:red;">We understand in more detail</mark>

For this, an example is provided in the README of the project:

```javascript
const fs = require('fs')
const metering = require('wasm-metering')

const wasm = fs.readFileSync('fac.wasm')
const meteredWasm = metering.meterWASM(wasm, {
  meterType: 'i32',
  fieldStr:'energyUse'
})

const limit = 90000000
let energyUsed = 0

const mod = WebAssembly.Module(meteredWasm.module)

const instance = WebAssembly.Instance(mod, {
  
    'metering': {

        'energyUse': energy => {
    
            energyUsed += energy
          
            if (energyUsed > limit) throw new Error('No more energy for contract!')
        
        }
          
    }

})

const result = instance.exports.fac(6)
console.log(`Result:${result}, energy used ${energyUsed * 1e-4}`) // Result:720, energy used 0.4177
```

This defines the global variable _<mark style="color:purple;">**energyUsed**</mark>_ and the energy limit. As you can see from these lines, the module takes the bare bytecode and returns the modified bytecode where it injects a function reference from the outside (in this case, the _<mark style="color:purple;">**energyUse**</mark>_ function from the imported _<mark style="color:red;">**metering**</mark>_ object).

If the limit is exceeded, the work stops and we catch exceptions. Although the EWASM documentation describes the principle of operation, we will still not only hear, but also see how it works.

By the way, here is a detailed and good description on GitHub

![](<../../.gitbook/assets/image (22) (1).png>)

{% embed url="https://github.com/ewasm/design/blob/master/metering.md" %}

### <mark style="color:red;">Check the modified WASM module</mark>

After changes are made to our module, let's write this set of bytes to a .wasm file, and then decompile to .wat from where we can look at the insides The original AssemblyScript module. Let's choose something more complex, for example a loop

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
import metering from 'wasm-metering'
import fs from 'fs'

const wasm = fs.readFileSync('test.wasm')

const meteredWasm = metering.meterWASM(wasm,{
    meterType: 'i32',
    fieldStr:'energyUse'
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
import loader from '@assemblyscript/loader'
import metering from 'wasm-metering'
import fs from 'fs'

const wasm = fs.readFileSync('test.wasm')

const meteredWasm = metering.meterWASM(wasm,{
    meterType: 'i32',
    fieldStr:'energyUse'
})

const energyLimit = 2000000
let energyUsed = 0

let wasmMetered = await loader.instantiate(meteredWasm,{
    
    'metering': {

        'energyUse': energy => {
    
            energyUsed += energy
          
            if (energyUsed > limit) throw new Error('No more energy for contract!')
        
        }
          
    }
    
});

const result = wasmMetered.exports.testAdding(8,20);

console.log(`Result:${result}, energy used ${energyUsed * 1e-4}`);
```

```
Result:160, energy used 1.0672000000000001
```

Decompile to .wat format

```
wasm2wat metered.wasm
```

And check the file

```wasm
(module
 (type $i32_=>_none (func (param i32)))
 (type $i32_i32_=>_i32 (func (param i32 i32) (result i32)))
 (import "metering" "energyUse" (func $fimport$0 (param i32)))
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
 (import "metering" "energyUse" (func $fimport$0 (param i32)))
```

Thus, everywhere in the code where this function will be called, we will understand that there is an energy count. So you can see that the function is called when entering the main _<mark style="color:purple;">**testAdding**</mark>_ function, at the beginning of the loop, when returning from the function, and so on.

With the help of these tools you can play and test the mechanics of work yourself

{% hint style="info" %}
Stay tuned to this page so you don't miss anything important
{% endhint %}

### <mark style="color:red;">**Links**</mark>

{% embed url="https://ewasm.readthedocs.io/en/mkdocs/" %}
