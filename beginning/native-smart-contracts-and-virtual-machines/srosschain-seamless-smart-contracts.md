---
description: An important feature of KLYNTAR VM
cover: >-
  https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FphIHWZY173DpNXBbDjVg%2Fuploads%2FbKmFlTTJpfNRamMnbzai%2Fwp7083319.jpg?alt=media&token=8b81194d-abc6-4371-b254-3b1205f8b407
coverY: -191.06127946127947
---

# 🤞 Сrosschain seamless smart contracts

### <mark style="color:red;">Cross-chain smart contracts with KLYNTAR VM</mark>

It would be great to write smart contracts with cross-chain logic. When part of your contract is executed on Polygon, part on KLYNTAR and one more on conditional Litecoin (yes, yes, we will make it possible to use even chains without smart contracts).

Since KLYNTAR nodes in the framework of _<mark style="color:yellow;">**symbiote-hostchain**</mark>_ interactions somehow interact with hostchains, this connection could be used to perform cross-chain logic. In addition, nodes that work on a certain symbiote probably have nodes or at least APIs for working with host chains, which means that it will not be difficult to use them for smart contracts.

### <mark style="color:red;">Another reference to the flexibility of the symbiotic structure</mark>

Each symbiote will provide its own access to different networks. That is why, when choosing, you should check whether the symbiote supports the networks you need. The operators of the nodes of a certain symbiote themselves are allowed to choose the balance between the number of hostchains, their set, etc.

If one symbiote provides an API to work on less popular host chains than another, then the income of the nodes on this may be less and the symbiote will lose validators and nodes. Similarly, in the other direction - if the symbiote is too "expensive" to launch, then people will leave from here. And although this is not particularly critical due to [_<mark style="color:purple;">**Mutualism**</mark>_](../releases/mutualism.md), it is still recommended to maintain a balance.

### <mark style="color:red;">**Example**</mark>

Let's assume that you want to write an on-chain cross-chain smart contract on KLYNTAR between the networks that were already in the example - Polygon (EVM logic), KLYNTAR (main logic and cross-chain communication) and Litecoin.

Let our application be something like an exchanger with additional logic (not just the exchange of tokens, but also the performance of some functions). Users can contribute tokens and coins to the Polygon contract and at the same time send coins to the corresponding addresses on Litecoin for certain smart contract operations (both Polygon and KLYNTAR). As part of our imaginary contract, we will write an extremely simple application, something like HelloWorld, but with the theme described above. Let's have this functionality:

<mark style="color:orange;">**Polygon**</mark>

We'll define 2 functions on Polygon contract

```solidity
function spendTokens(uint256 amount, address destination,string memory extradata) public;

function getData(address actor) public view returns(string memory);
```

* _<mark style="color:purple;">**spendTokens**</mark>_\
  \
  A function that will be called from the outside (that is, direction **=> **<mark style="color:purple;">**Polygon**</mark>) and which, based on incoming data, allows the user to do something with tokens\

* _<mark style="color:purple;">**getDatа**</mark>_\
  \
  Returns some data about the address required for a smart contract on KLYNTAR

<mark style="color:orange;">**KLYNTAR**</mark>

{% hint style="info" %}
We will give an example in AssemblyScript. The syntax is similar to TypeScript, but even if you are not familiar with it, it should generally be simple and clear. We will also provide other examples in the future.
{% endhint %}

At KLYNTAR's WASM contract, the following functions will be defined:

```typescript
export function performLitecoinPolygonLogic(sender: string, data: string ): boolean;

export function performPolygonLitecoinLogic(sender: string, data: string ): boolean;
```

* _<mark style="color:purple;">**performLitecoinPolygonLogic**</mark>_\
  \
  A function that receives as input the address of the caller and data by API calling data from Litecoin. Returns the result of the operation\

* _<mark style="color:purple;">**performPolygonLitecoinLogic**</mark>_\
  \
  Here, in a similar way, but only before this function, KLYNTAR receives data from Polygon (by calling getData from the Polygon contract that we described above) and only then this function is called

<mark style="color:orange;">**Litecoin**</mark>

