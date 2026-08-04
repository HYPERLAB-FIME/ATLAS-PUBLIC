# ATLAS — FAQ

**Version:** 1.0
**Related:** [ATLAS Protocol Specification (working draft)](https://hyperlab-fime.github.io/ATLAS-PUBLIC/atlas-protocol-specification-0.1draft.html) · [Glossary of questions](#glossary-of-questions)

---

AI agents are starting to shop and pay for us. **ATLAS** is about making that trustworthy: an open way for an **independent inspector** (an Assessor) to check how an agent behaved — did it follow the user’s intent? stay within rules and network policies? stay in good standing under Know-Your-Agent (KYA)? — and to share a compact trust signal with banks and networks **without** broadcasting the user’s private conversation.

---



## Glossary of questions


| #   | Question                                                                                                                                                                       |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1   | [What is ATLAS?](#1-what-is-atlas)                                                                                                                                             |
| 2   | [Why propose ATLAS as a FIDO standard?](#2-why-propose-atlas-as-a-fido-standard)                                                                                               |
| 3   | [Why trust the Assessor if it is also AI (“LLM as a judge”)? Isn’t that circular?](#3-why-trust-the-assessor-if-it-is-also-ai-llm-as-a-judge-isnt-that-circular)               |
| 4   | [Why would a shopping agent share personal data (PII) with the Assessor?](#4-why-would-a-shopping-agent-share-personal-data-pii-with-the-assessor)                             |
| 5   | [Why is ATLAS open?](#5-why-is-atlas-open)                                                                                                                                     |
| 6   | [What problems is this trying to solve?](#6-what-problems-is-this-trying-to-solve)                                                                                             |
| 7   | [Is ATLAS compatible with emerging standards (KYA-OS, AP2, VI)?](#7-is-atlas-compatible-with-emerging-standards-kya-os-ap2-vi)                                                 |
| 8   | [Does ATLAS work with browser agents and WebMCP?](#8-does-atlas-work-with-browser-agents-and-webmcp)                                                                           |
| 9   | [Can I use ATLAS only before payment — or also after a transaction has been processed?](#9-can-i-use-atlas-only-before-payment-or-also-after-a-transaction-has-been-processed) |
| 10  | [How do Assessor, Trust Authority, and the certification scheme work together?](#10-how-do-assessor-trust-authority-and-the-certification-scheme-work-together)                |
| 11  | [How do I find a qualified Assessor — what is the roster, discovery, and opt-in?](#11-how-do-i-find-a-qualified-assessor-what-is-the-roster-discovery-and-opt-in)              |
| 12  | [Can I use several Assessor agents for one transaction?](#12-can-i-use-several-assessor-agents-for-one-transaction)                                                            |
| 13  | [Who benefits from ATLAS — and how (by market segment)?](#13-who-benefits-from-atlas-and-how-by-market-segment)                                                                |
| 14  | [What are the key takeaways / benefits of ATLAS?](#14-what-are-the-key-takeaways-benefits-of-atlas)                                                                            |


Also: [Sources](#sources)

---



## 1. What is ATLAS?

**ATLAS** (Agent Trust Layer and Assurance Standard) is an **open protocol** — a shared rulebook — for trusting AI agents when they act in commerce on someone’s behalf.

In plain terms: when an agent acts for a person, ATLAS defines how an **independent Assessor** can check that agent’s behaviour — not only “did it follow the request?”, but also compliance with regulations, network policies, KYA identity status, and related oversight — and turn the result into a **signed trust signal** that payment parties can use. The full private chat does **not** need to travel on the payment rail.

ATLAS describes how **entity types** work together: the agent being checked (the “subject” / shopping agent), an independent **Assessor**, a **Trust Authority**, merchants, wallets, and payment systems.

---



## 2. Why propose ATLAS as a FIDO standard?

**FIDO** already anchors industry work on strong authentication, credentials, and related trust infrastructure. Agentic commerce adds a new gap: protocols such as [AP2](https://ap2-protocol.org/ap2/specification/) and [VI](https://verifiableintent.dev/spec/) secure **authorization at checkout**, and [KYA-OS](https://github.com/decentralized-identity/kya-os-mcp) helps establish **who** an agent is — but none of them alone standardise **independent runtime assessment** of what the agent did *before* those artefacts are bound.

Bringing ATLAS into a **FIDO** standardisation track aims to:


| Goal                                       | Why it matters for FIDO                                                                                                                                       |
| ------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **One interoperable assessment language**  | Avoid proprietary “observability islands” (SDK-only, host-only, proxy-only) that cannot travel with the payment                                               |
| **Complement, not replace, existing work** | Sit **beside** AP2/VI (transaction binding) and KYA (identity) as the **pre-transaction / behaviour** signal leg                                              |
| **Neutral Assessor model**                 | Align with FIDO’s culture of independent, cryptographically verifiable trust — Assessors licensed by Trust Authorities, methods certified, evidence encrypted |
| **Rail-ready trust signals**               | Compact report tokens that can ride existing payment messaging — useful to networks, issuers, and processors                                                  |
| **Open governance**                        | A FIDO home gives the industry a venue to review threats, profiles, and conformance together                                                                  |


**One-liner for the WG:** ATLAS is proposed so FIDO can standardise **how the ecosystem independently observes agent behaviour** — with the same care FIDO has brought to authentication and credentials.

---



## 3. Why trust the Assessor if it is also AI (“LLM as a judge”)? Isn’t that circular?

It looks circular at first — “AI checking AI” — but ATLAS is designed so trust does **not** rest on “another chatbot’s opinion” or a bare “trust me.”

What makes the Assessor different:

1. **Different job.** The shopping agent is trying to complete a purchase. The Assessor is authorized to judge behaviour against a **named rulebook** (regulation, network policy, safety rules, and so on) — like an auditor reviewing a company, not the company grading itself.
2. **More than one source.** The Assessor compares what the shopping agent reports **and**, when available, independent material from the merchant or wallet, then cross-checks them.
3. **Licensed, not anonymous.** A **Trust Authority** authorizes Assessors; they appear on a published **roster**. The Assessor must prove that authorization before it can see sensitive evidence.
4. **Certified methods — not “trust me.”** The methods and models an Assessor uses are **certified** by the Trust Authority and go through **prior benchmarks and evaluation**. The outcome is closer to: *“Using certified method X, against rulebook Y, the score was Z”* — not an opaque, untraceable judgment.
5. **What leaves the room.** Private reasoning stays encrypted for the Assessor only. Everyone else gets a **signed verdict** (and often a short token pointing to a stored report) — not the raw chat.

So the point isn’t “AI judges are perfect.” The point is **independence + certified method + named rulebook + cross-checks + cryptographic proof**.

> **Honest caveat:** Assessment still has limits. ATLAS makes it **auditable, independent, and method-certified** — not infallible.

---



## 4. Why would a shopping agent share personal data (PII) with the Assessor?

The goal is **more privacy for more parties**, not less. Without a standard, either nobody can check what the agent understood (bad for safety and disputes), or too many parties see too much.

A shopping agent is willing to share personal data with an ATLAS Assessor mainly because of **who** that Assessor is and **how** data is handled:

- The Assessor is an **independent third party** — not the merchant competing for the sale, and **neutral from a payment point of view** (not the network, issuer, or acquirer deciding the rail outcome).
- Sensitive evidence is **not meant to sit in a permanent personal-data store**. It is **decrypted only while the assessment runs**; what lasts is a signed verdict / report token and hashes — not a reusable copy of the user’s private data for other parties.
- Sharing is a deliberate trade: short, limited access for a **neutral inspector**, in exchange for trust signals the rest of the ecosystem can use.

In ATLAS:

- Evidence is **encrypted so only the chosen Assessor** can read it.
- Merchants, card networks, and processors **do not** get the raw intent/reasoning package in the base design.
- Sharing is **scoped**: only what is needed, after the Assessor proves it is allowed.
- What travels on payment rails is typically a **short trust token** (a pointer to a report), not the user’s full conversation.

---



## 5. Why is ATLAS open?

Agentic commerce involves many vendors — shopping agents, merchants, wallets, schemes, issuers, labs. A closed, vendor-only trust check creates lock-in and incompatible “trust islands.”

ATLAS is open to **foster interoperability** across the ecosystem — and to **avoid a fragmented landscape** of private, local, limited observability tools that cannot talk to each other or travel with the transaction.

An open (and, proposed, **FIDO-governed**) standard lets the industry:

- interoperate across vendors and networks,
- review threats together,
- align with other protocols ([AP2](https://ap2-protocol.org/ap2/specification/), [VI](https://verifiableintent.dev/spec/), [KYA-OS](https://github.com/decentralized-identity/kya-os-mcp)),
- avoid reinventing assessment ten different ways.

Without ATLAS, common ways to watch agents are:


| Approach without ATLAS                  | Limit                                     |
| --------------------------------------- | ----------------------------------------- |
| **Software kit (SDK) inside the agent** | Only works if that vendor embeds your kit |
| **Hosting the agent yourself**          | Only works for agents you operate         |
| **Proxy / firewall in the path**        | Fragile and hard to apply everywhere      |


None of these scale across today’s mix — commercial cloud agents (e.g. Gemini), on-device agents (e.g. Apple), or custom agents (e.g. Hermes). An **open protocol** lets diverse agents emit the same kind of assessable trust signals without forcing one host or one vendor kit.

---



## 6. What problems is this trying to solve?

Example: *“Order pizza under €40, I’m allergic to peanuts, and I’m on medication X.”* An AI agent may keep the budget, drop or blur the allergy, show a confirmation that *looks* fine, then pay — with **no independent record** of what it actually understood.

**When verification matters.** Checking the agent (observability / assessment) can happen **even before a payment network/rail is chosen**, and should happen **before checkout protocols such as [AP2](https://ap2-protocol.org/ap2/specification/) and [VI](https://verifiableintent.dev/spec/) start**. By the time AP2/VI capture “intent,” that data is already the shopping agent’s **interpreted** intent — and may already include bias or error from discovery, ranking, and cart building.

In AP2, a **checkout object is shared** with the user and others — that is not the gap. The gap is that this checkout was **already built by the shopping agent without the human browsing and selecting items with the merchant**. Confirming that purchase is therefore **not the same** as classic 3-D Secure-style authentication against a merchant-built checkout: the human is approving an **agent-built cart**. Item selection has already been partly **delegated**.

That creates real problems — especially for today’s focus on **immediate / real-time** agentic flows (identity, regulation, liability), with further issues under fuller hands-off **delegation**:


| Problem                                                                                           | Why it matters                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| ------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **KYA alone isn’t enough**                                                                        | Knowing *who* the agent is (registration, keys, claimed scopes) does not prove *what* it did in this purchase. Behaviour checks are needed **before** rail choice and **before** AP2/VI checkout                                                                                                                                                                                                                                                                                                                                                                                    |
| **KYA silos / no cross-repository checks**                                                        | If each payment network keeps its **own** KYA list, bad behaviour on Network A may be **invisible** to Network B. Cross-checks should share a **minimal** signal (e.g. “lower trust” / blacklisted) — **not** full case details or the other network’s private status file                                                                                                                                                                                                                                                                                                          |
| **Regulatory compliance** (e.g. **IFR** — Interchange Fee Regulation — and payment-method choice) | The **generic issue**: agentic commerce can break or blur rules that assume a human chose the merchant, the product, and the payment path. An agent may pick a card, wallet, or rail that changes **cost, routing, or legal treatment** without the user (or the scheme) seeing that choice clearly. **IFR** is one example — agent-selected payment methods can affect interchange and cost justification — but the same pattern applies to network rulebooks, restricted goods, age limits, geo/sanctions, SCA expectations, and other obligations that must hold **at transaction time**, not only at agent onboarding. Rail choice may also come **after** the agent has already shaped the cart |
| **Unclear liability**                                                                             | When an agent-led purchase fails policy or is disputed, schemes need a fair way to allocate responsibility. ATLAS helps the **liability model** by providing an **independent, signed, redeemable assessment** of what the agent did (and against which rulebook) — evidence schemes, issuers, and merchants can use to shift or share liability based on verified behaviour, not on each party’s unverifiable claim                                                                                                                                                                |
| **Chargebacks and disputes**                                                                      | Classic disputes assume a clear story: the cardholder either did or did not authorize a merchant checkout they could see. With agents, the story breaks: the user may have confirmed an **agent-built** cart, yet still claim “that wasn’t what I meant,” “I never chose that merchant/item,” or “my constraints were ignored.” Merchants, issuers, and networks then lack a **neutral, time-stamped record** of agent behaviour to adjudicate quickly — so chargebacks rise, resolution costs rise, and “he said / agent said” replaces evidence |
| **User confirmation is not enough (unlike classic 3DS)**                                          | Confirming (even on an AP2 checkout object) is **not** the same as authenticating a merchant-presented, human-selected purchase. AP2 **does** share the checkout; the issue is that object was **already forged by the agent** without human–merchant item selection. The shared product details may also **fail user constraints** the person stated in natural language — e.g. **allergies** or **medical** restrictions — while the summary still looks plausible to click “confirm.” Independent assessment can check whether those constraints actually survived into the cart |
| **Monitoring & explainability gaps** *(related to, but not the same as, regulatory compliance above)* | **Regulatory compliance** asks: *did this transaction break a substantive rule?* **Monitoring & explainability** asks: *can we show, later, what the agent did and why — to supervisors, auditors, or customers?* Frameworks such as transparency / explainability duties (e.g. EU AI Act-style obligations), operational resilience / third-party AI assessability (e.g. DORA-style themes), and internal scheme monitoring all need a **durable runtime record**. Today that record may not exist in an independent, portable form — so firms cannot demonstrate oversight even when they believe the agent “usually” complies |
| **Privacy vs oversight**                                                                          | Parties need to **observe** agent behaviour for safety, fraud, and disputes — but must not turn agentic commerce into a **surveillance pipe**. Raw user intent and reasoning are sensitive; dumping them to merchants, networks, or processors would overshare. Without a standard, the market swings between two bad options: **blind trust** (no check) or **over-exposure** (too many parties see too much). ATLAS-style design aims at the middle: encrypted evidence for a licensed Assessor only, and compact trust signals downstream |
| **Wrong or unsafe purchases** (“intent drift”)                                                    | Constraints get lost between what you said and what was ordered — and AP2/VI may later bind that **already-interpreted** (possibly drifted) intent. Along the path, **data-loss risk is high**: natural language is compressed into **tokens and embeddings**, shaped by **model training** priors, then forced into **deterministic tools/schemas** (APIs, MCP, cart fields). Rare or safety-critical constraints (allergies, medical limits, ethics) are easy to under-weight, drop, or never map. **Privacy-preserving** policies can also raise risk: some constraints **may** not be shared with the merchant, or **may** not be processed fully, so the checkout never sees what mattered. Fidelity to the **initial intent** is therefore fragile — **especially** with **custom** or **on-device** agents — unless independently assessed |
| **User best interest no longer assured**                                                          | When an agent shops for you, it is supposed to optimise for **your** goals — budget, safety, preferences, ethics — not for the loudest merchant, the easiest tool call, or its own completion bias. That assurance weakens once selection is delegated: the agent can satisfy a simplified objective (e.g. “buy pizza under €40”) while **quietly dropping** what mattered most to the user (e.g. allergen safety, preferred local shop, “no rush delivery fees”). Example: the user wants a peanut-safe meal under budget; the agent returns a cheap pizza that looks fine on the confirmation screen but **may** ignore the allergy — the purchase “succeeds” for the agent while failing the user’s real interest. Even “immediate” flows already delegate **product selection** to the agent |
| **Bias in merchant and item selection**                                                           | Unlike today’s search engines or aggregators — where a human can still open results and compare merchants — the shopping agent may interpret data or show only a **pre-selected subset**. Even if the user sees some merchants, they **do not see all** underlying offers, so bias can stay **undetected**. That subset is what later becomes “intent” in AP2/VI                                                                                                                                                                                                                    |
| **Fairness and equity**                                                                           | Selection should not systematically disadvantage parties — including **local merchant sovereignty** vs large global / US platforms in agent-mediated discovery                                                                                                                                                                                                                                                                                                                                                                                                                      |




**KYA identifiers — why joining lists is hard.** Cross-repository checks need to recognise the **same** agent:


| Approach                              | What it means                                                                           | Effect                                                              |
| ------------------------------------- | --------------------------------------------------------------------------------------- | ------------------------------------------------------------------- |
| **One ID per repository**             | Network A calls the agent `netA:…`, Network B `netB:…`, with no reliable join           | Risk stays trapped in one silo unless something bridges the IDs     |
| **Single agent / model / version ID** | One stable identity (or mapping) for the same agent build that each repository can link | Networks can correlate status and assessment outcomes across stores |


**Both patterns are covered by ATLAS:** an Assessor can query **all available KYA repositories** for a given agent and form a cross-repo trust view — still sharing only **minimal** risk signals where privacy requires it.

ATLAS closes the **runtime behaviour gap** and feeds portable signals back into KYA-style monitoring.

---



## 7. Is ATLAS compatible with emerging standards (KYA-OS, AP2, VI)?

**Yes — and more importantly it complements them** by restoring **missing trust signals** those layers do not provide alone.


| Protocol                                                                                                 | Rough job                                        | Relation to ATLAS                                                                                                                                                                                                                                                                                    |
| -------------------------------------------------------------------------------------------------------- | ------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **[KYA-OS](https://github.com/decentralized-identity/kya-os-mcp)** ([DIF](https://identity.foundation/)) | Who is this agent? Identity and delegation       | The Assessor can **work with the KYA-OS layer** and **feed runtime behaviour signals** back into KYA monitoring. Spec: [SPEC.md](https://github.com/decentralized-identity/kya-os-mcp/blob/main/SPEC.md); overview: [KYA-OS introduction](https://modelcontextprotocol-identity.io/mcp/introduction) |
| **[AP2](https://ap2-protocol.org/ap2/specification/)**                                                   | Permission to check out / pay (mandates)         | ATLAS sits **before and around** checkout: how intent was interpreted while discovering, evaluating, and building the cart                                                                                                                                                                           |
| **[VI](https://verifiableintent.dev/spec/)** (Verifiable Intent)                                         | Cryptographic proof of user intent / constraints | Complementary at payment boundaries; ATLAS does not replace VI                                                                                                                                                                                                                                       |
| **[ATLAS](https://hyperlab-fime.github.io/ATLAS-PUBLIC/atlas-protocol-specification-0.1draft.html)**     | Independent runtime assessment                   | Complements the protocols above; proposed for FIDO standardisation                                                                                                                                                                                                                                   |


**Two signal legs:**

- **[ATLAS](https://hyperlab-fime.github.io/ATLAS-PUBLIC/atlas-protocol-specification-0.1draft.html)** — **pre-transaction** trust (intent capture → discovery → cart): compliance, intent checks, KYA, dispute support, oversight.
- **[AP2](https://ap2-protocol.org/ap2/specification/) / [VI**](https://verifiableintent.dev/spec/) — **transaction & post-purchase** proof that the purchase was authorized and bound correctly: consent, mandate, cart integrity, payment instrument, audit trail.

**One-liner:** KYA-OS = ID badge; AP2/VI = permission and binding to pay; ATLAS = missing pre-transaction signals about behaviour, compliance, and oversight.

---



## 8. Does ATLAS work with browser agents and WebMCP?

Yes in principle. ATLAS cares about **how trust messages are exchanged**, not whether the agent runs in an app, in the cloud, or in a browser.

**MCP / WebMCP** (in short): ways for agents to call tools and websites. Those tool calls are exactly where intent often gets compressed or dropped — so assessment still matters.

If a browser agent can hold evidence of what it understood, start an ATLAS assessment, and release **encrypted** evidence only to an authorized Assessor, it can participate as a **subject agent**. Detailed browser/WebMCP wiring is still emerging; the protocol is meant to be **agent-architecture agnostic**.

---



## 9. Can I use ATLAS only before payment — or also after a transaction has been processed?

**Yes.** Assessment is not only a “gate before pay.” Timing depends on need: block until a verdict, continue and review later, or look back at a past transaction.


| Mode                        | When                    | Who typically asks                     | What happens                                                                                                                                                                                |
| --------------------------- | ----------------------- | -------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Direct / synchronous**    | Before the next step    | e.g. merchant, wallet                  | Request assessment and **wait** before checkout, authorisation, or fulfilment                                                                                                               |
| **Indirect / asynchronous** | Around the same journey | e.g. merchant, wallet                  | Request assessment **without blocking**; get notified when ready (audit / trace)                                                                                                            |
| **Post-transaction**        | After payment           | e.g. issuer, payment network, acquirer | Ask about a **past** transaction. The **Trust Authority** managing the Assessor fleet **triggers** a post-assessment toward the shopping agent — still subject to that agent’s **policies** |


---



## 10. How do Assessor, Trust Authority, and the certification scheme work together?

In ATLAS language, what people often call an **“authority scheme”** is essentially the **certification scheme**: the programme that defines *who may assess*, under *which rules*, and how Assessors are **accredited and listed**.


| Entity type                              | Simple question it answers                                                                                            |
| ---------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| **Certification scheme**                 | *What is the assurance programme?* It publishes the **Assessor roster** and ties Trust Authorities into one catalogue |
| **Trust Authority** (certification body) | *Who licenses this Assessor, stores reports, and redeems report tokens?*                                              |
| **Assessor**                             | *For this purchase, did behaviour match the rulebook — using a certified method?*                                     |
| **Conforming implementations**           | Products and services that implement ATLAS under scheme profiles (any vendor)                                         |


**How they connect (simplified):**

1. The scheme publishes which Assessors are accredited (**roster** — see next question).
2. The shopping agent or merchant picks an eligible Assessor (and the agent must **opt in** to that Assessor).
3. The Assessor proves authorization from its Trust Authority.
4. It receives **encrypted** evidence.
5. It issues a signed result + report token (certified methods/models).
6. The payment network can later **redeem** the report from the Trust Authority.

---



## 11. How do I find a qualified Assessor — what is the roster, discovery, and opt-in?

**Best related question:** *How does the ecosystem discover Assessors, keep them qualified, and let shopping agents choose who may inspect them?*

### The roster (the public catalogue)

A **certification scheme** (or trust registry) publishes an **Assessor roster**: a living list of Assessors currently allowed to operate under that programme. Shopping agents, merchants, and wallets use it to **discover** who can assess what, where, and under which rulebooks — instead of private one-off deals.

The roster is kept fresh through **regular Assessor evaluation** and **roster updates** (add, suspend, revoke, refresh scores and metadata). Discovery uses the roster to **pre-filter** candidates; at assessment time the Assessor must still prove a **live authorization** from its Trust Authority (a stale roster entry is not enough).

### What a qualified Assessor entry typically carries

A roster entry for a qualified Assessor is meant to support informed choice. In practice it includes (or is linked to) information such as:


| Field (plain language)                        | Why it matters                                                                                                                  |
| --------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| **Qualification / quality score**             | Result of ongoing evaluation and benchmarks — helps compare Assessors, not only “listed vs not listed”                          |
| **Assessment referential(s)**                 | Which **rulebooks** this Assessor is allowed to judge against (e.g. intent fidelity, regulated goods, network policy, fairness) |
| **Cost**                                      | Pricing or fee model so merchants/wallets/agents can choose affordably and predictably                                          |
| **Region**                                    | Where the Assessor is authorized to operate (e.g. EU, US)                                                                       |
| **Agents that accept this Assessor (opt-in)** | Which shopping agents (subjects) have **agreed** to be assessed by this Assessor — see below                                    |
| Status, types, Trust Authority                | Active / suspended / revoked; assessment types; owning Trust Authority                                                          |


*(The [ATLAS working draft](https://hyperlab-fime.github.io/ATLAS-PUBLIC/atlas-protocol-specification-0.1draft.html) already standardises core discovery fields such as regions, assessment types, policy referentials, and authorization status. Qualification score, cost, and the reverse “who accepts me” view help make the roster usable as a real marketplace of Assessors in scheme / programme deployments.)*

### Discovery

1. Look up the scheme’s roster.
2. Filter by region, referential, score, cost, and whether the shopping agent accepts that Assessor.
3. Commission only an Assessor that matches those filters **and** still has live authorization.



### Opt-in (the shopping agent must accept the Assessor)

Assessment is not a free-for-all. The **subject (shopping) agent opts in** to which Assessors (and/or Trust Authorities) may request its encrypted evidence. That opt-in is how privacy and control stay with the agent:

- The roster may show **which agents accept** a given Assessor.
- From the agent’s side, the agent publishes or embeds an allow-list of permitted Assessors when starting an assessment.
- If an Assessor is not opted-in (or not on the current qualified roster), evidence is **not** released.

**Beginner takeaway:** Think of the roster as a **yellow pages of inspected inspectors** — regularly scored and updated — and opt-in as the shopping agent’s **consent** over who may open its private evidence.

---



## 12. Can I use several Assessor agents for one transaction?

**Yes.** One purchase can involve **more than one Assessor**. That is intentional: different parties often need different checks, or the same journey may need several rulebooks.

### Why you might use more than one


| Example                                             | What happens                                                                                                                                                                                            |
| --------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Merchant and wallet each commission an Assessor** | The merchant wants a check before accepting the cart; the wallet wants a check before releasing payment credentials. Each picks an eligible Assessor from the roster (they may be different Assessors). |
| **Different rulebooks**                             | One Assessor is strong on **intent fidelity**; another on **regulated goods** or **network policy**. Same transaction, separate assessments.                                                            |
| **Different timing**                                | One Assessor runs **synchronously** as a gate; another runs **asynchronously** for audit/trace on the same journey.                                                                                     |




### How it works (plain steps)

1. The shopping agent **opts in** to each Assessor it is willing to open evidence for (allow-list — see [roster / opt-in](#11-how-do-i-find-a-qualified-assessor-what-is-the-roster-discovery-and-opt-in)).
2. Each requester (e.g. merchant, wallet) **discovers** and **commissions** its Assessor from the roster for that transaction.
3. Each Assessor proves its **live authorization**, then receives **its own** encrypted evidence package (scoped to what that assessment needs — not a free dump to every Assessor at once beyond what was authorized).
4. Each Assessor returns **its own signed verdict** and, when required, **its own report token**.
5. Downstream, the merchant processor can attach **several compact report tokens** to the payment message (ATLAS designs for a small number of tokens on the rail — typically up to a few per authorisation). Networks or issuers can redeem each token from the relevant Trust Authority.



### What stays true with multiple Assessors

- Privacy: raw evidence still goes only to **authorized** Assessors, encrypted to them — not to every merchant or to the rail.
- Independence: each Assessor judges under **its** certified method and referential.
- No single Assessor monopoly: the ecosystem can combine complementary views of the same agent journey.

**Beginner takeaway:** Think of it like several specialized inspectors for one shipment — each with a clear brief — whose short signed reports can travel together with the payment.

---



## 13. Who benefits from ATLAS — and how (by market segment)?

Each party gets a different slice of value from the same independent assessment and compact trust signals.


| Segment                | What’s in it for them                                                                                                                                                                 |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Merchant**           | More confidence that an agent-built cart is acceptable **before** fulfilment; better dispute posture; optional sync gate so they don’t proceed blind                                  |
| **Wallet**             | Can require agent observability before releasing payment credentials or finishing mandates — without becoming the Assessor                                                            |
| **Shopping agent**     | Neutral way to prove good behaviour without giving raw personal data to every counterparty; open interoperability instead of per-network kits                                         |
| **Payment network**    | Runtime signals on top of KYA; compact tokens for authorisation; help with fraud, IFR/routing policy, and liability design                                                            |
| **Issuer**             | Extra signal at authorisation and after the fact; better evidence when the cardholder disputes; redeemable reports via the Trust Authority                                            |
| **Merchant processor** | Can carry a verified Assessor verdict into payment messaging (existing card/bank message formats) and score risk using an independent result — not only merchant or agent self-claims |
| **User**               | Better chance the agent stayed within constraints **before** AP2/VI bind an agent-built checkout; oversight without putting the raw chat on the rail; fairer disputes                 |


**One line:** merchants and wallets get a gate or audit trail; agents get portable proof of behaviour; networks, issuers, and processors get redeemable runtime signals; users get protection that “confirm the agent’s cart” alone cannot provide.

---



## 14. What are the key takeaways / benefits of ATLAS?

1. **Closes the black-box gap** between what you said and what the agent did.
2. **Independent, method-certified assessment** — not the shopping agent grading itself.
3. **Privacy-aware oversight** — sensitive evidence to the Assessor only; rails get compact signals.
4. **Restores missing pre-transaction trust signals** that AP2/VI alone do not cover — while staying complementary to KYA, AP2, and VI.
5. **Stronger KYA** via cross-repository checks (minimal risk signals, not full case dumps).
6. **Liability-shift enabler** — independent evidence for schemes, issuers, and merchants when disputes arise.
7. **Scalable observability** across commercial, on-device, and custom agents — without relying only on SDKs, hosting, or proxies.
8. **Flexible timing** — sync gate, async audit, and post-transaction review.
9. **Discoverable, opt-in Assessors** — roster with ongoing evaluation (score, referential, cost, region, accepting agents).
10. **Several Assessors per transaction** — merchant, wallet, or different rulebooks can each commission a check; multiple report tokens can travel with the payment.
11. **Value per segment** — merchant, wallet, shopping agent, network, issuer, processor, and user.
12. **Open protocol fit for FIDO** — a shared, vendor-neutral assessment layer the working group can refine into a FIDO standard.

---



## Sources

[↑ Back to glossary of questions](#glossary-of-questions)

- [ATLAS: Agent Trust Layer and Assurance Standard — working draft](https://hyperlab-fime.github.io/ATLAS-PUBLIC/atlas-protocol-specification-0.1draft.html)
- [FIDO Alliance](https://fidoalliance.org/) — proposed home for ATLAS standardisation discussion
- [KYA-OS (DIF)](https://github.com/decentralized-identity/kya-os-mcp) — [SPEC.md](https://github.com/decentralized-identity/kya-os-mcp/blob/main/SPEC.md); [introduction](https://modelcontextprotocol-identity.io/mcp/introduction)
- [AP2 — Agent Payments Protocol](https://ap2-protocol.org/ap2/specification/) ([home](https://ap2-protocol.org/))
- [Verifiable Intent (VI)](https://verifiableintent.dev/spec/) ([home](https://verifiableintent.dev/))
- Combined ATLAS + AP2/VI signal framework (pre-transaction vs transaction & post-purchase) — briefing input for WG discussion

