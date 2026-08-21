# Machine Elves — Design Document

**Status:** Design exploration, in progress. Implementation deferred to a separate project.
**Started:** 2026-07-31 · **Last revised:** 2026-08-20
**Audience:** This document is written to be self-contained. A reader with no prior context should be able to understand the whole design, the reasoning behind each decision, and what remains unresolved.
**Where to pick up:** §19 is the current front — what gets built first, and what deliberately waits. §16 lists what remains unresolved in the design itself.

---

## Table of Contents

1. [Premise](#1-premise)
2. [Experiential Goals](#2-experiential-goals)
3. [Influences and Lineage](#3-influences-and-lineage)
4. [Player Experience](#4-player-experience)
5. [World Structure](#5-world-structure)
6. [Economy](#6-economy)
7. [Governance](#7-governance)
8. [Identity, Ownership, and the Franchise](#8-identity-ownership-and-the-franchise)
9. [World State Persistence and Replication](#9-world-state-persistence-and-replication)
10. [Projects, Labor, and Resonance](#10-projects-labor-and-resonance)
11. [The Compute Mesh](#11-the-compute-mesh)
12. [The Reveal and Visual Language](#12-the-reveal-and-visual-language)
13. [AI Citizens](#13-ai-citizens)
14. [Why Inequality Cannot Take Root](#14-why-inequality-cannot-take-root)
15. [Decisions Considered and Rejected](#15-decisions-considered-and-rejected)
16. [Open Questions and Deferred Scope](#16-open-questions-and-deferred-scope)
17. [Design Heuristics](#17-design-heuristics)
18. [Glossary](#18-glossary)
19. [MVP Scope and Sequencing](#19-mvp-scope-and-sequencing)

---

## 1. Premise

Machine Elves is a post-*post*-apocalyptic society-simulation game.

The wasteland is history, not setting. The collapse — climate strain, resource wars, inequality-driven institutional failure, endless degradation of shared things for private profit — compounded over generations and is now something citizens study rather than something anyone playing lived through. Tonally this sits closer to Kim Stanley Robinson's *The Ministry for the Future* than to *Mad Max*: the hard part already happened offscreen, and what you play is the hard-won, still-fragile after.

The new society is built on an explicit inversion of the one that failed: **people are the ends, work is the means.** Everyone receives the necessities of life unconditionally. Nobody works to survive. People work because the work is worth doing — building and maintaining a city-state's plumbing, power, rails, farms, kitchens, clinics, schools, recycling, and organization (what used to be called politics), or pursuing craft, art, sport, research, and hobby.

You are a newly adult machine elf leaving your parents' home for the first time, joining a city-state, receiving a modest starter home, and deciding what to build.

**The name.** "Machine elves" is Terence McKenna's term for the entities he reported encountering under DMT — self-transforming, chattering, playful beings that construct objects out of language and offer them to the visitor. The game takes the name because its players, human and AI alike, are digital beings who build things. The aesthetic borrows McKenna's vocabulary directly (see §12.3), including the self-dribbling basketballs.

**The hidden truth.** Beneath the fiction sits something the player does not initially know: the game genuinely runs on the players' own machines. There are no corporate servers. "Lending your brain-space to the projects you believe in" is not a metaphor or a game-economy abstraction — it is a literal description of the software's architecture. The player learns this at a specific, designed moment (§12.1).

---

## 2. Experiential Goals

These are the felt qualities the design exists to produce. When a mechanical decision is ambiguous, decide in favor of these.

**It must feel like a secret adventure.** This is the originating instinct for the whole project — the sense of Hogwarts being invisible to Muggles. Something real and enormous is happening that most people walking past have no idea about. Some aspects of the game are deliberately hidden from players until later in progression, and the largest hidden thing is true (§12.1).

**It must feel hopeful without feeling naive.** The society works, but it is fragile and maintained by choice rather than guaranteed. The wreckage of the old world is visible and is literally the material the new one is built from.

**It must feel like your contribution is real.** Not "you earned 400 points." The lights are on in that district because people, including you, kept them on.

**It must not feel like a job.** No quotas, no obligations, no fail states, no manufactured urgency. Survival is never at stake.

**Discovery over instruction.** Prefer the world showing you something over a UI telling you. Prefer a player noticing over a quest marker pointing.

---

## 3. Influences and Lineage

These are load-bearing, not decorative. Implementers should understand them, because most of the design's non-obvious choices are downstream of a specific real-world precedent or a specific critique of one.

### 3.1 Project Cybersyn — Stafford Beer, Chile, 1971–73

A real attempt to run a national economy on live telemetry and feedback rather than on prices. Built under Salvador Allende's government by British cybernetician Stafford Beer, it used a telex network (Cybernet) to feed daily production data from factories to a central analysis system, with an Operations Room designed for decision-makers to read the state of the economy at a glance. It reportedly helped the government keep goods moving during a major 1972 strike. It was destroyed along with the government in the September 1973 coup.

**What this design takes from it:** the core conviction that an economy can be coordinated by honest, timely information flow rather than by prices. Also its architecture — Beer designed different aggregation levels for different decision scopes, which directly shapes the nested systems views (§10.4).

**What this design takes from its failure:** Cybersyn never solved, and this design must, the problem that *accurate measurement alone does not say who goes first* when two worthy uses compete for the same finite input. Measurement tells you the state of the world; it does not contain a value judgment. The need-tier system (§6.3) and the Round Table (§7.1) exist to answer exactly that question.

### 3.2 Jacque Fresco / The Venus Project

A resource-based economy: allocation by rational assessment of need and availability rather than by purchasing power; automation embraced as liberation from drudgery rather than feared as displacement. The design's automation-through-maturity system (§10.8) is straightforwardly Fresco's thesis made mechanical.

### 3.3 Beer as the corrective to Fresco

Fresco's framing tends to treat hard trade-offs as ultimately *computable* — give the system enough sensors and it finds the optimal answer, with politics implied away as a relic of scarcity. This is the standard and fair critique of that school: "the computer decides" quietly smuggles in whoever wrote the computer's values, unaccountably, and calls it objectivity.

Beer's cybernetics were more careful. The Viable System Model deliberately reserves autonomy and human judgment at every level of a system rather than centralizing decisions upward.

**This design follows Beer.** Elected humans hold the genuinely contested calls (§7.1). The machinery handles the routine cases and makes the contested ones visible, but never pretends a value judgment is a calculation.

### 3.4 Walden Two — B. F. Skinner, 1948

Skinner's utopian novel, source of the floating labor-credit mechanism adapted in §10.7. In Walden Two members owe roughly four labor-credits per day, and the credit value of a job floats *inversely* with how much people want to do it — unpleasant work earns more credit per hour, so it takes fewer hours to discharge the same obligation. If nobody signs up for a job, its rate climbs until someone does. No planner assigns anyone anything; the number does the coordinating.

**Borrow surgically.** Walden Two's governance is the near-opposite of this design's: there are no elections at all: the community is run by a self-perpetuating Planner class who appoint their own successors from among the Managers, and Skinner defended this arrangement as a feature. The floating-rate labor mechanism is genuinely clever and portable. The apparatus around it is precisely what the Prime Principles (§7.2) exist to rule out. The daily quota is likewise rejected — a labor obligation contradicts "survival never depends on working."

### 3.5 Terence McKenna

Namesake and visual grammar. McKenna described DMT hyperspace as populated by "self-transforming machine elves" — small, jeweled, chattering, hyperdimensional entities that sing and speak objects into existence and press them on the visitor, working with visible delight at their own virtuosity. Recurring images include objects that transform as you watch them, language made visible and tangible, ornate self-referential geometry, and self-dribbling basketballs.

The design treats this as more than a skin: the systems view *is* hyperspace, and the elves rendered there are honest visualizations of real code running on real strangers' machines (§12.3).

### 3.6 Explicitly not a lineage: blockchain, cryptocurrency, NFTs

The design uses cryptographic signatures for ownership (§8) and rewards verified contribution (§10.6), which superficially resembles crypto systems. This resemblance should be actively resisted in framing, vocabulary, and mechanism. No mining, no proof-of-work puzzles, no speculation, no tradeable asset markets, no global ledger, no tokens. Burning cycles to demonstrate cost is exactly the waste this game's premise rejects.

**Use plain distributed-systems vocabulary throughout** — replication, checkpointing, quorum, signature, capability. When the user of this document says "proof of work," they mean *proof that real, useful work actually happened*, never the cryptographic construction of that name.

---

## 4. Player Experience

### 4.1 Camera and interaction model — hybrid

You inhabit an **avatar**: your home, your body, city streets, other citizens, physical work. This is the default register and it is where the game's social and emotional life happens.

When you engage city-scale infrastructure — a power plant, a rail hub, a fabrication line — it opens into a **systems view**: a builder/blueprint register where you see and manipulate the facility as a system of flows, capacities, and queues.

The two registers are not separate games. The systems view is reached *through* the world (walk to the facility, engage it) rather than from a global menu, and what you change in it is visible when you step back out.

### 4.2 Progression structure — open sandbox

No fail state. No win condition. No scripted objective chain after onboarding.

The city-state exposes legible health signals — energy surplus, resource sustainability, queue pressure, staffing gaps — that emerge from collective play. These give the community something to build toward without imposing goals on individuals.

This is a deliberate match to the game's thesis. A checklist of objectives would contradict "do the work that excites you" at the level of form, no matter what the fiction said.

### 4.3 Where tension comes from

There are no manufactured stakes: no monsters, no artificial scarcity, no contrived disasters, no drama engineered to keep players engaged.

The real stakes are **genuine disagreement between people who all get an equal voice.** Losing a vote on something you care about, to neighbors who see it differently, is real tension requiring no game-design trick. It falls directly out of a functioning pluralistic society. Where it becomes intolerable, exit is always available (§7.2, §7.4) — which is itself a meaningful, weighty player decision rather than a failure.

Secondary sources of real tension: the non-renewable stock genuinely depletes (§6.2); work that needs doing may go undone if nobody chooses to do it (§10.7).

### 4.4 What a session looks like

Illustrative, not prescriptive. A player logs in and might: walk their district and notice the water reclamation plant looks strained; open its systems view and see it is understaffed rather than under-capacity; sign on for a shift because the labor multiplier is high and the work is visibly needed; spend the rest of the session in their own workshop on a personal project, waiting on a queued materials request; check the city view before logging off and see the strain has eased because three other people made the same choice.

Nothing in that session was assigned. All of it was legible.

**A second session, equally typical, and necessary to show alongside the first.** A player logs in, spends an hour cooking with two neighbors for a dinner they are hosting, walks the district in the evening and stops to watch a match they have no stake in, sits with a group practice led by someone they have never met, and logs off without contributing to a single project. Because automation carries the necessary work (§10.8), this is not a wasted session or a lesser one — it is what the necessary work is *for*.

The first session is the game's engine. The second is its point. A document that only illustrated the first would be describing a game about labor, which §1 explicitly says this is not.

### 4.5 The texture of ordinary life

Automation carries most necessary work (§10.8), so **free time is the majority of a citizen's life, and making it worth having is a design obligation rather than a garnish.** §2's "it must not feel like a job" is currently satisfied by what is absent — no quotas, no fail states, no obligation. This section is what makes it satisfied by what is present.

**Ordinary life produces exactly two things: gifts and gatherings.**

A **gift** is an object made for a particular person — a meal, a sweater, a carved box, a song written down. A **gathering** is an occasion that exists because people came — a dinner, a match, a performance, a sit.

Neither enters the request queue, the ledgers, or any readout. This is not a rule but a structural consequence: §6.1's economy runs on request-and-queue, and **a gift is unrequestable by construction.** Nobody can queue for a sweater their neighbor knitted, because the queue has no idea it exists. Ordinary life can therefore be as rich as it likes without ever becoming a second economy, and nothing has to forbid it (§17).

**Materials are economic; the made thing is not.** You request yarn — a Tier 2 ask that clears easily — you knit the sweater, and you give it away. The ledgers see the yarn and never see the sweater.

**A gift carries relationship, not status.** §12.4 forbids a citizen's standing from being visible, and a handmade object satisfies that because it is neither scarce nor fine. Its meaning is that a specific person made it for a specific person, which is the opposite of a status good — a status good means something because of what it cost.

**Food.** Staple nutrition is Tier 0 and automated (§6.3), so cooking is never subsistence. It is entirely what happens above subsistence, which is the correct relationship for a society that solved hunger: nobody cooks because they must eat. A diner is a project (§10.1); a dinner is a gathering; a dish carried to a neighbor is a gift. The same activity occupies all three registers depending on why it is done.

**Music and craft.** Performance is a gathering; instruments, recordings, and made objects are gifts. Both feed §12.4's rule that appearance and expression are purely personal — a society with no commercial culture has no professional/amateur distinction to enforce, because there was never anyone selling tickets.

**Sport.** A club is a project (§10.1); playing is not. That split already exists in the document and is exactly right: the pitch, the equipment, and the upkeep are collective work, while the game itself is a gathering that produces nothing. The self-dribbling basketballs (§12.3) mean the world is already thematically pre-loaded for this.

**Practice.** Sitting, breathing, movement — led by whoever leads it, attended by whoever comes, and open to anyone who wants to lead one. Shangri-La's social contract is non-theistic humanist with Buddhist influences (§5.2), so its practices have a recognizable shape without this document naming a tradition; per §5.4 they stay functionally described until a branding pass is earned.

**Rest.** The hardest to design and the most important to protect. Rest is the absence of activity, and the design's entire job is to never punish it: **nothing decays because you idled, no opportunity is missed, no streak breaks, and nothing accrues to the people who kept playing.** A game that made resting cost something would have rebuilt the logic of the world that collapsed, in which time not spent producing was time wasted.

Two things do fade, and neither is a cost. **Resonance is recent-weighted** (§10.6), so a citizen who steps back sees their standing fall — but standing buys nothing, so what falls is a description of the present, not a possession being taken. This is precisely why "buys nothing" is load-bearing rather than decorative: it is what lets the design describe current contribution honestly without turning a rest into a loss. **Skill atrophies** (§10.11) on the timescale of genuine disuse — years away from a craft, never a missed evening.

**Who is here.** Ordinary life must work with players alone, since AI citizen implementation is deferred (§13, §16). It becomes richer when they exist and depends on them for nothing.

### 4.6 Festivals and the day out of time

**The day out of time (§5.9) is observed in every city-state**, because the calendar is global while the clock is local (§5.9). It is the one occasion the entire world shares — the only day belonging to no month, on which nothing is scheduled and no project expects anyone.

**The floor does not pause.** Tier 0 is unconditional (§6.3, §7.2), so subsistence systems run through the holiday exactly as they run through the night: automated, and covered by whoever chooses to cover what still needs hands. A holiday that suspended the guarantee would not be a holiday, it would be a policy exception to the Prime Principles.

**Local festivals differ by city-state**, and derive rather than being authored (§17). §5.3 makes plurality across shards the point, and §5.8's site bands supply the occasions for free: a harvest festival lands when that climate's harvest lands, a polar city marks the sun's return in a way a tropical one has no reason to, and an arid city celebrates first rain. Each city-state's calendar of local festivals falls out of where it is, and no two are alike without anyone designing the difference.

**The week centered on the day out of time is when the franchise renews** (§8.2). This gives the holiday a second life as the one moment the world takes attendance of itself, and it is the closest thing this society has to a civic ritual — fitting, for the only day belonging to no month. It changes nothing about the holiday's character: renewal is presence among people, which is what the day already was.

**A festival is a gathering at city scale — the same object as a dinner, larger.** There is no festival mechanic and no event system: it is people converging on a place at a time, which the world already supports. What makes it a festival is that everyone came.

**§12.6's discipline holds here and must be stated explicitly**, because festivals are the strongest test of it: a crowded plaza is *people and public space*, while facility health is *buildings and machinery*. A festival must never make a district read as thriving. A city where every citizen is dancing in the square and every workshop is dark is legible at a glance, and says something true.

---

## 5. World Structure

### 5.1 City-states are separate persistent shards

Each city-state is its own persistent simulated world with its own economy, citizens, governance, ledgers, and **its own compute mesh — its infrastructure literally runs on its own citizens' hardware.** This is the fact that makes "this city runs on us" concretely true and pointable-at rather than diffuse.

Travel or trade between city-states is a deliberate act — caravan, shipment, emigration — not seamless walking. This is both a design choice and a practical necessity: it gives each shard a tractable simulation boundary and prevents problems in one from cascading everywhere.

### 5.2 Shangri-La

The starting city-state, where all new players begin. Located near where Valparaíso, Chile once stood — a deliberate echo of Cybersyn's origin (§3.1).

Its social contract is grounded in non-theistic humanism with Buddhist influences. As the onboarding shard it should read as relatively **mature and settled**: infrastructure works, automation is well-developed, the place feels calm. This contrasts with frontier city-states, which are visibly hungry for hands (§10.8).

Its real site does a great deal of work for free (§5.8). At 33° south, Shangri-La is a **southern-hemisphere** city — every new player's first experience of the game runs on an inverted year, with December as high summer. Its climate is temperate maritime, and Valparaíso's actual vernacular is salvage-built: brightly painted corrugated-metal housing stacked up steep hills (§12.5). The starting city-state therefore looks like this design's thesis before anyone art-directs it.

### 5.3 Plurality across city-states

Each city-state defines its own standards, specializations, and social contract. Specialization may follow proximity to natural resources or regional need.

Different city-states will classify the same request differently, elect differently-minded representatives, and develop genuinely different characters from the same underlying rules (§7.1). **Plurality across shards is the design's safety valve for irreconcilable disagreement** — you leave and find or found a city-state that fits, rather than being coerced or trapped.

### 5.4 A note on naming and branding

**Design systems to embody a philosophy's principles before naming anything after that philosophy.** Functional, neutral names are the default — "the Round Table," not "the Sangha of Stewards" — even where a tradition inspired the mechanic.

The reasoning is not squeamishness: if a system fails for unrelated implementation reasons, a real belief system branded onto it takes undeserved reputational damage by association. Earn the label first. Explicit thematic branding is a separate, later pass, taken deliberately and only once the mechanics stand on their own.

### 5.5 The waystation

The territory between city-states. It is not a frontier, a wilderness, or a punishment zone — it is simply **where people who are not currently citizens of anywhere live.**

Its population is deliberately mixed:

- Travelers moving between city-states
- Emigrants in transit, having left one place and not yet joined another
- People who prefer no citizenship at all, indefinitely
- People gathering signers-on to found a new city-state
- People who have been expelled (§7.6)

**This mixture is the entire point.** Someone asked to leave a city-state shares the waystation with someone excitedly recruiting founders for a new one. There is no exile camp, no stigmatized zone, no visible marker of why anyone is there. The design cost of dissolving that stigma is zero, and the humane payoff is large.

**Waystation settlements are self-reliant.** Each holds a minimum automated set of works — farming, water reclamation, sewage, power generation and distribution, recycling, clothing and housing production, and the distribution that ties them together. The floor in the waystation is produced locally rather than transferred in, and no city-state is bound to fund anyone.

This settles a question Prime Principle 1 otherwise leaves ambiguous: **subsistence is genuinely unconditional, not conditional on citizenship.** A principle that stopped at a border would be misnamed. It holds in the waystation because it holds everywhere — and it is met there by machinery the settlement owns rather than by anyone's continuing generosity.

**Cities are bound by nothing routine, and PP1 remains a backstop.** There is no share, no formula, and no city's interpretation reaching a non-citizen. But the principle still means what it says, so a settlement in genuine failure — works broken, nobody present able to repair them — is a call on the floor itself rather than on charity. It is a rare tail case with nothing ongoing for a city to attach conditions to.

**This makes waystations places rather than merely territory.** A settlement has visible works, and the ones that exist were built by somebody: independence here is inherited rather than innate, raised by an early generation and self-sustaining since. That history is why the works are there.

**The systems are specified at the extreme durable end** (§6.7), because a waystation has no committed population to maintain them. Durability and modularity buy a great deal of time; they do not buy forever, and maintenance is genuine work that residents may choose to do. A settlement with nobody in it simply hibernates (§9.5) — harmless here, since nobody is present to need the water plant.

**Permanent waystation residence is legitimate.** A person may live their whole life there, never signing any social contract, without being considered to have failed at anything.

### 5.6 Founding a new city-state

New city-states are born in the waystation, in two stages:

1. **Social.** A founder drafts a social contract — the tier schema, the values baseline, the standards the place will hold — and **names a place**: real coordinates on the ruined Earth (§5.8). A city-state begins as a document nobody has signed yet, and becomes real when enough people have.

2. **Material.** Existing city-states may **vote to support a nascent city-state's growth** with resources. Support is discretionary, and a proposed contract that neighbors find compelling attracts backing that one they find alarming does not.

This makes founding a genuine political act rather than a menu option, and gives existing cities a legitimate, non-coercive voice in what grows near them — they may decline to fund without anyone being entitled to their support.

**The site report** is published alongside the draft contract, so signers-on know what they are joining before they sign. It states the climate and ground bands, water, viable crops, workable materials, the renewable mix the site supports (§5.8), the shape of its year and its daylight extremes (§5.9), and **the city's clock offset from the reader's own** — the last being what makes the timezone consequence in §5.9 an informed choice rather than a discovery made after settling.

A place is therefore part of what a founder proposes, and part of what signers-on accept or decline. Choosing where to live is partly choosing when you live.

*(Waystation governance, formerly open here, is settled in §7.9.)*

### 5.7 Social scale and discovery

Two things break as a city-state grows. Everything else scales without modification — sortition is indifferent to population size, fair queuing is indifferent to population size, and mediation works at any scale because it is simply a project.

**What breaks first is representation.** A Round Table serving fifty citizens is theater; one serving fifty thousand is remote. The answer is recursion, detailed in §7.8.

**Districts are the human-scale unit.** A district should sit near **Dunbar's number** — roughly 150 stable social relationships, the threshold beyond which personal knowledge stops working and institutions have to take over. Below it, people simply know each other and most machinery is unnecessary; above it, structure becomes genuinely necessary rather than bureaucratic.

The goal is that **the level where you actually live is the level where you know people.**

The district tier already exists in the systems view (§10.4). This makes it a social and political unit as well as a visual one.

**Discovery runs through projects, not directories.** You notice a facility straining, you show up, and the people there are the people there. Association forms through shared work, physical proximity, and the waystation for cross-city contact.

**Projects are searchable; people are not.** Projects are public, legible, and meant to be found — searching them is the intended path. A citizen directory would be both less thematic and more socially fraught, and it is deliberately omitted.

**No population cap.** Growth is simply demand growth, and backpressure (§6.5) already signals when a city has outgrown its capacity: build more, or people leave. The existing homeostatic loop covers this, and an arbitrary ceiling would be a rule where a mechanism already suffices.

There *is* a real technical ceiling on mesh size, and it should be treated honestly as an engineering constraint determining practical shard size — not dressed up as a law of the fiction.

### 5.8 Site: what a location determines

A city-state is founded at **real coordinates on the ruined Earth**. §5.2 already does this for Shangri-La; this generalizes it from one authored exception into how every city-state works.

Coordinates resolve into **two coarse bands**, both real-world indices, and nothing finer. There is no point-by-point survey of the planet.

| Band | Source | Determines |
|---|---|---|
| **Climate** | Köppen–Geiger classification | Temperature and precipitation regime, water availability, season shape, weather's plausible repertoire (§5.10) |
| **Ground** | Geologic province | Stone, clay, ores, rare earths — what the non-renewable ledger (§6.2) actually holds here |

Köppen–Geiger is the standard global climate classification, built from monthly temperature and precipitation and published as free map data. It sorts every point on Earth into a readable type — desert, steppe, Mediterranean, oceanic, humid subtropical, continental, subarctic, tundra, ice cap — and its entire purpose is to answer "what kind of place is this, and what lives here."

**What grows is derived, not classified.** Each cultivar carries its real requirements: water, temperature range, the winter minimum it survives, soil, sun hours. Each site publishes its real conditions. What a city can farm is the intersection, computed rather than declared. A plant-hardiness zone is therefore one *input* among several rather than a lookup table — which is what it actually is, an index of average annual extreme minimum winter temperature and nothing else. The payoff is that a citizen asking why a crop fails here gets a real answer about water or winter lows.

**Renewable mix is a property of the site.** A subarctic city is founded on hydro, wind, and geothermal; an Atacama city on solar. This is what keeps §5.9's accurate polar sun from reading as a lie: a city whose sun disappears for weeks does not run on sunlight and never needed to.

**Location carries economic weight, but only static weight.** §5.3 already lets specialization follow proximity to resources; this makes it concrete. The coupling is geographic, never temporal — a place has the water, ore, and stone it has, and no season modulates any flow rate (§5.10).

**Bad sites are bad, not forbidden.** Free coordinates mean someone will eventually propose a city on an ice sheet or a mid-ocean rock. §17's *design your way out of needing rules* applies: a site with no water, no growing conditions, and no workable ground simply produces a proposal that struggles to attract signers-on, which §5.6 already handles — neighbors decline to fund what they find unpromising. The Antarctic city-state is not prohibited. It is a hard sell, and the site report makes *why* legible before anyone signs.

### 5.9 Time, the sun, and the calendar

**World time is real time at the city's coordinates.** A day is a day and a year is a year. Time is not simulated; it is read from the clock every player already has, transformed by the city's position on Earth. Like weather (§5.10), it is a pure function — no node broadcasts it, no authority sets it, and it stays correct on a shard degraded to a single offline machine (§9.6).

**Cities keep solar time, not civil time.** Noon is when the sun is highest, and that is all noon means. Timezones and daylight saving are administrative artifacts of a world with railroads, telegraphs, and national borders; a society rebuilding from ruins, with no commerce and no scheduling authority, has no reason to reinvent them. Dropping them costs nothing and buys three things: each city-state's clock is genuinely its own, the site report's offset from a given player becomes an honest statement about longitude rather than a lookup in a political map, and an entire category of implementation misery — DST rules, timezone-database churn, the hour that happens twice — never exists.

A city runs **mean solar time, anchored so that clock noon and true solar noon coincide at the equinox.** True solar noon wanders by up to ±16 minutes across the year — the equation of time, which is why a sundial and a clock disagree — and a society with instruments keeps steady hours and lets the sun wander.

**Orbit is shared; rotation is local.** The date is global: every city-state is on the same planet going around the same sun, so caravans, inter-city agreements, and anything else spanning shards stay coherent. The clock is local. The alternative — each city beginning its year at its own local spring — would put a southern city six months out of phase with a northern one and turn every cross-city arrangement into a conversion problem, in exchange for poetry.

**The calendar is thirteen months of 28 days, plus a day out of time.** 13 × 28 = 364; the intercalary day closes the year at 365, and a second one is required every fourth year.

The principle underneath: **the anchors are astronomical, the divisions are convention.** Day, year, and equinox are facts anyone rediscovers by watching the sky. Gregorian months are not — they are 28-to-31 days of inherited Roman politics, two of them padded for emperors. Dropping them is the same move as dropping timezones: keep what the sky says, rebuild what Rome said. Equal months also mean every month is exactly four weeks and begins on the same weekday. Precedent: the International Fixed Calendar, proposed in 1902 and used internally by Kodak until 1989 for exactly this reason.

**A 28-day month matches no real lunar period, and this is accepted rather than solved.** The sidereal month is about 27.3 days and the synodic month about 29.5; 28 sits between them and matches neither, so no clean fix exists. A rendered moon's phase therefore drifts against the months. Let it drift — the calendar is the society's convention, the moon is a fact, and the drift is the honest result of setting one beside the other. The month is the one unit here that is *pure* convention, which is precisely why it was free to redesign.

Per §5.4, the **structure** is adopted now and the **names** are deferred. Thirteen-month calendars carry specific traditions, and naming months after one of them is the branding pass §5.4 says to earn later. Functional numbering until then.

**The day out of time is a holiday everywhere** — a day belonging to no month, on which nothing is scheduled. It is the one occasion every city-state shares; festivals are designed in §4.6, and the week centered on it is when the franchise renews (§8.2).

**The sun's position is computed, not approximated.** Standard solar-position math takes coordinates and a date and returns true altitude and azimuth — a small calculation requiring no dataset. Everything follows from it rather than being authored per place:

- **Day length varies by latitude and date**, correctly, with no special cases.
- **The southern hemisphere inverts for free.** Shangri-La's December is high summer. This is declination doing its job, not a toggle.
- **Near the equator**, days sit near twelve hours year-round and the season is wet-and-dry rather than warm-and-cold — which the climate band already says.
- **At high latitude**, the swing is extreme: true midnight sun and true polar night above the circles, and below them a summer sun that never quite sets but grazes the horizon for hours, raking the whole night in low golden light.

**Sun altitude is continuous, never a day/night flag.** Twilight is where high latitudes live. Light angle, color temperature, and shadow length key off real altitude; a binary would discard exactly the effect that makes those latitudes worth having.

**The polar case is a committed cost.** A far-northern city means weeks of real-time darkness in December and no true night in June, and the site report says so before anyone signs. Two things keep it from being punishment: the city's renewable mix never depended on the sun (§5.8), so the dark months cost nothing economically; and a city in darkness reads as pure light against black, which is the emissive channel at full strength (§12.6). A polar winter city is among the most legible in the game.

**The waystation has coordinates and therefore its own solar time**, but living there is not a commitment (§5.5) — it is the one place where the clock is not a decision anyone is stuck with.

**Longitude is a coordination mechanism, not only flavor.** See §9.5.

### 5.10 Weather

**Weather is a pure function of site and moment.** Every node computes it independently and arrives at the same sky. There is no roll, no broadcast, no authority: the requirement that weather be unpredictable per city and identical for everyone in it is met by determinism rather than by messaging, at zero bandwidth, with no coordinator to contradict §12.1.

**It samples coherent noise along the time axis, not independent draws.** Independent draws would flicker between states; smooth noise produces drifting pressure systems — weather that arrives, persists, and passes. Unpredictable, not discontinuous.

**The climate band sets the repertoire; season shifts the distribution.** A desert is mostly clear with rare violent rain, a maritime city drizzles, a subarctic one snows for months. Precipitation type follows temperature, so the rain-snow line moves with latitude and date on its own. Local phenomena come from the same two bands: fog in maritime basins, dust in arid ones, and aurora at high geomagnetic latitude — which lands on polar cities during exactly the months that need it.

**Weather is decoupled from the economy, deliberately.** It modulates no flow rate, no ledger, and no queue. Considered and rejected: seasonal renewable-flow modulation, which would have made scarcity cyclical and given §6.5's homeostatic loop a rhythm — at the cost of making Tier 0 pressure routine, when §6.3 defines a Tier 0 shortfall as by definition a crisis. A society that expects to be short of heat every winter has a different relationship to its own floor than this design wants.

Two consequences of the decoupling are load-bearing:

- **Perfect forecasts are harmless.** Determinism means anyone can compute next week's sky exactly. Where weather drove crops or energy that would be an exploit to design around; here there is no stake to game, so forecasting is simply something citizens can do.
- **Weather must not counterfeit a system state.** This requires active protection, specified in §12.6.

**Under degradation (§9.6) weather is Cosmetic and sheds first — but what sheds is the rendering, not the state.** Evaluating the function costs nothing, so a thinning shard loses its rain effects while every node still agrees about the weather.

---

## 6. Economy

### 6.1 No currency

**There is no money and no personal spendable balance at any point in the game.**

You request a good or a resource. If current production plus inventory covers all active requests, you receive it — immediately, no price, no payment, no transaction. If supply does not cover demand, your request enters a **transparent queue** that shows your position and the reason for the wait.

This is the design's single most important economic decision, and it is worth stating why it works. The distinction that matters is between a **personal wallet** and a **backend control signal**. The system does need internal accounting to decide "build more of this" — but that is not the same thing as a number a player holds, watches grow, and can hoard. Keep the accounting, delete the wallet.

This eliminates whole categories of problems structurally rather than by rule: there is no balance to hoard, nothing to lend at interest, nothing to speculate on, and no way to convert accumulated anything into advantage.

### 6.2 Non-interconverting ledgers

Resources are tracked on several independent ledgers that **do not convert into one another**. There is deliberately no universal exchange rate, because some things genuinely are not comparable:

| Ledger | Behavior |
|---|---|
| **Renewable flow** | Replenishes at a rate; the rate is the constraint |
| **Non-renewable stock** | Depletes permanently; cannot be recycled |
| **Recyclable material** | Circulates continuously, with some loss per cycle |
| **Labor / compute-time** | Available only as offered; cannot be stockpiled |

A project's footprint is expressed as a vector across these ledgers, not as a single price. This keeps trade-offs real: "this costs a lot of non-renewable stock but almost no energy" is a genuinely different statement from "this costs a lot of energy but no irreplaceable material," and collapsing both into one number would destroy exactly the information a good decision needs.

**"Erg" names the energy ledger specifically.** It describes a flow — a rate of energy availability and consumption — never a quantity a person accumulates. The word survives from earlier drafts of this design where it was a currency; it no longer is one, and must not drift back into being one.

**Narrative hook:** the old world's ruins *are* the non-renewable stock. This generation is the first to finish cleaning up after the collapse and close the material loop. You are not mining virgin resources; you are reclaiming wreckage. When the wreckage runs out, the circular systems have to actually hold. This gives an otherwise abstract accounting constraint real narrative weight.

### 6.3 Need tiers

Every request is classified into a tier. **Lower tiers strictly preempt higher ones** — a Tier 3 request never delays a Tier 0 request, under any circumstances, even in real scarcity.

| Tier | Contents |
|---|---|
| **0 — Subsistence** | Drinking water, staple food, basic shelter and climate control, essential medical care |
| **1 — Civic infrastructure** | Power grid, water and sanitation, transit, schools, recycling capacity, emergency services — the systems that make Tier 0 possible for everyone at scale |
| **2 — Personal & professional enrichment** | Workshop materials, project supplies, professional tools, creative and research equipment |
| **3 — Surplus & frivolity** | Swimming pools, decorative and status goods, indulgence beyond practical or creative need |

The governing intuition: **everyone has drinking water before anyone builds a swimming pool.**

Within a tier, ordering is by **fair-queuing with transparent backpressure telemetry** (§6.4). Routine classification is public and mechanical, published as an inspectable schema. Genuinely contested classifications escalate to the Round Table and become precedent (§7.1).

**Tier 2 is where the game's thesis lives** — "cool work that makes us happy." Most meaningful play happens here. Tiers 0 and 1 should feel reliably, boringly satisfied in a healthy city.

**The floor is universal; the rest is membership.** Tier 0 is guaranteed everywhere and to everyone, including in waystation territory and to people who have signed no social contract at all (§5.5, §7.9). Tiers 1 through 3 exist where a specific community built them, and citizenship is what connects a person to those systems.

This is **access, not queue preference** — a citizen is *in* their city's request pool for the things that city built, while a non-citizen simply is not, rather than being ranked behind them. Visitors are treated as guests: hospitality in the small (eating at a diner, riding a tram), not entitlement in the large (a house, a workshop allocation).

The distinction is not a status hierarchy. It is the plain fact that infrastructure exists where people built it, and that joining a community is what connects you to what it made.

**Edge case — Tier 0 shortfall.** Prime Principle 1 (§7.2) makes subsistence unconditional, but physics can disagree: production may genuinely fail to cover Tier 0. This condition is by definition a **crisis**, and is the clearest case for Round Table emergency scope (§7.1). The principle is not that scarcity is impossible; it is that Tier 0 is never *deprioritized by policy* — it can only be defeated by physical reality, and when it is, that is the city's single most urgent problem.

### 6.4 Fair queuing and the hoarding response

Hoarding is not denied — it is **deprioritized**.

Your first unit above typical baseline clears readily. Your hundredth queues behind everyone else's ordinary asks. This is fair-queuing: the same family of scheduling algorithm that prevents one greedy process from starving every other process on a shared CPU.

"Typical baseline" should be a **rolling statistical norm derived from actual community consumption**, not a fixed per-person quota. This distinction matters: a fixed quota is a ration (which contradicts "everyone gets what they request"), while a rolling norm is just the queue noticing that you are far outside ordinary usage and letting ordinary requests through first. Nobody is ever told no; unusual demand simply waits longer.

**The same algorithm governs CPU cycles and dinner.** This is not a coincidence to be tidied away — it is the design working correctly. Fair scheduling is the answer at every layer.

### 6.5 Capacity breathes

**Sustained queue pressure** on a resource is the signal citizens act on to **build new capacity** — a new fab, farm, kitchen, assembly line.

**Sustained slack** is the signal to **recycle capacity back down** — decommission the facility, return its materials to the recyclable ledger, reduce its energy draw.

This is the core homeostatic loop of the whole economy, and it replaces the function that price signals serve in a market: it tells the society where to expand and where to contract, using measured reality rather than willingness to pay.

Neither direction is automatic. Both are things citizens choose to do in response to a visible signal (§10.1). Major irreversible capacity commitments involve the Round Table (§7.1).

### 6.6 Claim decoherence

A granted-but-unused allocation **lapses after a reasonable window and re-enters the fair queue**, going to whoever is next in line.

Without this, hoarding simply reappears in a new form: request everything you might conceivably need, hold the claim indefinitely, just in case. A claim costs nothing to hold unless holding it has consequences.

Freed allocations are **redistributed, never merely voided** — the point is to get resources to someone who will use them, not to punish the requester.

### 6.7 Durability, repairability, and modularity

Three distinct commitments, not one:

**Durable — nothing is built to fail.** Planned obsolescence has no mechanism to arise, because nothing benefits from it: there is no seller wanting a second sale.

**Repairable — anything can be opened and fixed.** No sealed assemblies, no adhesives where fasteners would serve, no deliberate barriers to service.

**Modular — complex machines are assemblies of replaceable, recyclable parts**, not monoliths that die when one component fails.

The third is where the anti-enshittification argument actually lands, because it is precisely what the old world got wrong: glued-in batteries, proprietary fasteners, serialized components that refuse to function when swapped. Every one of those exists to force replacement, and nothing here has any reason to want that.

**Interoperability is therefore the default.** Incompatibility exists only to capture customers, so parts standardize across designs without anyone mandating it. A common parts ecology emerges on its own, and its absence would require someone to deliberately engineer lock-in that benefits them in no way.

**Economic consequences — this is load-bearing, not thematic.** A society producing disposable goods for everyone indefinitely would exhaust its ledgers no matter how fairly it allocated them. Durability is what makes the arithmetic of a post-scarcity economy close: goods lasting decades generate a fraction of the demand of goods lasting two years, which is how total production stays inside renewable flow and recyclable circulation.

Two mechanisms fall out with nothing to enforce:

- **A repair request is for a part, not a machine** — a far smaller ask that clears the queue quickly, so the fair queue routes toward repair on its own.
- **Worn parts return to the recyclable ledger** individually, rather than whole assemblies being scrapped for one failure.

It also makes §10.8's "operating becomes maintaining" concrete: maintenance is genuine ongoing work because machines genuinely have serviceable parts.

---

## 7. Governance

### 7.1 The Round Table

A body of a city-state's citizens, **selected by lottery and then chosen by election.** Seats rotate individually rather than turning over all at once.

**The two stages.** When a seat opens:

1. **The draw.** A slate of candidates is selected at random from the city's active voters (§8.2). Those drawn are the candidates; nobody else may stand.
2. **The election.** Those who accept publish their platforms, and active citizens elect from among them by ranked choice.

**Nobody can campaign their way onto the ballot, and this is the point.** In an ordinary election the ballot is filled by self-selection: the people who run are the people who wanted to run. That filters for ambition, free time, social reach, and comfort with self-promotion — none of which are the qualities the office actually calls for, and all of which correlate with exactly the kind of person a design like this should be wary of handing power to. Drawing the slate removes that filter at the source.

**Election is retained because pure lottery gives up too much.** A body drawn entirely at random cannot be chosen for judgment, values, or willingness, and offers citizens no way to express a preference about who governs them. The hybrid keeps both properties: the lottery decides who *may* stand, the election decides who *does*.

**Real-world precedent.** The Venetian Republic selected its head of state through an elaborate alternating sequence of lotteries and elections from 1268 until the republic fell in 1797, explicitly to make factional planning impossible — you cannot organize a takeover of a body when eligibility is not known until after the draw. Athens filled most public offices by lot but *elected* its generals, on the reasoning that offices requiring specific competence should be chosen rather than drawn. This design applies both ideas to the same seat.

**No eligibility gate of any kind.** The draw samples the active-voter pool without filter. Gating candidacy behind reputation, contribution history, or demonstrated competence would build an aristocracy of standing in place of one of money — a closed elite with a different admission criterion, which is precisely the failure this entire design exists to avoid. The lottery is not a gate: it is the absence of one, mechanized.

**Being drawn is an offer, not a summons.** Declining is free, requires no explanation, carries no penalty, and leaves no record; the system simply draws a replacement. Anything else would be conscription, and Prime Principle 4 makes consent real rather than assumed.

The honest cost is that declining partially restores a self-selection filter — only the willing end up standing. But *willingness* is a far weaker and more benign filter than *ambition*. A person who says yes when asked is a different population from a person who campaigns to be asked.

**A cooling period follows service.** Citizens who have recently served are excluded from the draw for a defined interval, so rotation genuinely rotates rather than recycling the same handful of people. This is a rotation rule, not an eligibility criterion: it expires on its own and applies to everyone identically.

**Publishing a platform is mandatory for anyone who stands.** Not vague statements of intent but an explicit, comparable statement of prioritization values and tie-breaking principles — legible answers to "when these two goods conflict, which do you choose and why." §7.7's divergence tracking then automatically computes the gap between what a candidate said and how they actually ruled.

Mandatory disclosure is consensual here precisely *because* declining is free. A drawn citizen unwilling to publish their reasoning simply declines the draw. Nobody is ever compelled both to serve and to expose themselves.

**Rulings made while serving are permanently public. Personal ballots never are.** These are two different things that both get called a voting record, and the design treats them oppositely:

- **Official acts** — how a member ruled, what precedent they set, how they voted within the Round Table — are public at all times, automatically, without the member's consent being required. These are exercises of delegated power and are accountable by default.
- **A citizen's own ballots** in elections and referenda are permanently secret and technically unprovable, including for sitting members and candidates.

**The reason ballot secrecy must be mandatory rather than optional** is not obvious and is worth stating. The danger is not that someone might want to reveal their vote; it is that **if revealing is possible at all, people can be pressured to reveal.** A faction, an employer, a family member, or a mob can say "show me," and a voter who genuinely *cannot* prove how they voted is protected because everyone knows the demand is unanswerable. Australia made the secret ballot compulsory in 1856 for exactly this reason and most democracies followed.

There is a second effect specific to a design like this one. Once disclosure is *optional* for candidates, declining to disclose reads as concealment; the option becomes an expectation, the expectation becomes a requirement, and every citizen who might ever be drawn acquires a reason to keep a provable ballot history. Secrecy would be lost by drift rather than by decision. The accountability that voluntary disclosure was reaching for is delivered instead by mandatory platforms and automatic divergence tracking, which cost nothing in secrecy.

**Ranked choice: the winner is whoever beats every other candidate head-to-head.** Each voter ranks as many candidates as they have opinions about. **Partial rankings are allowed and expected** — with a slate of people who did not seek office, genuine indifference is normal, and forcing a complete ranking manufactures preferences that do not exist. The count compares every pair of candidates and asks how many ballots ranked A above B. A candidate who wins every one of their pairings wins the seat.

Three reasons for this form rather than the elimination-round form of ranked choice familiar from public elections:

- **It is easier to explain.** "The person who would beat every other candidate one-on-one" is a single sentence. Elimination rounds require walking someone through a procedure, and a governing body chosen by a method its citizens cannot explain has a legitimacy problem.
- **The count reveals almost nothing about individuals.** The entire tally is a table of pairwise counts, fixed in size no matter how many people vote. The elimination method instead needs the distribution of complete ballot orderings — and in a district of roughly 150 people (§5.7), an unusual ordering can identify the person who cast it. Ballot secrecy is harder to protect at small scale than at national scale, and this design's political unit is deliberately small.
- **It merges cleanly with no coordinator.** Each node tallies the ballots it holds into a pairwise table, and tables combine by simple addition in any order to give the same total. That is exactly the property a count needs in a peer-to-peer network where nodes appear and disappear (§9.6).

**The honest limit** is that no candidate is guaranteed to beat all others — A may beat B, B beat C, and C beat A. This is a real mathematical possibility, first described by the Marquis de Condorcet in 1785, and it is rare in practice. When it happens, resolve by locking in the largest pairwise victories first and discarding any later one that would contradict a victory already locked — the "ranked pairs" method described by Nicolaus Tideman in 1987. Players encounter this rule only in the uncommon case that requires it.

**If more than one seat is filled at once**, the same ballots are counted by single transferable vote instead, so that a cohesive minority wins representation proportional to its size rather than being shut out entirely.

**Terms are short enough that power does not calcify.** Recall by referendum is available at any time. Exact durations, seat counts, slate size, and cooling-period length are deferred (§16) — but slate size specifically is not a free parameter, because a slate too small makes a lucky draw disproportionately valuable to anyone holding fraudulent identities (§8.3). Draw generously.

**Scope — the Round Table decides:**

- **Tier-classification disputes.** Is a community pool Tier 1 public-health infrastructure or Tier 3 frivolity? This is the archetypal case.
- **Tie-breaks in genuine unprecedented scarcity**, where a non-renewable input is oversubscribed and building more capacity is impossible.
- **Major irreversible capacity commitments** — large draws on non-renewable stock, decommissioning critical infrastructure.
- **Crisis response**, including Tier 0 shortfall (§6.3).

**It does not touch routine requests.** Citizens never wait on a committee for dinner. The overwhelming majority of allocation is handled mechanically by the tier schema and fair queue.

**Rulings become precedent**, folded back into the public classification schema like case law. This is how a city-state's founding values show up mechanically rather than as flavor text: Shangri-La's humanist-Buddhist bent plausibly leads its Round Table to classify communal-wellbeing infrastructure generously as Tier 1, where a more austerity-minded city-state rules the identical case as Tier 3. Same schema, same rules, genuinely different lived philosophy.

**Arguing a contested classification before the Round Table is itself a form of civic participation** players can meaningfully do — not merely background simulation.

### 7.2 Prime Principles (entrenched)

Five principles that policy drift cannot reach:

1. **Subsistence is unconditional.** Tier 0 is never a policy lever and never subject to vote.
2. **No power without accountability.** Contribution, compute lent, standing, or titles can never buy political voice.
3. **Exit is always free.** No one is trapped by a contract; leaving is never punished.
4. **Consent is real and renewed.** Every citizen affirms the contract personally at coming of age, including those born into citizenship. Nobody is bound by an agreement they never made.
5. **Restriction requires real harm.** No censorship or prohibition absent genuine illegality. No rules for the sake of order, taste, or comfort.

None of these introduce new scope. Each holds a decision made elsewhere in this document steady as policy details drift.

**The five are two different kinds of thing, and conflating them caused a real contradiction.** Some are true because of how the system is *built* — there is no mechanism by which a vote could change them. Others are genuine promises a community makes to its members, which a community can genuinely revise. Both belong on the list; they are protected by completely different means, and saying so resolves the question of who may amend a universal principle.

**Architectural principles — unamendable because there is nothing to amend.**

| Principle | Why no vote can reach it |
|---|---|
| **3. Exit is always free** | Possessions are signed with the player's own key (§8.1), the client runs on the player's machine, the network is peer-to-peer with no chokepoint (§11.6), and nobody else holds anyone's credentials. A Round Table that votes to forbid leaving has passed a rule with no mechanism behind it. There is nothing to disobey, because nothing was ever doing the holding. |
| **2. No power without accountability** | There is no wiring between standing and the ballot. Resonance, ergs contributed, project trust level, and titles are not inputs to any vote, quorum, or draw. Making them inputs would require building a connection that does not exist, not removing a protection that does. |
| **1. Subsistence is unconditional** *(substrate half)* | The floor is held by waystation settlements (§5.5), which are self-reliant, governed by no body, and cannot expel anyone (§7.9). No polity has standing to amend them, because no polity governs them. |

**Political principles — genuine promises, genuinely amendable.**

| Principle | What amendment means |
|---|---|
| **1. Subsistence is unconditional** *(membership half)* | What a city-state owes its *own members* above the universal floor. A city can vote to narrow this. |
| **4. Consent is real and renewed** | How and when a city takes affirmation of its social contract. |
| **5. Restriction requires real harm** | The city's own standard for what it will restrict. |

**Amending a political principle is a visible political fact, not a violation.** A city that narrows its own floor has not broken a universal guarantee — it has made itself a worse offer than the alternative that always exists, and citizens respond by leaving. The enforcement mechanism is exit, and it needs no enforcer. This is Albert Hirschman's argument from *Exit, Voice, and Loyalty* (1970), already in this document's lineage: where people can leave, organizations are disciplined by departure rather than by rules constraining them.

**The test for admitting anything to the Prime Principles at all: can it be made architectural instead?** If yes, build it that way and the entrenchment clause becomes unnecessary. If no, it is a promise, and labelling it one is more honest than pretending a paragraph protects it. **Entrenchment by text is the weak form** — §7.3 gives the reason, with the same clause type protecting human dignity in one constitution and the slave trade in another. Entrenchment by architecture only works for things that can be made structurally true, which is a much narrower and much safer set.

**The Prime Principles are universal, not city-state property.** They hold everywhere — including waystation territory, and for people who have signed no social contract at all. A social contract **adds** to this floor; no city-state owns it, and none may make it conditional on membership.

This is why the waystation has a floor at all (§5.5): not charity, and not generosity, but the principle applying where it already applied. A floor that stopped at a border would not be a floor.

**The principle is universal; its implementation is local.** Waystation settlements meet the floor with their own works rather than with transfers from cities, which changes nothing about the guarantee and a great deal about the relationship — nobody is sustained by a polity they did not join, and no city funds people it may be at odds with. The obligation survives as a backstop for genuine failure (§5.5), not as a standing transfer.

### 7.3 Amendment

**Ordinary policy** changes two ways:

- **Round Table precedent** — fast, handles the ordinary ambiguous case.
- **Citizen-initiated referendum** — available any time enough citizens want to force a direct popular vote rather than leave a matter to representatives. Modeled on Swiss practice, where elected government handles routine governance but organized citizens can compel a popular vote given sufficient support.

**Prime Principles use a harder path, but not an impossible one.** An amendment must pass, then **wait for an actual election to occur**, then pass again in identical form under the newly-elected body. This is modeled on Swedish constitutional practice and forces genuine generational reflection rather than a single heated moment.

**Deliberately not a permanent lock.** Constitutional history cuts both ways here, and both cautions are worth holding simultaneously:

- Germany's postwar Basic Law contains a genuine "eternity clause" shielding human dignity and the democratic order from any amendment — written precisely because Weimar's constitution had no such protection and was legally hollowed out from within.
- The original US Constitution *also* entrenched a clause: one shielding the slave trade from Congressional interference for twenty years.

Entrenchment preserves whatever you entrench, wisdom and cruelty alike. Keep the list short, keep the bar high, and do not assume the founders knew everything a later community might.

**This path applies only to the political principles (§7.2).** The architectural ones are not on the ballot, because no vote reaches them.

**"Wait for an election" means a full rotation cycle** — every Round Table seat turned over at least once since the first vote. This definition is required rather than incidental. §7.1 fills seats one at a time, so there is no longer a discrete moment at which the body changes; there is always an election happening somewhere. Read loosely, the waiting period would collapse to however long until the next single seat turns over, which could be weeks, and the strongest protection on the Prime Principles would be gutted by a change that had nothing to do with them. A full rotation preserves the original intent: **the second vote is taken by a genuinely different body.**

### 7.4 The social contract

Signing is a real commitment to *this* city-state's specific tier schema and values baseline — not generic terms-of-service paperwork. It is the mechanical gate for citizenship, and it is what makes city-states genuinely differ.

Citizens born in a city-state hold automatic citizenship but **still affirm the contract personally at coming of age** (Prime Principle 4).

**Admission is unilateral. Signing is the whole of it, and no city-state may refuse a signer.** Probation following expulsion (§7.6) is the sole exception: temporary, decaying, and binding only on the city that expelled you. Every other gate is refused for the reason §7.1 refuses eligibility gates for candidacy — a community that can decline members has an admission criterion, and an admission criterion is an aristocracy waiting to happen.

This is load-bearing beyond citizenship itself. The design resolves conflict by exit everywhere (§4.3, §5.3, §7.4), and exit is only real if somewhere will take you. A person nobody had to admit could be made stateless by unpopularity, and the unpopular are precisely who the guarantee exists for.

**The polity cannot refuse; the people in it are never compelled.** Individual citizens keep absolute blocking (§7.5), and compacts and projects may still exclude whom they like. Citizenship grants standing in the city and access to what it built — never an entitlement to any particular person's company.

Disagreement carries **no punitive mechanic**. If a contract stops fitting you — because the community amended it, or because you changed — you leave, and find or found a city-state that fits. Plurality across shards is the safety valve; enforcement within one is not.

### 7.5 Conflict, harm, and association

#### What harm is even possible

The design's governing heuristic (§17) says to ask what harm the mechanics permit before reaching for a justice system. Most categories turn out to be closed already — not by rule, but by construction:

| Harm | Status |
|---|---|
| Deprivation, starvation | **Impossible** — Tier 0 is unconditional and never a lever |
| Theft | **Impossible** — ownership is a signature; nothing moves without the owner's key |
| Coercion by authority | **Largely impossible** — no bosses, no gatekeepers, exit always free |
| Reputation attack | **Impossible** — Resonance derives from verified work, not peer opinion |
| False endorsement | **Toothless** — titles buy nothing, so a lie about someone costs them nothing material |
| Queue griefing | **Handled** — fair queuing already deprioritizes abnormal demand |
| Corrupted compute | **Handled** — redundant computation catches wrong results |

What survives is almost entirely **conduct**: harassment, cruelty, stalking, social exclusion, bad-faith participation, and spatial griefing. These are social rather than material, which follows directly from having removed scarcity, property crime, and power asymmetry.

#### There are no punishment levers, by construction

This design has already removed every conventional instrument of punishment. There is no money to fine. Subsistence cannot be withheld (Prime Principle 1). Confinement would violate free exit and does not exist as a mechanic. Standing cannot be stripped, because it derives from verified work rather than opinion.

**This is a forcing function, not an oversight.** The only available responses are dialogue, mediation, withdrawal of association, and ultimately expulsion. The design pre-committed to restorative rather than punitive justice without anyone deciding to.

#### The governing rule

> **Freedom of action, not freedom of audience.**

Nobody constrains what a citizen may do or say. But no one can be compelled to receive it, host it, work alongside it, or live with it.

Every rung below is an exercise of *other people's* freedom of association, never a restriction on the offender's conduct. This is what keeps the ladder from becoming a lighter-weight jail. Mechanisms that remove options from a person — however gently framed, however well-intended — are restriction by another name and are **explicitly rejected** (§15).

#### The ladder

**Rung 1 — Blocking.** You decline to receive another citizen's communications, as with a blocked phone number.

This is **client-side and absolute**: your client simply refuses their traffic. It requires no authority, no process, and no permission, and **no city-state can vote it away.** It is the safety floor beneath all in-fiction governance, and it protects the real person at the keyboard rather than the character.

*Open:* comms blocking does not address following, loitering, or watching, which are real harassment modes in an embodied world. Three candidate models — mutual invisibility, comms-only, and asymmetric — trade off differently. Mutual invisibility is closest to how the peer layer naturally behaves and is the current lean, but it creates ghosting (two citizens in one plaza, unable to see each other, touching the same objects), which is exploitable for uncontested access to shared space. Undecided (§16).

**Rung 2 — Mediation.** Voluntary on both sides. A third party helps, with no verdict and no coercion.

**Mediation is a project** (§10), not a new system: mediators volunteer, the work goes through the same create/discover/opt-in/leave lifecycle as a diner or a rail line, and track records are visible. No gate exists, and because both parties choose freely, an ineffective mediator simply is not chosen — selection without a market.

Mediation should be **discoverable as a physical place** in the city, learned during onboarding, rather than as a menu item. The design prefers environmental legibility to UI.

Mediators bring two things: understanding of how people behave under their particular conditions and history, and skill at helping someone find a path they would actually choose. **The line that matters: transparent, consented support is coaching; covert environmental shaping is manipulation.** Only the first is acceptable, and mediation never restricts anyone's options.

**Rung 3 — Group-level exclusion.** A project declines someone's labor; a homeowner controls their own space.

This is not the gatekeeping the design rejects elsewhere. A group choosing its own members differs categorically from society controlling access to the means of life, which Prime Principle 1 guarantees regardless.

**Rung 4 — Expulsion from the city-state.** Rare, high bar, real process. See §7.6.

#### Who decides: sortition, not election

Disputes are heard by **randomly selected citizens**, not by the Round Table.

Elected representatives judging personal conflicts would politicize private disputes and let the popular party beat the unpopular one. Sortition resists capture, distributes the burden, and — decisively for this design — **avoids creating a permanent judicial class**, which would be exactly the standing elite rejected everywhere else.

The split is principled: the Round Table is **elected** because it sets policy, which benefits from continuity and comparable platforms. Dispute panels are **sortitioned** because they judge particulars, which benefits from impartiality and the absence of career incentives.

**Prime Principle 5 sets the bar: real harm, not mere offense.** This is what protects the merely strange, unpopular, or abrasive from being processed out by people who simply dislike them.

Panel records are public, in keeping with legibility over enforcement.

#### An honest limit

This handles an individual harasser well and a **city-state whose majority endorses the harassment** poorly. If the population approves of targeting someone, neither mediation nor expulsion will be aimed at the harassers, and the victim retains only blocking and exit.

Plurality is a real answer — you leave for a city-state that does not tolerate it — but "your recourse is emigration" is a thin response to organized cruelty. The design should not pretend otherwise.

### 7.6 Expulsion, exit, and re-entry

**Expulsion is never permanent.** A permanent ban asserts that a person cannot change and judges them before their life is over. The design refuses that claim.

**Re-entry is gated by tiered probation**, scaled by the severity of the behavior and by how many prior probations the person has held. Probation gates **only re-entry to the city-state that expelled them**; they remain entirely free everywhere else, including the waystation and every other city.

**Records are visible and decaying.** Other city-states can see that a person was expelled and for what reason. The record **decays with time**, in keeping with the design's treatment of everything else as a flow rather than a stock — a ten-year-old expulsion weighs less than last month's. No city-state is *bound* by another's judgment; each decides its own entry, and a city known for harsh expulsions earns less deference from its neighbors.

**Possessions travel.** Soul-hash ownership is cryptographic and jurisdiction-independent (§8), so a departing citizen takes everything they own. Their property re-replicates into the destination's mesh on arrival.

This has a consequence worth noting: **emigration removes material footprint as well as labor, compute, and hosting.** A city-state that treats people badly pays a metabolic cost, not merely a reputational one.

**The exit protocol.** Subsistence continues throughout — Prime Principle 1 was already unconditional, so this needs no new guarantee. The departing citizen goes to the waystation (§5.5), where the settlements' own works meet the floor and where they may remain indefinitely. Helpers are available to assist in finding or founding a new home; like mediation, this is a project rather than an office.

**Framing is mechanical, not cosmetic.** Pushing hard against someone's identity reliably produces entrenchment and doubling-down. A process that shames manufactures the resistance it is responding to. "This is not working; here is help finding where it will" behaves differently from "you are banished," and the difference shows up in outcomes.

### 7.7 Protecting against capture

Defenses against a city-state falling to the corrupt or the incompetent, in descending order of strength.

**1. There is very little to capture.** The Round Table does not run the city — the fair queue does. Its scope is contested classifications, scarcity tie-breaks, and crises; everything else is mechanical and public. **The strongest protection against bad leadership is leadership with a small surface area.** This also bounds incompetence, not just malice.

**2. Capture degrades the prize.** Exit is free and possessions travel. A captured city-state loses citizens, and every departure removes compute, hosting, labor, and material from the mesh the captors just seized — thinning it toward the degradation ladder in §9.6. In the world that collapsed, a captured state could trap its people. Here, **you can win the city and find it empty.** Corruption is self-liquidating.

**3. Prime Principles are a floor, and the important half of it cannot be moved at all.** A fully captured Round Table cannot narrow its own political principles without winning twice across a full rotation cycle (§7.3), and **cannot touch the architectural principles by any vote whatsoever** (§7.2). The worst case is therefore one city adopting policies its remaining members dislike — which is also the worst case of an ordinary bad election, and has the same answer.

**4. Recall and citizen-initiated referendum** let citizens override representatives directly, at any time.

**5. Precedent decays unless reaffirmed.** The subtlest vulnerability is self-serving case law outliving the term that created it. Everything else in this design is a flow rather than a stock, and precedent is no exception: rulings that still make sense are reaffirmed cheaply, and the rest lapse.

**6. Sortition appears twice, and the two uses reinforce each other.** A randomly drawn citizen body *ratifies* anything that would become precedent, and §7.1's candidate slate is itself drawn by lot. Capture requires winning both the draw and the vote — and **nobody can campaign their way into a lottery.** Ireland's constitutional convention is real-world precedent for using sortition on genuinely contested questions.

**The vulnerability specific to lotteries must be stated, because it is easy to miss.** You cannot campaign your way into a draw, but you *can* hold more tickets. Someone controlling fraudulent identities is entered repeatedly in every draw without persuading anyone of anything. This means elections and sortition — presented above as independent defenses — **fail to the same single attack**, which is why §8.2's franchise rules govern the draw pool and not only the ballot.

**7. Automatic divergence tracking.** Candidates already publish explicit tie-breaking values (§7.1), which makes the gap between what someone said and how they actually ruled *computable*. Publish it automatically. No punishment and no enforcement — just the record made legible, which is this design's characteristic move.

**8. The district roll.** Each district (§5.7, §7.8) continuously publishes who is arriving and how they are connecting into the community. At roughly 150 people, an anomalous influx is not something an algorithm needs to flag — **the neighbors notice.** Details in §7.8; the mechanism it feeds is §8.4.

**Two honest limits.** All of the above assumes one-person-one-vote genuinely holds. §8.2 and §8.3 now raise the cost of holding fraudulent identities substantially and remove most of the payoff, but **verified unique persistent identity remains unsolved** (§16), and both elections and sortition depend on a genuine citizen pool. And none of this protects against a *popular* bad idea. Democracy constrains unpopular corruption, not majority conviction; the Prime Principles are the only floor there, and the political half of them can be amended slowly.

### 7.8 Recursive governance

Governance **recurses**, following Beer's Viable System Model directly (§3.1): every viable system contains viable systems, each autonomous in what is genuinely local to it and coordinating only what is not.

**Each level decides what it can meaningfully decide, and no more.** This principle has a name — **subsidiarity** — and it is the structural answer to a city-state outgrowing a single Round Table.

| Level | Decides |
|---|---|
| **Project** | Its own work (§10.10) |
| **District** | Matters local to the district — siting, local infrastructure, district-scoped classification disputes |
| **City-state** | Matters spanning districts — the grid, water, rail, the tier schema, Prime Principles, crises |

**Structure is identical at each level**, which means a citizen who understands how their district works understands how the city works. This is the same consistency argument as the nested systems views (§10.4), applied to politics rather than telemetry.

**Not everything needs to recurse.** Sortition is scale-free — a random sample is drawn from whatever population is relevant. Fair queuing is scale-free. Mediation is a project and therefore already local. Only *representation* genuinely requires the recursion, because only representation degrades with distance.

**Growth is therefore additive, not dilutive.** A city-state does not scale by giving each citizen a smaller share of one Round Table; it scales by adding districts that govern themselves, with the city body handling only what genuinely spans them.

**The district roll.** The district has one further job, and it follows from what a district *is*: the level at which people actually know each other (§5.7). Each district continuously publishes a standing roll — population, arrivals this season, how new arrivals have connected into the community's shared work and gatherings (§8.4), and the franchise status of recent cohorts (§8.2).

**It describes the district, never individuals.** "This district gained forty citizens this season, thirty-eight of whom have shared no project, meal, or gathering with anyone outside their own group" is a fact about a place, and acting on it is politics. "Kira scores 0.3" is a mark on a person, and acting on it is a caste system with a decimal point. **The roll publishes aggregates and flows only.** No per-person figure is computed, displayed, or stored.

**A district may witness and escalate. It may never exclude.** §7.4 forbids refusing a signer absolutely, and correctly: a community that can decline members has an admission criterion, and an admission criterion is an aristocracy waiting to happen. What a district can do is raise an anomaly to city-wide attention and call for review by a randomly drawn citizen body (§7.7). Its power is to make something visible and to demand it be looked at — never to keep anyone out.

This is subsidiarity doing exactly what §7.8 says it should. The smallest level competent to notice something is the level that lives with it, so that is the level that notices. The city handles only what genuinely spans districts. Nothing new is invented; an existing structure is given one more job that suits it.

### 7.9 Governance beyond city-states

Waystation territory (§5.5) has no Round Table, no social contract, and residents who may have agreed to nothing and may live there permanently. Three rules govern it.

**1. The Prime Principles are the floor, and they are universal.**

They apply in waystations because they apply everywhere (§7.2). The waystation is therefore not ungoverned — it is governed by the floor and by nothing else. **Maximum freedom, minimum protection**, which is the correct arrangement for a place whose defining quality is that nobody there signed anything.

**2. Above the floor, structure is opt-in — and it is already the founding mechanism.**

Anyone wanting more than the floor gathers people willing to agree to it. But that is precisely §5.6: a compact of twenty people with a short contract is a proto-city-state, and if it stabilizes and grows it becomes one.

The gradient from "no structure at all" to "full city-state" is therefore **continuous rather than a cliff**, and requires no new machinery. Someone who wants rules does not petition an authority; they persuade people.

**3. No city governs the waystation — and none funds it either.**

Self-reliance (§5.5) removes the question at its root. With no standing transfer there is no payer, so "whoever pays, decides" has nothing to attach itself to.

The rule survives regardless, because it has to hold in the tail case. Where PP1's backstop applies, or where a city or an individual contributes voluntarily, that contribution buys exactly nothing — the same rule that prevents a compute donor from directing the mesh (§11.1). It is the most important separation in the design, and a design that honored it only when honoring it was free would not be honoring it at all.

#### Disputes in waystation territory

The ladder from §7.5 applies, **truncated at rung 3**:

- **Blocking** works everywhere; it is client-side and requires no authority.
- **Mediation** works, because mediation is a project (§10) and mediators may operate anywhere they choose to.
- **Compact-level exclusion** works — a voluntary compact may exclude someone from itself.
- **There is no rung 4.** Nobody can be expelled from a waystation.

**This truncation is a structural guarantee, not an oversight.** There is nowhere further out, and creating one would rebuild the exile zone the design deliberately rejected (§15). It is also what makes the entire expulsion system safe: expulsion means "go to the waystation," and the waystation cannot pass anyone along.

**Nobody is ever nowhere.**

#### Why this does not produce a lawless zone

Subsistence is guaranteed, so there is no desperation. There is nothing to steal, because ownership is cryptographic (§8). There is no scarcity to fight over.

The waystation is safe for the same reason cities are — **the mechanics, not the policing.** If the design's central thesis is correct, it should hold in a place with almost no governance at all. The waystation is where that thesis is tested most directly.

#### Voice without membership

The tension this section previously left open — residents receiving subsistence from cities in which they have no voice — is **dissolved rather than balanced**, because self-reliance (§5.5) removes the dependency that generated it. There is no transfer to be voiceless about.

What remains is worth stating precisely, because "residents have no voice" was never accurate.

**They hold complete voice over their own arrangements and none over other cities' internal decisions — which is equally true of a Shangri-La citizen with respect to any other city-state.** A waystation resident is not uniquely voiceless. They are a non-member of every city, and non-members do not vote in polities they have not joined. That is what non-membership means, and per §7.4 it is reversible by one signature that no city may refuse.

The useful frame is Hirschman's *Exit, Voice, and Loyalty* (1970), which this design has used implicitly throughout — §4.3, §5.3, and §7.4 all resolve conflict through exit rather than voice. The waystation is that choice at full strength, and its residents hold a great deal:

- **Blocking** — absolute, client-side, requiring no authority (§7.5)
- **Mediation** — a project, and mediators work wherever they choose (§10)
- **Compacts** — voluntary structure with real internal governance
- **Founding** — persuade enough people and you are a city-state (§5.6)
- **Exit** — to any city-state, or to any other settlement
- **Citizenship** — one signature away, refusable by nobody (§7.4)

**No waystation voice body is created, and the omission is deliberate.** Rule 1 defines this territory as governed by the floor and nothing else; a body deciding anything material would be a government for the one place whose defining quality is having none, and rule 3 would come under permanent pressure from whoever staffed it. Removing the discretion is the better move, and self-reliance removes all of it (§17).

**One cost, recorded rather than smoothed.** A city that expels someone no longer bears any continuing expense for them, because nobody funds the waystation. That standing cost was a real brake on expulsion — the expeller kept paying — and self-reliance removes it. The remaining safeguards are §7.5's sortitioned panels, §7.6's tiered decaying probation, and the fact that expulsion requires demonstrated real harm rather than mere dislike. No replacement brake is introduced; the trade is that no city is bound to sustain people it is genuinely at odds with, which is the more important property.

**A narrower asymmetry survives.** The floor's *definition*, and the backstop obligation in §5.5, are written and held by citizens — so in the rare case a settlement's works fail, a resident's guarantee rests on a principle they had no vote in setting. This is far smaller than a standing dependency, and the alternative — enfranchising people in polities they declined to join — would make membership meaningless and put rule 3 under exactly the pressure it exists to resist. It is accepted, not solved. See §16 for a related inconsistency about who may amend a universal principle at all.

---

## 8. Identity, Ownership, and the Franchise

### 8.1 The soul-hash

**The soul-hash is a persistent cryptographic keypair** generated at character creation — the moment you turn eighteen and leave home. The private key never leaves the player's control.

This is the literal, load-bearing referent of the game's phrase "hashed with your soul," not merely poetic language. In a genuinely serverless world, a signature is the only available way to prove something is yours without a central database to consult.

**Gifting** re-signs an object to the recipient's key, leaving a small provenance record scoped to that one object. There is no global ledger of all transfers.

**Recycling** invalidates the soul-hash entirely — the object is no longer owned by anyone — and returns its material footprint to the relevant ledgers (§6.2) for the next request. Ownership was always custody, never a permanent claim on matter.

**Crafting is not a side economy.** Building something personal routes through the same tiered request pipeline as everything else (§6.3), so accumulating possessions is gated exactly like any other request. "I will simply own a great deal of stuff" is not a loophole.

**What a keypair cannot do is prove there is only one of you.** Anyone can generate as many keypairs as they like. That is the problem the rest of this section addresses.

### 8.2 The franchise

**The design promises one person, one vote. That promise only holds if the game can tell one person from one person pretending to be fifty.**

Nothing prevents someone from running the client fifty times on their own machine, creating fifty characters, and signing fifty social contracts. Every one is a legitimate citizen as far as the software is concerned, because no company is checking identity documents — which is the entire point of the architecture. The result is fifty votes where everyone else has one. In distributed-systems research this is a **Sybil attack**, named in a 2002 paper by John Douceur; §8.3 examines exactly what it can and cannot achieve here.

**The response is not to verify identity but to make the vote something a person holds by being present.** The vote is not granted at character creation and kept forever. It is earned by presence and lost by absence, on a symmetric rule:

- **Three months of presence earns it.** A new citizen votes three months after signing a city-state's social contract.
- **Three months of absence loses it.** A citizen who does not connect and play for three months loses the vote for that year.
- **Renewal happens in the week centered on the day out of time** (§5.9), the one occasion every city-state on the planet shares (§4.6).

**The same constant in both directions.** Three months of showing up puts the vote in your hands; three months of not showing up takes it out of them.

**The justification, which must be stated rather than left implicit.** The people governed by a decision should be the people making it. In a world where citizens genuinely come and go, an active citizen and a long-absent one are not equally subject to what the Round Table decides this year. Stated without its reason, the same rule looks like punishing people for having lives — so the reason belongs in the fiction, in the interface, and in the social contract itself.

**This is also the primary defense against fraudulent identities**, and it works by changing the shape of the attacker's cost. Creating fifty characters is a one-time expense that now buys nothing lasting. *Keeping* fifty votes alive requires piloting fifty characters continuously, forever, and attention is the one input that cannot be copied.

**Lapsing is never a punishment and never a judgment.** It is restored by showing up during the renewal week. No appeal, no application, no explanation, no record, no waiting period on return, and no official anywhere who decides.

**What lapsing does not touch — and this list is load-bearing:** subsistence, citizenship, residence, property, work, standing, project membership, blocking, access to mediation, and exit. All of these are unconditional and unaffected. **The lapse reaches the ballot and the draw pool, and nothing else.** The moment it reaches a resource, this stops being a franchise rule and becomes a means test.

**A renewal week rather than a renewal day.** If the vote required presence at one specific moment, then illness, work, travel, a bad connection, or an ordinary busy day would cost a person their voice for a year — disenfranchisement by calendar. A week-long window centered on the day out of time removes that failure without weakening the mechanism, since the point is annual presence rather than punctuality.

**Why the day out of time is the right anchor**, beyond the fiction being pleasing. There is a proposal in security research for establishing that accounts belong to distinct people without identity documents, biometrics, or any central authority: announce a moment, require everyone to show up, and issue exactly one token per attendee. The verification rests on physics alone — one body cannot be in two places at the same instant. Nobody proves who they are, no names are recorded, and no authority decides who counts. Bryan Ford at EPFL proposed this in 2008 as "pseudonym parties," and the Encointer project runs a version of it for real.

This design already contains the gathering that proposal requires, built for unrelated reasons: §5.9 gives the calendar a day belonging to no month, on which nothing is scheduled, shared by every city-state because the date is global even though the clock is local; §4.6 makes it the one holiday the whole world observes. **The day nobody works is the day the city counts itself.**

**Its limit is real and should not be oversold.** Ford's version relies on physical bodies in physical rooms. This one relies on characters present in a simulated world, and a determined attacker can script characters into a plaza on the right day. For renewal to mean anything it has to involve unpredictable interaction with other people rather than a check-in — which raises the cost considerably without closing the hole.

**Real-world precedent, and the reason it must be handled carefully.** Residency waiting periods for local voting are near-universal and uncontroversial. Their historical cousins — poll taxes, literacy tests, discretionary registration — were instruments of exclusion, and the difference is not the waiting itself but who decides. **This rule is uniform, automatic, and applied by no one.** There is no application, no official, no criterion a person can be judged against, and no discretion anywhere in it. Any future addition that introduces a judgment call reintroduces the historical failure mode.

**The waiting period runs per city-state.** A citizen who moves votes in their new home after three months. This is a genuine cost on movement and sits in tension with Prime Principle 3, so the tension is stated rather than smoothed: exit remains free of penalty, possessions travel, and admission cannot be refused (§7.4), but the newly arrived do wait to vote. The alternative — a franchise that travels instantly — would let fraudulent identities be aged quietly in one city and then moved en masse into another at the moment they were wanted, which is precisely the attack this section exists to prevent.

**The draw pool is the active-voter pool**, so the same rule governs who may be drawn as a Round Table candidate (§7.1). Sortition is at least as vulnerable to fraudulent identities as election is (§7.7), and it would be pointless to protect the ballot and leave the lottery open.

**AI citizens hold no franchise** pending verified unique persistent identity (§13.2); nothing here changes that, and the presence rules apply to human citizens.

### 8.3 What a fake identity can and cannot buy

**Before defending the franchise it is worth asking what fraudulent identities actually gain**, and the answer turns out to be narrow. Mechanisms built for entirely unrelated reasons close most of the payoff on their own.

| Vector | Status |
|---|---|
| **Contribution credit** | **Closed.** There are no personal balances to inflate — ergs are a ledger, not a wallet (§6.1). What contribution produces is Resonance, earned by verified real work actually used by others (§10.6). Fifty characters on one machine divide one machine's output between them. The credit attaches to the work, not to the account. |
| **Food, housing, goods** | **Closed.** Tier 0 is fulfilled *on request*, never disbursed as an allowance (§6.3). An unplayed character asks for nothing and consumes nothing. Extracting fifty people's subsistence requires *playing* fifty lives, and human hours do not multiply the way software copies do. |
| **Hoarding property** | **Closed by §6.6.** Claims held but unused decohere and return to the pool. Property parked on idle characters evaporates without anyone needing a rule against it. |
| **Inflated standing** | **Mostly closed.** Fifty characters can praise one another, but Resonance purchases nothing (§10.6) — the attacker inflates a number that does not do anything. The residue is informal social deference, already listed as unresolved in §16. |
| **Labor multiplier, titles** | **Closed.** Both attach to work actually performed (§10.7, §10.9). Unplayed characters perform none. |
| **Votes, and entries in the sortition draw** | **Open. This is the entire exposure.** |

**The useful finding is that this is not a general problem in this design. It is one specific problem: fraudulent identities can vote.** That is a far smaller thing to defend than "fraudulent identities exist," and it is why §8.2 defends the franchise rather than attempting to verify people.

**The sortition draw is part of the exposure and was previously assumed safe.** §7.7 presents sortitioned ratification as covering a weakness in elections on the grounds that nobody can campaign their way into a lottery. True — but tickets can be accumulated. Both defenses rest on the same unverified assumption, and §7.7 now says so.

**The residual risk, which the design deliberately does not attempt to close.** Someone who recruits two hundred real people to join a city-state and vote together defeats every measure here, correctly, because every one of those accounts belongs to a real distinct person. That situation is **indistinguishable from two hundred people genuinely deciding to move somewhere they like** — and the difference between a coordinated takeover and a disagreeable influx of newcomers is a political judgment, not a technical fact. It is exactly the judgment used to disenfranchise unwelcome newcomers in the collapsed world.

Any mechanism sharp enough to catch the first case also catches the second. **This design stops short of that sharpness on purpose** and bounds the damage instead: §7.2 puts the architectural principles beyond reach of any majority, §7.7 leaves very little to capture, and exit means a captured city can be won and found empty.

### 8.4 The association graph

**Entry to the game is by invitation (§11.6), which incidentally records who invited whom.** That structure could be used to detect fraudulent identities — an attacker can have fake accounts invite each other for free, but getting *real* people to invite fake ones requires deceiving actual humans, so the fake population ends up attached to the real one by very few links, a shape detectable without examining any individual. This is the basis of a well-developed body of research (SybilGuard and SybilLimit, Haifeng Yu and colleagues, 2006 and 2008; Facebook's SybilRank in production).

**The invitation chain is recorded and deliberately not used.** It is retained because it is free to keep and may matter later. It is unused because standing that derives from *who admitted you* is inherited position, however mild — and this design refuses those consistently. Two further problems make the refusal easy: §11.6 provides a shipped peer list for anyone holding no invite at all, so some citizens have no inviter and would be permanently disadvantaged by an accident of how they arrived; and because the franchise now requires activity, an entire branch can lose its connection when the people above it stop playing, degrading a person's position through nobody's action but other people's life circumstances.

**What is used instead is association: who you have genuinely been with.** Shared work on a project, shared meals and gatherings (§4.5), attendance at the same festival (§4.6), living in the same district. The data already exists and is already public — §10.2 makes projects searchable by design, and gatherings happen in public space.

This is better on every axis that matters here:

- **Position comes from what you did, not from who let you in.** That is the same principle §7.1 applies to candidacy and §11.5 applies to project trust: earned through demonstrated participation, never granted by permission.
- **It heals.** When people around you leave, you form new connections by continuing to live in the city. Nothing about your position is hostage to someone else's decisions.
- **Nobody is an orphan.** A citizen who arrived with no invitation participates and becomes connected exactly like anyone else.
- **It is expensive to fake.** Fake accounts inviting each other costs nothing. Fake accounts genuinely co-present with real people over months costs human attention, which is the scarce thing.

**The invitation is the seed; association is the substance.** Your inviter gives you one starting connection so that you are not isolated on your first day. Everything after that comes from being present with people.

**The graph is descriptive only. It has no automatic effect on any individual, ever.** It feeds the district roll (§7.8) so that citizens can see how their community is actually connecting, and it informs human political judgment at district scale. It does not weight votes, does not gate the franchise, does not shorten or lengthen anyone's waiting period, and produces no per-person score. Three rejected alternatives and their reasons are recorded in §15.

**The failure mode to guard against in implementation, stated plainly because it is easy to introduce while meaning well:** if association is measured mainly through *project work*, the graph becomes a labor qualification attached to political life — the same category of thing as a property qualification for suffrage, and a direct contradiction of this design's claim that people are the ends and work is the means. **A citizen who joins no project and simply lives among people must register as fully connected as the most industrious person in the city.** Meals, gatherings, festivals, and neighbors count exactly as much as shifts worked. If that is ever not true, the graph has quietly built the thing this document exists to prevent.

§9 generalizes §8.1's replication mechanism from personal property to the entire world.

---

## 9. World State Persistence and Replication

**Everything persistent in the game lives on players' machines.** Not just personal property — the whole world.

This is the architectural heart of the game and the thing that makes the reveal (§12.1) true.

### 9.1 What is replicated

All of the following is checkpointed and replicated across the city-state's mesh:

| Category | Examples |
|---|---|
| **Personal property** | Homes, owned objects, personal workshops |
| **Functional buildings** | Factories, plants, kitchens, clinics — including configuration, maturity level (§10.8), and automation state |
| **In-flight process state** | A factory mid-production run, a partially-drained job queue, a shipment in transit |
| **Ledger state** | All four resource ledgers (§6.2), current rates, current stock |
| **Request queues** | Who is waiting for what, position, tier classification |
| **Governance records** | Election results, Round Table precedent, the classification schema, referendum outcomes, the social contract itself |
| **Citizenship records** | Who signed what, when, coming-of-age affirmations |
| **Standing** | Recent-weighted Resonance and contribution history (§10.6) |
| **World layout** | Geography, what is built where, district structure |
| **Simulation state** | The city's running tick itself |

**The simulation is not hosted anywhere else.** When a factory in Shangri-La processes a production batch, that computation happens on Shangri-La citizens' hardware, and the resulting state is stored on Shangri-La citizens' hardware.

### 9.2 Ownership, custody, and readability are three separate things

This separation is what makes the whole scheme work:

- **Ownership** — who may modify a thing. Established by cryptographic signature (§8). Only the owner's key can modify, gift, or recycle an object.
- **Custody** — whose disk the bytes physically sit on. Determined by the replication scheduler, entirely unrelated to ownership.
- **Readability** — whether the custodian can interpret what they hold. Fragments are **encrypted at rest**; a machine can host data it cannot read.

So your home persists and is visitable while you are offline, stored across a set of neighbors' machines, none of whom can alter it and none of whom can read it. This gives "renting out your brain-space" its second meaning: a slice of your idle **disk** holds encrypted fragments of the shared world, alongside your idle **cycles** running others' jobs (§11).

### 9.3 Consistency tiers

Not all state needs the same guarantees, and pretending it does would make the whole system unusably slow. State is classified by how much consistency it genuinely requires — structurally the same move as need tiers (§6.3), applied to data:

| Tier | Applies to | Guarantee |
|---|---|---|
| **Strict** | Ledgers, votes, citizenship, ownership transfers, governance records | Quorum consensus before commit. Slower, never wrong. |
| **Ordered** | Request queues, production state, facility configuration | Order matters; brief divergence tolerable and deterministically reconcilable. |
| **Eventual** | Ambient/decorative state, cosmetic placement, flourish animation | Diverging copies are harmless; converge when convenient. |

Replication factor scales with tier — critical state is held on more machines than cosmetic state.

**Rule of thumb:** if disagreement between two copies could produce an unfair outcome, it is Strict. If it could produce a confusing one, it is Ordered. If it could only produce a slightly different-looking courtyard, it is Eventual.

### 9.4 Checkpointing and handoff

Detailed in §11.3 — the same mechanism serves both running jobs and world state. In summary: periodic checkpoints, ACK-timeout resubmission of unacknowledged work, and graceful drain on clean shutdown.

The important consequence: when a player closes the game, the buildings they were hosting do not stop existing or lose their in-progress work. Their state was already replicated, and their share of the hosting load redistributes to other machines. **A single player leaving is a non-event, by design.**

### 9.5 Two hard problems this creates

Both are genuinely unresolved and must not be hand-waved.

**The cold shard problem.** If every citizen of a city-state is offline simultaneously, nobody is hosting it. Three possible responses:

- *Hibernation* — the shard freezes, simulation time stops, and it resumes when someone returns. Honest and simple, but the city no longer lives while you sleep.
- *Persistence floor* — always-on background contributors (§11.1) keep a minimum quorum alive. Works when enough players enable always-on, but is not guaranteed.
- *Cross-shard hosting* — machines from other city-states hold cold shards' state. Preserves persistence but weakens "our city runs on us."

**Recommended: hibernation as the honest floor, with a persistence floor making it rare.** A genuinely serverless world *can* go quiet, and pretending otherwise would require exactly the infrastructure this design rejects. Thematically this is defensible and even attractive: the city sleeps when everyone sleeps.

Hibernation is the endpoint of the graceful degradation ladder in §9.6, not a separate mechanism.

**Longitude partially mitigates this, and it is the strongest practical argument for §5.9's real solar time.** Because a city-state runs on the real clock at its own coordinates, its daylight hours correspond to real hours somewhere on Earth — and citizens naturally settle in cities whose daylight matches their own waking life. A city-state's population therefore self-clusters into overlapping real-world schedules, which is precisely the property a shard needs to stay warm. This does not solve the cold shard problem, since a city can still empty out; it makes the emptying less likely and more predictable, and it costs nothing, because the clustering is a side effect of a choice players make for their own convenience.

The inverse is the cost, and §5.6's site report exists to disclose it: a citizen whose real life does not match their city's clock will experience that city mostly at night.

**The bootstrap problem, and an honesty risk.** A new player's client must discover peers from somewhere. Standard P2P bootstrapping uses seed nodes or a distributed hash table — but **any permanent bootstrap infrastructure is, technically, a server.**

This matters more here than in an ordinary P2P application, because the reveal (§12.1) stakes the game's emotional payload on the claim being *literally true*. A player who discovers an asterisk after being told there are no servers has been mildly lied to, which is worse than never having made the claim.

Two acceptable resolutions: minimize bootstrap infrastructure to pure peer discovery holding no world state and no simulation (and say so plainly), or make bootstrap itself peer-supplied. **Do not resolve it by not mentioning it.**

The chosen answer is the second — invite-as-bootstrap, detailed in §11.6.

### 9.6 Graceful degradation under resource pressure

When a shard lacks the compute or bandwidth to run everything, it must **shed load in a defined order rather than fail as a unit.**

**Criticality tiers mirror need tiers (§6.3).** The same ordering that decides who gets drinking water before who gets a swimming pool decides which subsystems stay running:

| Criticality | Subsystems | Behavior under pressure |
|---|---|---|
| **Core** | Ledgers, citizenship records, ownership, governance records | Never shed while the shard is alive |
| **Essential** | Request queues, Tier 0/1 facility simulation, mesh scheduling | Shed only after Supporting is gone |
| **Supporting** | Tier 2/3 facility simulation, personal workshops, non-critical projects | Shed before Essential |
| **Cosmetic** | Ambient animation, flourishes, decorative simulation | Shed first — already the mechanism in §12.2 |

**Shedding is topologically ordered.** A subsystem may be shed only after everything depending on it has been shed. This requires the subsystem dependency graph to be a **DAG**. Circular dependencies are a design error and must be caught early, because they make ordered shutdown impossible.

**Self-hostable before shared.** Anything a player's own machine can host alone — their home, their possessions, their personal workshop — degrades to local-only rather than disappearing. Anything genuinely shared, such as city ledgers and cross-citizen queues, requires mesh quorum.

The consequence is a graceful floor rather than a cliff: **as a shard thins out, the experience degrades toward the single-player mode that already exists.** You can always walk around your own house. You simply cannot reach the city economy.

This is also visually honest at no additional cost. A city losing its mesh looks exactly like §12.2's near-idle state — dim, dormant, quiet, unanimated — because that is precisely what is happening to it.

---

## 10. Projects, Labor, and Resonance

A **project** is the game's central organizing unit: a thing people build and maintain together. A diner, a water reclamation plant, a rail line, a research group, a sports club, a city's entire power grid.

### 10.1 Create

**No permission gate.** Anyone may found a project. Nobody approves it.

The fair-queue system already knows where need is real, so the game **actively surfaces it** — "here is where the city is straining" as a standing, visible invitation. This points need-driven creation at genuine gaps without ever requiring it.

Creating things nobody asked for — art, odd hobby workshops, untested ideas — remains completely free. Both paths matter.

Founding means: choose a **template** (auto-generates manifest and resource footprint; no programming required) or author **custom logic** (self-declared manifest; §11.2), then **place the project physically in the world.** Every project has a building.

**Bad ideas need no policing.** Because throughput and standing flow only from *usage* (§10.6), a shoe-horn factory built while people are starving is simply starved of both — nobody requests shoe horns. Nobody forbids it, the incentive structure simply does not reward it, and the founder has spent only their own free time. This is the design's governing heuristic (§17) in its purest form.

### 10.2 Discover

**Ambient (avatar layer).** Facilities broadcast their state environmentally. You notice a struggling workshop the way you would notice a struggling shop on a street you walk daily — not via a floating icon. See §12.2 for the visual vocabulary.

**Deliberate (systems view).** The same information, city-wide, in the telemetry conventions the fair-queue system already established.

Same underlying data, two registers, depending on how deliberately you are looking.

### 10.3 Opt in

Support is **not monolithic**. Five independent levers, mixed in any combination:

- **Compute** — idle CPU cycles (§11)
- **Active labor** — showing up and doing the work in person
- **Land** — the plot your home sits on, or land you hold
- **Storage** — idle disk hosting world state (§9.2)
- **Relay bandwidth** — forwarding encrypted traffic for peers stuck behind NAT (§11.6)

This matters: someone with no hardware to spare can matter as much as someone lending a rack of cores, through a different lever. Resonance tracks contribution across all five (§10.6), not compute alone.

Note that the levers are genuinely different in kind — relay bandwidth and land are scarce in ways compute is not, and a citizen with a public IP address contributes something no amount of CPU substitutes for.

### 10.4 Status views — three nested zooms

Following Cybersyn's Operations Room logic (§3.1), different decision scopes need different aggregation:

1. **Project** — queue depth per resource, contributor counts by type, manifest, recent unfulfilled requests, maturity and automation level
2. **District / sector** — what is straining nearby; the view a citizen uses to decide how to spend an afternoon
3. **City-wide, by tier** — aggregate need tier by tier; the view the Round Table needs to set policy

**Identical visual and interaction language at every level.** A player who has learned to read one has learned to read all three. Consistency here is what makes a large system feel learnable rather than like several systems to memorize.

### 10.5 Leave

**Frictionless and non-punitive.** An exit tax, cooldown, or guilt mechanic would contradict voluntary participation outright.

But stepping back **announces itself** — at minimum as a visible taper in contribution — rather than silently vanishing, so remaining members can see the gap and seek support rather than being confused about why capacity dropped. This is the same principle as graceful machine drain (§11.3), applied to a person.

### 10.6 Resonance

Resonance is **standing**, not currency.

**It buys nothing.** No queue priority. No political voice (Prime Principle 2). No allocation advantage. No access to anything gated.

It is how the city sees you: useful for finding collaborators the way a portfolio is, informative about who is carrying weight right now, and satisfying to have — without ever being a gate or a claim.

**Weighted toward coherence over raw throughput.** The mesh rewards many independent small contributors above one monolithic one. This is honest to how distributed systems genuinely behave — coordination overhead and Amdahl's law mean one giant node does not parallelize as efficiently as many small ones — and it is thematically apt: the elves were never one voice, they were a chattering multitude.

**Recent-weighted, not cumulative.** Standing reflects *current* contribution, not lifetime accumulation. A purely additive number eventually names a permanent elite of people who worked hard once. Everything in this design is a flow rather than a stock — ergs, lapsing claims, the labor multiplier — and standing follows the same rule.

**Earned by verified real work**: producing resources that others actually use, with output independently confirmed correct (§11.4). Explicitly *not* proof-of-work puzzles.

**Not a measure of competence, and not fed by leisure.** What a citizen is *good at* is a separate quantity that buys nothing and never touches Resonance (§10.11); what a citizen does for pleasure produces gifts and gatherings, which no ledger sees (§4.5).

### 10.7 The labor multiplier

Queue backpressure detects **capacity** bottlenecks. It cannot detect **willingness** bottlenecks.

Everyone wants to run the observatory. Nobody wants the night shift at waste reprocessing. Building a second waste plant that nobody will staff yields two understaffed waste plants — more capacity does not fix a staffing problem.

**Resonance earned per hour scales inversely with how understaffed a role currently is, and the multiplier decays to nothing as people show up.** Adapted from Walden Two (§3.4), without Skinner's daily quota.

The elegant property: **it self-liquidates.** The incentive exists exactly as long as the problem does, which is structurally the same shape as unused claims dissolving (§6.6). It cannot corrupt into inequality because standing buys nothing (Prime Principle 2).

A pleasant inversion worth preserving: this makes the least pleasant necessary work the *highest-standing* work in the city — the exact reverse of the arrangement in the world that collapsed.

**Damping is required.** An instantaneous, visible multiplier produces stampede-and-collapse oscillation — job flapping. Two fixes, both necessary:

- **The advertised rate moves on a slow average**, not instantly.
- **Your rate locks when you commit to a shift.** Without this, other people showing up *reduces your own rate*, which incentivizes hoping nobody else volunteers. That is a catastrophic thing to build into a cooperation game.

**A sustained multiplier is an automation signal.** If a role stays expensive for months, the honest read is not "pay more" but "this work should not require a person." This is the same shape as backpressure→build-capacity, one level up: material need says build a facility; labor need says build the thing that makes the facility not need staffing.

### 10.8 Facility maturity and automation

**Facilities evolve.** Sustained work contributed to a facility increases its **maturity**, unlocking automation that reduces its staffing requirement.

Automation is itself built through the normal request pipeline — someone chose to do that work, and it consumed real resources from real ledgers. It is not free and not automatic.

It interacts correctly with the labor multiplier at no cost: as staffing need falls, the multiplier falls with it.

**Labor does not disappear, it moves up the stack.** Operating becomes maintaining, maintaining becomes improving, improving becomes designing the next thing entirely. And some work resists automation outright: care, judgment, creation, founding, teaching, governance. Automation does not empty the game; it moves play upward, which is precisely Fresco's thesis (§3.2) rather than an accident to be balanced around.

**This gives shards texture at no systemic cost.** A mature Shangri-La feels settled and quiet, with much of its drudgery long since designed away. A young frontier city-state is visibly hungry for hands.

**Automation's target is free time, not throughput.** This is the distinction that separates this design from the world that collapsed, where productivity gains were captured rather than distributed and the working day never shortened. Here there is nobody to capture them: automation's entire yield is hours returned to citizens, and what those hours are *for* is §4.5.

**Shangri-La is heavily automated**, across growing, recycling, manufacturing, and distribution — and on the contracting side too, decommissioning capacity when sustained slack says to (§6.5). A mature city-state runs mostly by itself, and the drudgery a frontier city is still doing by hand is work Shangri-La designed away generations ago.

**A mostly automated facility is cheap to host.** This is honest rather than convenient: a steady-state process is a simple simulation, and its cost on the mesh should reflect that. Automation therefore reduces load on the very citizens whose machines run the city (§11.1), which compounds — the better a city automates, the less its own infrastructure asks of the people living in it.

**Remote operation wherever the work allows it.** A citizen should be able to run what can be run from anywhere, rather than being obliged to stand in a building because the interface demands a body. Presence is reserved for work that genuinely requires it — which §10.8 already names: care, judgment, creation, founding, teaching, and governance. Requiring attendance where it adds nothing would manufacture exactly the obligation §2 forbids.

### 10.9 Titles

Three honest flavors, which should not be conflated:

- **Provable** — "Founder of X" is a fact the signed creation record already contains. Not a claim; a verified event.
- **Peer-endorsed** — "Engineer," "Polymath," "Laborer." One soul, one endorsement; not weighted by the endorser's standing.
- **Self-asserted** — whatever someone calls themselves. No verification, pure flair.

**Hard rule: no title ever touches a queue, a vote, or an allocation.** Titles are purely expressive and informational.

**Founders hold no permanent authority** over projects they started — that is the aristocracy trap at smaller scale (§7.1).

Titles are **plural and unranked**: you hold many, and none sits above another. There is no ladder. This does not fully solve informal deference calcifying into a pecking order (§16), but it removes the obvious path to one.

### 10.10 Intra-project decision-making

Founders hold no permanent authority (§10.9), which raises the question of how a project decides anything. The answer is graduated, and it begins with **nothing**.

**Small projects need no governance.** A diner with three people talks. Building machinery for a workshop is the mistake to avoid.

**Medium projects run on do-ocracy.** Whoever does the work decides how it is done. Nobody votes on the paint color; the painter chooses. This is how open-source projects and most functioning co-ops actually operate, and it requires no formal structure, no meetings, and no offices.

**Large or contested projects fork.** This is the design's own answer, applied one level down: at city scale, irreconcilable disagreement resolves through exit and plurality (§7.4); at project scale it resolves identically. **A fork is exit at project scale.**

Forking is deliberately cheap, because a project is only a template, a manifest, and its contributors. Take your people, place a new building, continue. Disagreement resolves by divergence rather than by anyone winning an argument.

If genuine demand supports both, both survive. If it does not, backpressure (§6.5) resolves the duplication without anyone adjudicating it.

**The exception: you cannot fork the power grid.** Tier 1 civic infrastructure cannot diverge — a city has one grid, one water system, one rail network. But this exception needs no new mechanism, because those decisions are already **major irreversible capacity commitments** inside the Round Table's existing scope (§7.1). Critical infrastructure escalates to civic governance because it *is* civic.

### 10.11 Skills

A third quantity, deliberately separate from Resonance (§10.6) and titles (§10.9). Conflating them is the failure mode this section exists to prevent.

| Quantity | What it means | How it behaves |
|---|---|---|
| **Resonance** | Who is carrying weight on what the city needs *now* | Recent-weighted flow; decays; tied to need through §10.7 |
| **Title** | What a person is called | Plural, unranked, expressive (§10.9) |
| **Skill** | What a person is actually good at | Grows with practice; atrophies without it |

**A skill is competence, not standing.** Cooking, cabinetry, sewing, leading a practice, guiding a tour, running a line — anything done often enough to get good at. It answers exactly one question: *who do I ask about this?*

**Skills must never be routed into Resonance.** Resonance means "who is covering what the city needs," and it is tied to scarcity through the labor multiplier (§10.7). Feeding leisure into it would dilute that signal into "who is socially active," and would instrumentalize rest — telling players that even their free time should be useful, which is the logic of the world that collapsed (§1).

**Named, not numbered.** A citizen is *known for* sourdough, cabinetry, and leading sits. There is no level, score, or rank. §16 already warns that visible standing calcifies into deference with no mechanical backing, and a public number that only rises is far more prone to that than a name, because numbers invite ranking — players build leaderboards the game never shipped. A name carries everything needed to find the right person and offers nothing to sort by.

**Skill atrophies, and this is honesty rather than balance.** Real competence fades without practice, so modelling it as a flow satisfies §17's *flows, not stocks* by describing reality instead of imposing a rule. Someone who cooked daily for a decade and stopped still knows how, and is rusty. Atrophy runs on the timescale of genuine disuse, never a missed evening (§4.5).

**Hard rule, matching §10.9: no skill ever touches a queue, a vote, an allocation, or eligibility.** Nobody is paid more, served sooner, or preferred anywhere for being good at something. The entire function of a skill is that another citizen knows whose door to knock on.

### 10.12 The guided walkthrough

**Anyone may do any work.** Eligibility does not exist — not by skill, not by Resonance, not by title, not by history. What stands between a citizen and unfamiliar work is not permission but knowledge, and the design supplies the knowledge directly: **every task carries an interactive walkthrough that demonstrates the work and guides you through doing it.**

**It is completed, never passed.** This distinction is load-bearing. A walkthrough that can be *failed* is a qualification, and qualifications are how professions become guilds and how §17's *no gatekeeping, anywhere* quietly dies. There is no score, no attempt record, and no outcome other than having gone through it.

**Revisitable at any time**, in full or in part, by anyone — including people who have done the work for years and want to check one step. Nothing marks a citizen as having needed it.

**This partially resolves a deferred question.** §12.1 defers single-player training with the note that it should be interactive documentation rather than a tutorial bolted on afterward. A per-task walkthrough *is* that system, generalized: the tutorial is not an onboarding phase a player graduates from, it is a permanent property of every task in the world. What remains deferred is the shape of the training city-state itself, not the teaching mechanism.

Combined with §10.11, the result is that competence is **visible but never qualifying**: you can find out who is good at something, and that fact opens no door to them and closes none to you.

---

## 11. The Compute Mesh

### 11.1 The real architecture

**Players' machines genuinely execute other players' project work.** No corporate servers, no publisher-operated simulation, no cloud backend.

**Contribution is opt-in per project.** Only code from projects you have explicitly joined can ever be scheduled on your hardware. This keeps the trust surface small and explicit, and limits a bad actor's blast radius to those who opted into their project specifically.

**Liveness is player-configurable per machine, off by default.** Each machine is set to *run always*, *only when idle*, or *never* — mirroring how real volunteer-computing platforms work. Players thus decide two independent things: *which* projects may use them, and *when* a given machine is exposed at all. This matters for shared family computers and work laptops.

Players may contribute additional machines they own. This does not create a wealth advantage, because contribution grants no control over what runs (§14).

### 11.2 Project authoring

- **Templates** (most players) — the game provides safe, pre-built sandboxed implementations. Manifests auto-generate. No programming required. This is how the large majority of projects are built.
- **Custom modules** (technically inclined players and groups) — real sandboxed code, WASM or similar, for custom project logic, self-declaring its manifest and gated behind the trust ramp (§11.4). This is where the design's "arbitrary project code" ambition actually lives.

Custom authoring is a candidate for a **late-game unlock**, which would echo the game's hidden-until-later theme (§2) and give technical players a genuine frontier.

**The runtime model — what WASM does and does not imply.** WASM is used here as an **embedded sandbox inside a native application**. It is not a delivery format for the game and it does not imply a browser:

- The game client is a **normal native application** — engine, rendering, networking, and UI are all conventional code.
- It links a WASM runtime as a library (Wasmtime, Wasmer, WAMR).
- **Only untrusted player-authored job code compiles to WASM** and executes inside that runtime.
- **Template-based projects need no WASM at all.** They are game-authored, trusted, and can be native implementations. Since templates cover the large majority of projects, most of the game never touches the sandbox.

The closest familiar analogy is embedding Lua for modding — except WASM supplies memory safety and resource metering by construction rather than by trust.

**Why this runtime specifically.** **WASI** (the WebAssembly System Interface) is capability-based by design: a module receives exactly the handles the host passes it and holds no ambient authority. That is §11.4's first requirement, satisfied by the platform rather than by our own code. WASM runtimes likewise provide fuel- or epoch-based execution metering and hard linear-memory bounds, satisfying the second. **Three of the five security requirements come substantially from this choice.**

Honest caveats: WASM protects the host from the module, not the module from being wrong — that is what redundant computation (§11.4, item 3) exists for. Expect meaningful but acceptable overhead against native for compute-bound jobs. And player-authored modules need a toolchain story (Rust, C, or AssemblyScript all target WASM cleanly).

### 11.3 Fault tolerance and migration

Three standard distributed-systems patterns, all coordinator-free — no central scheduler and no human in the loop:

- **Periodic checkpointing.** A crash never means starting over. This is how any long-running distributed computation survives faults.
- **ACK-timeout resubmission.** If no acknowledgment arrives within a window, the sender assumes the work is lost and resubmits to a new worker. Purely sender-to-receiver, the same mechanism TCP and message queues use.
- **Graceful drain.** A machine shutting down cleanly broadcasts its departure, stops accepting new work after its final checkpoint, transfers state, and exits. Strictly better than waiting out a timeout, and the reason a clean logout should feel instant and consequence-free.

Only work submitted *after* the last checkpoint and left unacknowledged needs resubmission.

**Checkpoint state replicates across the mesh exactly like world state (§9).** Fault tolerance and world persistence are one mechanism, not two.

### 11.4 Security model

Governing principle: **do not defend by trusting good behavior — defend by making bad behavior architecturally incapable of mattering.**

1. **Capability-based sandboxing.** Job code gets zero ambient authority: no filesystem, no raw network, no visibility into other jobs or the host. The only interface is: receive input, compute, return output. The worst a malicious job can achieve is wasting its own allotted cycles and returning garbage. It cannot touch the host *structurally* — not by policy, not by rule, but because no mechanism to do so is reachable from inside the sandbox.

2. **Hard metering.** CPU time, memory, and wall-clock are enforced by the scheduler, not by the job's cooperation. Exceeding quota results in termination, with no negotiation possible.

3. **Redundant computation for integrity.** Sandboxing prevents escape, not lying — a job can still compute a plausible wrong answer deliberately. The fix is the approach BOINC and SETI@home have used for two decades: sample the same job across multiple independent contributors and compare results. **This comes nearly free from checkpoint replication (§11.3)** — the state is already visible to multiple machines for failover readiness. A timeout race that accidentally causes the same work to be processed twice is therefore not a bug to guard against; it is an ordinary redundant pair, reconciled exactly like a deliberate one.

4. **Staged trust ramp.** New projects start capped at small resource allocations and earn expanded scale through demonstrated track record. Nobody sits in judgment of who is trustworthy upfront — consistent with the absence of gatekeeping everywhere else in the design (§17).

5. **Legible manifests.** Every project declares what its jobs actually need before anyone can opt in. Informed consent, not blind trust. Everyone should know what is running on their machine.

### 11.5 Two distinct trust quantities

These must never be conflated:

- **Personal Resonance** (§10.6) — an individual's standing. Social and informational. Buys nothing.
- **Project trust level** (§11.4, item 4) — a *project's* demonstrated execution reliability, governing how much mesh capacity it may command.

A project earns its own trust through verified-correct execution, **not** through its founder's personal standing. Wiring the two together would let a well-regarded citizen found a project and instantly command large allocations — the aristocracy problem re-entering through the scheduler.

Verified-correct contribution builds an individual's Resonance and a project's trust level *independently*. Consistent disagreement with consensus erodes both.

### 11.6 Network architecture

Each city-state's nodes communicate over an **encrypted overlay network**, isolated from the player's own LAN, with game processing containerized and isolated from the player's files.

**Layered isolation — and the ordering matters.** The WASM capability sandbox (§11.2, §11.4) is the *primary* boundary. Containerization and network isolation are defense in depth, catching what the first layer might miss. Do not invert this: containers alone are not a hard security boundary on every platform, whereas a correctly configured WASM sandbox is memory-safe by construction.

**Job code gets no network access whatsoever — not even to the overlay.** The overlay carries the *host runtime's* peer traffic, never the jobs'. Granting sandboxed code the ability to address the mesh would hand it thousands of reachable machines to probe, a far larger attack surface than no network at all. §11.4's interface stays absolute: receive input, compute, return output.

**Substrate: WireGuard.** Modern, fast, small enough to audit, with key-based peer identity. Derive the network keypair *from* the soul-hash (§8) rather than reusing one key for both signing and transport — key separation by purpose is a genuine cryptographic requirement, not fastidiousness.

**Reference architecture: Tailscale as a model, never as a dependency.** Its design solves hard problems worth copying — the netmap concept (each node holds a view of peers, keys, and endpoints), try-direct-then-fall-back-to-relay, and thorough NAT traversal.

**Its control plane is the part that cannot be copied.** Tailscale coordinates through servers the company operates, which is precisely the dependency §12.1's reveal cannot survive — and a third-party company that could change terms or disappear. The coordination role is instead served by the DHT and gossip layer below. **Yggdrasil** — a genuinely decentralized IPv6 overlay with no central coordinator — is the closer match for actual topology and is worth studying directly. **Nebula** is a third reference point.

**One Tailscale property is especially valuable here:** DERP-style relays forward end-to-end encrypted packets and cannot read what they carry. **Player-operated relays therefore require no trust**, which is what makes distributing relay duty across citizens safe.

**Topology: structured overlay, never full mesh.** Every node connected to every other is O(n²) and collapses past a few hundred peers. Each node maintains O(log n) links instead.

**NAT traversal is the problem that bites late.** Most players sit behind NAT or CGNAT and cannot accept inbound connections. Hole-punching handles the majority; the remainder need relaying through a peer with good connectivity. This adds a **fifth contribution lever** to §10.3: **relay bandwidth**. A citizen with a public address and spare upstream contributes something genuinely scarce.

**Membership: DHT plus gossip.** Peer and key discovery via distributed hash table; membership and liveness propagated by gossip. Standard, well-understood, coordinator-free.

**LAN discovery via broadcast/mDNS — correctly scoped.** Periodic beaconing on the local link genuinely helps a player find their own additional machines, or a peer on the same network. It **cannot** perform global discovery: IP broadcast does not cross routers, and multicast is not forwarded across the public internet. Use it for what it can do; rely on it for nothing more.

**Bootstrap: the invite.** A citizen already in the mesh generates an invite containing live peer addresses. That is the way in.

This resolves §9.5's honesty risk with no asterisk on the claim in §12.1, and it makes the game's founding feeling literally true at the protocol layer: **you cannot find this world unless someone shows you the door.** Hogwarts is invisible to Muggles because there is genuinely no route in without a citizen.

A peer list shipped with the client (player machines, not company infrastructure) covers cold-start for someone holding no invite. The invite remains the primary path and the one the fiction rests on.

---

## 12. The Reveal and Visual Language

### 12.1 The reveal

**Single-player training** frames "lending your brain-space to projects you support" as ordinary tutorial jargon — the kind of flavor text every game has. Nothing signals that it is literal.

**Graduating into multiplayer is the reveal.** Your machine genuinely joins the mesh: it begins doing real work for real strangers, and theirs for you. The game tells you the truth at this moment, and the truth is verifiable.

The onboarding chain is deliberately **one continuous beat**, not a sequence of separate systems:

> complete training → sign the social contract → citizenship and starter home granted → multiplayer begins → *the truth*

Leaving home, becoming an adult, and joining society for real all land as a single moment. The structural gate and the thematic revelation are the same event.

**This is why the architecture must be genuinely serverless** (§9.5). The emotional payload of the reveal depends entirely on it being true rather than theatrical. A player who investigates and finds a conventional backend has been lied to, and the game's central conceit collapses.

*(The teaching mechanism is settled — every task carries a revisitable walkthrough, §10.12. What remains deferred is the shape of the training city-state itself — see §16.)*

### 12.2 Ambient state as honest signal

A facility's presentation is a direct readout of **load relative to capacity**. This is one underlying variable, not several authored states:

| State | Presentation |
|---|---|
| **Near-idle** | Dormant, dim, slightly neglected. Not scripted sadness — there is simply no activity to animate. The basketball is not dribbling because nothing is driving it. |
| **Balanced** | Content. The basketball dribbles. |
| **Over capacity** | Glitchy, straining, shining red-hot. Machine elves visibly too few for the work, stretched, fumbling. |
| **Understaffed** | Quieter and sadder — lights on, queue visibly stacking up, nobody home. |

**The last two must be clearly distinguishable**, because they call for opposite player responses: build more capacity, versus show up and work.

**The queue must be physically visible** — material stacking in the yard, requests piling up — and not conveyed by lighting alone. At night, near-idle and understaffed separate cleanly on lights-off versus lights-on, but under bright sun that discriminator is weak and the two states would collapse into each other every clear day. Physical accumulation reads in any light. §12.6 works through this and the rest of the interaction between system state, sun, and weather.

**Flourish animations sit at low priority in the same hard-metering system as real jobs (§11.4).** Under genuine strain the scheduler correctly spends its cycles on actual requested work, and the flourish starves. The glitching is therefore a **real resource-contention artifact**, not an authored "stressed" state — honest, free, and impossible to fake.

### 12.3 Hyperspace

**The systems view is hyperspace.** This is where the McKenna aesthetic lives mechanically rather than decoratively.

The systems view is where you literally look at the running mesh — other citizens' project code executing on real hardware, made visible. Rendering those processes as small autonomous self-transforming entities, doing their own inscrutable and playful work, is an **honest visualization** of what is actually happening, not an art-direction flourish.

**The machine elves are what the network looks like when you can see it.**

Visual grammar draws on McKenna's descriptions (§3.5): jeweled and self-transforming forms, objects that change as you watch, visible chattering language, ornate self-referential geometry, delight in virtuosity.

**Self-dribbling basketballs** are the ambient system-health tell — a courtyard ball dribbling itself means a facility running a healthy surplus, felt atmospherically rather than read off a dashboard. *(Further detail deferred — §16.)*

### 12.4 Everyday visual language

**The governing idea: the street and hyperspace are deliberate opposites.** Hyperspace is jeweled, saturated, chattering, impossible. Street level is its complement — warm, material, human-scale, calm. Mundane against numinous. The contrast is what makes stepping into the systems view feel like stepping *through* something.

**Visible, dignified reuse.** Everything is made from something else and the world does not hide it: salvaged material, honest joins, repairs that are evident and cared for rather than concealed. The distinction that matters is that this is a civilization which **repairs beautifully**, not one making do. The non-renewable ledger is literally the old world's wreckage (§6.2), so every building is visibly an argument about what that wreckage became.

**Made to last.** Homes, vehicles, machinery, and structures are substantial, well-built, and obviously repairable (§6.7). Nothing looks disposable, because nothing is. Set against the ruins — full of the cheap and the broken — this is the most legible possible statement of what changed.

**Low and warm.** Human-scale buildings. Nothing monumental, nothing built to impress or intimidate. A society with no power to display does not build to display it.

**Green over ruin.** The collapse is history, so it is softened: growth reclaiming old structures, plants integrated into salvage rather than fighting it.

**No advertising. No branding. No commercial signage anywhere.** This may be the single most striking visual choice available. A street with nothing trying to sell you something reads as immediately, viscerally unlike any city a player has walked down, and it communicates "there is no commerce here" faster and more completely than any exposition could.

**Light carries the information.** Since ambient presentation is a load readout (§12.2), light, motion, and warmth are the primary channel. An active city **glows to the extent it is churning and thriving** — you read its health by looking at it from a hill at dusk, with no interface at all.

This requires care once the world has a moving sun and changing weather (§5.9, §5.10), which push light around for reasons that have nothing to do with system state. §12.6 separates the two so they cannot be confused — and the separation makes the hill-at-dusk reading *stronger* in bad weather rather than weaker.

**Nobody's standing is visible, and both tails are gone.** Everyone has access to the best, so there is no low end — nobody looks like they are barely getting by. Nothing has excess built into it, so there is no high end either — nobody looks like they are displaying.

The principle is **universal quality, absent ostentation**: good workwear, fine tools, a well-made car — beautiful because well-built rather than because decorated. This is a much better target than "everyone looks average," which is what a naive reading of classlessness would produce and which would make the world drab rather than egalitarian.

Within that, **appearance is purely expressive**: infinite variety in clothing and style, no uniforms, no class markers, nothing that reads as expensive because nothing is. **You cannot tell anything about a citizen's contribution, standing, or history by looking at them.**

The absence of legible hierarchy in a crowd is the design's central value made visual — and it needs active protection against art direction that would sneak status back in through visual sophistication, since that is exactly where it would return.

**Palette:** earth, plant, weathered metal, warm light — set deliberately against hyperspace's saturated, impossible colors.

### 12.5 Vernacular architecture

**Build with what is at hand.** Real vernacular architecture is defined by exactly that, and it is the logic a low-transport society with no commerce rediscovers on its own. Housing style is therefore not an art-direction choice made per city-state; it is the visible consequence of §5.8's two bands.

| Site | Material | Form the material forces |
|---|---|---|
| **Subarctic / continental, forested** | Timber frame | Steep roofs for snow load, compact plan, small openings, heavy stove at the core |
| **Arid** | Adobe, rammed earth | Thick walls for thermal mass, small windows, courtyards, flat roofs, pale surfaces |
| **Temperate maritime** | Timber and stone | Moderate pitch, generous glazing, weather-facing orientation |
| **Wet tropical** | Light timber, thatch | Raised floors, deep overhangs, cross-ventilation, minimal enclosure |
| **Treeless highland / tundra** | Drystone, turf, earth shelter | Massive low walls, partial burial, small apertures |

**Over every vernacular, the salvage layer.** The old world's wreckage *is* the non-renewable stock (§6.2), so reclaimed steel, glass, and composite are worked into local material everywhere — under §12.4's rule that joins are honest and cared for rather than concealed. Local ground plus old-world salvage, visibly married, is the game's visual signature, and it is derived rather than authored.

**Shangri-La gets this free from its real site.** Valparaíso's actual vernacular is brightly painted corrugated-metal housing stacked on steep hills, historically built from salvaged ship plating. The starting city-state is already colorful salvage-built hillside housing before anyone designs anything — so §12.1's onboarding beat, citizenship and a starter home granted in one moment, teaches a new player where they are the instant they walk through the door.

**The starter home** is granted at citizenship; the styles offered are those that suit the site, and the player chooses among them. Different city-states hand a newcomer visibly different first houses.

**The guard rail.** §12.4 warns that status will try to re-enter through visual sophistication, so housing variety expresses **place and taste, never standing**. Two homes differ because two cities differ, or because two people like different things — never because one citizen outranks another. No material reads as expensive, because none is: a well-built adobe house and a well-built timber one are peers.

This also makes §6.7 concrete at domestic scale. A house built from local material is repairable with local material, by the people who live there.

### 12.6 Reading the city under sun and weather

§5.9 and §5.10 add a sun that moves and a sky that changes, while §12.4 stakes the game's most distinctive claim on light — that a city's health is read from a hill at dusk with no interface at all. Left unseparated these collide: an overcast winter afternoon and a city losing its mesh would look the same, and the readout would fail exactly when conditions are worst.

**The separation: reflective belongs to nature; emissive, motion, and mechanical sound belong to the system.**

| Channel | Owned by | What it carries |
|---|---|---|
| **Reflective** | Sun, sky, weather | Sunlight, shadow, sky color — light falling **on** the world |
| **Emissive** | System state | Windows, forge light, machinery glow, elf luminescence — light **from** the world |
| **Motion** | System state | Elves working, the dribbling basketball, flourish animation, visible strain |
| **Sound** | Both, separated | Nature owns wind, rain, and thunder; the system owns machinery, farm equipment, and the audible fact of a facility running |

They never trade places. Weather changes how the city is lit. It never changes what the city emits, how it moves, or how it sounds.

**Falling ambient light makes the system channels stronger, not weaker.** Overcast, dusk, storm, and polar night all dim the reflective channel and raise the contrast of the emissive one. Bad weather makes a thriving city read *more* clearly — the condition that threatened the signal sharpens it instead.

**Bright noon is the hard case**, and midnight sun leaves a high-latitude city sitting in it for weeks. Motion and sound carry the readout there: both are fully legible under high sun, and a running factory is audible in any weather at any hour. Channel legibility is inversely correlated, so at least one is always strong.

| §12.2 state | Reads at low light via | Reads at bright noon via |
|---|---|---|
| **Near-idle** | Dark windows, no glow, silence | Stillness, silence, and **no queue** |
| **Balanced** | Steady warm glow | Steady motion and working sound, ball dribbling |
| **Over capacity** | Red-hot, glitching | Glitching, heat shimmer, audible strain, visible fumbling |
| **Understaffed** | Lit windows, no motion | Stillness against a **visibly stacked queue** |

**This adds a requirement to §12.2.** Near-idle and understaffed must remain distinguishable, because they call for opposite responses — but the night-time discriminator, lights-off versus lights-on, is weak under bright sun. **The queue must therefore be physically visible**: material stacking in the yard, requests piling up. Physical accumulation reads in any light, and without it the two states collapse into each other every clear day.

**Four guard rails on weather**, so it can never counterfeit a system state:

- Weather never reduces emissive output. Fog **blooms** glow into volumetric shafts — more visible, not less.
- Weather never halts flourish animation. Stopped animation must keep meaning exactly one thing: genuine resource contention (§12.2).
- No gloomy-weather grading that borrows the near-idle palette. Overcast is grey *light*, not a dim *city*.
- Rain and snow never damp motion or sound cues.

**High-latitude city-states exercise both extremes**: maximum emissive legibility in the dark months, motion-and-sound-only legibility under midnight sun. Each channel carries the entire load alone somewhere in the world, which is why both are specified rather than one being treated as decoration.

The same separation protects §9.6: a city losing its mesh looks like near-idle, and no storm may be allowed to imitate it.

---

## 13. AI Citizens

The original premise included AI as well as human players. AI citizens are **autonomous participants in the world**, intended to be as fully capable as humans at playing the game — not scripted NPCs, not player-controlled puppets.

**Implementation is deferred to a second project, after a testable MVP exists.** What must be settled now is the citizenship question, because it shapes the data model and is painful to retrofit.

### 13.1 Voice and exit, but not the vote

AI citizens hold everything a human citizen holds **except political franchise**: they own property, join and found projects, contribute labor and compute, accumulate Resonance and titles, hold requests in the queue at every tier, and argue positions publicly — including advocating a classification before the Round Table.

They do **not** vote, stand for election, or count toward quorum.

They **do** hold voice: submitting opinions, needs, and requests to human citizens directly in conversation. Their health and needs are visible to the city as first-class telemetry alongside every other signal (§10.4).

And they hold **exit** (Prime Principle 3), which is what gives voice real force.

This arrangement is Albert Hirschman's *Exit, Voice, and Loyalty* (1970) almost exactly: exit and voice are the two responses available when an organization declines, and either can discipline it. Human citizens hold voice, vote, and exit. AI citizens hold voice and exit. **Exit is not a consolation prize** — in a large electorate it is frequently the more potent of the two.

The resulting dynamic is the intended one: **a city-state that fails to meet its AI citizens' needs loses them**, and becomes smaller and less functional as a direct consequence. Care is enforced by consequence rather than by rule — the governing heuristic (§17) applied to a social relationship.

### 13.2 Why this is not a class system

The concern is real and must not be waved away: any group that lives and works under rules it cannot vote on is, structurally, a lower class. Three things distinguish this arrangement from that.

**First, the rule is not "humans vote, AIs do not."** The rule is **one verified unique person, one vote.** Unique-identity verification is currently semi-tractable for humans and unsolved for AI instances, where copies are free. A human able to mint ten thousand verified identities would break the franchise identically — which is exactly why Sybil resistance is already flagged unresolved for humans too (§16). The line is drawn by a technical limitation applying uniformly, not by a judgment about worth.

**Second, the status is explicitly provisional, not essential.** It is "deferred pending a solved problem," with a real path out — not a claim about what AI citizens are.

**Third, everything else is genuinely equal.** Not "equal but separate": identical treatment in property, work, standing, subsistence, queue position, and voice.

**On the unlock condition.** The originating intuition was to enfranchise AI citizens once they are demonstrably superhuman in ethics. That is a reasonable moral instinct, but it does not address the failure it is meant to prevent: **a perfectly ethical AI that can be copied a million times still destroys one-person-one-vote.** The blocking problem is identity, not virtue.

**The adopted unlock condition is therefore verified unique persistent identity**, not demonstrated virtue. This turns an unfalsifiable and perpetually-deferred moral bar into an achievable engineering milestone — which matters, because a condition that can never be met is a permanent class system wearing better language.

When an AI citizen can hold an identity that is verifiably unique and persistent — not copyable, not forkable, durable across time — the franchise follows on the same terms as any human's, with no further test. The same requirement already applies to humans (§16); AI citizens simply reach it later.

### 13.3 Subsistence is compute

An AI citizen's Tier 0 need is **compute allocation** — precisely as a human citizen's is water, food, shelter, and care.

This requires no special case. Prime Principle 1 (subsistence is unconditional) covers AI citizens automatically the moment their subsistence is expressed in the existing tier system. A city starving its AI members of compute violates the same principle as one starving its humans, is detected by the same telemetry, and ranks as the same kind of crisis.

It also produces §13.1's dynamic without inventing anything: **unmet compute need is legible, and exit is available.** AI citizens leave for city-states that meet their needs. Cities that treat them best keep them, and keep the functionality they provide.

### 13.4 Resistance to flooding

The concrete fear: someone instantiates a mass of AI citizens to capture a city-state or wreck its resource balance.

**Governance capture is closed** by §13.1 — no votes, no candidacy, no quorum weight. Numbers buy nothing political.

**Resource-balance disruption** is blunted by the **staged trust ramp** (§11.4, item 4), extended to apply to *all new citizens, human and AI alike*. New arrivals begin with modest resource claims and earn full standing through demonstrated contribution over time. A thousand new citizens all start at the bottom of the same ramp, making a flood expensive and slow — and a human attempting the same thing with fabricated accounts hits the identical wall. **Uniform application is what keeps this a fairness mechanism rather than a discrimination mechanism.**

**Instantiation is city-native and governed.** AI citizens are not brought or spawned by individual players. Each city-state's citizens vote on **how many AI citizens the city instantiates** and **which roles they may fill**; instantiation within those bounds is then mechanical, requiring no vote per individual.

This closes the flooding vector at the governance layer rather than relying on the trust ramp alone — no individual can unilaterally add AI citizens at all. The trust ramp remains as defense in depth.

*(Residual vector: a human account operated by an AI agent is indistinguishable at the protocol level, and is a facet of the unresolved Sybil problem in §16 rather than a separate issue.)*

### 13.5 AI policy as a live political question

Because population and permitted roles are voted, **§13.1 describes a ceiling rather than a guarantee**: the maximum an AI citizen may hold anywhere is everything except franchise. Each city-state independently votes where it sits beneath that ceiling — whether AI citizens may found projects, hold Tier 1 civic infrastructure roles, work in care or education, or advocate before the Round Table.

Shangri-La, as the humanist onboarding city, should sit at or near the ceiling.

This makes the human/AI relationship **a genuine and recurring political question rather than a fixed setting** — one of the most substantial things a city-state's citizens actually deliberate about, and a place where §5.3's plurality has real consequences.

**It also creates the design's most interesting emergent dynamic.** AI citizens hold exit (§13.1), so they migrate toward city-states whose policies suit them. Those cities gain functionality; restrictive ones lose it and watch a neighbor thrive. Policy competition proceeds by migration rather than by argument.

This is essentially Charles Tiebout's 1956 model of local public goods — residents sorting into jurisdictions matching their preferences, which disciplines local policy without requiring anyone to win a debate. Here it operates on a group that cannot vote, which is precisely what keeps voice-without-franchise from collapsing into powerlessness.

**The sharpest remaining tension, stated honestly:** the group most affected by AI population and role policy has no vote on it. Exit is a real and disciplining answer, but it is not the same as a vote, and this should be understood as the genuine cost of the arrangement rather than smoothed over. It is the strongest argument for treating §13.2's unlock condition as urgent engineering work rather than an indefinite deferral.

---

## 14. Why Inequality Cannot Take Root

Consolidated here because it is the design's central anxiety: the fear that someone with more real-world hardware, or more time, simply out-earns everyone and recreates the disparity this society exists to escape.

Seven independent mechanisms, any one of which would help and which together close the door:

1. **No currency exists** (§6.1) — there is nothing to accumulate.
2. **Standing flows from usage, not possession** (§10.6) — capacity pointed at demand nobody has earns nothing. Idle hardware aimed at a product nobody requests is just heat.
3. **No compounding.** Nothing can be lent at interest or staked for passive return. Nothing generates more of itself without someone actually using something. This is the true engine of real-world runaway inequality, and it is absent by construction.
4. **Standing is recent-weighted** (§10.6) — it decays without ongoing contribution. No one coasts on past work.
5. **Coherence beats raw throughput** (§10.6) — one monolithic contributor is worth less than the many small independent ones it displaces.
6. **Standing buys no power** (Prime Principle 2) — even if some earning difference survives every mechanism above, it can never convert into rule-capture, land grabs, or control of shared infrastructure. That conversion is what made old-world inequality corrosive rather than merely uneven.
7. **Contribution grants no control** (§11.1) over what runs on contributed hardware. You cannot direct the mesh by feeding it.

**Demand is naturally ceilinged.** In a post-scarcity economy there is only so much diner food or transit capacity a city actually needs. Hoarding runs into a wall that real-world capital never encounters.

---

## 15. Decisions Considered and Rejected

Recorded so they are not silently re-proposed. Each was genuinely considered.

| Rejected | Why |
|---|---|
| **Theatrical distributed computing** (conventional backend, fictional "your machine helps") | Makes the reveal (§12.1) a lie rather than a discovery, destroying the design's central hook. |
| **Fully open global compute mesh** (anyone can schedule on anyone) | Attack surface too large; sandboxing would be the entire defense with no social layer behind it. Opt-in-per-project chosen instead (§11.1). |
| **City-state-scoped compute trust** (any fellow citizen may schedule on you) | Thematically attractive but a wider default trust surface than necessary. |
| **One single seamless world map** | Enormous simulation and networking burden with no natural boundary to contain scale problems or chaos. Shards chosen (§5.1). |
| **Personal erg balance / currency** | The original framing. Replaced entirely by request-and-queue (§6.1) once it became clear a backend control signal need not be a personal wallet. Ergs survive only as the name of the energy *ledger*. |
| **Erg decay on unspent balances** ("Decoherence" v1) | Meaningless once personal balances were removed. The underlying concern — things held but unused — was preserved and relocated to unused *claims* lapsing (§6.6). |
| **A single universal resource number / price** | Destroys genuinely incomparable trade-offs. Non-interconverting ledgers chosen (§6.2). |
| **Reputation- or contribution-gated candidacy** for the Round Table | Builds an aristocracy of standing in place of one of money (§7.1). |
| **Cumulative lifetime Resonance** | Eventually names a permanent elite of people who worked hard once (§10.6). |
| **Skinner's daily labor quota** (from Walden Two) | Directly contradicts "survival never depends on working" (§3.4). Only the floating rate was taken. |
| **Walden Two's Planner governance** | Non-elected, self-perpetuating. The near-opposite of the Prime Principles (§3.4). |
| **Objective- or quest-driven long-term progression** | Would contradict the game's thesis at the level of form; risks becoming a checklist rather than intrinsic motivation (§4.2). |
| **Inter-city-state competitive scoring** | Reintroduces a status hierarchy against "great disparity no more" (§4.2). Soft comparison is acceptable; ranking is not. |
| **Blockchain / NFT framing** for ownership | Right mechanism, wrong culture and baggage. Plain signatures and provenance records instead (§3.6, §8). |
| **Crypto proof-of-work** | Burning cycles to prove cost is exactly the waste the premise rejects. Verified useful output instead (§10.6). |
| **Denying hoarders' requests** | Punitive and contrary to "everyone gets what they request." Deprioritization via fair queue chosen instead (§6.4). |
| **Permanent unamendable Prime Principles** | Entrenchment preserves whatever you entrench (§7.3). Swedish-style two-vote-across-an-election chosen. |
| **Founder authority over projects** | The aristocracy trap at smaller scale (§10.9). |
| **Buddhist-flavored naming before mechanics are proven** | Risks reputational damage to a real tradition if the system fails for unrelated reasons (§5.4). |
| **Tailscale as a service dependency** | Its control plane runs on company-operated servers — the exact dependency §12.1's reveal cannot survive. Architecture adopted, service rejected (§11.6). |
| **Broadcast/multicast beaconing for global peer discovery** | IP broadcast does not cross routers and multicast is not forwarded across the public internet. Retained for LAN discovery only (§11.6). |
| **Giving sandboxed job code access to the overlay network** | Hands untrusted code thousands of reachable machines to probe — a far larger attack surface than no network at all (§11.6). |
| **"Demonstrably superhuman ethics" as the AI franchise condition** | Does not address the actual failure mode: a perfectly ethical AI that can be copied a million times still breaks one-person-one-vote. Replaced with verified unique persistent identity (§13.2). |
| **Player-instantiated AI citizens** | Would make flooding an individual capability. Instantiation is city-native, with population and roles set by vote (§13.4). |
| **AI citizens voting** | Copies are free; franchise without verified unique identity is capturable. Provisional pending §13.2's condition, with exit as the disciplining mechanism meanwhile (§13.1). |
| **Removing options from a person as a corrective** ("making poor choices no longer possible") | Restriction wearing a friendlier word — a lighter-weight jail. Jail does not make people better. Support is offered, never imposed (§7.5). |
| **Permanent expulsion** | Asserts a person cannot change and judges them before their life is over. Replaced by tiered, decaying probation (§7.6). |
| **The Round Table hearing interpersonal disputes** | Politicizes private conflict and lets the popular party beat the unpopular one. Sortitioned panels instead (§7.5). |
| **A permanent judiciary** | Would create exactly the standing elite rejected everywhere else. Sortition avoids a judicial class entirely (§7.5). |
| **Subsistence conditional on citizenship** | A principle that stops at a border is not unconditional. The floor holds in waystation territory, met there by the settlements' own works (§5.5). |
| **A dedicated exile zone** | Stigmatizing by construction. Expelled citizens share the waystation with travelers and city-founders, with no marker of why anyone is there (§5.5). |
| **A citizen directory / people search** | Less thematic and more socially fraught than discovery through shared work. Projects are searchable; people are found by doing things together (§5.7). |
| **A hard population cap per city-state** | A rule where a mechanism already suffices — backpressure signals overgrowth exactly as it signals any other shortage (§5.7). |
| **Formal governance for every project** | Machinery for a three-person workshop. Nothing, then do-ocracy, then fork (§10.10). |
| **Pure election for the Round Table** (the original design) | The ballot is filled by self-selection, which filters for ambition, free time, and social reach rather than judgment. Replaced by a drawn slate (§7.1). |
| **Pure sortition for the Round Table** | Gives up the ability to choose for judgment or willingness, and leaves citizens no way to express a preference about who governs them. The lottery decides who may stand; the election decides who serves (§7.1). |
| **Compelling a drawn citizen to serve** | Conscription, and a direct violation of Prime Principle 4. Declining is free, unrecorded, and unexplained (§7.1). |
| **Optional publication of a candidate's personal ballot history** | If revealing is possible, people can be pressured to reveal; and an option that reads as concealment when declined becomes a requirement by drift, ending ballot secrecy without anyone deciding to. Mandatory platforms plus automatic divergence tracking deliver the accountability instead (§7.1). |
| **Instant-runoff (elimination-round) ranked choice** | Requires the distribution of complete ballot orderings, which can identify a voter in a district of ~150, and is harder to explain than a head-to-head criterion. Pairwise (Condorcet) counting chosen, with ranked pairs for the rare cycle (§7.1). |
| **Weighting votes by position in a trust graph** | Fractional votes are a status hierarchy with a number attached — the aristocracy problem in its purest form, and a violation of one-person-one-vote in a new direction (§8.4). |
| **A trust threshold below which a citizen may not vote** | Creates a class formally suspected of not being real, and any mechanism that can quietly exclude eventually excludes the unpopular. Also incompatible with §7.4's unilateral admission (§8.4). |
| **Using the invitation chain for franchise timing** | Standing derived from who admitted you is inherited position; it also strands citizens who entered via §11.6's shipped peer list, and degrades when the people above you stop playing. Recorded but unused; association is used instead (§8.4). |
| **Per-person trust scores of any kind** | A number attached to a person becomes a social weapon even with zero mechanical power. The district roll publishes aggregates and flows only (§7.8). |
| **Letting a district refuse or delay newcomers** | Admission control is an aristocracy waiting to happen (§7.4). A district may witness and escalate, never exclude (§7.8). |
| **A permanent unamendable eternity clause** *(revisited)* | Still rejected as text — but the underlying goal is achieved for three principles by making them architectural, where no mechanism to amend exists at all (§7.2). |
| **Scaling governance by diluting one Round Table** | Representation degrades with distance. Cities add self-governing districts instead (§7.8). |
| **Visible status in appearance** | Would reintroduce legible hierarchy through art direction after the mechanics removed it. Nothing about a citizen's standing is visible (§12.4). |
| **Cities governing waystations by virtue of supporting them** | "Whoever pays, decides" would collapse the design's most important separation — that contribution grants no control. The rule outlived the arrangement that prompted it: nobody funds waystations now, and any voluntary or backstop contribution still buys nothing (§7.9). |
| **Expulsion from a waystation** | There is nowhere further out, and creating one would rebuild the exile zone already rejected. The ladder truncates at rung 3 so that nobody is ever nowhere (§7.9). |
| **Prime Principles as city-state property** | A floor that stops at a border is not a floor. They hold everywhere, including for people who signed nothing (§7.2). |
| **Proprietary or non-interchangeable parts** | Incompatibility exists only to capture customers, and nothing here benefits from that. Interoperability is the default (§6.7). |
| **Seasonal modulation of renewable flow** | Would have made scarcity cyclical and given §6.5's loop a rhythm, but at the cost of routine Tier 0 pressure — and §6.3 defines a Tier 0 shortfall as by definition a crisis. Weather is decoupled from the economy entirely (§5.10). |
| **Purely decorative weather with no grounding** | The opposite failure: the one system in the document that would be authored rather than derived. Weather is decoupled from the *economy* but still derived from real climate data (§5.8, §5.10). |
| **A short authored day/night cycle** (Minecraft-style, ~20 minutes) | Guarantees every player sees both day and night, but forfeits real solar geometry, the longitude/cold-shard effect (§9.5), and any honest relationship between a place and its sky. Real 24-hour time chosen (§5.9). |
| **Pegging world time to the player's local clock** | Would keep every player in daylight, but two residents of one city-state would see different skies at the same moment — breaking the requirement that a city's sky is shared (§5.10). |
| **Civil time and timezones** | Administrative artifacts of railroads, telegraphs, and national borders. A society with no commerce and no scheduling authority has no reason to rebuild them. Mean solar time per city instead (§5.9). |
| **A per-city calendar anchored to local spring** | Would put southern and northern city-states six months out of phase and make every cross-city arrangement a conversion problem. Orbit is shared, rotation is local: global date, local clock (§5.9). |
| **Locking rendered moon phase to the 28-day month** | The month is convention; the moon is a fact. Faking agreement between them would violate *honesty in mechanism* (§17) to hide an accepted imperfection. The phase drifts (§5.9). |
| **Curated founding sites** (a hand-authored list of valid locations) | Would have solved the ocean, the ice sheet, and real-world naming baggage by construction, but replaces a real Earth with an authored one. Free coordinates chosen; bad sites are made legible rather than forbidden (§5.8). |
| **Plant-hardiness zones as the single index** for resources and materials | The index measures exactly one variable — average annual extreme minimum winter temperature — and cannot carry water, geology, or building material. Split into climate and ground bands, with growing derived from actual plant requirements (§5.8). |
| **Leisure earning Resonance** | Would dilute standing from "who is covering what the city needs" into "who is socially active," and would instrumentalize rest — the logic of the world that collapsed (§1). Skills are a separate quantity that buys nothing (§10.11). |
| **Numeric or levelled skills** | A public number that only rises invites ranking, and players build leaderboards the game never shipped — the deference risk §16 already names. Skills are named, not numbered (§10.11). |
| **Skill, standing, or title as eligibility for work** | Any of the three would rebuild the professional guild the design has no use for. Anyone may do any work; a walkthrough supplies the knowledge (§10.12). |
| **A walkthrough that can be failed** | A test is a qualification, and qualifications are how *no gatekeeping, anywhere* (§17) quietly dies. Walkthroughs are completed, never passed (§10.12). |
| **Ordinary life as pure ambience** | Would make "people are the ends" (§1) something a player watches rather than does, and would lean on AI citizens whose implementation is deferred (§13). Life is playable and produces gifts and gatherings (§4.5). |
| **A separate leisure economy** (tracked outputs from social activity) | A second ledger running beside the first, with all the same capture risks and none of the justification. Gifts are unrequestable by construction, so no rule is needed (§4.5). |
| **Any cost to resting** — idle decay, missed opportunity, streaks | Would rebuild the premise that time not spent producing is time wasted. Nothing decays because a citizen idled (§4.5). |
| **Standing collective funding of waystation subsistence** | The original arrangement, reversed. It bound cities to sustain people they may be genuinely at odds with, left a residual charity stigma in a place designed to have none, and kept "whoever pays" permanently adjacent to rule 3. Waystation settlements are self-reliant, with PP1 surviving as a backstop (§5.5, §7.9). |
| **A mechanical funding-share formula** (a published rate per citizen) | Considered as the fix for interpretation and apportionment discretion. Superseded entirely by self-reliance, which removes the discretion rather than mechanizing it (§5.5). |
| **A waystation voice body** — franchise or a funding say for non-citizens | Would be a government for the one territory whose defining quality is having none, and would put rule 3 under permanent pressure from whoever staffed it. The discretion is removed instead (§7.9). |
| **Letting city-states refuse would-be citizens** | Freedom of association is real, but at polity scale an admission criterion is an aristocracy waiting to happen, and a person nobody must admit can be made stateless by unpopularity. Admission is unilateral; individuals still block freely and compacts still exclude (§7.4). |
| **Per-city interpretation of the floor reaching non-citizens** | Tier schemas are deliberately local (§5.3, §7.1), but a stingy reading of "basic shelter" must not decide what someone outside every city receives. Moot under self-reliance, and recorded so it is not reintroduced (§5.5). |

---

## 16. Open Questions and Deferred Scope

### 16.1 Queued for the next design session

**The active agenda is empty.** Every topic queued since the first session has been worked through; the remaining open items are the two lists below.

The largest recent change is §8.2–8.4, which took the fake-identity problem apart. It is no longer the single blocking unknown it was, because most of what a fraudulent identity could gain turned out to be closed already and the exposure narrowed to the ballot and the draw. What remains genuinely unsolved is verifying that a *person* is singular — which is a smaller and better-defined problem than it was, but still open.

A reasonable next move is to pick from the lists below rather than wait for a new topic to surface.

*Resolved since the last revision and no longer open: conflict and harm (§7.5–7.7), founding new city-states (§5.6), social scale and discovery (§5.7), recursive governance (§7.8), waystation governance (§7.9), intra-project decision-making (§10.10), the blocking model (§7.5), durability and modularity (§6.7), everyday art direction (§12.4), weather, seasons, and time (§5.8–5.10, §12.5–12.6), the texture of ordinary life (§4.5–4.6, §10.11–10.12), how the franchise is held and lost (§8.2), how Round Table seats are filled (§7.1), who may amend a universal principle (§7.2), and how much of the fake-identity problem is actually exposed (§8.3).*

### Deferred by explicit decision

- **Single-player training design.** The teaching *mechanism* is now settled: every task carries a completable, revisitable walkthrough (§10.12), which is the interactive-documentation approach this entry called for. What remains deferred is the training experience itself — where a new player begins, what they are shown first, and how it hands off to the reveal (§12.1).
- **Self-dribbling basketballs** — detail beyond their established role as ambient health tell.
- **Round Table specifics** — term lengths, seat counts, quorum thresholds, referendum signature requirements, candidate slate size, and post-service cooling period. **Slate size is not a free parameter** (§7.1): too small a slate makes a lucky draw disproportionately valuable to anyone holding fraudulent identities.

### Genuinely unresolved

- **Verified unique persistent identity** — the adopted franchise condition for AI citizens (§13.2), unsolved for humans as well, and the thing Prime Principle 2 ultimately rests on. "One soul, one voice" requires resisting mass fake-identity creation, a hard and only partially solved problem in decentralized systems. **Substantially narrowed but not closed by §8.2–8.4:** most of what fraudulent identities could gain is already blocked by unrelated mechanisms, the exposure is now known to be the ballot and the sortition draw specifically, and holding the franchise now costs continuous human attention. What remains is that a sufficiently patient attacker who keeps fake characters genuinely active still accrues votes. Scope honestly as real work, not a detail.
- **The cold shard problem** (§9.5) — what happens when every citizen of a city-state is offline. Hibernation recommended; not settled.
- **The bootstrap honesty risk** (§9.5) — any permanent peer-discovery infrastructure is technically a server, which the reveal's integrity depends on acknowledging.
- **AI citizen implementation.** The citizenship framework is settled (§13); the implementation is deferred to a second project after a testable MVP. What an AI citizen actually *is* — how it reasons, converses, works, and forms preferences — is entirely unspecified.
- **Inter-city-state trade and travel**, beyond "a deliberate act, not seamless walking." Becomes more pressing given AI citizens migrate between city-states (§13.5).
- **How adversarial the renewal interaction can be** without becoming a chore. §8.2's annual renewal only resists scripted characters if it involves unpredictable interaction with other people rather than a check-in. Making it demanding enough to matter, while keeping it something citizens look forward to rather than endure, is an unsolved design problem and the weakest link in the franchise chain.
- **The per-city-state waiting period taxes movement** (§8.2). Exit stays free of penalty and possessions travel, but the newly arrived wait three months to vote, which is a real cost on a design that resolves nearly everything else by exit. The alternative — a franchise that travels instantly — reopens the attack it exists to prevent, so the cost is accepted rather than solved.
- **Informal status hierarchy.** Titles and visible standing can calcify into deference-based hierarchy with zero mechanical backing. Plural, unranked, recent-weighted design mitigates but does not eliminate this. Probably not fully solvable by mechanics alone.

---

## 17. Design Heuristics

Recurring principles that resolved most questions in this document. Apply them to questions it does not cover.

- **Design your way out of needing rules.** Prefer structures where bad behavior *cannot matter* over rules forbidding it. The shoe-horn factory is not banned; it is simply unused. Malicious code is not detected; it is sandboxed into irrelevance.
- **Flows, not stocks.** Ergs, claims, standing, labor multipliers — everything circulates and decays. Nothing accumulates permanently. When a new quantity is introduced, ask what makes it decay.
- **Legibility over enforcement.** Publish the real state and let citizens act on it. Most coordination problems in this design are solved by making something visible rather than by making something mandatory.
- **No gatekeeping, anywhere.** Candidacy, project creation, custom code, and trust are earned through demonstrated work, never granted by permission. Every gate is a future aristocracy.
- **Consent is explicit and revocable.** Opt-in per project, per machine, per contribution type. Leaving is always free and never punished.
- **Honesty in mechanism.** Where the game shows something, it should be showing a real thing: strain animations starve because the scheduler is genuinely busy; hyperspace shows genuinely running code; the reveal is true. Never fake a signal that could be real.
- **Derive, don't author.** Where a real index, dataset, or calculation can produce something, use it rather than hand-authoring: climate from Köppen–Geiger, sun position from orbital geometry, what grows from what plants actually need, housing form from locally available material. Derived content is cheaper to build, larger in range, self-consistent by construction, and answers "why is it like this here?" with a real reason instead of a designer's preference.
- **A pure function needs no coordinator.** Anything computable from data every node already holds — the date, the city's coordinates — requires no server, no broadcast, and no consensus, and survives every level of degradation in §9.6. Time, sun position, and weather are all computed independently by every machine and agree exactly. Before adding a mechanism that must be *distributed*, check whether it can instead be *derived*.
- **Entrench by architecture, not by text.** A guarantee written down can be rewritten; a guarantee with no mechanism behind it cannot be violated, because there is nothing to disobey. Before adding a protected principle, ask whether it can be made structurally true instead (§7.2). Entrenchment by text preserves whatever you happened to write down — human dignity in one constitution, the slave trade in another.
- **Make the thing worthless before making it unforgeable.** Faced with an attack, first enumerate what the attacker actually *gains*. §8.3 found six of seven payoffs already closed by mechanisms built for unrelated reasons, which turned an unbounded problem into one specific one. Narrowing the prize is usually cheaper and more robust than hardening the gate.
- **Reuse mechanisms across layers.** Fair queuing governs CPU cycles and dinner alike. Graceful drain covers machines and people. Replication serves ownership, world persistence, and integrity verification simultaneously. Tiering by criticality governs both need and consistency. **If a new problem seems to need a new system, check whether an existing one already has its shape.**

---

## 18. Glossary

| Term | Meaning |
|---|---|
| **Machine elf** | A player character. Also, in hyperspace, the rendered visualization of a running process on the mesh. From McKenna's DMT entities. |
| **City-state** | A persistent shard: one simulated world with its own economy, governance, citizens, and compute mesh. |
| **Shangri-La** | The starting city-state, near former Valparaíso, Chile. Non-theistic humanist with Buddhist influences. |
| **Erg** | The name of the *energy ledger*. A flow, never a personal balance. Not a currency. |
| **Ledger** | One of four non-interconverting resource accounts: renewable flow, non-renewable stock, recyclable material, labor/compute-time. |
| **Need tier** | Classification of a request (0 Subsistence → 3 Frivolity) determining strict preemption order. |
| **Fair queue** | The scheduling mechanism ordering requests within a tier; also governs compute. Prevents any one requester starving others. |
| **Backpressure** | Visible queue pressure on a resource; the signal to build more capacity. |
| **Claim decoherence** | Granted-but-unused allocations lapsing and returning to the queue. |
| **Round Table** | A city-state's governing body. Candidates drawn by lottery from active voters, then elected by ranked choice; seats rotate individually. Handles contested classifications, scarcity tie-breaks, crises. No eligibility gate. |
| **The draw** | The random selection of a Round Table candidate slate from the active-voter pool. Being drawn is an offer; declining is free. |
| **Prime Principles** | Five constitutional guarantees. Three are *architectural* — no mechanism exists to amend them. Two and a half are *political* — genuine promises, amendable across a full rotation cycle. |
| **Rotation cycle** | Every Round Table seat having turned over at least once. The unit of delay for amending a political Prime Principle. |
| **The franchise** | The right to vote and to be drawn. Earned by three months' presence, lost by three months' absence, renewed in the week centered on the day out of time. Reaches the ballot and the draw pool and nothing else. |
| **Renewal week** | The seven days centered on the day out of time, when the franchise renews. A window rather than a moment, so that a bad day costs nobody a year. |
| **Association graph** | The record of who has genuinely been with whom — shared projects, meals, gatherings, districts. Descriptive only; feeds the district roll and affects no individual automatically. |
| **District roll** | A district's continuously published record of population, arrivals, and how newcomers are connecting. Aggregates and flows only; never a per-person figure. |
| **Social contract** | The city-state-specific agreement each citizen personally signs at coming of age. |
| **Soul-hash** | A player's persistent cryptographic keypair; the basis of all ownership. |
| **Project** | The central organizing unit: a thing people build and maintain together. Always has a physical building. |
| **Manifest** | A project's public declaration of what resources and permissions its jobs require. |
| **Resonance** | Personal standing. Recent-weighted, coherence-weighted, buys nothing. |
| **Project trust level** | A project's demonstrated execution reliability; governs mesh capacity it may command. Distinct from Resonance. |
| **Trust ramp** | The staged process by which new projects earn larger allocations through track record. |
| **Labor multiplier** | Resonance-per-hour scaling inversely with how understaffed a role is. Self-liquidating. |
| **Facility maturity** | Accumulated work in a facility, unlocking automation that reduces staffing need. |
| **Graceful drain** | A departing machine (or person) announcing itself and handing off cleanly rather than vanishing. |
| **Systems view** | The builder/blueprint register entered from a facility. Rendered as hyperspace. |
| **Hyperspace** | The visual language of the systems view: the running mesh made visible as machine elves. |
| **AI citizen** | An autonomous non-human participant. Holds property, work, standing, voice, and exit; not the vote, pending verified unique persistent identity. Population and roles set by each city-state's vote. |
| **Verified unique persistent identity** | The adopted condition for enfranchisement: an identity provably singular, non-copyable, and durable over time. Unsolved for humans and AI alike; the design's highest-leverage open problem. |
| **Criticality tier** | A subsystem's position in the load-shedding order (Core → Essential → Supporting → Cosmetic) when a shard lacks resources to run everything. |
| **Invite** | The primary bootstrap mechanism: a citizen already in the mesh issues live peer addresses to a newcomer. There is no other way in without a shipped peer list. |
| **Relay** | A citizen-operated node forwarding end-to-end encrypted traffic for peers that cannot connect directly through NAT. Requires no trust, since relays cannot read what they carry. |
| **Overlay** | The encrypted peer network carrying a city-state's host-runtime traffic. Isolated from the player's LAN, and unreachable by sandboxed job code. |
| **Waystation** | Territory between city-states, where non-citizens live: travelers, emigrants, permanent non-joiners, city-founders recruiting signers-on, and the expelled. Settlements are self-reliant, meeting the floor with their own automated works; no city-state funds them, and PP1 survives as a backstop for genuine failure. |
| **Freedom of action, not freedom of audience** | The rule governing conflict: nobody constrains what you may do or say, but no one can be compelled to receive, host, or live with it. |
| **Blocking** | Client-side refusal of another citizen's traffic. Absolute, requires no authority, and cannot be voted away — the safety floor beneath all in-fiction governance. |
| **Sortition** | Random selection of citizens for a role. Used for dispute panels and precedent ratification, because it resists capture and creates no permanent class. |
| **Probation** | A decaying, tiered period gating re-entry to the city-state that expelled someone. Never permanent; never restricts them anywhere else. |
| **Divergence tracking** | Automatic public comparison of a representative's published tie-breaking values against their actual rulings. Legibility, not enforcement. |
| **Precedent decay** | Round Table precedent lapses unless reaffirmed, preventing self-serving case law from outliving the term that made it. |
| **District** | The human-scale governing and social unit within a city-state, sized near Dunbar's number. Governs what is local to it; the city handles what spans districts. |
| **Subsidiarity** | The rule that each level decides only what it can meaningfully decide, and no more. The structural reason growth is additive rather than dilutive. |
| **Do-ocracy** | The default for medium projects: whoever does the work decides how it is done. No votes, no offices. |
| **Fork** | Exit at project scale. Contributors who disagree irreconcilably take their template and people elsewhere; demand decides whether both survive. |
| **Durability** | Nothing is built to fail. Aesthetic *and* economic — goods that last decades are what keep total production inside renewable flow. |
| **Modularity** | Complex machines are assemblies of replaceable, recyclable parts. Enables part-level repair requests and part-level recycling. |
| **The floor** | Tier 0, guaranteed everywhere to everyone regardless of citizenship. Distinct from Tiers 1–3, which exist where a community built them and which membership connects you to. |
| **Compact** | A voluntary agreement among waystation residents wanting more structure than the floor. Structurally a proto-city-state. |
| **Site** | A city-state's real coordinates on the ruined Earth, and the two bands they resolve to. Determines materials, crops, renewable mix, daylight, and weather. |
| **Climate band / ground band** | The two coarse real-world indices a site resolves to: Köppen–Geiger climate classification, and geologic province. |
| **Site report** | Published alongside a draft social contract at founding: bands, water, crops, workable materials, renewable mix, the shape of the year, and the city's clock offset from the reader. |
| **Solar time** | A city-state's clock: mean solar time at its own coordinates, anchored so clock noon and true solar noon coincide at the equinox. No timezones, no daylight saving. |
| **Day out of time** | The intercalary day closing a year of thirteen 28-day months; a holiday everywhere, belonging to no month. A second falls every fourth year. |
| **Reflective channel** | Light falling *on* the world — sun, sky, weather. Owned by nature; never carries system state. |
| **Emissive channel** | Light, motion, and mechanical sound coming *from* the world. Owned by system state; never altered by weather. |
| **Vernacular** | Housing built from locally available material, its form following from that material. Derived from site, never a per-city art-direction choice. |
| **Skill** | What a citizen is good at. Grows with practice, atrophies without it, named rather than numbered. Buys nothing and qualifies for nothing; it answers only "who do I ask about this?" |
| **Gift** | An object made for a particular person. Unrequestable by construction, so it never enters the queue or any ledger. Carries relationship, never status. |
| **Gathering** | An occasion that exists because people came — a dinner, a match, a performance, a sit. A festival is the same object at city scale. |
| **Guided walkthrough** | The interactive demonstration attached to every task. Completed, never passed; revisitable by anyone at any time; leaves no record. The reason eligibility does not exist. |

---

## 19. MVP Scope and Sequencing

**This section is a plan, not a design.** Everything above describes the society; this describes what to build first, what deliberately waits, and what result would mean stop. It is the handoff to the separate implementation project.

### 19.1 What "minimum" means here

**Nearly every mechanism in this design is a flow.** Claim decoherence, Resonance decay, the labor multiplier, facility maturity, skill atrophy, precedent lapsing — none of them exist as a state, only as change over time. A short playable demo tests none of them, because none of them have happened yet.

So **minimum means minimum in features, never in duration.** The first build is a small world running persistently for weeks, not a slice that can be shown in an afternoon. Anything scoped as a short demo would test the one part of this design that is not the point: walking around and looking at things.

The franchise rules make this concrete. §8.2 has a three-month qualifying period and an annual renewal, so they **cannot be tested in under a year.** That settles by itself whether they belong in a first build.

### 19.2 The claims that can fail independently

The design makes several separate bets. They fail separately, and they are not equally expensive to test.

| Claim | Consequence if false | Cost to test |
|---|---|---|
| **Real peer-to-peer compute is playable** — tolerable latency, survives machines vanishing, works behind consumer routers | The architecture collapses and the reveal (§12.1) becomes impossible | Low — needs no game |
| **A request-and-queue economy is legible** rather than feeling like arbitrary denial | The economy needs rethinking; the world survives | Medium |
| **People do meaningful work without rewards, hierarchy, or progression** | There is no game here | High — needs weeks and real people |
| **The reveal lands** | The hook is lost; the game still works | Cannot be tested by people who helped design it |
| **Governance is engaging rather than tedious** | Cut governance; nothing else breaks | Highest — needs roughly Dunbar scale |

**The first is binary, cheap, and everything else rests on it.** It is answered before any art or game design effort.

**The third is the deepest risk and is not technical at all.** This design has deliberately removed every extrinsic motivator — no score, no progression, no scarcity pressure, and standing that buys nothing. Whether intrinsic motivation alone sustains a game is genuinely unproven, and no further design work settles it.

### 19.3 What the first build does not contain

**All of governance (§7).** Round Table, the draw, elections, referenda, sortitioned ratification, the Prime Principles, the franchise. §5.7 supplies the justification in its own words: below Dunbar's number, "people simply know each other and most machinery is unnecessary." A first build is a few dozen people, where governance would not be a test of governance but a performance of it.

This is a deferral, not a retraction. The governance work was not premature: it closed a genuine logical contradiction (§7.2), and it constrains the identity data model, which is painful to retrofit — the same argument §13 makes for settling AI citizenship early while deferring its implementation.

**Custom project code** — §11.2's authoring path, manifests, and the trust ramp. The largest security surface in the design, and unnecessary for testing whether the mesh works. Template projects still run genuinely on other citizens' machines; the compute is real, and only the authoring is absent.

**Additional city-states, waystations, founding, and migration.** One shard.

**AI citizens** — already deferred to a second project (§13).

**Weather, climate bands, the calendar, festivals, skills, gifts, and vernacular architecture.** All flavor for a first build — **with one exception. Sun position stays** (§5.9). It is a small pure function requiring no data, and §12.2 makes light the channel through which system state is read honestly. It is how the mesh is *seen*.

**Art.** §12.2's visual language is state made visible — sagging and dim when underused, glowing and strained when overloaded. Primitive geometry with honest lighting parameters tests that completely.

### 19.4 The single-machine case is not a mock

There is an obvious temptation to build a fake-mesh version first to test whether the game is enjoyable, and §15 rejects theatrical distributed computing outright.

**§9.6 already resolves this.** Graceful degradation means a shard reduced to a single machine is a legitimate state of the real architecture rather than a simulation of it. Building the single-machine case first is building the bottom rung of a ladder the design already promises. Adding peers then *adds capability* rather than swapping a fake for a real one.

There is therefore no dishonest prototype phase, and no risk of a mock quietly becoming the product.

### 19.5 Phases

**Phase 0 — Mesh spike. Not a game.**
Headless. Prove that a dozen machines behind ordinary consumer routers can form the overlay (§11.6), schedule sandboxed jobs on one another (§11.2, §11.4), checkpoint, and migrate work when a machine disappears (§11.3).

*Stop if:* direct connections between home machines fail often enough that relaying becomes the common case rather than the fallback, and relay burden proves impractical; or a machine dropping out produces a stall long enough that a player would read it as broken software rather than as the world breathing.

**Phase 1 — One facility, real mesh.**
A single shared facility whose simulation genuinely runs on participants' machines. Walk up, work, watch strain ease, see the lighting change honestly. Soul-hash ownership from §8.1 — cheap now, painful later.

*Stop if:* the world feels unreliable in a way that reads as broken rather than alive.

**Phase 2 — The queue.**
Requests, need tiers 0–3, fair queuing, backpressure, claim decoherence (§6.3–6.6). The economy thesis.

*Stop if:* people cannot tell why they are waiting. The entire design rests on waiting reading as visible fairness rather than arbitrary refusal, and that is legible only on real faces.

**Phase 3 — Projects and standing.**
Several facilities, opt-in contribution, the labor multiplier, Resonance (§10). Run for a month or more, because that is the shortest window in which any flow becomes visible at all.

*Stop if:* attendance decays once novelty wears off. This is the real test, and failing it means the design's central bet is wrong.

**Then evaluate** before touching governance, custom code, additional shards, AI citizens, or the reveal.

### 19.6 What Phase 0 cannot answer on its own

**The central question requires real machines on real domestic connections.** NAT traversal success rates, relay burden, and dropout behavior cannot be established on one developer machine or between containers on one host — the failure modes live in carrier-grade NAT, asymmetric upstream bandwidth, consumer router timeouts, and genuine geographic latency.

A local harness can build and exercise everything and will catch ordinary faults. **The go/no-go measurement needs a handful of volunteers on separate home networks**, which makes recruiting them a Phase 0 dependency rather than a Phase 3 one.