This is more interesting, because Litecoin, being a fork of Bitcoin, does not have traditional smart contracts in Turing complete language and operates only with primitive opcodes. But we don't need more from him.

For such languages, KLYNTAR will provide special APIs, so that when writing your smart contracts, you will use them.

There is no problem in this, because if there is no possibility of executing smart contracts, then all the possibilities of cryptocurrency come down to simple transactions. This means that all that can be squeezed out of such a cryptocurrency is standard calls like _<mark style="color:orange;">**getTransaction(txID)**</mark>_, _<mark style="color:orange;">**getInputs(address)**</mark>_ (if we are talking about cryptocurrencies with UTXO type) and so on.

The good news is that you can create a very large set of such functions with very different functionality - somewhere you can get a clean array of transaction outputs, check if it was a TAPROOT transaction, filter and get only the transaction time, and much more.

Now let's talk more about execution.

### <mark style="color:yellow;">Step one - write a smart contract on Polygon and deploy it to the network</mark>

The first thing you do is write the contract logic for Polygon. We have described the necessary functions and their signatures above, the functionality is omitted for simplicity. Then you get the bytecode and ABI you need to work with the contract. You deploy the contract to Polygon and store the ABI.

{% hint style="info" %}
Also, do not forget about open source code if your project requires it.
{% endhint %}

### <mark style="color:yellow;">Step two - write a smart contract on KLYNTAR and deploy it to the network</mark>

Similarly, you are writing a part to work with KLYNTAR. In the example above, we used AssemblyScript. Function signatures and the general principle of operation should be clear. You compile the contract to .wasm and get ready for step 3.

### <mark style="color:yellow;">Step Three - Binding</mark>

At this stage you have

* Contract on Polygon
* Its ABI(you must have it locally)
* Written contract for KLYNTAR and its .wasm bytecode

Now we need to connect everything so that everything works. To do this, before deploying everything to the KLYNTAR network, you will need to create something like a call map, thanks to which everything will work as a single organism.

KLYNTAR nodes just need to know that if a call comes in for some contract X, then you just need to open its call map and see what to do next. For our application with you, such a call map may look like this

```json
{
    "performLitecoinPolygonLogic":[
        {   "type":"Litecoin",
            "func":"getTransaction",
            "params":["txid","address"]
        }
    ],
    
    "performPolygonLitecoinLogic":[
        {
            "type":"EVM",
            "func":"getData",
            "params":["sender"],
        }    
    ]
}
```

A call map is essentially a JSON object whose properties define the names of the KLYNTAR smart contract functions. The values of these properties are arrays that contain objects that describe the required function call BEFORE this one. After the array ends, this function is called with the parameters that were obtained as a result of calling the last subfunction in this chain.

In general, the call map may look something like this.

```json
{
    "KLYNTAR_CONTRACT_FUNCTON_1":[
        {   "type":"SomeCrypto",
            "func":"Contract function or API function by KLYNTAR",
            "params":["param1","param2","param3",...]
        }
    ],
    
    "KLYNTAR_CONTRACT_FUNCTON_2":[
        {   "type":"AnotherCrypto",
            "func":"Contract function or API function by KLYNTAR",
            "params":["param1"]
        },
        {
           "type":"SomeEVMCrypto",
            "func":"letsTest",
            "params":["hello","world"]
        }
    ],
    
    "KLYNTAR_CONTRACT_FUNCTON_3":[
        {   "type":"SomeCrypto",
            "func":"Contract function or API function by KLYNTAR",
            "params":[]//no params
        }
    ],

}
```

For functions that will not require interaction with other networks, it is not necessary to create and add to the call map.

### <mark style="color:yellow;">Back to our application</mark>

So, after you have a call map, you start deploying to KLYNTAR. You need to send

* ABI for Polygon contract
* .wasm KLYNTAR contract module
* Call map

All this will be saved under the BLAKE3 function identifier and you can start interacting with the contract. Let me remind you that our map looks like this

```json
{
    "performLitecoinPolygonLogic":[
        {   "type":"Litecoin",
            "func":"getTransaction",
            "params":["txid","address"]
        }
    ],
    
    "performPolygonLitecoinLogic":[
        {
            "type":"EVM",
            "func":"getData",
            "params":["sender"],
        }    
    ]
}
```

