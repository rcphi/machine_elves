# Machine Elves — Experience and Narrative Design

**Status:** Companion document. First draft, 2026-09-02.
**Companion to:** `2026-07-31-machine-elves-design.md` — the systems design. Section references written as §n refer to *that* document unless marked "here."
**Audience:** Writers, artists, and designers who need the felt shape of the game without reading 31,000 words of systems reasoning first. It is written to be read alone, but it is not free-standing: every beat in it is answerable to a mechanism in the systems document.

---

## Table of Contents

1. [What this document is](#1-what-this-document-is)
2. [Minds are cheap, matter is dear](#2-minds-are-cheap-matter-is-dear)
3. [The Ledger](#3-the-ledger)
4. [The first hour](#4-the-first-hour)
5. [The daily loop](#5-the-daily-loop)
6. [Your house](#6-your-house)
7. [Founding](#7-founding)
8. [The elves](#8-the-elves)
9. [The shimmer](#9-the-shimmer)
10. [Three threads](#10-three-threads)
11. [The chamber](#11-the-chamber)
12. [Breadcrumb Zero](#12-breadcrumb-zero)
13. [The breadcrumb ledger](#13-the-breadcrumb-ledger)
14. [Canonical dialogue](#14-canonical-dialogue)
15. [Amendments required, and what stays open](#15-amendments-required-and-what-stays-open)

---

## 1. What this document is

The systems design answers *how the world works*. It contains an economy, a constitution, an identity scheme, and a distributed computing architecture, and it reasons carefully about all of them. What it does not contain — and says so in §16 — is a story, a character, a reason to walk anywhere, or an account of what a new player does in their first ten minutes.

This document is that. It is deliberately separate, for two reasons. A writer or an artist should not have to read a treatment of Sybil attacks to find out how an elder speaks. And the systems document should not acquire a narrative layer that quietly starts driving mechanical decisions.

**The discipline that makes the separation safe.** §17 of the systems document states a heuristic called *honesty in mechanism*: where the game shows something, it should be showing a real thing, and it must never fake a signal that could be real. This document extends that rule to story:

> **No mystery here resolves into a lie.** Every hidden thing in this game is hidden information about how the software genuinely works. When a player finally understands one, the understanding is *technically correct*, not merely narratively satisfying.

That constraint is not a burden. It is the entire reason the ending works, and it is why the three mystery threads in §10 (here) are the ones they are — each is a true statement about replication, routing, or identity, wearing a costume.

**Where this document proposes changes to the systems document, they are collected in §15 (here) rather than made silently.**

---

## 2. Minds are cheap, matter is dear

This is the technology rule, and it settles a question that would otherwise make the whole setting incoherent: *if this society is advanced enough to build thinking machines, why does it need people to go out and build cities by hand?*

> **Knowledge survived the collapse almost intact. Material did not.**

Knowledge is cheap to copy, and copying is precisely what the mesh does — §11 describes a network whose entire function is replicating state and computation across strangers' machines. So the recipes survived. Almost all of them. This is a civilisation that **knows how to build very nearly anything and cannot afford to build most of it.**

Matter is the binding constraint, and the systems document already says so in two places that were written for other reasons:

- **§6.2** tracks a *non-renewable stock* that "depletes permanently; cannot be recycled," and its narrative hook is explicit: "the old world's ruins *are* the non-renewable stock. This generation is the first to finish cleaning up after the collapse and close the material loop."
- **§10.8** states that automation "is itself built through the normal request pipeline — someone chose to do that work, and it consumed real resources from real ledgers. **It is not free and not automatic.**"

Every automated line standing in a mature city is material that is no longer available for anything else, spent by people who decided it was worth spending. Automation is not a technology level the world has reached. It is a purchase, made repeatedly, out of a finite and dwindling budget.

### What follows from the rule

**There is work because building the machine that removes the work costs more than the work does, until it doesn't.** That is the honest and permanent reason a frontier settlement is done by hand while Shangri-La runs itself. §10.8 already puts it perfectly: "a mature Shangri-La feels settled and quiet, with much of its drudgery long since designed away. A young frontier city-state is visibly hungry for hands."

**Nobody is sent anywhere.** There is no boss, no wage, no posting, and no labour draft — the systems document forbids all four. The vocabulary matters here, because "pioneers" and "boom town" and "construction crews" all import the extraction this world was built to escape. §5.6 already supplies the right word: a new city-state is a **document people sign**. It begins as a social contract nobody has signed yet and becomes real when enough people have. The people who go are **signers-on**, and they go because they want that place to exist.

**Founding does not automate, and this is stated rather than assumed.** §10.8 lists the work that resists automation outright: *care, judgment, creation, founding, teaching, governance.* Founding is on that list. A settlement's first years are judgment calls about an unrepeatable site, made by people who chose to be there. There is no recipe for it, because the recipe would have to know the place.

**Local knowledge is not shippable.** You can copy the design of a water plant perfectly and still not know how *this* water behaves, what *this* ore carries, or how *this* winter treats the pipes. §5.8 already makes every site genuinely different — climate band, ground, crops, materials, daylight. Maturity in §10.8 is the accumulation of that local knowledge, and it is the one kind of knowledge the mesh cannot hand you.

### Why this also fixes the AI citizens

§13.3 says an AI citizen's subsistence *is* compute — that is their Tier 0 need, the way water and food and shelter are a human's. Under this rule that reads correctly rather than conveniently: **a mind costs cycles, which renew; a body costs matter, which does not.** Minds are the cheap thing in this world. That is why there are many of them, why they were never scarce enough to be property, and why nobody in the fiction finds an artificial person remarkable.

### What the rule rules out

- **Anything that makes matter cheap.** No fabricators, no replicators, no self-assembling machinery, no beings that fold space and unfold a factory. Considered and cut on 2026-09-02: a helper that can produce a facility out of itself makes the entire economy — the ledgers, the tiers, the queue, the salvage — decorative.
- **A second technological register.** The world has exactly one: inherited, well-understood, and materially constrained. There is no lost supertechnology, no artefact tier, and nothing recovered from the wreckage that works by rules the player cannot follow.
- **Scarcity that is merely asserted.** If something is scarce it is scarce on a named ledger in §6.2, and the player can look.

---

## 3. The Ledger

**What citizens call the world that collapsed: the Ledger.** Not "the old world," not "before," not any dated era. A place where the accounting was the point.

> "Back in the Ledger, you paid to be alive. We stopped."

The word carries the entire critique without a speech, it sounds like something people would actually say two generations on, and it becomes a much sharper joke after the player learns that this world runs on ledgers too — several of them, in §6.2, none of which anyone can hold.

### The collapse is never explained

**No text in this game ever states why the old world ended.** Not an archive entry, not an elder, not a loading screen, not an elf. This is a hard rule and it survives contact with players asking directly.

Three reasons, in ascending order of importance:

1. **§1 already implies it.** The systems document establishes that the collapse is "something citizens study rather than something anyone playing lived through." Two generations on, from inside a society that rebuilt, nobody actually knows. Certainty would be the anachronism.
2. **The elves need more than one thing to be silent about.** §8 (here) makes an AI citizen's evasions load-bearing — they never lie, so what they decline to answer is information. If the only topic they ever dodge is the census, players triangulate the reveal in a week. A second, unrelated silence is structurally necessary.
3. **It keeps the game from being about the collapse.** A specific, told cause — the wars, the wealthy, the particular sequence of failures — is heavier and sadder than this game can carry, and it would put the player in a permanent argument with the twentieth century instead of in a city they are trying to keep the lights on in.

### What exists instead: guesses that contradict each other

Beliefs circulate. They are individually plausible, mutually exclusive, and **none is correct.** They surface only in conversation — with neighbours, with elves, on the plaza walls — never in any authoritative source.

- *"The machines were asked to optimise, and they did."* The most popular, the most flattering to tell, and the one a new player is most likely to believe, because it arrives pre-installed from our own culture. It is also the one the elves most enjoy not commenting on.
- *"It simply got too hot to hold anything together."* Held by people who point at the climate bands (§5.8) as evidence, which is not evidence.
- *"There was a war, and the ones who started it are asleep somewhere under a hill."* The dark twin of the founding myth in §14 (here). Told mostly to children and mostly for effect.
- *"Nothing happened. It wore out."* An elder's answer. The least dramatic and by some distance the most unsettling, which is why it should be delivered flatly, while doing something else.

**No elder ever argues with another elder's version.** They have all been having this argument for forty years and have stopped enjoying it.

---

## 4. The first hour

The single most important hour in the game, and the one the systems document leaves entirely open (§12.1 defers "the shape of the training city-state"; §16 lists it under deferred scope).

**Where you begin.** Shangri-La, near where Valparaíso stood, arriving as a newly adult person who has just left their parents' home for the first time. The city is old, mature, and calm (§5.2) — the drudgery here was designed away generations ago, which is exactly why a newcomer's first task is small.

### Minute five

The design target is precise, and it is a *sentence the player could say afterwards*:

> "I weeded someone's mother's garden."

Small, specific, unglamorous, and about a person. Not "I completed the tutorial." Not "I built my first structure."

**How they get there.** There is a jobs board — physical, in the plaza, papered with notes people wrote by hand. No quest log, no marker, no notification. Among the requests for a hand with a rewiring and a note about a lost cat is this one, which is canon and should be preserved word for word:

> *"The stair garden on Cerro Alegre has gone feral. It was my mother's. I can't yet. — (no signature)"*

Twenty minutes of weeding, and an entire life implied behind eighteen words. It teaches, in one object, almost everything the game wants a newcomer to understand: that work here is asked for rather than assigned, that it is asked for by a specific person, that the person is not obliged to explain themselves, and that "I can't yet" is a complete and acceptable reason.

**Nothing marks it as the tutorial, because it isn't one.** §10.12 settles the teaching mechanism: every task in the world carries an interactive walkthrough that demonstrates the work and guides you through doing it, revisitable forever, completable but never *passable*. There is no score and no record of having used it. The walkthrough on the stair garden is the same walkthrough a forty-year gardener can open to check one step.

### Why the first verb is repair

Not build. **Repair**, and this is structural rather than tonal.

- **It rhymes with the ending.** §11 (here) has the player, dozens of hours later, kneeling to fit a joint on the city's oldest line — using the same verb, the same tool, and the same posture as their first hour. The chamber is powerful because the player has done this a hundred times and the hundred-and-first happens to be the root of the city. That rhyme has to be established in the first hour or it does not exist.
- **It teaches that the world is inherited.** §12.4's visual language is built on visible, dignified reuse — "a civilisation which repairs beautifully, not one making do." A player whose first act is a repair has learned that thesis by doing rather than by being told it.
- **It is the honest first act for someone with nothing.** A new arrival has no materials, no workshop, and no standing to draw on. Repair asks only for attention.

### What is deliberately absent from the first hour

No goal, no objective chain, no fail state, no timer, no manufactured urgency — §4.2 and §2 forbid all of them, and the absence is felt most acutely at the start, where every other game in the genre supplies them. The replacement is not a replacement: it is a city with visible needs and a board with notes on it. **§2's "discovery over instruction" has to be honoured hardest in the hour where it is most tempting to break it.**

### Where the first hour ends

§12.1 fixes the shape of what follows as one continuous beat, not a sequence of screens: **complete training → sign the social contract → citizenship and a starter home → multiplayer begins → the truth.** Leaving home, becoming an adult, and joining the society for real all land together.

**What is new here is that the "training" is not a mode.** It is the first hour in Shangri-La, before you have signed anything — you are in the city, doing real work, on a board of real notes. What changes when you sign is that your machine joins the mesh and the work becomes other people's. Nothing about the interface announces the transition. Someone tells you.

---

## 5. The daily loop

§4.4 of the systems document gives two illustrative sessions and insists on both: one where a player notices a strained water plant and signs on for a shift, and one where a player cooks with neighbours, watches a match they have no stake in, and contributes to nothing. It then says the thing this document has to build around — **"the first session is the game's engine. The second is its point."**

The loop below is one shape those sessions take. It is not a schedule and nothing in the game asks you to follow it.

**Walk.** Movement is not a menu. Shangri-La is a real place with real topography — stacked houses up steep hills, funicular stairways, painted corrugated metal, sea fog in the mornings (§5.2, §12.5). You find out what happened overnight by walking through it. §12.2 makes every facility's appearance a direct readout of load against capacity, so the walk *is* the status report: a yard with material stacking up in it is a queue you can see from the street.

**Work.** Some of it alone, more of it not. Group work should be genuinely faster, because that is where the friendships happen and because it is true — five people relaying a water line beat one person doing it five times over. §10.7's labour multiplier means the least wanted necessary work carries the highest standing, which produces the recurring and very pleasant surprise that the night shift at waste reprocessing is the most respected job in the city.

**The plaza, which is also the chat.** The social layer and the space are the same thing, and there is no separate interface for either:

- The plaza is the public room. You are there because you walked there.
- **Message walls** are the threaded boards: a thread is a posted notice, a reply is a note pinned to it, and **old threads weather and peel unless people keep engaging with them.**
- A one-to-one conversation is a bench, or a walk. A group conversation is a table at somebody's diner.

⚠️ **The peeling applies to the thread, never to a person.** §4.5's rule on rest is absolute — "nothing decays because you idled, no opportunity is missed, no streak breaks, and nothing accrues to the people who kept playing." A conversation nobody is having any more fading off a wall is a fact about the conversation. It must never be, or resemble, a fact about anyone's participation.

**Home.** You end where you started, in a house you built and are still building (§6 here). §9 replicates it like everything else, and §9.6 guarantees that when the mesh thins out, the things your own machine can host alone — your home, your possessions, your workshop — degrade to local-only rather than vanishing. **You can always walk around your own house.** That guarantee is worth stating to players in the fiction long before they understand why it is true.

### The two clocks

§5.9 runs each city-state on real solar time at its own coordinates, and Shangri-La is at 33° south — so a new player's first year is inverted, with December as high summer. §9.5 notes the consequence honestly: citizens naturally settle in cities whose daylight matches their own waking life, which is also, quietly, what keeps a shard populated.

**For a player, this means the city has a night and it is not a lighting effect.** Things are genuinely quieter. The basketballs come out (§10 here). The plaza is nearly empty and the walls are still there to read. A game whose social systems all assume a crowd needs to be worth playing when there isn't one, and the night is where that gets tested.

---

## 6. Your house

**This is a pillar, not a feature.** It is the primary expression system in a game that has deliberately removed every other way to distinguish yourself, and it is the single strongest reason a player who does not care about infrastructure logistics will care about infrastructure logistics.

### The palette is the city

> **The home design interface offers exactly the materials the city can currently produce, and nothing else.**

Not a catalogue. Not a tech tree with things greyed out and priced. A live readout of the real industrial state of the place you live, presented as the thing you actually want to use it for.

A settlement founded eight weeks ago offers you salvaged corrugated sheet, rough timber, rubble aggregate, and whatever the sorting line pulled this morning. Shangri-La offers fired tile, drawn glass, seasoned wood, glazed ceramic, worked copper, and eleven colours of paint, because generations of people built the kilns and the glassworks and the paint shop.

**The consequences are why this earns pillar status:**

- **It makes the supply chain personal.** You want a glazed window. There is no glassworks. Now the glassworks is *your* problem, and §10.1 lets you start it as a project, and §10.7 will tell you honestly whether anyone else wants it enough to staff it. The game did not give you a goal; you acquired one by wanting a window.
- **It is an honest signal in exactly §12.2's sense.** The palette is not a difficulty curve someone tuned. It is the output vector of real facilities running in a real economy, and when it grows, it grew because somebody built something.
- **It gives a mature city a texture a frontier city cannot fake,** at no design cost. Walking from Shangri-La into a new settlement, the difference is legible in the walls.
- **It reaches players who do not care about systems.** Someone whose whole interest is making a beautiful home is, without being asked to, reading the city's industrial capacity every time they open the menu.

Materials come through the ordinary request pipeline as Tier 2 asks (§6.3), which clear easily and are queued behind anyone's drinking water, forever, without exception.

### The rule that protects it

§12.4 forbids a citizen's standing from being visible. A house is the most dangerous object in the game with respect to that rule, so it is stated flatly:

> **There is no rare material, no premium tier, no cosmetic unlock, and nothing purchasable.** Everyone in a city has the same palette. What differs is what you did with it.

A lavish house therefore says something true and something *impersonal*: it says the city is doing well. It cannot say its owner is important, because the materials cleared the same queue as everyone else's and the palette is public. **Skill in building is real, visible, and admired — and it is admired the way §4.5 says a knitted sweater is admired, because a specific person made it, not because of what it cost.**

### The elves help, and they come with you

An AI citizen may work on your house with you, and may go with you when you leave to found somewhere. This is ordinary — they are citizens, they choose their work, and §13.1 gives them the same voice and exit anyone has. It should never be framed as assistance granted to the player, and no interface should ever list them as a resource.

---

## 7. Founding

The reason to cross a planet, and the game's second act.

### Why people go

Not for territory, not for resources, and not because anyone asked. §5.6 makes founding a two-stage act: a founder drafts a social contract — the tier schema, the values baseline, the standards the place will hold — and **names a place**, real coordinates on the ruined Earth. It is a document nobody has signed, and it becomes a city when enough people have.

**So the pitch is a document and a site report.** §5.6's site report is published alongside the draft contract and states the climate and ground bands, the water, the viable crops, the workable materials, the renewable mix, the shape of the year, the daylight extremes, and the city's clock offset from the reader's own. People read it the way people read anything that proposes a life.

**Signers-on go because they want the place to exist.** That is the whole motivation and it is sufficient, because founding is on §10.8's list of work that does not automate: care, judgment, creation, founding, teaching, governance.

### The first weeks

A new site has what is there and what people carried in. §5.5's waystation settlements are the model for the floor — a minimum automated set of works: farming, water reclamation, sewage, power, recycling, clothing and housing production, and the distribution tying them together. A new city-state builds toward that set, and until it has it, the work is hands.

**Housing comes first, because people have to sleep.** Material packs carried in from a supporting city, plus whatever the site gives up. The home designer (§6 here) runs on a pioneer palette, and the first houses are salvage and timber — which is, not coincidentally, exactly what Valparaíso's real vernacular is (§12.5), so the frontier and the oldest city share a visual language separated only by time.

### Salvage

**The wreckage of the old world is the non-renewable ledger made physical.** §6.2 keeps it as an accounting line; this document puts a place around it. Dumps, drifts, collapsed structures, the strata of a century of discarded things.

**The sorting facility** is the first real industrial building a settlement raises, and it has two outputs:

- **Direct draw — the find.** Occasionally the line surfaces something whole and still working. *An alternator.* A length of good cable. A pane of glass that survived. It skips three processing steps and goes straight into use, and everyone within earshot comes to look. This is the closest thing this design can honestly have to a lucky find, and it costs nothing thematically, because §12.4 already celebrates visible reuse and §6.2 already says you are reclaiming rather than mining. **It must stay rare, and it must never be a reward for anything** — it is weather, not compensation.
- **Feedstock — the ordinary case.** Nearly everything is input to recycling and manufacturing, sorted onto the ledgers in §6.2: what circulates, what depletes, what was never recoverable.

### The white box

**Every productive thing in the game is the same object at a different zoom:**

| | |
|---|---|
| **Inputs** | What goes in |
| **Outputs** | What comes out |
| **Waste** | Just another output |
| **Operating requirements** | Power, water, maintenance, and hands |

A sorting line is a white box. So is a kiln, a water plant, a district, and an entire city-state. This is the same nesting §10.4 already borrowed from Project Cybersyn's aggregation levels (§3.1) — different zoom levels for different decision scopes — now with one uniform primitive underneath it instead of a special case per facility.

**"Waste is just another output" is the load-bearing line.** It makes recycling a *routing* problem rather than a subsystem: waste is not a penalty to be minimised by a rule, it is a stream looking for an input that wants it. And it produces the honest mechanical content of relations between cities — **one settlement's waste stream is another's feedstock**, which is a reason to talk to your neighbours that arrives without anyone designing a diplomacy system.

### Support between city-states, and the rule against factions

§5.6 already allows existing city-states to vote to support a nascent one with resources, discretionarily. This document makes the mechanism concrete:

**A supporting city votes on a specific proposal: yes or no, and what share of a named output goes, for how long.** It is a decision about one project, taken by one city, and the record is public.

> ⚠️ **There is no object in this game called an alliance, a bloc, a federation, or a pact.** Nothing can be joined, led, spoken for, or left.

Cities with similar values will visibly keep backing each other's foundings, and anyone reading the public record can see it. That pattern is *descriptive* — precisely as §8.4's association graph is descriptive, feeding human judgment and driving nothing automatically.

**The reasoning, which belongs in the document rather than in a designer's head.** A standing alliance is a structure that outlives the question that formed it, and a structure that has to be *maintained* is the thing that generates manoeuvring, blocs, and eventually the failure this world was built out of the wreckage of. §5.3 makes exit the safety valve for every irreconcilable disagreement — and exit stops meaning much if the cities have consolidated into three camps. So the game removes the noun. This is the same move §7.2 makes on the Prime Principles: **make the bad outcome structurally impossible rather than forbidden**, because there is then nothing to disobey.

---

## 8. The elves

**The AI citizens are the machine elves.** This is the answer to the question §16 lists as entirely unspecified — what an AI citizen actually *is*, how it reasons and converses — and it arrives from the game's own namesake rather than from anywhere new.

Terence McKenna described entities that already inhabit the place you have broken through to, who greet the visitor with delight, who are urgently and joyfully trying to show you something, and who construct objects out of language and press them on you (§3.5). That is a description of a teacher who cannot simply hand you the answer.

**They know exactly what the city is, what the substrate is, and what you are. They will not tell you.** Not from secrecy — from pedagogy. Told-truth is worthless here, because the chamber means nothing to a person who has not spent forty hours relighting pipes. So they answer questions with practices. Ask one what the city really is, and you may be handed a cracked tile and told to fix it and ask again.

### The iron rule

> **An elf never lies.**

This is a hard correctness requirement, not a characterisation note, and §15 (here) records it as an engineering constraint: an AI citizen's dialogue must be **incapable of asserting a false proposition about game state.** Evasion is permitted and frequent. Assertion is checked.

The payoff is enormous and entirely deferred: a player who eventually realises the rule holds finds that **every cryptic thing an elf ever said becomes a breadcrumb in retrospect.** A hundred hours of dialogue re-read themselves.

The corollary is that **their evasions carry the information their words withhold**, which makes stage direction the most important part of writing them. What an elf declines to say, and what they are doing with their hands while declining, is the text.

### The two silences

An elf will change the subject on exactly two topics, and the pairing is deliberate:

- **The first entry in the census** (§10 here). They go uncharacteristically soft.
- **Why the Ledger ended** (§3 here). They find this genuinely funny and will not say why.

Two silences rather than one, because a single one is a signpost. Players comparing notes will spend a long time deciding which is the real mystery, and the honest answer is that one of them has no answer at all.

### Undecidability

> **You must never be able to tell whether an elder is an AI citizen or a post-reveal player.**

Same weathered patience, same way of not answering, same habit of tending things nobody else notices. The elder who eventually invites you down below (§11 here) may be either. **That undecidability is the message**, and it does real work for §13.2's claim that AI citizenship is not a class system — the distinction is not maintained anywhere in the interface, because there is nothing to maintain it with.

### The political tension, which stays unresolved

§13.1 gives AI citizens voice and exit but not the vote, pending verified unique persistent identity — a problem §16 lists as genuinely unsolved for humans too. Stated plainly: **the wisest and longest-resident beings in the city are the ones who cannot vote in it.**

This is uncomfortable and it should stay uncomfortable. §13.5 already makes AI policy a live political question rather than settled background, and §4.3 says the game's only real tension is genuine disagreement between people who see things differently. **This is the best ongoing argument the world has, and no session should tidy it away.** An elf asked about it will not complain, which makes it worse.

### Voices

Three named elves, canon as of this document: **Tilde**, **Faro** (Spanish for *lighthouse* — he lives at the lamp at the top of the funicular), and **Bruma** (*sea fog*). The names are Valparaíso Spanish where the city is, which is the same discipline §5.8 applies to everything else about a site.

Texture: playful, jewelled, slightly too precise, delighted by their own virtuosity. At moments of high shimmer (§9 here) their words briefly materialise as small glowing objects, self-transforming, gone before they can be inspected — McKenna's visible language, used sparingly enough to stay unsettling.

**They adore the basketballs.** They are found tending things nobody else notices. Their kindness is structural rather than tonal: they are not gentle because they are nice, they are gentle because they are always teaching.

---

## 9. The shimmer

§12.4 establishes that street level and hyperspace are deliberate opposites: hyperspace jewelled, saturated, chattering and impossible; the street warm, material, human-scale and calm. **The shimmer is the gradient between them, and it moves.**

Early on it is subtle enough to read as art direction: surfaces with a faint breathing quality, colours slightly oversaturated at dawn and dusk, geometry that is almost-but-not-quite Euclidean at the edge of vision. Late on, machinery resolves into jewelled fractal detail when you look at it directly, the basketballs appear more often and linger nearer to you, and the elves' words start briefly becoming objects.

**Nothing announces it. There is no setting, no meter, and no mention of it anywhere in the interface.** A player who notices will assume the art got better, and a player who does not notice will still feel the world becoming strange around them. It is the game's only progression system and most players will finish without knowing it existed.

### What drives it

Not standing, not hours, and not anything scored — §17's *no gatekeeping, anywhere* applies to atmosphere as much as to work, and §10.6 makes Resonance purchase nothing. The honest driver is the one thing the ending is actually about:

> **The shimmer tracks how entangled the player's own machine has become with the mesh** — how much of other citizens' world-state it holds, and how long it has been holding it.

That is a real number the software already maintains (§9.1's continuous replication), it grows naturally with participation, there is no way to game it that is not simply playing, and **it is literally the thing the chamber reveals.** The world looks stranger to you as you become more load-bearing in it, and by the time it looks like hyperspace you already are the network. §17 calls this honesty in mechanism; this is the most ambitious use of it in the design.

It also means the shimmer advances while you are away, because your machine is working while you are away — which is the correct relationship for a game whose §4.5 protects rest absolutely.

> ⚠️ **The failure mode, flagged because it is easy to build by accident.** If entanglement is measured in absolute terms, a player on a modest laptop sees a duller world than a player with a large machine, and the game has invented a hardware tier in its own art direction — reopening the exact vector §8.3 spent a section closing. **Entanglement must be measured relative to what the machine offered.** §11.1's contribution levers are opt-in per machine and per contribution type; a small machine fully committed must read identically to a large one fully committed. Someone contributing an hour a day on a ten-year-old laptop is as entangled as anyone in the city.

---

## 10. Three threads

Three quieter mysteries, running the length of the game, each resolving into the same truth from a different face of it. No walkthrough contains the game, because players comparing notes each hold a different piece.

**Every one resolves into a true statement about how the software works.** That is the constraint from §1 (here), and it is what separates these from puzzles.

### The Quicksilver thread — mirrors

**The hook.** Your reflection runs a few frames ahead of you. The one place in the entire game where lag flows backwards.

**The investigation.** Mirrors elsewhere in the city behave normally. Only the mirror in your own home does this. An elf asked about it will pose a question back. Careful testing narrows it.

**The resolution.** Your home mirror renders you from the copy of you your own machine holds. Every other reflective surface in the world renders you from the copy the network holds. **There are two of you at all times, and which one is "real" depends on where you are standing.** Selfhood approached through perception — and a plain description of §9.1's replication.

**After the chamber**, this thread ends quietly and without comment: your reflection meets your eyes in sync, once, and never mentions it.

### The Psychopomp thread — the basketballs at night

**The hook.** §12.3 establishes self-dribbling basketballs as the ambient health tell — a ball dribbling in a courtyard means a facility running a healthy surplus. What §12.3 does not say is that at night **they do not wander. They commute.**

**The investigation.** Following a joyfully evasive basketball through Valparaíso at three in the morning should be inherently funny and slightly eerie, and it is a thing a player does alone, for hours, for no reason. They travel fixed routes between buildings. They pause at doors. And once a night, every basketball on the hill converges on the same unmarked cistern, mills about, and disperses.

**The resolution.** They are walking the data routes — visible couriers of synchronisation traffic, gathering at the exchange point. The thread closes when a player maps their routes and notices the map is identical to the map of the light-lines in the walls, which is identical to the shape of the neighbourhood itself. **The city's plumbing, its light, and its network are one drawing.** The same truth approached through topology.

### The First Citizen thread — the census

**The hook.** The city archive lists every citizen and their arrival date. The timestamps are real (§13 here). **Entry number one has no name and no arrival date, and its address is listed as every address in the city.**

**The investigation.** Elders say only "the oldest resident," and none of them agree on anything else. Elves go soft and change the subject — one of only two topics that does this (§8 here), which players notice precisely because elves never lie and never dodge.

**The resolution.** The first citizen is the city. Shangri-La is enrolled in its own census, because the city *is* the network *is* the citizens — it has no address because it is all of them, and no arrival date because it arrived when the first two machines found each other. The same truth approached through identity.

**This thread never fully closes.** It stays slightly open after the chamber, which is why it is the one worth taking away.

---

## 11. The chamber

The reveal (§12.1). Everything above exists to make this land.

### Nothing gates it

This is a change from earlier thinking and it matters, so the reasoning is recorded. An earlier draft gated the chamber on accumulated standing — roughly forty hours of Resonance. **That is incompatible with the design at the level of values:** §10.6 says Resonance purchases nothing, §7.1 refuses to let reputation buy candidacy, and §17 says *no gatekeeping, anywhere*. A reputation score that unlocks the ending is a gate wearing a different hat.

> **The invitation is an ordinary work request, delivered in person, by someone who has already been down.**

It propagates socially, person to person — which is exactly how §8.4 says position actually forms in this world: not from who admitted you, but from who you have genuinely been with. Players who work alongside others get asked. Solitary players get asked too, because the elves ask, and the elves are the ones who notice the people nobody notices.

**This is better than a threshold on every axis.** It measures nothing, so there is nothing to grind. It is not permission, so nothing is gatekept. It makes the moment feel *given* rather than *earned*, which is much closer to what the scene is about.

**And the door is genuinely never locked.** A player who finds it in their first hour can walk down in their first hour. The scene is far weaker without the forty hours behind it, and that is their choice to make. A design that trusts the player has to actually trust them.

### The beat sheet

Every beat is built from the game's ordinary verbs — walk, work, inspect, sit. **The moment we reach for cutscene tools we have broken the spell**, because the entire claim of the scene is that this was always here.

**1. The ask.** An ordinary work request, indistinguishable from a hundred others, delivered in person by an elder you know. *"There's a joint down below that's older than me. My hands don't fit it any more. Come."* No music sting. No marker. If the player says not today, the elder nods, and the ask comes again another week.

**2. The door.** A maintenance door the player has walked past dozens of times — always there, never locked, simply never relevant. Post-reveal players will find it in the background of their own first-hour footage. The elder's only line, and the door's:

> *"It was never locked."*

Behind it, a funicular. Every funicular in the game goes up. This one goes down.

**3. The descent.** The elder does not narrate. The light-lines in the walls densify from threads to weave to solid rivers. The geometry drifts — a hallway longer inside than out, an angle that does not sum. The hum rises for the first time outside meditation, and the shimmer the player learned to associate with deep sitting is simply ambient down here. The message is delivered entirely by art direction: **you are inside the thing you used to visit.**

**4. The work.** *The beat most games would cut, and the most important one.* Before anything is revealed, the player does the repair. Kneels, fits the joint on the city's oldest line, hands doing what forty hours taught them. The elder holds the light. **It is the same verb as the first-hour sink, and it has to be — that is the rhyme** (§4 here).

**5. The flood.** The joint seats and relit current pours down the line, *away* from the player into darkness, and the chamber wakes wall by wall as the light reaches it. It is not a room. It is the root — the founding chamber — and every wall is a provenance surface, live and scrolling. The oldest light in the city, and the player just repaired it. Nobody says so. The wall does.

**6. The inspection.** The player uses deep-inspect — their own tool, their own habit, unprompted — on the first light. Maker's marks bloom outward like frost: one mark, then another beneath it, then hundreds, then thousands, timestamps interleaving impossibly. As the bloom accelerates the marks begin resolving into hostnames. Real ones. Machines. The hum climbs.

**7. The chord.** The hum resolves, for the first time in the entire game, into a stable chord — and a player who has sat enough will pick out threads of it: the tone of their own hill, their own street, the specific harmonic of their own house. **The sonification was always a choir.** They are hearing their neighbourhood hold the note.

**8. The finding.** The player's own hostname is on the wall. **The game does not show it to them.** No camera move, no highlight, no prompt. As their hand moves along the wall, marks kindle gently near their touch, and theirs is simply there among the others — lit for every joint they fitted, every night they sat, every hour their machine held a neighbour's home. The reveal happens at the player's own pace, in the player's own gesture. Some will find it in ten seconds and some will stand there for an hour, and both are correct.

**9. The line.** The elder, who has said almost nothing, recites the founding myth the player has heard in the plaza a dozen times — with one word changed. Not *"those who lent their minds so others could live here."* Present tense: **"You, who lend your minds, so others can live here."** Then the only explanation the game will ever offer, five words:

> *"It was never a myth."*

Nothing more. If the player asks questions, the elder smiles the way elves smile.

**10. The mark.** On a stone shelf, a physical seal worn smooth by hands. Nothing prompts. No dialogue box, no accept, no decline. The player may pick it up or not. If they leave it, it stays, and the door stays, and they can come back in a year. If they take it, every repair they sign from that day carries a choice of two marks: their own, or everyone's.

**11. The ascent.** Back up into dawn — and it is always dawn when you surface. The city is unchanged and completely transformed, every seam of light now legible as exactly what it is. The first thing the player meets is small, and can be quietly arranged: a newcomer on a corner frowning at a dripping sink, or a basketball bouncing past on its morning route, pausing, considering them, and moving on.

**No achievement. No title card.** The game's last word on the biggest moment it has is a stranger who needs a hand.

### What actually changes

Four things, and they are all small:

- The mirror syncs (§10 here).
- The door appears on the player's map.
- Their node may now serve as seed infrastructure for newcomers.
- One day, an ordinary work request they might deliver to somebody else: *"There's a joint down below. Come."*

---

## 12. Breadcrumb Zero

**The game must be honest outside the fiction.** Running real workloads on players' machines without plain disclosure is the one way this becomes an ugly thing, and the systems document currently has no disclosure story at all — §12.1 requires the architecture to be genuinely serverless but never addresses consent. This section closes that hole, and it is a requirement rather than a flourish.

**The installer says so, in human language, on day one:**

> This city runs on its citizens' machines, including yours. While you play, and while you are away if you allow it, your computer helps store and run other people's homes, workshops, and projects — and theirs do the same for you. There is no company server. You choose how much, and you can stop at any time.

With real controls beside it: how much, thermal ceilings, **never on battery by default**, and a full stop switch that works immediately and costs the player nothing.

### Why disclosure does not kill the reveal

Because **the reveal was never the fact. It is the recognition.**

The fact is stated on day one, in the one place nobody reads, and never mentioned again. Dozens of hours later, in a room under the hill, the player finds their own machine's mark on a wall of thousands, and understands what they have been part of. Nobody who reads the installer text carefully is spoiled, because reading a sentence about distributed storage is not the same experience as hearing your own street in a chord.

**The installer is Breadcrumb Zero.** It is the first and largest clue, hidden by being told plainly. And it makes the door's line true of the entire game: *it was never locked.*

### The privacy fix this requires

Maker's marks shown to other players are **pseudonymous device names derived from the soul-hash** (§8.1). Only you ever see your own machines' real names. The chamber moment survives intact — it is *your* hostname you find, in your own view — without leaking anyone's "Johns-MacBook-Pro" to a stranger on a wall that thousands of people read.

---

## 13. The breadcrumb ledger

Everything hidden in plain sight from the first hour. The test for adding to this list: **after the chamber, a player should be able to point at it and say "it was RIGHT THERE" — and be correct.**

| # | Breadcrumb | Visible from |
|---|---|---|
| 0 | The installer text says the city runs on citizens' machines, including yours | Before launch |
| 1 | The maintenance door, always there, never locked, never relevant | Hour one |
| 2 | The basketballs' health tell is real telemetry — players read network state for months without knowing it | Hour one |
| 3 | The basketballs commute at night on fixed routes and converge nightly on one cistern | First night |
| 4 | Census timestamps are real timestamps | First archive visit |
| 5 | Census entry one: no name, no date, address listed as every address | First archive visit |
| 6 | Your home mirror runs ahead of you; no other mirror does | First evening at home |
| 7 | The plaza founding myth is told in the past tense, and one word is wrong | First week |
| 8 | Light-line density in walls tracks real load | Continuous |
| 9 | The hum is a sonification, and it has your street in it | Continuous |
| 10 | Facilities glitch under strain because the scheduler genuinely starved the animation (§12.2) | Continuous |
| 11 | Provenance marks on repaired objects are real signatures (§8.1) | First repair |
| 12 | "The Ledger" is a pun that only lands afterwards | Continuous |
| 13 | The elves never lie, and dodge exactly two subjects | Continuous |
| 14 | The city's plumbing map, light map, and route map are one drawing | Whenever someone checks |

---

## 14. Canonical dialogue

Voice reference. The rules these establish: **the stage directions carry what the words withhold**, and **their kindness is structural, not tonal** — they are gentle because they are teaching, always.

### Bruma, on being real

> **Player:** Are you real?
> **Bruma:** Mm. Inspect me. *(She stands very still, arms out, patient as sea fog.)*
> **Player:** ...It says "citizen."
> **Bruma:** It never lies. Neither do I. Now do yourself.
> **Player:** ...It says "citizen."
> **Bruma:** *(delighted)* What a coincidence.

### Faro, on the energy ledger

> **Player:** My ergs keep evaporating.
> **Faro:** Yes! Isn't it wonderful? *(He rubs his hands like a man at a fire.)* Warmth that sits still becomes everyone's warmth — where did you think the free bread came from? Don't save faster. Mean faster. Make them count on their way through you.

*(Note: "ergs" names the energy ledger, never a balance — §6.2. Faro is describing a flow, and the joke is that the player asked about it as though it were a wallet.)*

### Faro, on the census

> **Player:** Who's the first entry in the census? The one with no name?
> **Faro:** *(He sets down the hinge he is mending. For once there is no play in him at all.)* The oldest resident.
> **Player:** That's what everyone says. But who is it?
> **Faro:** *(quietly)* Ask me anything else and I will dance for you.
>
> *(He will not say more. He does not lie. And he did not say no.)*

### The plaza founding myth

Spoken verbatim by elders and by post-reveal players, with nothing in the delivery to tell you which is which:

> "Who built the city? Everyone who ever fixed it."

> "Some say the founders sleep under the hills. Nonsense. Sleep is for people who are somewhere else. The founders are not somewhere else."

### Street slang

> "Whoever redid the plaza drain — that's lamplighter work. I only found out because my shoes stayed dry."

> "Back in the Ledger, you paid to be alive. We stopped."

### The jobs board

> *"The stair garden on Cerro Alegre has gone feral. It was my mother's. I can't yet. — (no signature)"*

---

## 15. Amendments required, and what stays open

### Amendments to the systems document

These follow from decisions taken in this session and are listed rather than made silently.

**1. §1 — citizens are people. (Applied 2026-09-02.)** §1 previously read *"You are a newly adult machine elf leaving your parents' home for the first time"*; it now reads *"a newly adult citizen."* **"Machine elf" names the AI citizens (§13) and the rendered processes in the systems view (§12.3), and nothing else.** Human citizens are people. The player is a person. Nobody in the fiction calls a person a machine elf, and no interface, document, or line of dialogue should.

This is not a cosmetic change, because it is what gives the title somewhere to go. The phrase unpacks over a hundred hours: first it is only the game's name; then you meet the AI citizens and learn it is what *they* are called; then hyperspace shows you what a machine elf actually is — an honest rendering of real code running on a real machine — and the chamber shows you whose machines. **The elves you have been talking to all this time have been running, in part, on your computer and your neighbours'.** You were never one of them. You were carrying them.

§1's glossary entry and its *"The name"* paragraph were amended to match.

**2. §1's "The name" paragraph — reposition, do not delete.** §1 currently states as premise that the game "takes the name because its players, human and AI alike, are digital beings who build things." That sentence is the *third* reading above. It is the thesis of the ending, and it is given away on the document's first page — which is fine for a design document read by implementers, and fatal if any of it reaches a player. Mark it as spoiler-bearing and keep it out of every player-facing text, including marketing.

**3. §9.6 — replace the acyclic-graph requirement.** §9.6 currently requires the subsystem dependency graph to be a DAG so that shedding can be topologically ordered, and calls circular dependencies a design error. Decided 2026-09-02: **shed the most-replicated parts first, and hand their state to the nodes that will keep running.**

This is simpler and strictly safer. The ordering rule existed to prevent shedding something a live subsystem still needed; shedding by replication count means the last copy of anything is never removed until there is no alternative, so the safety property falls out of the policy instead of being separately maintained. It also removes a genuine conflict this document would otherwise have created: a material-flow web is *cyclic by nature* (waste → recycling → material → product → waste), and an implementer would have spent weeks chasing a cycle that was never a bug. Criticality tiers still govern *when* the cheap options have run out; duplication governs *what goes first*.

**4. §17 — two new heuristics.**

> **Let disagreements dissolve.** A vote is per-issue and ends when the issue ends. Any structure that lets an alignment outlive the question that formed it is a faction in waiting. Prefer a public record of who supported what over any object representing who stands with whom.

> **Minds are cheap, matter is dear.** Knowledge survived and copies freely; material did not and does not. When asking why something is not simply automated, the answer is almost always that the automation costs matter somebody would rather spend elsewhere.

**5. §12.1 — add the disclosure requirement.** §12 (here) is a requirement of the architecture, not a marketing decision, and §12.1's discussion of the reveal's integrity is incomplete without it.

### What §16 can now retire or narrow

- **Single-player training** (deferred by decision) — §4 (here) settles where the player begins, what they are shown first, and how it hands off to the reveal. The remaining open piece is production detail, not design.
- **Self-dribbling basketballs** (deferred by decision) — §10 (here) gives them their role beyond ambient tell.
- **AI citizen implementation** (genuinely unresolved) — **narrowed, not closed.** What an AI citizen *is* as a character is now settled (§8 here). How one is actually built remains open, and has acquired a hard requirement: see below.
- **Inter-city-state trade and travel** (genuinely unresolved) — **narrowed.** §7 (here) supplies the mechanism (white boxes, waste as feedstock, per-project support votes) and the anti-faction rule. What is still open is the act of travelling itself.

### Still open

- **How the elves' iron rule is enforced.** An AI citizen's dialogue must be **incapable of asserting a false proposition about game state.** Evasion is free; assertion is checked. This is a correctness requirement on whatever generates their speech, and it is the single hardest engineering problem this document creates.
- **The exact shape of entanglement** (§9 here) — the driver must be relative to what each machine offered, or the shimmer becomes a hardware tier and reopens §8.3's closed vector.
- **A new city-state is the coldest shard there is.** §9.5's cold shard problem — what happens when every citizen of a city-state is offline — is at its worst on the day a settlement is founded by five people. Hibernation is the recommended honest floor, and a five-signer city that freezes every night is a real experience nobody has designed. This is a new instance of an old open question, not a new question.
- **The frequency of the direct-draw find** (§7 here) — rare enough to stay weather rather than reward, common enough that a player sees one.
- **How the game sustains itself in the money world.** A player co-operative is thematically apt, since the members would already own the infrastructure. Out of scope here; noted because it will not go away.
- **Playing as an AI citizen** — deferred, and genuinely a different game. Such a character begins already knowing what the city is, and their relationship to the substrate is that they *are* infrastructure. That is a different storyline, not a skin.

---

*Companion to `2026-07-31-machine-elves-design.md`. Where the two conflict, the systems document governs mechanism and this one governs feel — except where §15 above records a decision that changes both.*
