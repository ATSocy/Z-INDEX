Thread: ann-i-n-e-r-t-i-a-nom-smart-contracts
EovE7Kj | 2024-11-20 15:26:51 UTC | #1


---

# *i n e r t i a* 

> 1. the natural tendency of objects in motion to stay in motion

> 2. an object's resistance to changes in its motion

> 3. an object with more inertia will also have a greater potential to maintain its momentum

**a novel WASM-based smart contract framework, purpose-built for the Network of Momentum.**


**URL:** https://github.com/EovE7Kj/inertia

**Team:** *EovE7Kj and Co.* 
- ACTIVELY SEEKING ADDITIONAL DEVELOPERS.

------
 **Funding**

PHASE 1/?
**Total Requested Funding for phase 1** : 5000 ZNN and 50000 QSR


So far, we've made progress integrating key components for blockchain interaction, WASM contract handling, and a gas metering mechanism. Here's a summary of what we've done:

### 1. **WASM Runtime Integration**

* We've built the foundational logic for loading and executing WebAssembly (WASM) contracts. This is done using the `wasmer-go` library, which allows us to load WASM modules and execute functions from these modules.
* A `WASMRuntime` struct was implemented to manage the WASM engine, store, and module.
* We added methods to load and execute contracts (`LoadContract` and `ExecuteContract`), which interface with the WASM runtime.

### 2. **Gas Metering**

* To prevent infinite execution and ensure fair resource usage, we've added a simple gas metering mechanism through the `QasMeter` struct. This tracks gas usage and ensures that a contract cannot exceed a predefined limit.
* The `ConsumeQas` method within `QasMeter` is responsible for checking if the contract execution exceeds the gas limit and throws an error if it does.

### 3. **Contract Execution with Gas Consumption**

* We've modified the contract execution flow to track the gas consumption associated with each contract execution. Each function call in the contract deducts gas from the `QasMeter`.
* In the `ExecuteContract` method, we first check if the contract has enough gas to proceed. If not, an error is thrown, and the operation is aborted.

### 4. **API Exposure and Contract Invocation**

* The `ExposeAPI` method was introduced to allow interaction between the blockchain environment and the contract. This method registers functions that the WASM module can call, such as `write_state`, which interacts with the blockchain's state.
* We've created a function to handle the full contract invocation cycle, from loading the contract to executing the functions and interacting with the blockchain API (`HandleContractInvocation`).

### 5. **Testing**

* A `test/` directory was established with a trivial `contract.wasm` file and a Go test file (`test.go`). This will allow us to test the WASM contract handling and gas metering mechanisms in a controlled environment.


------

**Roadmap**

1. **WASM Runtime Interface**: Integrate a WASM runtime library into `go-zenon` to handle smart contract execution. The runtime should include sandboxing for security and gas metering for performance.
2. **Develop a Contract API**: Expose network functionalities (e.g., state storage, transactions) to WASM contracts via APIs, enabling them to interact with the NoM.
3. **Update Node Logic**: Extend transaction processing logic to validate and execute WASM contracts, ensuring consensus mechanisms are updated accordingly.
4. **Tooling for Developers**: Provide SDKs or compilers that support compiling smart contracts from languages like Rust or AssemblyScript into WASM, along with debugging and deployment tools.
5. **Governance and Upgrades**: Ensure proper governance around smart contract execution, potentially requiring changes to the consensus rules or protocol.

-----

-------------------------

0x3639 | 2024-11-19 10:51:10 UTC | #2

[quote="EovE7Kj, post:1, topic:1968"]
**Governance and Upgrades**: Ensure proper governance around smart contract execution, potentially requiring changes to the consensus rules or protocol.
[/quote]

Thank you for this update.  What sort of consensus or protocol changes do you have in mind?  

Also, was the AZ you submitted for the repo that was just added?  Or does it include other items in the roadmap?  I reviewed the code and looks like it's exactly what you described: "WASM contract handling, and a gas metering mechanism".  

For those if you who cannot read the code.  Here is the `gas metering mechanism`:
```
package wasm

type QasMeter struct {
	qasLimit uint64
	qasUsed  uint64
}

func NewQasMeter(limit uint64) *QasMeter {
	return &QasMeter{qasLimit: limit, qasUsed: 0}
}

func (gm *QasMeter) ConsumeQas(amount uint64) error {
	if gm.qasUsed+amount > gm.qasLimit {
		return fmt.Errorf("out of qas")
	}
	gm.qasUsed += amount
	return nil
}

func (gm *QasMeter) RemainingQas() uint64 {
	return gm.qasLimit - gm.qasUsed
}

func (gm *QasMeter) Reset(limit uint64) {
    gm.qasLimit = limit
    gm.qasUsed = 0
}
```

and here is the `WASM contract handling`

