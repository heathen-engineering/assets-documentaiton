# Heathen Engineering Standards

## Our Philosophy

At Heathen Engineering, we approach development as a **living, iterative system**. We treat each project as a structured progression from concept to end-of-life, ensuring clarity, traceability, and quality at every stage. This lifecycle also allows our B2B clients to understand how we approach planning, production, and support for both games and tools.

We separate **design and iteration** from **production**, enabling teams to experiment and refine without affecting the final deliverable. This ensures that when production begins, all content is release-ready and consistent with the project’s goals.

### Why should you care?

If you plan on doing this professionally, having a "rigour" around your engineering practice is not just critical but required if you hope to avail of supports, financing, etc.

{% hint style="success" %}
We are Irish, so we use Irish examples, \
Do note that many regions offer some sort of program; while our examples are Irish, the concepts we talk about here will apply to most areas.
{% endhint %}

For example, here in Ireland, there is a "Digital Games Relief" where up to 32% of qualifying expenditure can be recovered as a tax credit. To avail of this or any similar program from any government, region, organisation, etc., you will be required to document your project's life cycle and, in particular, the phases of it as the "qualifying exercise" clause usually only applies to specific activities, typically "production" only ... so what is "production"

## Incubation

The start of everything and the least "rigid" phase. Here, we concept and prove ideas, but nothing is committed or "set in stone". This is where most solo projects spend most of their time and may even "ship" form. It is important to define when this phase "ends" more so than when it starts, as the end of this phase marks the start of production, or the death of the project, as the case may be.

### Concept

This is the typical term we use in Game Dev, though we all have a different meaning for it. In general, however, it is the "brainstorming" or "theorising" or "ideation" about what you could do and want to do.

Generally, there are no supports or credits for this phase. Thus, you want to minimise the time and money spent here while still ensuring only viable concepts move on. To help with that, we use the following sub-phase

### Pre-production

This is a slightly more "rigorous" version of concepting. It's still ideation, so most supports won't apply to this process, but it's structured enough to help "early out" ideas that just won't work or modify them so they can work.

Note that in pre-production, we will effectively "build" the game in theory, that is, with paper and pencil. We may go as far as to do a few "MVP" or "Minimal Viable Product" so we can test if something is possible, and if it's even fun. And we could do some "Proofs" where we create a system or a mini-game to test a theory. But we aren't "creating" anything, we haven't even created the code/engine project yet that will be used to build the game ... it's all just "theory" at this point, and maybe a few messy sandbox engine projects that we will NEVER ship and will definitely throw away when we are done with them.

The most important "output" from this phase has nothing at all to do with code, game engine projects, artwork, etc. ... it's as shown below.

#### Market Analysis

This is the process of researching the current market relative to your idea/concept to get a feel for how many possible customers you could reach ... take into account limits on your marketing capacity, platform reach, etc. This should also express how much per user you might get for your product. This will be useful later when determining the price you should set for your product.

How do you do this?\
For game dev, you can use tools like Steam Spy, Steam DB, etc., review similar games and get an idea for how they performed. If you have the budget, there are professional firms usually associated with marketing firms that can help you with this process.

Why do this?\
The result is basically a monetary range telling you how much you're likely to make from this project, given your limitations and the market limitations.&#x20;

#### Bill of Materials

Aka the BOM: This outlines everything you think will be required to deliver this project. For a game, this would be a list of every NPC, every item, every environment, and ideally every thing in every environment.&#x20;

The point of a BOM is to enable you to do a "real" estimate on how long and how much this project will cost. It's required for the next output, which is the most important output of pre-production.\
How "granular" you get with your BOM depends on you; the more granular, the more detailed your budget, but also the higher chance of error.

The general rule of thumb to use is to go as detailed as you need to fit within the "range" of the budget you can afford. For example, if you can afford 100-200k ... then get your BOM's level of detail down to 10s of thousands in costings.

#### Return on Investment

Aka the ROI: Simply put, this tells you if you should or should not pursue this project further. It can also be used to compare 2 viable projects to see which would be better to do now. How you create the ROI is fairly straightforward: you compare the market analysis to the bill of materials. If the result is negative ... you shouldn't continue with this project ... or you should adjust the project such that the BOM is smaller ... or the Market Analysis is bigger.

Considerations:\
Remember, it's not always about money ... if your company exists to make money, you will fail. Your company exists to ... well, that is up to you, but probably something like "make fun games people want to play" ... as a result, you may "value" building a reputation, and this is correct, with a positive reputation, you can reach a wider market, and future games will have a more positive monetary ROI. The point is, don't just compare € to € ... consider non-monetary values as well... how much is experience, reputation, etc, worth to your company/team/venture.

How to use it!\
An ROI should boil your project down to a single scalar value, e.g. a whole number.&#x20;

