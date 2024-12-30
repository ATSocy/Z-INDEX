Thread: zenon-ai-model
mehowbrainz | 2023-02-09 19:40:35 UTC | #1

It's been mentioned in Discord that there's interest to develop an AI model (like ChatGPT) but for Zenon exclusively. I've done the preliminary research with some ML engineers, and I'd like to share my vision / knowledge of the matter before we begin hacking partial solutions which could fragment / duplicate data into unnecessary places.

**The Vision**

Feed structured and unstructured data into a trained model so that it can be then called by various channels via an API.

The Zenon AI can be then used to assist various channels:

- A chatbot on the organic site.
- A chatbot on the landing pages (help people complete the conversion of the funnel).
- A bot anyone can call in discord or telegram or the forums.
- A reply bot on Twitter.

The model can be fed from the following data sources:

- **Organic Site:** zenon.org  = Verified ([see this link](https://forum2.zenon.org/t/zenon-org-website-preview/1196) to access development URLs)
- **Documentation**: docs.zenon.org  = Verified
- **Forum**: forum.zenon.org = Unverified
- **Discord / Telegram** = Unverified
- **Git Repositories**  = Verified

---------

**Data Verification**

We cannot assume that all data from sources are correct. We need to develop a method for the model to know which data is verified. This is specifically for Discord / Telegram / Forum conversations we'd feed to the model, as we can assume that the organic and docs sites will have verified data.

---------

**Preparing the Data**

A Question / Answer data structure is what's most required to train such model. The more data we feed the model in such structured format, the more it will know how to answer the user, using the the various data we feed to it (organic/docs/forum/discord/telegram etc). We do NOT need to provide questions / answers for all possible things, the model should be able to comprehend questions asked. It should do fine if we organize Q/A for the most common things people may ask.

I quote from the ML engineer:

> Structured data helps in training. For instance, having a pair of most commonly asked questions and their answers as we would explain it in person, along with the wider context will get us really accurate results. So models trained on such question answer dataset will perform very well. In case the question is from that list the model will give the accurate output. But someone asks a related question which is not in the training set would still be answered based on its similarity to other questions.

The key is to build this Q/A development methodology into a process within the sources we chose to feed the model-with. For example:

While I build a page on zenon.org, I can tag my data with a question/answer for the model. As I push the update to the website, the Q/A data for the model gets updated, output into a format designed to train the model. An automated workflow can then be triggered = new data available = trigger a re-training of the model (GPUs) = new model output = all services using the model are updated. Perhaps it doesn't need to be done after each push ofc, but rather periodically or after some major updates are made. All depends on the cost to retrain the model etc.

Such retraining process can be developed for all other sources. It is our job to develop a community-operated methodology to structure and tag our data for continuous retraining. **We act like alien-bees in a major hive.**

---------

**AI Replies**

The model can also be trained to source its replied. For example:

Discord sourced example:

> User's question: How can I convert my wZNN to native ZNN?
> AI reply: You can refer to the guide on the Discord server.  To learn more go to: [https://discord.com/channels/920058192560533504/1065658520462176256/1065768065888952362](https://discord.com/channels/920058192560533504/1065658520462176256/1065768065888952362)

Docs sourced example:

> User's question: The wallet's data is stored into what?
> AI reply: The wallet data is stored inside a KeyStore. To learn more go to: [https://docs.zenon.org/hypercore/technical/phase-1/cryptography#wallet](https://docs.zenon.org/hypercore/technical/phase-1/cryptography#wallet)

If an answer is not available, the question can be fed into a honeypot where the community sees what people are asking. We can then use that data to improve our data and retrain the model.

---------

**Quotes from the ML Engineer**

> Pretrained Huggingface transformer models are the best fit for this task. Those are scalable and performance is good. We can use seq-to-seq language models like T5 or GPT2 or BERT models for this scenario. These models can be finetuned one the input data to provide sophisticated output closer to ChatGPT. Besides using large amount of data for training, ChatGPT used reinforced learning based on human responses so we cannot possibly achieve that smoothness here. But we can still get smart and relevant answers since these transformer models are also pre-trained on a very large data. [...] My approach would be to first explore BERT and GPT2 models.

> QA based performance will outperform significantly. One thing is, if I dont use QA structure, the responses will be different every single time. Sometimes those might be very irrelevant since these ML system are not 100% accurate but approximations. So more we leave it to the model, lesser its performance.

---------

**Discussion**

As you may understand, before we get into training a model, we need to organize ourselves to develop that hive.

1. Let's agree on the various data sources.

2. Let's discuss about the hierarchy of various data sources (and their verified/unverified status).

3. Let's develop a methodology to tag a question/answer format into the various data sources. You can assume that zenon.org can develop a method to tag its content in such format. The question is more for: Discord, Telegram, Forum. This could develop into a role/paid job using AZ to fund community to structure data.

4. Should the model be told that answers from certain vetted members are automatically assumed to be verified? i.e. Kaine and a few other notable members?

5. Git repositories / code hasn't been really considered yet, but would be useful for technical minds. I think we should keep it in our back pocket to see if we can use zenon repos to learn code at some later date once the first versions of such project are developed.

6. Let's organize a crew to handle the technical documentation of docs.zenon.org/hypercore (I can handle the preliminary organization of the HyperGrowth sections). The basic formats for HyperCore have been created, but the community will greatly benefit from developers to work alongside marketing teams. It's the dream synergy.

7. Let's discuss and eventually outline the specific needs for the project so that the community can hire an ML engineer through AZ. 

---------

**Preliminary Requirements**

- Defined data hierarchy (as the model must be trained to give the best answer possible)
- Defined training workflows (as data sources are constantly updated)
- Open sourced code
- Web-based training (GPUs)
- API to develop chatbot services in different contexts (Discord Zenon AI Chatbot vs. Chatbot embedded on zenon.org landing pages vs. Twitter reply Chatbot etc).

---------

Community project, open for anyone to contribute.

-------------------------

mehowbrainz | 2023-01-23 16:38:40 UTC | #2

Between all the data sources, IMO we can assume that:

* **Organic Site:** [zenon.org](http://zenon.org) = Basic content on all categories.
* **Documentation**: [docs.zenon.org](http://docs.zenon.org) = Detailed content on some categories/topics.
* **Forum**: [forum.zenon.org](http://forum.zenon.org) = Community ideas / takes on topics.
* **Discord / Telegram** = Can be both basics and detailed content on all topics.

-------------------------

cryptocheshire | 2023-01-23 21:26:40 UTC | #3

@0x3639 wen do we start

-------------------------

mehowbrainz | 2023-01-23 21:40:57 UTC | #4

We definitely need the technical docs to get a content facelift by some willing devs. Will be interested to see how GitBook content can get fed into a format readable by the training code.

-------------------------

cryptocheshire | 2023-01-23 22:04:58 UTC | #5

Maybe we should just start implementing an faq and existing code. Once people see the value of it they will be more inclined to help curate the content.

Start quick and dirty, imorove iteratively over time. 

@0x3639 can set up the model n bot, and together we can start collecting content and test.

-------------------------

mehowbrainz | 2023-01-23 22:10:56 UTC | #6

If you wanna go that route. The FAQ (aka Q/A I refer to) is only used to help teach the model how to answer. But you'll need sources of greater information, and that'll come from the data sources I listed above: websites, discord, telegram, forum. If you decide to skip the whole verification recommendations made above, you'll in the beginning likely get odd replies. 

I personally would've preferred we discuss this solution with everyone to design methodologies properly as opposed to trying to hack an MVP that'll likely perform poorly, and we'll circle back to point 1.

I also don't know if the OpenAI referenced in Discord is the solution for this. At least that's not how the ML engineer told me it should be built.

-------------------------

coinselor | 2023-01-23 23:56:10 UTC | #7

This is a great idea, as always, mehowz. I think the value a trained AI chatbot will bring to our community will be immense. Regarding the verified/unverified sources, it's not clear to me whether the model completely disregards the unverified data or simply applies less weight to it. Other than that, your initial data sources suggested made perfect sense to me. Whitelisting certain humans can always backfire, regardless of who it is, it might be much better for the community to curate ie. Mr. Kaine messages into a Q/A format to feed the model.

My biggest concern, given how fast this space seems to be evolving, is that we put resources to build and train our custom AI chatbot model, only to see someone release a better version we might choose to implement in the future since it just performs better.

I might be overestimating the amount of work required, maybe this is just as simple as doing the work we should do anyway (documenting the project, both technically and non-technically) but with an emphasis on Q/A format to feed the model. Then hiring someone that hacks a chatbot in a week.

Regardless, it seems clear we should start prioritizing the Q/A format for a lot of our documentation. Even if we use our custom bot or a commercial bot that is released later on, it seems the output of the bot will always be better with that training dataset (given our objective with the chatbot).

-------------------------

mehowbrainz | 2023-01-24 00:57:20 UTC | #8

[quote="coinselor, post:7, topic:1195"]
Regarding the verified/unverified sources, it’s not clear to me whether the model completely disregards the unverified data or simply applies less weight to it.
[/quote]

If the model is trained on both a good Discord data (tagged verified), and some degenerate non-sense data (tagged unverified), it will not know which is correct, and from what I understand it'll possibly use either. The verification tagging is for weight.

[quote="coinselor, post:7, topic:1195"]
it might be much better for the community to curate ie. Mr. Kaine messages into a Q/A format to feed the model.
[/quote]

That's an alternative option too.

[quote="coinselor, post:7, topic:1195"]
only to see someone release a better version we might choose to implement in the future since it just performs better.
[/quote]

And hence why I believe it's important that we research this project properly, develop a methodology / workflow, and hire the right ML engineering talent to build this. If we develop the whole without being experts in it, I think we're going to have a hard time maintaining it. The more we define in the scope, the more we can have someone implement all the requirements (with hopes to make its maintenance/updating easy for us).

[quote="coinselor, post:7, topic:1195"]
I might be overestimating the amount of work required, maybe this is just as simple as doing the work we should do anyway (documenting the project, both technically and non-technically) but with an emphasis on Q/A format to feed the model.
[/quote]

Yes for the documentation part, but for Discord / Telegram / Forum data I think it becomes a little trickier, if used. It requires a workflow within those environments. And for each data source we have to figure out what kind of data exporters are available, are they manual or through some API, how does the data need to be structured for the model to be trained? etc there's so much to consider here, starting from the various sources of data, down to the role community could play when seeing a worthy comment in Discord by someone, and knowing how to tag it with a question? To properly engineer this, we may even need the ML engineer to help us define a bunch of the scope based on his understanding of how such system would be architected. I'm always interested in building solutions with a clear and organized workflow on both the maintenance and deployment side.

[quote="coinselor, post:7, topic:1195"]
Regardless, it seems clear we should start prioritizing the Q/A format for a lot of our documentation.
[/quote]

We won't get very far if we don't have docs.zenon.org HyperCore content filled up properly. I don't think the model (even if it was fed some Q/A + Discord data) would answer more technical questions properly atm. Likely to throw out some gibberish. The technical documentation here is key, and I think it's the part we're most desperate-for atm.

-------------------------

mehowbrainz | 2023-01-24 01:10:35 UTC | #11

Build it properly and it becomes a zApp-as-a-Service someday.

https://twitter.com/ZenonOrg/status/1617690099441102848?s=20

-------------------------

cryptocheshire | 2023-01-24 07:56:26 UTC | #12

yeah you're right, better to set this up the right way

-------------------------

mehowbrainz | 2023-02-09 19:40:17 UTC | #13

As discussed with @cryptocheshire, we should consider with #marketing as to how the model can be used to develop various AI-based social brand ambassadors, each trained/tuned for a specific audience/segment.

-------------------------

mehowbrainz | 2023-02-09 20:06:19 UTC | #14

At ZenonOrg we hired a new dev to refactor the Zenon.Org code while upgrading to Nuxt 3. We will be discussing internally how zenon.org pages + docs.zenon.org content can be transformed to fit such model in the future.

-------------------------

mehowbrainz | 2023-02-09 20:12:17 UTC | #15

Topic moved to #development:funding-staging

-------------------------

mehowbrainz | 2023-03-15 18:08:29 UTC | #16

If we want to expedite the delivery of such AI assistant, @Zashounet tagged me on this: https://www.intercom.com/ai-bot

I would then:

* Explore the idea of converting Docs.Zenon.Org GitBook to Intercom's Help Desk solution (for technical content management).
* Explore if we could automatically feed data source content into the Intercom Help Desk via APIs, i.e. tagged Discord/Telegram/Forum/Website content. From a first glance at their docs, it looks like their Help Center API allows us to create/update/delete collections and sections. This would simply be a game of coding an aggregation method from Discord, Telegram, Forums and Websites. Easily doable. This way we could source content from the Help Centre, but also from verified pushed data from Discord/Telegram/Forums. This is something that the Zenon.Org developer can likely be assigned via an AZ proposal.

Looking at Intercom's product suite... it looks very powerful for marketing as well. Will be evaluating the idea to build on their stack.

[poll type=multiple results=always min=1 max=1 chartType=bar]
* Yay
* Nay
[/poll]

-------------------------

mehowbrainz | 2023-03-17 20:44:18 UTC | #17

Update: ZenonOrg got approved for the [Intercom Early Stage Program](https://www.intercom.com/early-stage).

The discounted subscription expires March 2024. I quote:

* You get a 95% discount on *everything*
* Early Stage includes [Support](https://www.intercom.com/customer-support-software) Pro (10 seats) & [Customer Engagement](https://www.intercom.com/customer-engagement) Pro (5 seats)
* You’ve also got the [Product Tours](https://www.intercom.com/product-tours) add-on

Time to get started on the Intercom implementation on Zenon.Org :slight_smile:

-------------------------

mehowbrainz | 2023-08-22 17:52:04 UTC | #18

I tested a way to get the forum's sitemap urls and read all the content using a using an LLM service and local vector store (with gpt-4), then I asked it questions:

> Question: Even though the text does not provide specific information about what the community is complaining about, tell me what you can assume they're complaining about.

> Response: The community appears to be expressing concerns about several aspects of their project, which is likely a software or platform development given the language used. Key issues raised include:

> 1. A lack of clear goals and strategy, particularly for attracting and focusing on new users. There's a belief that the current approach is too broad and not targeted enough.

> 2. Concerns over their content and social media strategy, with criticism that the content is not adequately tailored or distributed to their intended audience.

> 3. The use of key performance indicators (KPIs) and tracking metrics not providing adequate insight into the performance and impact of their efforts.

> 4. A lack of a clearly defined duration for certain activities and projects.

> 5. The budget allocation for various tasks is called into question, with some believing it to be excessive for the proposed goals.

> 6. There's also a discussion about the need for more transparency on the roles of the team and the features they plan to implement.

> 7. Some community members are also pushing for attention to be given to bugs and issues in their platform, Syrius.

> 8. Lastly, there's a sentiment that the community needs to do more for the project, including increasing awareness initiatives and creating content to attract developers. There's a call for more active participation from the community and the pillars.

-------------------------

dat_she_pepe | 2023-08-22 18:19:24 UTC | #19

Why not using ChatGPT contexts with their API?

https://www.searchenginejournal.com/chatgpt-custom-instructions/492228/

Having our own model seems overkill and ressource consuming.

-------------------------

mehowbrainz | 2023-08-22 19:59:44 UTC | #20

That's not the same feature, that one allows you to set a context before a conversation. Kind of like a default profile i.e. "Act like a doctor".

The idea of exporting sitemap urls + reading the content is a little more complex as no good browser plugins in GPT4 can read large sitemaps properly. Many error out. I found a [GitHub](https://github.com/mkwatson/chat_any_site) project which focused on sitemap urls exclusively (using openAI api), wanted to test the viability and performance. If ever built for Zenon, it would be tailored to the ideas in this thread.

-------------------------

coinselor | 2023-08-22 20:08:30 UTC | #21

OpenAI recently released GPT 3.5's ability to be fine-tuned, literally 30 minutes ago.

https://openai.com/blog/gpt-3-5-turbo-fine-tuning-and-api-updates

A fine-tuned version of 3.5 should literally outperform everything else out there. Process seems very straight forward, upload data, run the fine-tuning process, call the new model.

-------------------------

dat_she_pepe | 2023-08-22 23:18:47 UTC | #22

Let me try it with my TB database of pornhub transcript.

-------------------------

coinselor | 2023-09-11 23:08:47 UTC | #23

Building on @mehowbrainz's idea, I believe we should create an AI tool that benefits everyone in our ecosystem, from developers to meme creators.

I propose a community-driven initiative to gather resources for fine-tuning the ChatGPT 3.5 model. Some potential data sources include:

* Whitepapers
* Medium articles
* Tweets
* Hypercore/ZenonORG forum posts
* Selected TG messages (e.g., from Kaine, George)
* Community updates
* Network codebase

Imagine the potential: we could even craft specialized models, like a Sigli support bot.

Though I'm not an expert, my experience with Langchain and LlamaIndex gives me a unique perspective. Let's consider future-proofing our data. For instance, a tweet might be structured as:


```
{
  "created_at": "2023-09-11T23:54:40Z",
  "type": "tweet",
  "text": "This is a tweet.",
  "username": "zenon_network",
  "media": {
    "amount": 1,
    "ipfs_url": "ipfs://QmX7a795B24k72s95x8348fX46529d8795864493587f68c"
  }
}
```
While we're currently focused on text, I believe we should also incorporate multimedia. It's likely that multimodal capabilities will emerge soon, and we should be ready. We can discuss data optimization later.

Unfortunately, Twitter data might be challenging to gather, but we can streamline the process for other sources once we finalize a data schema.

-------------------------