```
package wasm

import (
        "fmt"
        "io/ioutil"

        "github.com/wasmerio/wasmer-go/wasmer"
)

type WASMRuntime struct {
        engine  *wasmer.Engine
        store   *wasmer.Store
        module  *wasmer.Module
        imports *wasmer.ImportObject
        qasMeter *QasMeter
}

var gasCosts = map[string]uint64{
    "write_state": 200,
}

// initialize runtime
func NewWASMRuntime(qasLimit uint64) *WASMRuntime {
        engine := wasmer.NewEngine()
        store := wasmer.NewStore(engine)
        return &WASMRuntime{
                engine: engine,
                store:  store,
                qasMeter: NewQasMeter(qasLimit),
        }
}

func (r *WASMRuntime) LoadContract(filepath string) error {
        wasmBytes, err := ioutil.ReadFile(filepath)
        if err != nil {
                return fmt.Errorf("failed to read WASM file: %w", err)
        }

        module, err := wasmer.NewModule(r.store, wasmBytes)
        if err != nil {
                return fmt.Errorf("failed to compile WASM module: %w", err)
        }

        r.module = module
        return nil
}

func HandleContractInvocation(tx *Transaction, api *BlockchainAPI, runtime *WASMRuntime) error {
        // Load contract
        err := runtime.LoadContract(tx.ContractBinary)
        if err != nil {
                return fmt.Errorf("failed to load contract: %w", err)
        }

        // Expose API
        runtime.ExposeAPI(api)

        // Execute function
        _, err = runtime.ExecuteContract(tx.FunctionName, tx.Args...)
        if err != nil {
                return fmt.Errorf("contract execution failed: %w", err)
        }

        return nil
}

func (r *WASMRuntime) ExposeAPI(api *BlockchainAPI) {
    r.imports.Register("env", map[string]wasmer.Int32ToVoid{
        "write_state": func(key, value int32) {
            cost := gasCosts["write_state"]
            if err := r.qasMeter.ConsumeQas(cost); err != nil {
                fmt.Printf("Error: %v\n", err)
                return
            }
            api.WriteState(int32ToString(key), int32ToString(value))
        },
    })
}


func (r *WASMRuntime) ExecuteContract(functionName string, args ...interface{}) ([]byte, error) {
    if err := r.qasMeter.ConsumeQas(100); err != nil {
        return nil, err
    }

    instance, err := wasmer.NewInstance(r.module, r.imports)
    if err != nil {
        return nil, fmt.Errorf("failed to instantiate WASM module: %w", err)
    }
    defer instance.Close()

    function, err := instance.Exports.GetFunction(functionName)
    if err != nil {
        return nil, fmt.Errorf("function '%s' not found: %w", functionName, err)
    }

    result, err := function(args...)
    if err != nil {
        return nil, fmt.Errorf("failed to execute function '%s': %w", functionName, err)
    }

    if err := r.qasMeter.ConsumeQas(uint64(len(result.([]byte)))); err != nil {
        return nil, err
    }

    return result.([]byte), nil
}
```

-------------------------

sultanofstaking | 2024-11-19 14:31:21 UTC | #3

* How many additional developers are needed, and what skills are you looking for?
* What specific deliverables will be completed in Phase 1?
* How many phases are anticipated, and what will the total funding look like?
* What is the estimated timeline for completing Phase 1?
* Are there any critical dependencies or risks that could delay progress?

-------------------------

0x3639 | 2024-11-19 11:51:55 UTC | #4

@EovE7Kj how does this work?

https://github.com/EovE7Kj/inertia/blob/c52dc4830e1dd0215da3b34249b648875b08e491/app/app.go#L5

-------------------------

vilkris | 2024-11-19 11:57:47 UTC | #5

The test.go is not functional.

-------------------------

TrevorLeahy3 | 2024-11-19 13:53:11 UTC | #6

Can you take it easy on the AZ submissions until theres some more substance in the repos? Why are you so keen to keep submitting after only making a forum post?

-------------------------

0x3639 | 2024-11-19 14:59:15 UTC | #7

Until we can get more clarity on this work I've voted no.  

I definitely support this work, but I'm confused by this last commit, the work in it, and the roadmap.

-------------------------

EovE7Kj | 2024-11-19 18:38:29 UTC | #8


[quote="0x3639, post:7, topic:1968, full:true"]
Until we can get more clarity on this work I’ve voted no.

I definitely support this work, but I’m confused by this last commit, the work in it, and the roadmap.
[/quote]

I'm going to go full-Linus here, and if it upsets the SAME ~20 people here (and the 5 other identical forums), so be it.

### **This is literally the initial commit** for a project that will take **at least 10 months** to develop, test, and integrate.

### What’s committed so far is **preliminary work** on WASM runtime integration. You know, the **foundation** for everything else that’ll follow.

* **99% of my work lives in a Git repo.** I commit constantly—every few minutes. I have **10 git aliases** in my rc just for this purpose. Any real developer will tell you why. If you need me to explain it too, we’re having the wrong conversation.
* The repo is **my dev process.** It’s not here to be a slideshow for Pillars or a showcase for anyone expecting deliverables after THE FIRST commits. It’s called **work in progress.**
* And Git? It’s a tool to organize and maintain **ongoing projects.** Not to ship you a product after the first step.

