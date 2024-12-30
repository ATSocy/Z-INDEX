Thread: how-does-zenon-network-interoperate-with-bitcoin
0x3639 | 2024-03-27 15:20:16 UTC | #1

According to a recent Telegram conversation with Mr. Kaine:

"Interoperability with Bitcoin can go beyond value transfer."

"off-chain payment networks like Lightning Network work by operating with locked btc with final settlement happening on-chain.  They "wrap" btc by locking it in a payment channel, thus avoiding on-chian fees.  Pillars can act as TSS signers and hold native btc vaults"

Mr. Kaine goes on to say Bitcoin and the Network of Momentum (NoM) might be able to share resources. NoM generates Proof of Work links to create Plasma used in transactions which might be usable to merge mine with Bitcoin.  And the opposite could be true to.  Bitcoin could merge mine ZNN to create plasma for Bitcoin feeless transactions. 

![FO7ihP6WQA0mG2Q|506x413](upload://qWXdN6GO26Cd4QaWPGD81u8Qzkr.png)

And for those more technically savvy, here are excepts from @georgezgeorgez sharing knowledge on Telegram with the community on how Bitcoin could interoperate with Zenon Network.  These are exact quotes from the chat.  The original chat can be found here: https://t.me/zenonnetwork/235674 
- - 
“Thinking about how atomic swaps would work.  We don’t have outputs. We have balances. Would we need to make an HTLC contract?  Send tokens to the contract address, and specify

1. An address which can unlock
2. A timelock
3. The hash
4. (Maybe a hash type?)
- - 
In order to withdraw the funds, the specified unlock address needs to sign a tx sending the right data to unlock the hash lock to the contract address. Otherwise, once the timelock is expired, the original address can get the funds back from the timelock.
- - 
Trustless swaps between two assets. Can be across two different chains as well
- -
You could maybe use an entire account chain as an output. But our signature verification is relatively straightforward right now. Is it better to keep account chain verification logic simple. While moving complexity into the contracts?
- - 
I think no matter what, we will want multisig account chains? I need to do a lot more reading. Looking at scriptless scripts which mr kaine linked saying htlc not needed
- - 
For scriptless sigs first funding multisig outputs, isn’t a timelocked exit still needed?
- -
So it goes back to the question of… Should timelock functionality be implemented at the account chain level? Or at a contract level with entries like the rest of our lockups A contract would be more consistent. It would also decouple multisig implementation from atomic swaps
- - 
I need to see what these scriptless script adapter functions look like
- - 
Regretting years of slacking off lmao now that I actually give a shit about something
- - 
(MT Responds) Timelock functionality is already there - staking is one example of timelocked ZNN
- - 
Yup I was thinking a similar contract could be used with slightly different logic for withdrawal
- - 
(Mr. Kaine Responds) Yes. And the hash lock is pretty easy to add. And you can do even better: use precompiled contracts like EVM for near instant execution time.
- - 
https://www.evm.codes/precompiled
https://www.bitcoininsider.org/article/154490/customizing-evm-stateful-precompiles

Yup. When you send funds to the staking address. It triggers computation as defined in go-zenon code. As opposed to code someone else uploaded and stored in the network, the code is in the znnd binary itself
- - 
So it seems like we could define a pre compiles interface as well. Instead of RequiredGas, RequiredPlasma instead
- -
(B_Zed Responds) **Makes sense, imo this would be the ideal way to interact with bitcoin**
- - 
Still need a coherent plasma pricing strategy. If we did implement a wasm runtime,  would it be able to use pre compiled.  If it was in the same language
- - 
“WASM eliminates Ethereum’s reliance on precompiled contracts.”
https://hackernoon.com/the-virtual-machines-wars-wasm-vs-evm

https://www.secondstate.io/articles/extend-webassembly/
 
https://webassembly.org/docs/non-web/ 
- - 
One criticism of atomic swaps is the free call option. What if instead specifying an address that can withdraw. The contract mints an nft when you deposit. In addition to the time lock, any user can send the contract the nft (burn) in addition to the hashed data to withdraw.
- - 
So we’ve tokenized the option. The nft can be traded like anything else. So you can actually collect a premium for the option.
- - 
Hmmm but then there’s the question of how do you sell the nft lol. If you want to give the free option, you can just send it. If you want to charge a premium for it? Would it make sense to do an atomic swap for it (without the nft of course). Idk if it would make sense. Need to spend more time on it
- - 
https://eprint.iacr.org/2019/896.pdf

If the NFT is atomic swapped with the roles reversed, is that then fair?  The amounts locked for the nft swap would be much smaller
- - 
(B_Zed Responds) Nft > call option premium. Maybe I'm way off but the nft could be it's own market in some sense
- - 
Yeah you could have a derivatives market
- - 
Swaps on the same chain can be done directly through contracts
- - 
If both are zts. Then you can just have vending machine contracts
- - 
Taproot allows for practical large multisig. Meaning you could have validators be the wrappers
- - 
I don’t mean individual wrappers. The wrappers as a set. The wrapped BTC would be as decentralized as Zenon itself.
- - 
(Fxteam Responds) So once btc is wrappped in this way its trustless and also free to send.
- - 
Yup yup
- - 
(Fxteam Responds) Programable money
- - 
The challenge is what happens when you get new pillars. Or some deconstruct. You need to adjust the signatory set. Meaning an on-chain BTC tx. Meaning fees.  This could be dynamic. And not a fixed percentage
- - 
Maybe a portion of orbital can be used for the fees. Pillars buy zbtc and burn it
- - 
Meaning the BTC is over collateralized
- -

-------------------------

crypto_iverson | 2022-04-20 22:57:23 UTC | #2

great summary zer 

project has evolved over time, and currently there is no interop w/ btc but there are ideas, and devs like to keep cards close to the vest

for many, znn is an upside bet on eventual interop w/ btc so that you can have defi on top of btc.. kaine presents some great possibilities for how to get there w/ things like merge mining

-------------------------

