
# Zilliqa Blockchain Workshop & Hackathon for Developers, King's College London
This repositry is my collection of notes and realted documents for the workshop and hackathon by Zilliqa.  

- 
- Zilliqa - the scalable and secure blockchain platform for hosting decentralized applications.  
- SCILLA  - Safe-By-Design intermediate-level smart contract language being developed for Zilliqa.  

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