The repo is **my dev work**, not some elevator pitch to convince you I know what I’m doing.

---

I have a full-time, demanding job. I travel constantly. I spend weeks away from my family. And yet, I’ve spent **months of my free time** working on these projects—because I believe in this Network. I don’t have the time (or frankly the patience) to waste on explaining why we need Sentinels for smart contracts or walking everyone through **the same WP you’ve all already read**. 

If what you want is **a flashy slide deck** to impress the crypto Twitter crowd, **allocate some more AZ funds for another marketing submission.**  

---
[quote="TrevorLeahy3, post:6, topic:1968, full:true"]
Can you take it easy on the AZ submissions until theres some more substance in the repos? Why are you so keen to keep submitting after only making a forum post?
[/quote]

This is **open development**. I thought submissions keep the community informed and engaged with ongoing progress.  If transparency about early stages of a **long development cycle** is something you have a problem with, maybe you need to think about what AZ is supposed to be for.

You want “substance”? Then define what the hell “substance” means a first commit into a project like this.

> **"ZENON is community"**

Back when the WP droppped, it looked like the OG BTC community. This... this is not that. 
> "~~Dont trust, verify.~~" 
> "PrIcE gO uP." - Satoshi Nakamoto

-------------------------

DrD3 | 2024-11-19 19:06:44 UTC | #9

To be fair I do believe the community is being a bit harsh towards @EovE7Kj . He did not ask for funding and claim the product to be finished- the AZ request is literally in its proposal phase- a placeholder cementing a certain commitment.

Asking for substance is a more plausible request when it actually comes to the request of funding and even then how many AZs have we passed for a whole lot less?

-------------------------

SugoiBTC | 2024-11-19 19:08:24 UTC | #10

Professor, we gotchu. Please tell us how we can help by setting up a requirements list so we can find devz to assist you in integrating zApps.  

The core community knows that good things take time. Many of us have been holding for a long time and will continue to do so, no matter what.  

As per your comments on the .network website, there is a web dev currently giving it a makeover to appeal to builders instead of speculators.

Satoshi 4 life — may his spirit live forth in us aliens.

-------------------------

TrevorLeahy3 | 2024-11-19 22:35:29 UTC | #11

[quote="EovE7Kj, post:8, topic:1968"]
You want “substance”? Then define what the hell “substance” means a first commit into a project like this
[/quote]

Thanks for the reply.

This is not a new conversation, i assumed you were around for other submissions where the lack of well defined goals and objectives has grown into an issue of confidence for the community. We are simply asking for more information on what you intend to build.

Im mainly asking why youre setting this kind of example, ie full AZ submissions with only broad descriptions for whats to be expected. Timeline and actionable goals would mean alot. 

If this the initial commit for a certain length of work, 10 months you think? why wouldnt you describe that scope in the AZ? How many phases?

Appreciate any information that will lead to clearer expectations of your work so ppl can figure out on their own where that equates to value for NoM.

-------------------------

0x3639 | 2024-11-19 20:25:07 UTC | #12

[quote="EovE7Kj, post:8, topic:1968"]
I’m going to go full-Linus here, and if it upsets the SAME ~20 people here (and the 5 other identical forums), so be it.
[/quote]

Well if we are going full retard, let's go for it.  

You are not the only person here with a full time and demanding job.  I also travel all over the country and manage money for other people.  You are not the only person here with world class skillz.  Does your dad work at Nintendo too?

I might not write code that is consequential to the network but I've dedicated all my free time for YEARS to help this network.  So join the club.  You are not the only one stretched thin doing hard work.  In fact, the same retarded 20 people you refer to are all in the same boat.  We bust our ass for this project and have nothing but good intentions.  No one here is attacking you.  We want to understand so we can help and improve the project.

You asked us to help you find devs and be more vocal about the project.  Why would you ask for us to help if we cannot understand what you are doing.  So clearly we are asking retarded questions.  And I'm sure they are irritating.  We try getting answers (in TG) before we post here, but it's the same old bullshit.... read between the lines.

If this is an individual effort I get that too.  Just say that.  I'm going to do X.  It's going to do Y.  It's going to cost about Z.  I need help from smart devs but ONLY if you can solve this...  In the meantime, don't ask me questions I'll be back later.  But if you want to engage the community (or expect us to do something) you need to expect to do some hand to hand combat with some autistic retards.

[quote="EovE7Kj, post:8, topic:1968"]
I don’t have the time (or frankly the patience) to waste on explaining why we need Sentinels for smart contracts or walking everyone through **the same WP you’ve all already read**.
[/quote]

Honestly? This is a massive slap in the face to the people here busting their ass.  Maybe you think you are the only person here working hard.   NEWS FLASH!!!  You aren't.

-------------------------

vilkris | 2024-11-19 21:03:41 UTC | #13

