Thread: polkadot-parachain-auction-model
Stark | 2023-10-30 14:12:15 UTC | #1

Reference material fyi:

Link to original: https://www.polkadot.network/features/auctions/

Content:

# Parachain Slot Auctions

Parachains connect to Polkadot by leasing a slot on the Relay Chain for up to 96 weeks at a time, with the option to renew. Parachain slots are assigned by an on-chain auction, with auction winners locking up a bond in DOT for the duration of the lease. Auctions and crowdloans raise the bar for blockchain projects, incentivizing them to demonstrate their technology and gain community support prior to launch.

## How Auctions Work

Bonding

To bid in an auction, parachain teams agree to lock up (or bond) a portion of DOT tokens for the duration of the lease. While bonded for a lease, the DOT cannot be used for other activities like staking or transfers.

Auction Cost

After the lease, the full amount of DOT is unlocked, meaning auctions do not require teams to “spend” DOT. The cost of the lease is best characterized as the opportunity cost of not being able to use the bonded DOT for other activities.

Crowdloans

Some parachain teams will fund their auction bid with the help of a crowdloan campaign, which allows them to accept contributions from DOT holders. Crowdloan contributors get their DOT back at the end of the lease, and parachain teams can choose to reward them in various ways, including with a distribution of the parachain’s native token.

Auction Duration

Auctions on Polkadot have an open bidding period of approximately 1 week. At the end of the bidding period, the precise moment of the auction’s close is determined retroactively. This prevents last-minute “auction sniping” and promotes more accurate price discovery [(See the case for candle auctions)](https://www.polkadot.network/blog/research-update-the-case-for-candle-auctions/).

Slot Duration & Lease Periods

Each slot on the Relay Chain can be leased for a maximum duration of 96 weeks. When bidding on a slot, parachains can choose the length of their desired lease by selecting a contiguous range of 12-week increments known as lease periods. Multiple parachains can win a single auction if they successfully bid on non-overlapping lease periods.

## Auctions timetable

Each auction takes place over the course of 1 week and assigns a total slot duration of 96 weeks (divided into 8 12-week lease periods). The schedule is determined via Polkadot’s on-chain governance community.

-------------------------

0x3639 | 2023-10-30 15:18:09 UTC | #2

Is this related to NoM?  I participated in these parachains and regretted it for 2 years.  These parachains got so twisted and complicated it required a PhD just to know what the hell you owned.  Each chain had a different liquid token and everyone had different terms.  Some project pulled out (Enjin) and others flamed out.  Some still have not released their token rewards.  It became abundantly clear that the projects building on DOT are 100% centralized with total control.  

Personally the only thing I think we can learn from DOT is never copy anything they did.  The polkadot.js wallet is so insanely complicated.  I cannot believe they created tech that is so difficult to use.  

I finally got 50% of my locked DOT back recently, and sold everything that second.  I have another 50% to go in the coming months and will sell all of it them.  I'm counting the days until I'm done with DOT.

-------------------------

Stark | 2023-10-30 16:31:17 UTC | #3

Fortunately, my only experience with parachains was to collect an nft drop. I too, found it to be a mess as a user experience.

I was thinking along the lines of how they utilized the auctions to mobilize the communities that they onboarded. I was a member of the Origin Trail TRAC community when they switched from their own L1 over to a DOT parachain.

I took it as a red flag in that particular case and shut down my nodes, left my locked jobs, and exited - but I also thought the way that the process which required TRAC holders to "vote" for a parachain slot by staking DOT, was interesting. 

I think parachains are somewhat analagous to  extension chains. I shared this with the interest to study and or discuss an example from which to learn.

-------------------------

0x3639 | 2023-10-30 17:13:27 UTC | #4

cool - makes sense.

-------------------------

