Thread: draft-bitcoin-scaling-on-nom-notes-for-discussion
0x3639 | 2024-03-17 16:39:52 UTC | #1

Over the past few days some community members have been engaged in a discussion about how Bitcoin and NoM will interact. Can the community reverse engineer a potential design that is directionally accurate? This post will explore that topic.  

But before we get started, let's review some background before diving in.

## Background
- **March 2019:** Zenon Network was launch with xStakes, an innovative funding mechanism that required a Bitcoin deposit.  Early investors speculated [xStakes included a novel "smart contract"](https://medium.com/@shaimo/the-zenon-enigma-782f8b293bd6) between Bitcoin and NoM.
- **November 12, 2021:** @georgezgeorgez wrote an article explaining the [limitations of Lightning Network](https://medium.com/@georgezgeorgez/a-message-to-humans-an-aliens-guide-to-lightning-network-watchtower-limitations-and-beyond-96138967fa9b) and proposed a new design that could overcome the shortcomings. 
- **November 15, 2021:** Taproot was activated and @zenon_network tweeted ["Never doubt you can make history. You already have"](https://twitter.com/Zenon_Network/status/1460240120309760010?t=k58m11sk6kqykJKh1dbaLQ)
- **March 22, 2023:** Mr. Kaine told George to [check out xClaim:](https://t.me/zenonnetwork/274875).  Here is the [xClaim whitepaper](https://eprint.iacr.org/2018/643.pdf).
- **Dec 2023:** @Nostromo started to question the [purpose of Sentinels and Sentries](https://forum.hypercore.one/t/network-of-momentum-phase-1/253/11?u=0x3639) after several posts by @aliencoder about the potential use of Sentinels and Public Nodes.  
- **March 2024:** Quantum PP in Telegram started to ask [questions about Sentinels](https://t.me/zenonnetwork/354359) and discuss how NoM might interact with the Bitcoin Network. qPP also pointed out three interesting graphics in the [Zenon Network marketing video](https://www.youtube.com/watch?v=UqAequz4mgk) and in the [Zenon.network](https://zenon.network) website. The first image appears to be a black hole sucking in Bitcoin.  The second image references a cross-chain presence with Orbital Liquidity Staking.  And the third image highlights the goal to interoperate with Bitcoin while tapping into its security and decentralization.    
![Screenshot 2024-03-16 at 5.45.14 PM|690x313](upload://8LNDeKSx9kZj8DRyzshwKEac1CZ.jpeg)
![Screenshot 2024-03-16 at 5.44.22 PM|381x500](upload://pDXT8jA7ADZMqXJBApOr5GHXt0d.jpeg)
![Screenshot 2024-03-16 at 5.56.28 PM|690x293](upload://lQxu5MViExBZQIEPjLZVvQCY0Mz.jpeg)


## ChatGPT Bitcoin Interoperability Network Design

WARNING:  This design is speculation and not endorsed by any developer.  These are notes and ideas for further discussion and criticism.  These ideas were developed by chatGPT and directed with training data from xClaim, Zenon Network, Lightning Network, Schnorr Multi-Signatures, Taproot and community ideas from Telegram.  

---

Designing a system that leverages Bitcoin's Taproot, xClaim, and Schnorr Multi-Signatures to put Bitcoin into a "vault" within the Bitcoin network involves a blend of these technologies to create a secure and flexible structure. The system would utilize designated vaults on the Bitcoin network, where only Sentinels have the authorization to interact with the deposits. Here's an outline of how such a system could be designed, based on the information provided and the underlying principles of the technologies mentioned:

### Taproot and Schnorr Multi-Signatures

Taproot, introduced in BIP 341, enhances Bitcoin by enabling more privacy and efficiency in transactions. It allows for the combination of the Pay-to-PubKey (P2PK) and Pay-to-Script-Hash (P2SH) spending conditions into a single new output type that is indistinguishable from others. Taproot takes advantage of Schnorr signatures, which allow for key aggregation - multiple public keys can be aggregated into a single one, requiring cooperation from all participants to sign for it .

### xClaim Framework

xClaim represents a framework for cross-chain claims, allowing assets to be represented and moved between different blockchains. In the context of creating vaults on the Bitcoin network, the xClaim framework could facilitate the representation of Bitcoin in these vaults, enabling assets to be locked in a Bitcoin transaction and then used within the Zenon Network or another chain.

### System Design

1. **Vault Creation**: Utilize Taproot to create a vault, which is essentially a Bitcoin address that allows for flexible control over the funds through Schnorr signatures and MAST. The vault would be controlled by a script that includes conditions for depositing and withdrawing Bitcoin. The script is only revealed when the conditions are met, enhancing privacy.

2. **Sentinel Authorization**: Sentinels are special entities with the authority to approve transactions related to the vault. Their public keys are aggregated using Schnorr's key aggregation feature, creating a single public key that represents the combined authority of the Sentinels. This aggregated key is used in the Taproot script for the vault, ensuring that only transactions approved by the Sentinels can spend the vault's funds.

3. **Deposits and Withdrawals**: To deposit Bitcoin into the vault, a user sends BTC to the vault's address. The transaction would be structured to allow the Sentinels to execute a withdrawal based on predefined conditions, possibly involving interaction with the Zenon Network or another blockchain for cross-chain operations.

4. **Cross-Chain Representation with xClaim**: When Bitcoin is deposited into the vault, a corresponding representation of the BTC can be issued on the Zenon Network (or another chain), using the xClaim protocol. This process involves locking the Bitcoin in the vault and minting an equivalent amount of tokenized Bitcoin on the Zenon Network.

5. **Security Measures**: To ensure security, the system can incorporate measures such as time-locks and hash-locks. Time-locks prevent funds from being prematurely withdrawn, giving enough time for any disputes to be resolved. Hash-locks can be used in cross-chain operations to ensure that actions on one chain (e.g., releasing the tokenized Bitcoin) are conditional upon actions on another chain (e.g., locking the actual Bitcoin in the vault).

This system leverages the security and flexibility of Bitcoin's Taproot and Schnorr signatures to create secure vaults controlled by designated entities (Sentinels). By integrating with xClaim, it enables a seamless and secure cross-chain representation of Bitcoin, facilitating new use cases and interoperability between Bitcoin and other blockchains.

---

## Q&A with ChatGPT on the proposed design

Given the system design above, I asked ChatGPT if the vault design would allow Alice to deposit 1 BTC into the vault, receive 1 xBTC on NoM, transfer 0.5 xBTC to Bob, and allow Bob to withdraw 0.5 BTC from the vault.  Here is the response.

---

Yes, with the proposed system design, it is possible for Alice to deposit 1 BTC into the vault, receive 1 xBTC on the Zenon Network (or any other blockchain integrated with this system), send 0.5 xBTC to Bob on that network, and then allow Bob to withdraw his 0.5 xBTC back to native Bitcoin without impacting the remaining 0.5 BTC Alice owns in the vault. Here's how this could be achieved:

1. **Initial Deposit**: Alice deposits 1 BTC into the Bitcoin vault designed with Taproot and controlled by Sentinels. This action triggers the creation of 1 xBTC in the Zenon Network, representing Alice's 1 BTC deposit.

2. **Alice Sends xBTC to Bob**: Alice then sends 0.5 xBTC to Bob within the Zenon Network. This transaction is recorded on the Zenon Network, and Alice's balance is updated to reflect that she now owns 0.5 xBTC.

3. **Bob's Withdrawal to Native Bitcoin**:
    - Bob decides to withdraw his 0.5 xBTC to native Bitcoin. To facilitate this, the system checks the equivalent value in the Bitcoin vault.
    - The Sentinels, leveraging the xClaim protocol, verify Bob's ownership of 0.5 xBTC on the Zenon Network. They then authorize a withdrawal from the vault corresponding to Bob's 0.5 xBTC.
    - A transaction is prepared, signed by the Sentinels (using their aggregated Schnorr signature), and broadcasted to the Bitcoin network. This transaction sends 0.5 BTC from the vault to Bob's specified Bitcoin address.
    - To ensure that Alice's remaining 0.5 BTC in the vault is not affected, the system updates the records on both the Bitcoin and Zenon Networks. This update reflects that 0.5 BTC has been withdrawn from the vault, and Alice still owns the remaining 0.5 xBTC on the Zenon Network.

4. **Ensuring Isolation of Withdrawals**: The crucial part of this system is the ability to track and verify individual ownership and transactions of xBTC on the Zenon Network. By keeping detailed records and using cryptographic proofs, the system ensures that withdrawals only impact the specific portion of the BTC in the vault corresponding to the xBTC being redeemed. 

5. **Final State**:
    - Alice retains ownership of 0.5 xBTC on the Zenon Network, which is securely backed by 0.5 BTC in the vault.
    - Bob receives 0.5 BTC in his native Bitcoin address, completing the withdrawal process.

This process involves intricate coordination between the Bitcoin vault, the Zenon Network, and the Sentinels to ensure that transactions and withdrawals are securely and accurately processed. It showcases the potential for interoperable blockchain solutions, allowing for seamless asset transfers and withdrawals across different blockchains while maintaining the integrity and security of the underlying assets.

---

## Discussion

I think there are a number of issues with this design.  This implementation feels more like wrapped Bitcoin controlled by decentralized  actors.  In the lightning network either party in a liquidity channel can force a channel to close leaving them in "control" of the Bitcoin.  However, the parties likely need to rely on watchtowers, centralized entities in many cases, to prevent fraud after channels are closed.  

On a positive note, according to ChatGPT, the vault is fungible.  Alice can deposit 1 BTC into the vault and Bob can remove his 0.5 BTC share after receiving that amount in xBTC. 

Unfortunately, the system does not address how to handle adding and subtracting sentinels from the network.  I asked ChatGPT how we can create a dynamic threshold signature scheme with hundreds of Sentinels that are constantly changing.  It proposed the following design which seems inflexible and impractical.   

### 1. **Establishing the Initial Threshold Scheme**

- **Key Generation Ceremony**: Initially, all Sentinels participate in a distributed key generation protocol. This process results in each Sentinel possessing a unique secret share and all Sentinels collectively sharing a public key that represents the entire group. This public key can be used to verify signatures generated by any subset of Sentinels meeting the threshold.

- **Threshold Setting**: The threshold is set at 66%, meaning that any transaction or action requires signatures from at least 66% of the current Sentinels to be considered valid.

### 2. **Adapting to Changes in Sentinel Membership**

- **Joining Sentinels**: When new Sentinels are added, a rekeying process is initiated. This can be achieved through a distributed key generation protocol that includes the new Sentinels. The existing Sentinels and the new ones collaboratively generate new shares and a new aggregated public key, adjusting the threshold accordingly.

- **Leaving Sentinels**: When Sentinels leave or are removed, a similar rekeying process is necessary. The remaining Sentinels engage in a protocol to redistribute secret shares and generate a new public key that reflects the current set of Sentinels, ensuring the threshold is maintained.

### 3. **Ensuring Security and Efficiency**

- **Secure Key Management**: Each Sentinel must securely manage their secret share. Loss or compromise of secret shares can pose security risks. Advanced cryptographic techniques, secure hardware, or multi-party computation can be employed to safeguard these shares.

- **Efficient Signature Generation and Verification**: Given the potentially large number of Sentinels, it's crucial to employ a threshold signature scheme that supports efficient signing and verification, even as the set of signers changes. Schnorr signatures are beneficial here due to their aggregation properties, but additional research into multi-signature and threshold signature optimizations may be needed.

- **Robust Protocol for Dynamic Changes**: Implementing a protocol that allows for dynamic changes in the Sentinel set requires careful consideration of network consensus, synchronization among Sentinels, and the potential for disputes or misbehavior. Blockchain technology or a distributed ledger could be utilized to transparently and securely manage these dynamics.

### 4. **Practical Considerations**

- **Communication and Coordination**: Effective communication channels and protocols must be established among Sentinels to coordinate the key generation, signing processes, and threshold adjustments. This coordination is critical during dynamic changes to the Sentinel set.

- **Legal and Governance Framework**: Depending on the system's application and jurisdiction, a legal and governance framework may need to be established to define the roles, responsibilities, and procedures for adding or removing Sentinels.

- **Testing and Auditing**: Before deployment, the threshold signature scheme and its dynamic adjustment mechanisms should be thoroughly tested and audited by security experts to identify and mitigate potential vulnerabilities.

Implementing a dynamic threshold signature scheme with hundreds of Sentinels presents complex challenges but is feasible with careful cryptographic design and operational management. It offers a robust and flexible solution for managing permissions and actions in decentralized systems, leveraging the strengths of Schnorr signatures and threshold cryptography.

## Conclusion

If anyone wants to engage with my custom trained chatGPT bot to explore these ideas you can find it here: https://chat.openai.com/g/g-KySzqRGST-btc-scaling-on-nom.  I think we've come up with some interesting concepts with no workable solution.  

Maybe some of these concepts are directionally useful.  It seems like a highly skilled network architect could improve on these ideas to realize some of the goals established in the [Zenon Network website](https://zenon.network):

- "Atomic swaps and the decentralized cross-chain bridge will enable users to access and transfer value in a censorship resistant way, while unlocking new use-cases with enhanced portability."
- "Interoperability with Bitcoin is a core focus to tap into the security and decentralization of the primordial time-chain."

I also think some of the concepts in @georgezgeorgez [article](https://medium.com/@georgezgeorgez/a-message-to-humans-an-aliens-guide-to-lightning-network-watchtower-limitations-and-beyond-96138967fa9b) relating to "flipping the script" make sense but relate more to making improvements to the Lightning Network.  Can these concepts be applied to xBTC on NoM?  I asked ChatGPT this question and it concluded that adding an approval > oracle > consensus layer to xBTC transactions on NoM would not provide additional security and would only slow transactions.  

![Screenshot 2024-03-17 at 5.11.59 AM|690x207](upload://xTRiA9Z0Wv51u15eVODbBHN5iKc.png)

-------------------------

Shazz | 2024-03-25 23:22:54 UTC | #2

This is great!

-------------------------