The code in the repository you're showcasing is not functional, yet you state you've "made progress integrating key components for blockchain interaction, WASM contract handling, and a gas metering mechanism.".

Why does test.go have such obvious errors?

-------------------------

Samwinter1888 | 2024-11-19 21:30:03 UTC | #14

Guys, people that are developing and and doing work for the project, are doing really good job.  The community really appreciates it!

Please do not fight over some missunderstandings, we are all on the same side and want Zenon to suceed! 

And I want to say Thank You All for putting in all those efforts!

-------------------------

romeo | 2024-11-19 22:34:35 UTC | #15

Let's not forget the base AZ process involves A) the initial submission (i.e. pillars vote that the proposal is warranted and worthwhile) and B) subsequent funding requests after delivery.

This submission is currently only for A.

Questions should be asked to clarify deliverables, costings and time estimates etc. 

Discourse and discussion is good! Let's be respectful and helpful though.

I support this proposal - @EovE7Kj has a proven track record of development, and as explained his repo is WIP and he'll update us here as progress is made for major milestones I imagine.

When phases are submitted for funding that should be the trigger for reviewing code and effort

-------------------------

0x3639 | 2024-11-19 22:55:02 UTC | #16

[quote="romeo, post:15, topic:1968"]
I support this proposal
[/quote]

If you support this proposal, can you please explain to me what it includes?  Have you looked at the repo?  Is he asking for a full AZ for what has been submitted?

-------------------------

crack | 2024-11-19 23:14:51 UTC | #18

[quote="EovE7Kj, post:1, topic:1968"]
we’ve made progress integrating key components for blockchain interaction, WASM contract handling, and a gas metering mechanism.
[/quote]

[quote="EovE7Kj, post:8, topic:1968"]
**99% of my work lives in a Git repo.** I commit constantly—every few minutes. I have **10 git aliases** in my rc just for this purpose. Any real developer will tell you why. If you need me to explain it too, we’re having the wrong conversation.
[/quote]

Dont Trust, BUT 
Community Unable to Clarify

-------------------------

EovE7Kj | 2024-11-19 23:42:51 UTC | #19

[quote="vilkris, post:13, topic:1968, full:true"]
The code in the repository you’re showcasing is not functional, yet you state you’ve “made progress integrating key components for blockchain interaction, WASM contract handling, and a gas metering mechanism.”.
Why does test.go have such obvious errors?
[/quote]


Just a question - do you just jump into a codebase and start firing away code at random? Even when there is no readme in the parent folder?  Are you familiar with typical software project structure? `./test/` dir is almost always exclusively for the **developer** testing. 

You're like someone walking into a car factory and being stunned to find that the cars are not fully-assembled.  
`Crash test? What is this thing, the car is ruined! I don't plan to drive straight into a wall!`

[quote="EovE7Kj, post:8, topic:1968"]
**This is literally the initial commit** for a project that will take **at least 10 months** to develop, test, and integrate.
[/quote]

It seems like nobody here has pieced together that at the present the repository is basically framework-level WASM interface intended to patch into a running node.  `./test/` will grow as the testing progresses! You don't have all the pieces because: 
1. the solution is still being formulated
2. the code is still being rewritten, and will likely be reworked
3. THE REPO IS FOR THE DEV(s) WRITING IT

## Does everyone here understand what git is? 

I wasn't delivering YOU a piece of software. I was only making public (parts of) my own local git repo.

-------------------------

EovE7Kj | 2024-11-19 23:49:00 UTC | #20

[quote="0x3639, post:12, topic:1968"]
This is a massive slap in the face to the people here busting their ass. Maybe you think you are the only person here working hard.
[/quote]


I meant no disrespect to you or anyone else working on this project.  

I just get the feeling that around here, development takes a back seat to ephemeral chasing after exposure. I don't want people to notice this blockchain because it's pumping like XRP.  **I want people to notice this blockchain because it does shit that no other blockchain can do.**   And it seems like people here want that too, but their feeble solution is to sit around and wait for professor-z and co. to miraculously reappear and do it all for us.  

The pieces are there.  You need people to actually DO the work.

-------------------------

romeo | 2024-11-20 00:15:02 UTC | #21

[quote="EovE7Kj, post:1, topic:1968"]
**Roadmap**

1. **WASM Runtime Interface**: Integrate a WASM runtime library into `go-zenon` to handle smart contract execution. The runtime should include sandboxing for security and gas metering for performance.
2. **Develop a Contract API**: Expose network functionalities (e.g., state storage, transactions) to WASM contracts via APIs, enabling them to interact with the NoM.
3. **Update Node Logic**: Extend transaction processing logic to validate and execute WASM contracts, ensuring consensus mechanisms are updated accordingly.
4. **Tooling for Developers**: Provide SDKs or compilers that support compiling smart contracts from languages like Rust or AssemblyScript into WASM, along with debugging and deployment tools.
5. **Governance and Upgrades**: Ensure proper governance around smart contract execution, potentially requiring changes to the consensus rules or protocol.
[/quote]

