# Heathen Engineering Standards

## Our Philosophy

At Heathen Engineering, development is treated as a **living, iterative system**. Each project follows a structured progression from concept to end-of-life, providing clarity, traceability, and quality at every stage. This lifecycle also gives our B2B clients insight into how we plan, produce, and support both games and tools.

We deliberately separate **design and iteration** from **production**, allowing teams to experiment and refine ideas without impacting the final deliverable. When production begins, all content is fully release-ready and aligned with the project’s objectives.

### Why Should You Care?

If you plan on developing professionally, having a structured **rigour** around your engineering practice is not just recommended—it’s essential for accessing supports, financing, and other programs.

{% hint style="success" %}
We are Irish, so we use Irish examples.\
Do note that many regions offer some form of support; while our examples are Irish, the concepts here apply broadly.
{% endhint %}

For instance, in Ireland, there is the "Digital Games Relief," where up to 32% of qualifying expenditure can be recovered as a tax credit. To access this or similar programs, you must document your project's lifecycle, particularly the phases considered "qualifying exercises." Typically, this applies to **production** activities—but what counts as production?

## Incubation

The start of everything and the least "rigid" phase. During incubation, we **conceptualise and prove ideas**, but nothing is committed or "set in stone." Many solo projects spend most of their time in this phase, and in some cases, projects may even ship directly from here (experiments, previews, etc.).

The critical part of incubation is defining **when it ends**, as this marks the transition either to production or to project termination.

### Concept

This term is widely used in game development, though interpretations vary. In general, it refers to **brainstorming, theorising, or ideation** about what could be done and what you want to do.

There are typically **no supports or credits** for this phase. The goal is to **minimise time and expense** while ensuring only viable concepts progress. To aid in this, we introduce a structured sub-phase: **Pre-Production**.

### Pre-Production

Pre-production is a more **rigorous extension of concepting**. While it still involves ideation and typically **does not qualify for most supports**, it is structured enough to allow early filtering of ideas—either modifying them to be viable or discarding them entirely.

During pre-production, we effectively **"build" the game in theory**—using paper, pencil, and planning tools. This may include creating a few **Minimal Viable Products (MVPs)** to test feasibility and fun, or conducting small **proof-of-concept exercises** like systems or mini-games.

Importantly, **no production-ready code or engine projects have been created yet**. Any sandbox engine projects used are experimental and **will never be shipped**; they are temporary tools for testing ideas.

The most critical output of pre-production is **not code, artwork, or game engine assets**, but structured documentation and planning, as detailed in the following sections.

### Market Analysis

Market Analysis involves researching the current market in relation to your idea or concept to understand potential reach, audience size, and revenue expectations. Consider factors like **marketing capacity**, **platform reach**, and **user monetisation potential**. This analysis is crucial later for setting realistic pricing and assessing overall project viability.

#### How to Do This

For game development, you can use tools such as **Steam Spy**, **SteamDB**, and review similar games to understand their performance. If your budget allows, professional market research firms can provide deeper insights, often in collaboration with marketing agencies.

#### Why Do This

The outcome provides a **monetary range** estimating how much the project could realistically earn, given your resources and market conditions. This helps in decision-making and planning during pre-production.

### Bill of Materials

Also known as the **BOM**, this is a comprehensive list of everything required to deliver your project. For a game, this includes every **NPC**, **item**, **environment**, and ideally, every element within those environments.

The purpose of the BOM is to provide a **realistic estimate** of time and cost, forming the foundation for budgeting, scheduling, and resource planning. It is also a prerequisite for producing your **Return on Investment (ROI)** analysis.

#### Granularity

The level of detail in your BOM is up to you. Greater granularity offers more accurate budgeting but increases the chance of error. The general guideline is to detail the BOM enough to fit within the **budget range you can afford**. For example, if your budget is €100–200k, structure your BOM to reflect **tens of thousands in costings** for each component.

### Return on Investment

Also known as **ROI**, this metric helps determine whether to pursue a project further. It can also be used to compare two viable projects to see which is more advantageous to undertake.

ROI is calculated by comparing your **Market Analysis** against your **Bill of Materials (BOM)**. A negative result indicates that the project should either be **adjusted** by reducing the BOM or increasing the Market Analysis—or **shelved** for later.

#### Considerations

ROI is not solely about monetary gain. If your company exists only to make money, you may fail to achieve other valuable goals. Projects can also provide **reputation**, **experience**, and other strategic advantages. Incorporating these non-monetary factors can improve long-term ROI and help guide your decision-making.

#### How to use it

Condense your ROI into a **single scalar value**.

* If the value is negative, do not proceed with the project as-is. Adjust the design or budget, or defer the project.
* Compare this ROI with other ideas. The project with the higher ROI—monetary or otherwise—is typically the better choice.
* Ensure non-monetary gains, such as **reputation** or **experience**, are factored into your assessment.

## Production

The **Production** phase is generally where expenses become **eligible for tax credits, cultural programs, and other supports**. To validate that this phase meets government or sponsor requirements, you must have completed the **Pre-Production** phase.