Suppose that within the framework of the logic it was set so that some transaction should take place on Litecoin and after that you can run the code on KLYNTAR. Conditional sender generates an event on KLYNTAR

{% hint style="info" %}
Pseudocode will be shown below. The actual data format may differ from what is presented here.
{% endhint %}

```json
{
    "version":"1.33.7"
    "sender":"GVaWomidXy6TVXegvezhvL45psyod6X5TqMk7GVm13rE",
    "event":"CONTRACT_CALL",
    "payload":{
        "id":"<SOME BLAKE3 HASH - ID OF CONTRACT>"
        "func":"performLitecoinPolygonLogic",
        "params":["aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa","LRAUdHk9qT4xA7fh49b3Y4DzddFWTLApaX"]
    },
    "fee":13.37,
    "nonce":1337,
    "signa":"pL0B3548WN/SRr1X8VSBd5wuAfcoBW4BfB1JKBaSV4polHfyBl/hojif3LQkU3CYkbKFHFiiT7UM+z1bQV0sDA=="
}
```

This is sent to the KLYNTAR network on the appropriate symbiote and further execution takes place.

Having received this, the nodes (or the primary validator that will execute this) take the contract ID and retrieve the call map from the store.

Since the performLitecoinPolygonLogic function is there, the following happens:

Having such a pipeline for this function

```json
 "performLitecoinPolygonLogic":[
        {   "type":"Litecoin",
            "func":"getTransaction",
            "params":["txid","address"]
        }
    ],
```

The node understands that we are talking about the Litecoin API and, based on the received parameters, calls the _<mark style="color:orange;">**getTransaction**</mark>_ function, passing there the array received from the KLYNTAR contract call

```
["aaaaaaa...","LRAUdHk9qT4xA7fh49b3Y4DzddFWTLApaX"]
```

After that, suppose that the function returned the transaction to us in hex form

```
aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
```

Then we look at the call map

```json
"performLitecoinPolygonLogic":[
        {   "type":"Litecoin",
            "func":"getTransaction",
            "params":["txid","address"]
        }
    ]
```

Since there is nothing else here, now we call the _<mark style="color:red;">**performLitecoinPolygonLogic**</mark>_ function itself

Recall that its signature is

```typescript
export function performLitecoinPolygonLogic(sender: string, data: string ): boolean;
```

Since at the last step we received the transaction in hex form, it is passed to this function as a parameter. Now we call

```javascript
performLitecoinPolygonLogic(
    "GVaWomidXy6TVXegvezhvL45psyod6X5TqMk7GVm13rE",
    "aaaaaa..."
)
```

Вот собственно и всё. Хоть мы и не затестили функцию для работы с Polygon, но в целом принцип такой же. Так же можно и усложнять и проводить более сложные операции.

### <mark style="color:red;">What else can be added</mark>

The possibilities here are endless - it will be possible to build various kinds of adapters for data, set up your own commission policy, include many circuits in 1 call to the KLYNTAR contract, KLYNTAR nodes will be able not only to receive data and check, but also, if there is, for example, a balance on Polygon, conduct "paid" calls and so on. We will keep you updated on our developments and progress. Submit your ideas and help solve problems :thumbsup:

### <mark style="color:red;">Prospects</mark>

Thanks to the symbiotic structure and the default sharding principle, KLYNTAR allows you to choose the symbiotes you need. Thanks to the release of Mutualism, you will be able to pay the nodes of other symbiotes, if necessary, so that they also check your contracts. You will be able to manually assign only select validators who will be allowed to fulfill your contracts, and due to the fact that KLYNTAR will be very social (this can be understood from the links even at the node configuration level where you can share your site, mail or a way to contact you) you will be able to easily untie the tasks you need.

Now your tokens will rely on the security of KLYNTAR - which means the security of the entire industry, your users will have access to advanced cryptography, will use the maximum speeds of the entire industry thanks to SpookyAction, phantom blocks, total asynchrony and more.

Follow KLYNTAR and, if it's not difficult for you, help us by sending a donation to our [_<mark style="color:purple;">**addresses**</mark>_](../social-media.md)_<mark style="color:purple;">****</mark>_