I believe this is the deliverable list for the AZ ask - I don't expect to see it in the repo until funding phases are raised

-------------------------

Stark | 2024-11-20 01:06:42 UTC | #22

![Screenshot 2024-11-19 at 7.56.29 PM|690x188](upload://olYIAOJRl1AaymHLEGLftHDiRcm.png)
Sir, 

I wholeheartedly agree.
 
Several of us are working very hard to attract attention, capital, and talent in a highly oversaturated market. I appreciate your contributions and that you've been communicative. The reason why I [asked about qas](https://forum.zenon.org/t/unikernel-z-a-unikernel-for-the-network-of-momentum/1871/218) is because I want to be able to describe use cases and the advantages of NoM in order to attract the right kind of attention to make this network a success.

Regards,
Stark

-------------------------

0x3639 | 2024-11-20 01:38:56 UTC | #23

[quote="EovE7Kj, post:20, topic:1968"]
I just get the feeling that around here, development takes a back seat to ephemeral chasing after exposure. I don’t want people to notice this blockchain because it’s pumping like XRP. **I want people to notice this blockchain because it does shit that no other blockchain can do.** And it seems like people here want that too, but their feeble solution is to sit around and wait for professor-z and co. to miraculously reappear and do it all for us.
[/quote]

With all due respect, you clearly do not know the 20 people you just shit on and all the work we do.  Maybe you are referring to chadass or all the other moonboyz that got spit out the back.  They are gone.  We've been shitting them out the back for years.  The only people who can hang now are the beasts.  

We are the hardened contributors busting our ass every day with complete disregard to price and all the reasons this project should fail.  It feels like this response was from 2022 and it teleported itself to 2024. 

We want "**people to notice this blockchain because it does shit that no other blockchain can do**" too.  The people trying to explain it (the 20 here) simply do NOT have the tools.   We cannot explain the BTC interoperability and we cannot clearly explain the SC architecture.  Should we stick with "trust me bro"?

I asked you for an AMA so we can build the tools to make that possible but instead you told us to do the work.

So you should either ask us to put our pencils down or you will need to explain things so we can sell others on why our blockchain is so fucking bad ass.

-------------------------

0x3639 | 2024-11-20 01:42:31 UTC | #24

[quote="romeo, post:21, topic:1968"]
I believe this is the deliverable list for the AZ ask -
[/quote]

I don't think so.  That is the full road map that will take 10+ months.  But I'm honestly not sure which is why I asked.

-------------------------

EovE7Kj | 2024-11-20 02:06:32 UTC | #25

I respect you and the work you've put in.  And that goes to for all the people you are probably alluding to.  What I am trying to say is that if the community wants the network to fulfill the goals of the WP, then the community needs to make it happen.  If there aren't people with the blockchain knowledge, that's fine. This shit is complicated. 

If we can get the right people making the technology happen, we won't have to sell this to anyone. It will sell itself.

-------------------------

0x3639 | 2024-11-20 02:18:34 UTC | #26

Thank you.  

We are here to help.

-------------------------

vilkris | 2024-11-20 07:48:15 UTC | #27

You're asking for devs to help you and you're asking pillars to support your work financially. At the same time you're presenting non-functional pseudocode and overstating its merits. As a developer that raises questions, since I can only go off of what you have said and presented.

What test.go is supposed to do is really simple. Are you saying you didn't run the test and verify it works before commiting it? Why would you do that? If you want to convince the community you have the technical skills required to complete the project you're proposing, you shouldn't lash out at these simple questions.

-------------------------

vilkris | 2024-11-20 13:17:44 UTC | #28

I looked at your previous [zapps code](https://github.com/EovE7Kj/zApps/tree/main) that was supposed to be a working PoC, which you were paid for, but it is completely non-functional as well.

-------------------------

EovE7Kj | 2024-11-21 05:25:13 UTC | #30

 Since you brought it up, did you understand even understand what the `uk-dev` is?  This is using Docker to allow anyone who cares to write an app in a stripped-down linux image containing only the components and dependencies necessary for that app (yeah, I wrote a "unikernel-wrapper" that only uses Docker). This was a repo to help other devs to get their Apps in a unikernel. The zApp toolkit is supposed to enable the community to deploy once we have smart-contracts in the network.  No this wasn't a "functional" zApp -- **how was I supposed to write one without a working smart-contract mechanism?** (thanks for the segue back to this AZ by the way).  


No, I wasn't lashing out.  I was defending my work.  I have been trying to lay the groundwork for several different interworking components that all rely on one another, and I have been doing it alone thus far. Unikernel, zApp and Smart Contracts are a huge undertaking. I haven't had anyone lending a hand or contributing to this work, instead a bunch of skepticism and criticism from people who don't even understand what I am trying to do.   This community has seen very few major development endeavors... if you take away the work of aliencoder, not very much has been done since alphanet went live. 

If you're hoping that the fundamental goals outlined in the WP (Bitcoin interoperability, zApps, etc.) are just going to fall into our laps without any funding or DEVELOPMENT (yeah, that means in-progress repos) then you're going to be disappointed.

-------------------------

vilkris | 2024-11-21 10:51:23 UTC | #31

Lots of words but no explanation to my questions about test.go.

You don't need a working smart contract mechanism to make a compilable application. The Go code in the zapps repository and the inertia repository are littered with ridiculous issues, which is at odds with your claims of being a competent programmer.

-------------------------

TrevorLeahy3 | 2024-11-21 11:34:37 UTC | #32

Thanks for sharing your perspective on this.

-------------------------

0x3639 | 2024-11-24 11:38:04 UTC | #33

I've read all these posts again.  Despite some aliens believing this is an elaborate hoax, I actually believe this work is legit.  However, I'm going to continue to vote NO for the following reasons: `Don't trust, verify`

[quote="EovE7Kj, post:8, topic:1968"]
Back when the WP droppped, it looked like the OG BTC community. This… this is not that.

> “~~Dont trust, verify.~~”
> “PrIcE gO uP.” - Satoshi Nakamoto
[/quote]

He accuses us of only focusing on price go up, yet when we try to verify his AZ we get no response.

[quote="sultanofstaking, post:3, topic:1968, full:true"]
* How many additional developers are needed, and what skills are you looking for?
* What specific deliverables will be completed in Phase 1?
* How many phases are anticipated, and what will the total funding look like?
* What is the estimated timeline for completing Phase 1?
* Are there any critical dependencies or risks that could delay progress?
[/quote]

He claims to be working alone, yet implies he is a group.

[quote="EovE7Kj, post:1, topic:1968"]
**Team:** *EovE7Kj and Co.*
[/quote]

The repos also have two different email addresses implying at least two people are working on this.  

He is asking for devs to join him yet he will not explain aspects of the project to us.

[quote="EovE7Kj, post:1, topic:1968"]
ACTIVELY SEEKING ADDITIONAL DEVELOPERS.
[/quote]

[quote="EovE7Kj, post:8, topic:1968"]
I don’t have the time (or frankly the patience) to waste on explaining why we need Sentinels for smart contracts or walking everyone through **the same WP you’ve all already read**.
[/quote]

The code does look like an LLM hallucination.  However, if what he is saying is true, it's only a portion of the work in `git` >> What is [git](https://en.wikipedia.org/wiki/Git) (for the deplorables)? 

He has an [address](https://zenonhub.io/explorer/account/z1qpp32t3uctrelxpwdq9wrz8avh0njpsvcy8ewc?page=18) that dates back to 2021 and he made a [delegation yield optimizer](https://zenonhub.io/explorer/account/z1qpp32t3uctrelxpwdq9wrz8avh0njpsvcy8ewc?tab=delegations) from his AZ rewards.  It's unlikely a scammer would do that.

The facts here are really confusing.  I believe this work is legit, however I'm going to vote no because when "real" scammers come looking for an AZ and are able to concoct an elaborate hoax we need to be able to spot them.

If he cannot (or will not) answer @sultanofstaking questions why is this even up for debate?

-------------------------

Stark | 2024-11-24 14:31:47 UTC | #34

@EovE7Kj I think it's important to try to take all of the feedback as pertaining to the proposal itself, as well the questions put forth, especially from Sultan. I want to believe. We just have to be careful.

[quote="EovE7Kj, post:20, topic:1968"]
I want people to notice this blockchain because it does shit that no other blockchain can do.
[/quote]

hear, hear. :clap:

-------------------------

sultanofstaking | 2024-11-25 14:46:10 UTC | #35

Going to abstain until my questions are answered

-------------------------

EovE7Kj | 2024-11-25 16:08:17 UTC | #36

[quote="sultanofstaking, post:3, topic:1968"]
How many additional developers are needed, and what skills are you looking for?
[/quote]
- at least 2 dedicating ~2-3 hours a day 

[quote="sultanofstaking, post:3, topic:1968"]
What specific deliverables will be completed in Phase 1?
[/quote]

- A working POC with on testnet (ie. a full release of go-zenon with  smart-contract integration)


[quote="sultanofstaking, post:3, topic:1968"]
How many phases are anticipated, and what will the total funding look like?
What is the estimated timeline for completing Phase 1?
[/quote]


- Full AZ funding for the POC above. I don't really see a way to incrementally fund this project with meaningful deliverables
- **A absolute minimum of 6 months given my current resource allocation.**  Obviously this changes if additional devs are brought on. 

[quote="sultanofstaking, post:3, topic:1968"]
Are there any critical dependencies or risks that could delay progress?
[/quote]

- Absolutely. Too many to name (personal or professional constraints, for example)

  * If I could afford to dedicate all my time and resources to this project, I wouldn't think twice about it.  If I was in retirement, I would make this my passion project. Unfortunately, I'm not in that position, and my progress on this is going to be largely at the mercy of my day job schedule.
- NO requests for funding will be submitted until the working POC is delivered and running

-------------------------

EovE7Kj | 2024-11-25 16:19:07 UTC | #37

[quote="0x3639, post:33, topic:1968"]
The code does look like an LLM hallucination. However, if what he is saying is true, it’s only a portion of the work in `git` >> What is [git](https://en.wikipedia.org/wiki/Git) (for the deplorables)?
[/quote]

Really stunned that I have to defend myself to this community after delivering its first docker.io img and unikernel qcow2
- `docker.io/eove7kj/znnd:latest` 
-  https://github.com/EovE7Kj/unikernel-z/releases/tag/unikernel-znnd 

[quote="0x3639, post:33, topic:1968"]
He has an [address](https://zenonhub.io/explorer/account/z1qpp32t3uctrelxpwdq9wrz8avh0njpsvcy8ewc?page=18) that dates back to 2021 and he made a [delegation yield optimizer ](https://zenonhub.io/explorer/account/z1qpp32t3uctrelxpwdq9wrz8avh0njpsvcy8ewc?tab=delegations) from his AZ rewards. It’s unlikely a scammer would do that.
[/quote]

My time on this network greatly predates the alphanet migration and Syrius.  All ZNN and QSR there in 2021 were from the migration.  Some of those ZNN were staking rewards from the OG wallet (running 24/7) and the majority came from OTC via Shai. 

Again, even having to explain this is unbelievable.

-------------------------

sultanofstaking | 2024-11-25 18:03:39 UTC | #38

Updating to yes.  Payout at POC demo makes sense. Maybe good candidate to launch POC on hyperqube? That could help force testing & awareness. Can ask around in polkadot/kusama for any wasm devs looking for additional work - still have some friends there from when i ran their infra - no promises.

-------------------------

coinselor | 2024-11-25 21:55:45 UTC | #39

Keep being you Professor. You are inspiring aliens:

![image|584x500](upload://uMUBIrSxCtU50bYqUVRkgkyPse3.png)

Quite [a funny interaction](https://altz.wtf). I LOLed.

-------------------------

Stark | 2024-11-26 01:30:51 UTC | #40

![IMG_7339|500x500](upload://rc6C63wPPaPJx0eZ00G97KRTp4X.png)

-------------------------

0x3639 | 2024-11-28 01:27:38 UTC | #41

[quote="EovE7Kj, post:37, topic:1968"]
Again, even having to explain this is unbelievable.
[/quote]

Well you did call us retarded moonboyz.  So maybe that has something to do with it?? LOL.  Let's hit the reset button and try to restart a professional dialogue.

Some of the other developers have not followed the unikernelZ work closely.  The new repo was confusing (to me) but I think your explanation make sense.  

BTW this was funny.  

[quote="EovE7Kj, post:8, topic:1968"]
### **This is literally the initial commit** for a project that will take **at least 10 months** to develop, test, and integrate.

### What’s committed so far is **preliminary work** on WASM runtime integration. You know, the **foundation** for everything else that’ll follow.

* **99% of my work lives in a Git repo.** I commit constantly—every few minutes. I have **10 git aliases** in my rc just for this purpose. Any real developer will tell you why. If you need me to explain it too, we’re having the wrong conversation.
* The repo is **my dev process.** It’s not here to be a slideshow for Pillars or a showcase for anyone expecting deliverables after THE FIRST commits. It’s called **work in progress.**
* And Git? It’s a tool to organize and maintain **ongoing projects.** Not to ship you a product after the first step.

The repo is **my dev work**, not some elevator pitch to convince you I know what I’m doing.
[/quote]

Welcome to the reset Zenon Community.  Glad you are here.  Let us know if you need any help.

-------------------------

0x3639 | 2024-11-29 13:57:19 UTC | #42

We might be retarded, but our videos rock!!!  @Chainemane for the win!!  

https://youtu.be/M08Vh0MvN-Q

-------------------------

romeo | 2024-12-03 04:55:08 UTC | #43

@EovE7Kj can I please ask that you re lodge the AZ again now that the majority of concerns around payment have been addressed?

-------------------------

EovE7Kj | 2024-12-04 19:16:17 UTC | #44

Given the recent pushback  to proposals, the professor has decided take a sabbatical from the forum and AZ. Any of my work done on this network will remain in my own domain until it is ready for the community (or vise-versa)

I appreciate the interactions and hope to reconnect when the time is right.

-------------------------

cryptocheshire | 2024-12-05 10:31:59 UTC | #45

Mate just stick around, resubmit and lobby for support. Dont let some mouthbreathers discourage you.

-------------------------

0x3639 | 2024-12-06 00:04:53 UTC | #46

[quote="EovE7Kj, post:44, topic:1968"]
I appreciate the interactions and hope to reconnect when the time is right.
[/quote]

Sir, I wanted to apologize for any of my behavior that you feel was unfair or rude.  

Let me explain what happened.  You posted that AZ.  I started to look at the commit you posted and I could clearly see the roadmap of the work. It was like the first step in a 10 mile hike, but I did not fully appreciate that at that time.  I asked some questions about the AZ and the response was not clear to me.  I asked some devs to take a look and they were equally perplexed because no one understood this was just the very start of your work.  Of course it did not run.  

It appeared to me (and I think others) that first commit was the basis for a full AZ request.  That did not seem right and we started to push back.  You went full Linus.  We went full retard.  And here we are.  

Under normal circumstances the community would have rallied behind your AZ and pushed to get it approved, like we did on the last one.  Because of the interactions here the community was not so keen on pushing, and it failed.  However, it did not fail because we don't support the work.

We want to help you.  We want to understand your work without being retarded interns.  Meanwhile, some new devs are [proposing work](https://forum.hypercore.one/t/taproot-bridge-discussion/565) that make certain assumptions about what a Sentinel is.  I believe these assumptions are not consistent with the WP and probably your work.  But I'm not sure.

We want to make sure we don't have two different teams working on Sentinels assuming they do different things.  Meanwhile, both teams are preparing to submit for AZs that conflict with each other.  We want to avoid this for obvious reasons.

So I would like to help you coordinate your activities with other devs so: (1) they understand your work, and (2) to avoid two teams working on sentinels while thinking they do different things.  

We both want the same thing - for Zenon to succeed.  

`{"zenon":true}`

DM me on matrix if you want help `@deeznnutz:zenon.chat` and thanks to @Stark for solving the problem.

```
import base64
import gzip

encoded_string = "H4sIAAAAAAAAA8tIzcnJV0jMyUzNK+YqycgsVgAi1/wyV3PvLD0ucwNLM2MjHQVlEz0FLgChcDRLKwAAAA=="

# Decode base64 string
decoded_string = base64.b64decode(encoded_string)

# Decompress gzip data
decompressed_string = gzip.decompress(decoded_string)

print(decompressed_string.decode("utf-8"))  # Output: {"zenon":true}
```

-------------------------

coinselor | 2024-12-06 09:52:47 UTC | #47

For the record, I voted NO exclusively for this reason:

![image|690x460](upload://xws3rQnSdGs7AQLuq9surMBUxzZ.png)

I fully support @EovE7Kj's work and look forward to developing a hello wolrd zApp in the future.

Also shoutout to @0x3639 for the tactful response ^^

-------------------------

cryptocheshire | 2024-12-07 07:11:33 UTC | #48

On behalf of the rest of us retards thank you for this sers

-------------------------

0x3639 | 2024-12-09 14:58:00 UTC | #49

Rugged
https://github.com/EovE7Kj

-------------------------

EovE7Kj | 2024-12-09 21:34:15 UTC | #50

[quote="0x3639, post:49, topic:1968, full:true"]
Rugged
[https://github.com/EovE7Kj ](https://github.com/EovE7Kj)
[/quote]

[quote="EovE7Kj, post:44, topic:1968"]
Any of my work done on this network will remain in my own domain until it is ready for the community (or vise-versa)
[/quote]

Ironic to see you use a term for scamcoins when all I have been trying to do is legitimize this project

-------------------------

SugoiBTC | 2024-12-09 22:54:31 UTC | #51

#Bullieve

-------------------------

0x3639 | 2024-12-10 00:37:28 UTC | #52

In a generic sense - it's `404`.  

![image|375x500](upload://da83MKonfFvn0aYdusBbA2m0qhC.jpeg)

I hope we see you again and we can support your work. I also hope we can coordinate your work, while you advance it alone.  In the meantime, other developers are making new assumptions about functions sentinels can perform.

https://forum.hypercore.one/t/taproot-bridge-discussion/565

I also wanted to point out that maintainers of `go-zenon` are starting to establish review criteria and it would be great if we can find a way to give you the space you want while maintaining some level of coordinating with the rest of the project.  See George's criteria.  I hope others publish their criteria too.  

https://zenon.wiki/index.php/User:George

My offer stands to help you coordinate your work with others in the community while giving you space.

-------------------------

0x3639 | 2024-12-10 09:51:33 UTC | #53

Translation:

> I used that word not because I believe it, but to disprove it.

we make puzzles too!!  :rofl:

-------------------------

WAGMI | 2024-12-11 22:55:34 UTC | #54

I think its a disservice to progress if we are discouraging contributors who have a track record of completing previous tasks.

-------------------------

0x3639 | 2024-12-26 15:34:17 UTC | #55

Merry Christmas & Happy New Year @EovE7Kj

-------------------------

SugoiBTC | 2024-12-28 16:29:58 UTC | #56

I've been following this project that's built in Rust, they're building a framework for AI-agents and their devs are giga cracked. Currently they're focusing on Solana, but could be integrated into NoM when it's ready.

They are eager to work with other Rust devs, so could be a good place for us to scout talent.

X: https://x.com/Playgrounds0x
Website: https://rig.rs/

https://github.com/0xPlaygrounds/rig

-------------------------