This is also when you establish your official **project repository**—GitHub, Perforce, or similar—and set up the **codebase and game engine** for production work.

> **Important:** Never use sandbox projects for production. A production project should contain **only production-ready content**. Do not import demos, store assets, or unapproved content directly. Always pull assets into sandboxes first, clean, fix, and approve them before adding to the production project.

Once this is done, you now have:

* **Market Analysis**
* **Bill of Materials (BOM)**
* **Return on Investment (ROI)**

With these, you can efficiently brief **contractors, artists, programmers**, and other team members, providing a clear, preformatted list of exactly what is needed and when. This also enables accurate budgeting, time allocation, and progress tracking—essential for estimating **release dates** and planning **Go-Live** and **Operations** phases.

{% hint style="danger" %}
**Pro-tip:** Keep your mouth shut.

Unless you are a seasoned veteran who knows with high reliability exactly what the output of production will be, avoid marketing your game until it is near complete or fully complete.

You get **exactly one first impression** with each potential user. Do not spoil it by showing an incomplete project—or worse, just an idea. Make sure anything you reveal is something you can deliver on or exceed. Even AAA studios get this wrong, overhyping projects they cannot deliver. You, however, do not have millions to spend on correcting hype mistakes—so just don’t.

Wait until your project is set in stone, nearly complete, and ready to deliver. This is achieved through the **Post-Production** subphase.
{% endhint %}

### Post-production

Sometimes called "content complete" or "Gold" as in "the project has gone Gold".

This phase indicates that all content required to ship the game is complete, and base testing and optimisation have been performed. You now have everything necessary to begin validation testing and packaging in preparation for operations.

Post-production is also when you start preparing marketing assets: gather screenshots, plan ad campaigns, release demos, or participate in events such as Steam Next Fest.

It is critical to perform these activities only once you are confident of your game’s go-live date. For Steam releases, this is also when you begin building wishlists. You should aim to meet your wishlist targets before launching, or gather as many wishlists as possible if hitting the target is unlikely. For more advice on launching a game on Steam, see our [Launch article in the Steamworks Knowledge Base](https://app.gitbook.com/s/kfE3ZAs6TeNW5sBM2C3i/launch).

## Operations

Once your game is complete, tested, and validated, and your marketing efforts have built anticipation, it’s time to press the big green "Launch" button (a Steam feature) and begin operations.

Launching does not mark the end of your work—it has only just begun. Game creation is the easy part compared to managing live operations. Even with thorough testing and validation, expect potential issues such as bugs, critical errors, and refund requests.

Have a support plan in place: tools like Zendesk can help manage incoming cases, and if possible, establish a community site with managers to engage your players. For Steam releases, the [Community Hub](https://app.gitbook.com/s/kfE3ZAs6TeNW5sBM2C3i/features/community-hub) is an invaluable resource.

Operations are ongoing for as long as your product is available and may continue for a period after delisting. Launching establishes a legal obligation between you and your customers, so maintain your responsibilities diligently.

## Archival

Every product reaches the end of its lifecycle, and at that point, you have both ethical and, increasingly, legal obligations to manage its end-of-life and archival. This process ensures that your product is properly retired while protecting your company, your users, and any sensitive data associated with the project.

Archival planning should consider several key areas:

1. **Data Retention and Deletion**\
   Any user data collected during the game’s operation—accounts, progress, purchases, analytics—must be handled according to relevant privacy laws (e.g., GDPR in Europe, CCPA in California). Decide what data you will retain for historical, legal, or support purposes, and what must be securely deleted.
2. **Code and Asset Preservation**\
   Maintain a full archive of the final codebase, assets, and project files. Even if the game is no longer live, retaining these files ensures that patches, legacy support, or future re-releases remain possible. Include version history, dependencies, and build instructions to prevent future teams from losing context.
3. **Licensing and Third-Party Dependencies**\
   Document and store all third-party licenses, assets, and tools used in the project. Some licenses may have expiry dates or restrictions that affect your ability to maintain or republish the game. Ensuring this documentation is complete avoids legal complications later.
4. **Documentation**\
   Archive all design documents, BOMs, ROI analyses, QA reports, and operational notes. This provides historical context for your team, supports compliance requirements, and enables auditing if needed. A thorough archive can also inform future projects, preventing repeated mistakes and guiding improved workflows.
5. **Server and Online Services Decommissioning**\
   For live services, plan a structured shutdown: notify users in advance, provide options to export or save data where possible, and ensure online services are turned off securely. Retire backend servers responsibly to avoid security vulnerabilities.
6. **Financial and Legal Closure**\
   Ensure that any remaining financial obligations, royalties, or contractual agreements are completed. File final reports for government or funding bodies if applicable, and confirm that all legal and contractual responsibilities have been fulfilled.

Archival is not just a formality—it protects your company, maintains your reputation, and ensures that your obligations to players and regulators are met. Properly planned archival allows you to close a product responsibly, giving your team clarity to focus on new projects without leaving unresolved risks behind.
