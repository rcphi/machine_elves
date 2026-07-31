# Machine Elves — Design Document

**Status:** Design exploration. Implementation deferred to a separate project.
**Date:** 2026-07-31
**Audience:** This document is written to be self-contained. A reader with no prior context should be able to understand the whole design, the reasoning behind each decision, and what remains unresolved.

---

## Table of Contents

1. [Premise](#1-premise)
2. [Experiential Goals](#2-experiential-goals)
3. [Influences and Lineage](#3-influences-and-lineage)
4. [Player Experience](#4-player-experience)
5. [World Structure](#5-world-structure)
6. [Economy](#6-economy)
7. [Governance](#7-governance)
8. [Identity and Ownership](#8-identity-and-ownership)
9. [World State Persistence and Replication](#9-world-state-persistence-and-replication)
10. [Projects, Labor, and Resonance](#10-projects-labor-and-resonance)
11. [The Compute Mesh](#11-the-compute-mesh)
12. [The Reveal and Visual Language](#12-the-reveal-and-visual-language)
13. [Why Inequality Cannot Take Root](#13-why-inequality-cannot-take-root)
14. [Decisions Considered and Rejected](#14-decisions-considered-and-rejected)
15. [Open Questions and Deferred Scope](#15-open-questions-and-deferred-scope)
16. [Design Heuristics](#16-design-heuristics)
17. [Glossary](#17-glossary)

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

---

## 5. World Structure

### 5.1 City-states are separate persistent shards

Each city-state is its own persistent simulated world with its own economy, citizens, governance, ledgers, and **its own compute mesh — its infrastructure literally runs on its own citizens' hardware.** This is the fact that makes "this city runs on us" concretely true and pointable-at rather than diffuse.

Travel or trade between city-states is a deliberate act — caravan, shipment, emigration — not seamless walking. This is both a design choice and a practical necessity: it gives each shard a tractable simulation boundary and prevents problems in one from cascading everywhere.

### 5.2 Shangri-La

The starting city-state, where all new players begin. Located near where Valparaíso, Chile once stood — a deliberate echo of Cybersyn's origin (§3.1).

Its social contract is grounded in non-theistic humanism with Buddhist influences. As the onboarding shard it should read as relatively **mature and settled**: infrastructure works, automation is well-developed, the place feels calm. This contrasts with frontier city-states, which are visibly hungry for hands (§10.8).

### 5.3 Plurality across city-states

Each city-state defines its own standards, specializations, and social contract. Specialization may follow proximity to natural resources or regional need.

Different city-states will classify the same request differently, elect differently-minded representatives, and develop genuinely different characters from the same underlying rules (§7.1). **Plurality across shards is the design's safety valve for irreconcilable disagreement** — you leave and find or found a city-state that fits, rather than being coerced or trapped.

### 5.4 A note on naming and branding

**Design systems to embody a philosophy's principles before naming anything after that philosophy.** Functional, neutral names are the default — "the Round Table," not "the Sangha of Stewards" — even where a tradition inspired the mechanic.

The reasoning is not squeamishness: if a system fails for unrelated implementation reasons, a real belief system branded onto it takes undeserved reputational damage by association. Earn the label first. Explicit thematic branding is a separate, later pass, taken deliberately and only once the mechanics stand on their own.

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

---

## 7. Governance

### 7.1 The Round Table

A body elected by a city-state's citizens.

**No eligibility gate of any kind.** Any citizen may stand. Gating candidacy behind reputation, contribution history, or demonstrated competence would build an aristocracy of standing in place of one of money — a closed elite with a different admission criterion, which is precisely the failure this entire design exists to avoid.

Competence is achieved instead through **informed voters**, not access control. Candidates publish an explicit, comparable statement of their prioritization values and tie-breaking principles — not vague platforms but legible answers to "when these two goods conflict, which do you choose and why." Voters weigh candidates' track records themselves.

Terms are short enough that power does not calcify. Recall by referendum is available at any time. Exact durations, seat counts, and thresholds are deferred (§15).

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

None of these introduce new scope. Each is a promise that a decision already made elsewhere in this document stays true as policy details drift.

### 7.3 Amendment

**Ordinary policy** changes two ways:

- **Round Table precedent** — fast, handles the ordinary ambiguous case.
- **Citizen-initiated referendum** — available any time enough citizens want to force a direct popular vote rather than leave a matter to representatives. Modeled on Swiss practice, where elected government handles routine governance but organized citizens can compel a popular vote given sufficient support.

**Prime Principles use a harder path, but not an impossible one.** An amendment must pass, then **wait for an actual election to occur**, then pass again in identical form under the newly-elected body. This is modeled on Swedish constitutional practice and forces genuine generational reflection rather than a single heated moment.

**Deliberately not a permanent lock.** Constitutional history cuts both ways here, and both cautions are worth holding simultaneously:

- Germany's postwar Basic Law contains a genuine "eternity clause" shielding human dignity and the democratic order from any amendment — written precisely because Weimar's constitution had no such protection and was legally hollowed out from within.
- The original US Constitution *also* entrenched a clause: one shielding the slave trade from Congressional interference for twenty years.

Entrenchment preserves whatever you entrench, wisdom and cruelty alike. Keep the list short, keep the bar high, and do not assume the founders knew everything a later community might.

### 7.4 The social contract

Signing is a real commitment to *this* city-state's specific tier schema and values baseline — not generic terms-of-service paperwork. It is the mechanical gate for citizenship, and it is what makes city-states genuinely differ.

Citizens born in a city-state hold automatic citizenship but **still affirm the contract personally at coming of age** (Prime Principle 4).

Disagreement carries **no punitive mechanic**. If a contract stops fitting you — because the community amended it, or because you changed — you leave, and find or found a city-state that fits. Plurality across shards is the safety valve; enforcement within one is not.

---

## 8. Identity and Ownership

**The soul-hash is a persistent cryptographic keypair** generated at character creation — the moment you turn eighteen and leave home. The private key never leaves the player's control.

This is the literal, load-bearing referent of the game's phrase "hashed with your soul," not merely poetic language. In a genuinely serverless world, a signature is the only available way to prove something is yours without a central database to consult.

**Gifting** re-signs an object to the recipient's key, leaving a small provenance record scoped to that one object. There is no global ledger of all transfers.

**Recycling** invalidates the soul-hash entirely — the object is no longer owned by anyone — and returns its material footprint to the relevant ledgers (§6.2) for the next request. Ownership was always custody, never a permanent claim on matter.

**Crafting is not a side economy.** Building something personal routes through the same tiered request pipeline as everything else (§6.3), so accumulating possessions is gated exactly like any other request. "I will simply own a great deal of stuff" is not a loophole.

The next section generalizes this mechanism from personal property to the entire world.

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

**The bootstrap problem, and an honesty risk.** A new player's client must discover peers from somewhere. Standard P2P bootstrapping uses seed nodes or a distributed hash table — but **any permanent bootstrap infrastructure is, technically, a server.**

This matters more here than in an ordinary P2P application, because the reveal (§12.1) stakes the game's emotional payload on the claim being *literally true*. A player who discovers an asterisk after being told there are no servers has been mildly lied to, which is worse than never having made the claim.

Two acceptable resolutions: minimize bootstrap infrastructure to pure peer discovery holding no world state and no simulation (and say so plainly), or make bootstrap itself peer-supplied. **Do not resolve it by not mentioning it.**

---

## 10. Projects, Labor, and Resonance

A **project** is the game's central organizing unit: a thing people build and maintain together. A diner, a water reclamation plant, a rail line, a research group, a sports club, a city's entire power grid.

### 10.1 Create

**No permission gate.** Anyone may found a project. Nobody approves it.

The fair-queue system already knows where need is real, so the game **actively surfaces it** — "here is where the city is straining" as a standing, visible invitation. This points need-driven creation at genuine gaps without ever requiring it.

Creating things nobody asked for — art, odd hobby workshops, untested ideas — remains completely free. Both paths matter.

Founding means: choose a **template** (auto-generates manifest and resource footprint; no programming required) or author **custom logic** (self-declared manifest; §11.2), then **place the project physically in the world.** Every project has a building.

**Bad ideas need no policing.** Because throughput and standing flow only from *usage* (§10.6), a shoe-horn factory built while people are starving is simply starved of both — nobody requests shoe horns. Nobody forbids it, the incentive structure simply does not reward it, and the founder has spent only their own free time. This is the design's governing heuristic (§16) in its purest form.

### 10.2 Discover

**Ambient (avatar layer).** Facilities broadcast their state environmentally. You notice a struggling workshop the way you would notice a struggling shop on a street you walk daily — not via a floating icon. See §12.2 for the visual vocabulary.

**Deliberate (systems view).** The same information, city-wide, in the telemetry conventions the fair-queue system already established.

Same underlying data, two registers, depending on how deliberately you are looking.

### 10.3 Opt in

Support is **not monolithic**. Four independent levers, mixed in any combination:

- **Compute** — idle CPU cycles (§11)
- **Active labor** — showing up and doing the work in person
- **Land** — the plot your home sits on, or land you hold
- **Storage** — idle disk hosting world state (§9.2)

This matters: someone with no hardware to spare can matter as much as someone lending a rack of cores, through a different lever. Resonance tracks contribution across all four (§10.6), not compute alone.

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

### 10.9 Titles

Three honest flavors, which should not be conflated:

- **Provable** — "Founder of X" is a fact the signed creation record already contains. Not a claim; a verified event.
- **Peer-endorsed** — "Engineer," "Polymath," "Laborer." One soul, one endorsement; not weighted by the endorser's standing.
- **Self-asserted** — whatever someone calls themselves. No verification, pure flair.

**Hard rule: no title ever touches a queue, a vote, or an allocation.** Titles are purely expressive and informational.

**Founders hold no permanent authority** over projects they started — that is the aristocracy trap at smaller scale (§7.1).

Titles are **plural and unranked**: you hold many, and none sits above another. There is no ladder. This does not fully solve informal deference calcifying into a pecking order (§15), but it removes the obvious path to one.

---

## 11. The Compute Mesh

### 11.1 The real architecture

**Players' machines genuinely execute other players' project work.** No corporate servers, no publisher-operated simulation, no cloud backend.

**Contribution is opt-in per project.** Only code from projects you have explicitly joined can ever be scheduled on your hardware. This keeps the trust surface small and explicit, and limits a bad actor's blast radius to those who opted into their project specifically.

**Liveness is player-configurable per machine, off by default.** Each machine is set to *run always*, *only when idle*, or *never* — mirroring how real volunteer-computing platforms work. Players thus decide two independent things: *which* projects may use them, and *when* a given machine is exposed at all. This matters for shared family computers and work laptops.

Players may contribute additional machines they own. This does not create a wealth advantage, because contribution grants no control over what runs (§13).

### 11.2 Project authoring

- **Templates** (most players) — the game provides safe, pre-built sandboxed implementations. Manifests auto-generate. No programming required. This is how the large majority of projects are built.
- **Custom modules** (technically inclined players and groups) — real sandboxed code, WASM or similar, for custom project logic, self-declaring its manifest and gated behind the trust ramp (§11.4). This is where the design's "arbitrary project code" ambition actually lives.

Custom authoring is a candidate for a **late-game unlock**, which would echo the game's hidden-until-later theme (§2) and give technical players a genuine frontier.

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

4. **Staged trust ramp.** New projects start capped at small resource allocations and earn expanded scale through demonstrated track record. Nobody sits in judgment of who is trustworthy upfront — consistent with the absence of gatekeeping everywhere else in the design (§16).

5. **Legible manifests.** Every project declares what its jobs actually need before anyone can opt in. Informed consent, not blind trust. Everyone should know what is running on their machine.

### 11.5 Two distinct trust quantities

These must never be conflated:

- **Personal Resonance** (§10.6) — an individual's standing. Social and informational. Buys nothing.
- **Project trust level** (§11.4, item 4) — a *project's* demonstrated execution reliability, governing how much mesh capacity it may command.

A project earns its own trust through verified-correct execution, **not** through its founder's personal standing. Wiring the two together would let a well-regarded citizen found a project and instantly command large allocations — the aristocracy problem re-entering through the scheduler.

Verified-correct contribution builds an individual's Resonance and a project's trust level *independently*. Consistent disagreement with consensus erodes both.

---

## 12. The Reveal and Visual Language

### 12.1 The reveal

**Single-player training** frames "lending your brain-space to projects you support" as ordinary tutorial jargon — the kind of flavor text every game has. Nothing signals that it is literal.

**Graduating into multiplayer is the reveal.** Your machine genuinely joins the mesh: it begins doing real work for real strangers, and theirs for you. The game tells you the truth at this moment, and the truth is verifiable.

The onboarding chain is deliberately **one continuous beat**, not a sequence of separate systems:

> complete training → sign the social contract → citizenship and starter home granted → multiplayer begins → *the truth*

Leaving home, becoming an adult, and joining society for real all land as a single moment. The structural gate and the thematic revelation are the same event.

**This is why the architecture must be genuinely serverless** (§9.5). The emotional payload of the reveal depends entirely on it being true rather than theatrical. A player who investigates and finds a conventional backend has been lied to, and the game's central conceit collapses.

*(Single-player training design is deliberately deferred — see §15.)*

### 12.2 Ambient state as honest signal

A facility's presentation is a direct readout of **load relative to capacity**. This is one underlying variable, not several authored states:

| State | Presentation |
|---|---|
| **Near-idle** | Dormant, dim, slightly neglected. Not scripted sadness — there is simply no activity to animate. The basketball is not dribbling because nothing is driving it. |
| **Balanced** | Content. The basketball dribbles. |
| **Over capacity** | Glitchy, straining, shining red-hot. Machine elves visibly too few for the work, stretched, fumbling. |
| **Understaffed** | Quieter and sadder — lights on, queue visibly stacking up, nobody home. |

**The last two must be clearly distinguishable**, because they call for opposite player responses: build more capacity, versus show up and work.

**Flourish animations sit at low priority in the same hard-metering system as real jobs (§11.4).** Under genuine strain the scheduler correctly spends its cycles on actual requested work, and the flourish starves. The glitching is therefore a **real resource-contention artifact**, not an authored "stressed" state — honest, free, and impossible to fake.

### 12.3 Hyperspace

**The systems view is hyperspace.** This is where the McKenna aesthetic lives mechanically rather than decoratively.

The systems view is where you literally look at the running mesh — other citizens' project code executing on real hardware, made visible. Rendering those processes as small autonomous self-transforming entities, doing their own inscrutable and playful work, is an **honest visualization** of what is actually happening, not an art-direction flourish.

**The machine elves are what the network looks like when you can see it.**

Visual grammar draws on McKenna's descriptions (§3.5): jeweled and self-transforming forms, objects that change as you watch, visible chattering language, ornate self-referential geometry, delight in virtuosity.

**Self-dribbling basketballs** are the ambient system-health tell — a courtyard ball dribbling itself means a facility running a healthy surplus, felt atmospherically rather than read off a dashboard. *(Further detail deferred — §15.)*

---

## 13. Why Inequality Cannot Take Root

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

## 14. Decisions Considered and Rejected

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

---

## 15. Open Questions and Deferred Scope

### Deferred by explicit decision

- **Single-player training design.** To be designed once the first version exists; treat as interactive documentation rather than a tutorial bolted on afterward.
- **Self-dribbling basketballs** — detail beyond their established role as ambient health tell.
- **Round Table specifics** — term lengths, seat counts, quorum thresholds, referendum signature requirements.

### Genuinely unresolved

- **Sybil-resistant identity.** "One soul, one voice" requires resisting mass fake-identity creation, which is a hard and only partially solved problem in decentralized systems. Prime Principle 2's guarantee depends on it. Scope honestly as real work, not a detail.
- **The cold shard problem** (§9.5) — what happens when every citizen of a city-state is offline. Hibernation recommended; not settled.
- **The bootstrap honesty risk** (§9.5) — any permanent peer-discovery infrastructure is technically a server, which the reveal's integrity depends on acknowledging.
- **AI players.** The original premise included AI as well as human players, and this was never explored. What is an AI citizen? Does it hold a soul-hash, vote, own property, stand for the Round Table, count toward quorum? Potentially a significant unexplored dimension.
- **Multiplayer social scale.** How large a city-state grows before it needs internal structure; how citizens discover each other; how new city-states are founded and by whom.
- **Inter-city-state trade and travel**, beyond "a deliberate act, not seamless walking."
- **Everyday art direction** outside the hyperspace view — the look of streets, homes, and people.
- **Intra-project decision-making** for large or contested projects, given that founders hold no authority.
- **Informal status hierarchy.** Titles and visible standing can calcify into deference-based hierarchy with zero mechanical backing. Plural, unranked, recent-weighted design mitigates but does not eliminate this. Probably not fully solvable by mechanics alone.
- **Conflict and harm between citizens.** "Restriction requires real harm" (Prime Principle 5) implies real harm can occur, but no mechanism exists for adjudicating or responding to it.

---

## 16. Design Heuristics

Recurring principles that resolved most questions in this document. Apply them to questions it does not cover.

- **Design your way out of needing rules.** Prefer structures where bad behavior *cannot matter* over rules forbidding it. The shoe-horn factory is not banned; it is simply unused. Malicious code is not detected; it is sandboxed into irrelevance.
- **Flows, not stocks.** Ergs, claims, standing, labor multipliers — everything circulates and decays. Nothing accumulates permanently. When a new quantity is introduced, ask what makes it decay.
- **Legibility over enforcement.** Publish the real state and let citizens act on it. Most coordination problems in this design are solved by making something visible rather than by making something mandatory.
- **No gatekeeping, anywhere.** Candidacy, project creation, custom code, and trust are earned through demonstrated work, never granted by permission. Every gate is a future aristocracy.
- **Consent is explicit and revocable.** Opt-in per project, per machine, per contribution type. Leaving is always free and never punished.
- **Honesty in mechanism.** Where the game shows something, it should be showing a real thing: strain animations starve because the scheduler is genuinely busy; hyperspace shows genuinely running code; the reveal is true. Never fake a signal that could be real.
- **Reuse mechanisms across layers.** Fair queuing governs CPU cycles and dinner alike. Graceful drain covers machines and people. Replication serves ownership, world persistence, and integrity verification simultaneously. Tiering by criticality governs both need and consistency. **If a new problem seems to need a new system, check whether an existing one already has its shape.**

---

## 17. Glossary

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
| **Round Table** | A city-state's elected governing body. Handles contested classifications, scarcity tie-breaks, crises. No eligibility gate. |
| **Prime Principles** | Five entrenched constitutional guarantees, amendable only across an election. |
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