If that number is negative ... you simply should not do this. Either go back and adjust the design to lower the BOM or increase the Market Assessment ... or shelve this project for later.

Next, compare the ROI of this project with other ideas you have... the one with the "bigger" ROI is usually the better idea, e.g. it will result in the most gain for your company monetarily or otherwise ... remember your ROI assessment should "value" non-monetary gain as well, such as reputation, experience or other "gains"

## Production

This phase is generally "eligible expenses" for tax credits, culture programs, etc., validating that this phase isn't just smoke and mirrors and does meet the requirements of your government, sponsor, etc., means you do need to have completed the Pre-Production phase described above.

{% hint style="warning" %}
This next part is VERY important, read it carefully.
{% endhint %}

This is also the point at which you create your "Project", e.g. you GitHub, Perforce, etc., the code base, game engine, and so on.&#x20;

You ABSOLUTELY DO NOT use one of your sandboxes. A production project should never have anything in it that is not production-ready. So you NEVER import demos, store assets, etc. directly ... you pull those into sandboxes, clean them, fix them, approve them and only then do you pull that into the production project.

As a result, the idea that "O that AI art just slipped in" is a blatant lie or gross incompatibility...  ( looking at you, EA )

{% hint style="success" %}
If you strictly follow the above, you will ensure

* Your project is fully auditable and thus eligible for Tax Credits, Culture grants, etc.
* Your project is pure and isolated, and thus an auditable proof against DMCA / IP infringement take-downs
* Your project is lean and efficient, with no bloat from unused code, placeholder assets, or unoptimized resources.
* Maintainable, this project is 100% self-contained, meaning any 3rd parties are copied into it, not simply referenced. This ensures that in 5 years, when you need to rebuild and release a patch because Unity has a critical security flaw (as happened in 2025), you can do so without needing to update 5 years of updates from all your 3rd-party tools.
{% endhint %}

Okay, so you now have a valid

* Market Analysis
* Bill of Materials
* Return on Investment statement.

You can use these contract artists, programmers, etc., providing them with a clear, preformatted list of exactly what you need and when you need it. You will also have a clear understanding of how much each part of your game should cost in time and money, and so you will clearly see your % progress, helping you more effectively estimate release date ... a critical step for go-live and operations planning.

{% hint style="danger" %}
Pro-tip

Keep your mouth shut.&#x20;

Unless you're a seasoned veteran who knows with a high degree of reliability precisely what the output of production will be, you should keep your mouth shut and not start marketing your game until it's near complete ... or complete.\
\
You get exactly one 1st impression with each potential user of your project. Do not spoil it by showing an incomplete project or worse, just an idea ... and make very sure what you do show them, you deliver on or exceed. Even AAA get this wrong and hype up something they can't deliver ... you, however, do not have millions you can spend in marketing to fix that mistake ... so just don't make it.\
\
Shut your mouth until your project is set in stone, nearly complete and about to deliver... we do this via the "Post-production" subphase.
{% endhint %}

### Post-production

Sometimes called "content complete" or "Gold" as in "the project has gone Gold".

This means you have completed all the content needed to ship the game, you have base testing and optimisation done, and thus you have everything you need to start validation testing and packaging in preparation for operations.

This is when you gather screenshots for marketing, when you start running ads, and when you release your demo, join in on Steam Next Fest, etc. You make sure you do this only once you KNOW when your game will -( CAN )- go live.

If you're releasing on Steam, this is when you start building Wishlists ... you DO NOT want to go live until you hit your wishlist targets or if you can't hit that target when you have gathered as many wishlists as you can. For more advice on launching a game on Steam, see our [Launch article in the Steamworks Knowledge Base](https://app.gitbook.com/s/kfE3ZAs6TeNW5sBM2C3i/launch).

## Operations

So you have your game complete, tested, validated, you have a pile of wishlists, and your marketing team has whipped your target market into a mild fury, hungry for your game ... great ... press the big green "Launch" button (a Steam thing) and start operations.

Your work is not "done" when you launch your game. It has only just started. Creating the game was the easy part, and if you did a good job in testing and validation, you should have a smooth launch ... most games do not have a smooth launch though, so be prepared for bugs, critical issues, refunds and more.

Have a support plan ready, set up Zendesk or some similar tool to help you manage incoming support cases. If you can set up a community site and enable community managers to help manage your players. If you're on [Steam, the Community Hub](https://app.gitbook.com/s/kfE3ZAs6TeNW5sBM2C3i/features/community-hub) can help here.

Understand that this will be an ongoing line of work for as long as you offer this product for sale and for some period of time after you delist the product. You have launched a game and established a legal obligation between you and your customers.

## Archival

At some point, every product ends, and you have an ethical and increasingly a legal obligation to plan for the end of life and archival. Exactly what this means for your project depends on your product and the regions it has operated in. Simply be aware that you can't just release it and walk away; you do have obligations under the law in most regions.
