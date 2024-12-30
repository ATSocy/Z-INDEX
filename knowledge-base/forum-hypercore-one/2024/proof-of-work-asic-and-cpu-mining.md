Thread: proof-of-work-asic-and-cpu-mining
0x3639 | 2023-09-11 15:12:40 UTC | #1

During our developer call I mentioned PoW and the potential for ASIC mining on NoM.  I got the sense that @MoonBaze had other ideas.  But I'm not 100% sure.  I wanted to make sure my understanding of the potential for PoW on NoM is accurate.

In the future we will have two types of PoW.  One type is related to dynamic plasma and the other is related to Sentinels and PoW links.  

 ### Dynamic Plasma has 2 implementation steps ([source](https://t.me/zenonnetwork/285662)):
1. Order transactions by Plasma amount and remove the cap
2. Switch to CPU friendly PoW (RandomX).  This PoW is handled by the device requesting the TX.  
3. find a way to balance PoW and QSR fusing ([source](https://t.me/zenonnetwork/275773))


### Sentinel PoW Links 
1. "What NoM has and the rest don't is the PoW component - crucial for decentralization and security; and a bonus feature that will balance ASIC and CPU friendly PoW - very important." ([source](https://t.me/zenonnetwork/278356))
2. "Sentinels won't need to compute PoW. Just process and relay information." ([source](https://t.me/zenonnetwork/265294))
3. "What I meant is that Sentinels can outsource the PoW generation to other sources." ([source](https://t.me/zenonnetwork/265526))

Maybe I should stop thinking that Sentinels will perform some PoW.  As Kaine says, they will relay messages with PoW "outsourced" to someone else.  Maybe the Sentinel operator will run their own PoW miners and maybe they will rely on BTC miners to merge mine.  Maybe it's way to early to know too.

-------------------------

