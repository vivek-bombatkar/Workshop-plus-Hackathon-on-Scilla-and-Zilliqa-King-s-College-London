
# Zilliqa Blockchain Workshop & Hackathon for Developers, King's College London
This repositry is my collection of notes and realted documents for the workshop and hackathon by Zilliqa.   

> Follow me on,  [LinkedIn](https://www.linkedin.com/in/vivek-bombatkar/), [Github](https://github.com/vivek-bombatkar)  

-  Zilliqa - the scalable and secure blockchain platform for hosting decentralized applications.  
-  SCILLA  - Safe-By-Design intermediate-level smart contract language being developed for Zilliqa.  


## Hack topic - Blockchain-backed analytics : Adding blockchain-based quality gates to data science projects
[Link to the paper](https://github.com/vivek-bombatkar/Workshop-plus-Hackathon-on-Scilla-and-Zilliqa-King-s-College-London/blob/master/8292.pdf)  
> this paper was presented in 2nd International Conference on Advanced Research Methods and Analytics (CARMA2018)  

- We will be done using one 'smart contracts'
- this smart contract will maintain the 'map' of transitions againt the owner and account 
- with 2 transitions
- One is 'setTransitions'
    - this will be implementing 'mpa' internally 
    - 2 parames in K,V format.
    - K : timestamp
    - V : JSON containing data file or model code  
- Second is 'validateTransitions' 
    - to validate the transaction by checking it against map  
- Code for smart contracts : FIXME
```

import ListUtils

(***************************************************)
(*               Associated library                *)
(***************************************************)
library BlockchainBackedAnalytics


let one_msg = 
  fun (msg : Message) => 
  let nil_msg = Nil {Message} in
  Cons {Message} msg nil_msg

let not_owner_code = Int32 1
let set_hello_code = Int32 2

(***************************************************)
(*             The contract definition             *)
(***************************************************)

contract BlockchainBackedAnalytics
(owner: ByStr20)

field welcome_msg : String = ""
field id : Uint128 = Uint128 0
field id_map : Map ByStr20 Uint128 = Emp ByStr20 Uint128

(*chek tx# present in blockchain*)
transition setTransitions (msg : String)
  one = Uint128 1;
  tmp <- id;
  res = builtin add tmp one;
  id := res;
  is_owner = builtin eq owner _sender;
  match is_owner with
  | False =>
    msg = {_tag : "Main"; _recipient : _sender; _amount : Uint128 0; code : not_owner_code};
    msgs = one_msg msg;
    send msgs
  | True =>
    tmp1 <- id_map;
    tmp2 = builtin id_map 
    welcome_msg := msg;
    msg = {_tag : "Main"; _recipient : _sender; _amount : Uint128 0; txid : res};
    msgs = one_msg msg;
    send msgs
  end
end

(*chek tx# present in blockchain*)
transition setTransitions (msg : String)

end
```


## Hands on smart contract
- IDE
    > [1. ide for Zilliqa writing smart contracts ](https://ide.zilliqa.com/)  
    > [2. souped-up IDE for testing Scilla smart contracts](https://savant-ide.zilliqa.com/)  

- Other Links
    > https://github.com/Zilliqa/Zilliqa  
    > https://wallet.zilliqa.com/home
    > https://scilla-lang.org/
    > https://zilliqa.com/  
    > https://explorer.zilliqa.com/home  
    > https://github.com/Zilliqa/scilla-docs/blob/master/docs/source/scilla-by-example.rst  
    > https://github.com/Zilliqa/savant-ide  
    > 

- Zilliqa capable of processing thousands of transactions per second with ***sharding*** built into it.   
- ***Sharding*** 
    - > https://medium.com/@giottodf/zilliqa-a-novel-approach-to-sharding-d79249347a1f  
    - > https://blog.zilliqa.com/https-blog-zilliqa-com-the-zilliqa-design-story-piece-by-piece-part1-d9cb32ea1e65  

    - sharding is a mandatory approach for scalability of blockchains which want to be more than just settlement layers.  
    - is a mechanism that allows the Zilliqa network to be divided into smaller groups of nodes each referred to as a shard. 
    - Simply put, imagine a network of 1,000 nodes, then, one may divide the network into 10 shards each composed of 100 nodes.  

- Zilliqa has the potential to match throughput benchmarks set by traditional payment methods (such as VISA and MasterCard). More importantly, Zilliqa’s transaction throughput increases (roughly) linearly with its network size.  

- High throughput- you can focus on developing your ideas without worrying about network congestion, high transaction fees or security which are the key issues with legacy blockchain platforms.

- The approach that Zilliqa has chosen with sharding is that every single node will have a copy of the current state (the bank balances in our example) but then the transactions history will be split in pieces so that not everyone will have to have a full copy of it.


## run your contract on IDE  
> https://savant-ide.zilliqa.com/  
- ***Development cycle***  : wtrite > save > Check > Deploy > Call
    - write : writre scilla code  
    - save : save file as .scilla  
    - chcek : click 'check' to syntaxt checking  
    - depoloy :     
       - deploy to the blockchain
       - select account
       - selct contract (.scilla file)
       - ammount / gas  / gas price could be untouch 
       - fill the params needed for contract, like account # etc. This could change based on what param you have define  
       ```
       Your contract was successfully deployed to 0xC900AE444C600557BC8CF483D4B974581D3188C3
        Gas used: 53
        Gas price: 1
        Transaction cost: 53 ZIL
        ```
     - Call
        - select account #
        - select contract 

> https://github.com/Zilliqa/scilla-docs/blob/master/docs/source/scilla-by-example.rst  

- ***contract may looks like this***
```
import abcUtils

library libName
let varName

contract contractName

field fieldName # mutable veriable 

transition transition_1_Name (field1 : String)
end

transition transition_2_Name ()
end

```

- ***HelloWorld.scilla  
```
(* HelloWorld contract *)

import ListUtils

(***************************************************)
(*               Associated library                *)
(***************************************************)
library HelloWorld

let one_msg = 
  fun (msg : Message) => 
  let nil_msg = Nil {Message} in
  Cons {Message} msg nil_msg

let not_owner_code = Int32 1
let set_hello_code = Int32 2

(***************************************************)
(*             The contract definition             *)
(***************************************************)

contract HelloWorld
(owner: ByStr20)

field welcome_msg : String = ""

transition setHello (msg : String)
  is_owner = builtin eq owner _sender;
  match is_owner with
  | False =>
    msg = {_tag : "Main"; _recipient : _sender; _amount : Uint128 0; code : not_owner_code};
    msgs = one_msg msg;
    send msgs
  | True =>
    welcome_msg := msg;
    msg = {_tag : "Main"; _recipient : _sender; _amount : Uint128 0; code : set_hello_code};
    msgs = one_msg msg;
    send msgs
  end
end


transition getHello ()
    r <- welcome_msg;
    e = { _eventname : "SedingHello"; caller : _sender; msg : r };
    event e
end

```


- mutable variable welcome_msg  
- immutable variable owner  
- interface getHello  
- Libraries : A Scilla contract may come with some helper libraries that declare purely functional (with no state manipulation) components of a contract
- only owner of the contract can call the contract with below check
```   is_owner = builtin eq owner _sender; ```  
- library HelloWorld "FIXME" 
```
library asdasdasd
>>> Type-checking failed. 
```


## key words

- ***Nonce***
    - increment every time   
    - used for solving 'double spending' by sequencing the calls     
    
- ***Message vs Event***  
> Message
1. internal between nodes
2. Messages could be seen in "STATE" tab, under individual 'Contract State' > messageLog section   
```
    r <- welcome_msg;
    e = { _eventname : "SedingHello"; caller : _sender; msg : r };
    event e
```

> Events
1. to the external world  
2. Seen in the "Event" section as list of events / email , having contract deployment address mention in them  
```    
r <- welcome_msg;
e = { _eventname : "SedingHello"; caller : _sender; msg : r };
event e 
``` 
    



