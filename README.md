Here's the full document as plain text — select all and copy directly from this message:

---

# PRODUCT QUEST — DELIVERABLE PACKAGE
## TeamPulse: AI Prep Copilot for People Managers
*An AI-native manager-enablement capability for a mid-market HR/People Analytics SaaS platform*

**Scenario type:** Synthetic B2B SaaS company and synthetic customer materials, built for this exercise (no real company, customer, or dataset is represented).
**Track:** Product Management / AI-Native Product Development / Business Strategy
**Prepared for:** MUST Company — Product Owner Quest submission

---

## Scenario Context

TeamPulse is a synthetic mid-market HR technology company (a fictional composite, not a real business) offering a people-analytics platform (engagement pulse surveys, performance review workflows, and org data) to companies with 200–2,000 employees. The buyer is typically a VP of People or CHRO; the primary end users are frontline and mid-level people managers.

For this exercise I invented a plausible dataset: retired-style synthetic materials including a support-ticket theme summary, a set of synthetic manager interview notes, and illustrative market/pricing benchmarks. These are clearly labeled as synthetic throughout and are used to simulate the kind of qualitative and quantitative inputs a real Product Owner would triage.

## 1. Customer Problem Selection

### 1.1 Problem Candidates Considered

Three candidate problems surfaced from the synthetic research corpus (support tickets, 12 synthetic manager interviews, and churn-survey verbatims). Each was scored against reach, frequency, pain intensity, and strategic fit with TeamPulse's existing data assets.

| Candidate Problem | Reach (of managers) | Frequency | Pain Intensity | Fit w/ Existing Data | Decision |
|---|---|---|---|---|---|
| Managers spend hours manually prepping for 1:1s, pulling context from scattered tools | ~78% | Weekly | High | Strong (TeamPulse already holds pulse, review, and org data) | SELECTED |
| HR admins spend excessive time building quarterly board people-metrics decks | ~15% (HR admins only) | Quarterly | Medium | Strong | Deferred — low frequency |
| New managers lack structured onboarding into people-management best practices | ~20% (first-year managers) | One-time / onboarding | Medium | Weak — needs new content library | Deferred — needs new capability build |

### 1.2 Selected Problem Statement

Frontline and mid-level people managers at mid-market companies spend an estimated 2–4 hours per week manually assembling context ahead of 1:1s and performance conversations — pulling engagement-survey scores, past 1:1 notes, goal-tracking status, and recent feedback from separate tools (TeamPulse, Slack, a calendar, and a spreadsheet or notebook). This manual assembly is inconsistent, is frequently skipped under time pressure, and results in shallow or reactive 1:1s. Shallow 1:1s are a leading indicator TeamPulse already tracks as correlated with regretted attrition in its engagement data model.

### 1.3 Supporting Evidence (Synthetic)

- Synthetic support-ticket theme analysis: "manual prep" and "can't see history in one place" appeared in a plausible 31% of manager-tagged tickets over a simulated 90-day window.
- Synthetic interview finding: 9 of 12 simulated manager interviews described reconstructing 1:1 context from memory or ad hoc notes rather than a system of record.
- Synthetic churn-survey theme: departing employees' free-text comments referenced "inconsistent check-ins" or "manager didn't seem prepared" in a simulated 22% of exit surveys at mid-market accounts.

Because none of this is real customer data, it is treated in this package strictly as a hypothesis generator, not as proof — see Section 4 (Validation Plan) and Section 7 (Limitations) for how this would be checked against real data before being trusted.

### 1.4 Target Customer / ICP

| Attribute | Definition |
|---|---|
| Buyer | VP of People / Head of HR at a 200–2,000 employee company (existing TeamPulse customer, expansion motion — not new logo) |
| End user | Frontline and mid-level people managers (typically managing 4–12 direct reports) |
| Trigger | Company already runs a regular 1:1 or performance-check-in cadence and already uses TeamPulse for pulse surveys or reviews |
| Segment priority | Existing TeamPulse customers in the 500–1,500 employee band, where manager headcount is high enough to matter but org complexity is still manageable |

## 2. Product and Business Hypothesis

### 2.1 Product Hypothesis

We believe that people managers at mid-market TeamPulse customers struggle to prepare meaningfully for 1:1s because relevant context is scattered across systems. If we build an AI-generated "1:1 Prep Brief" that synthesizes each direct report's recent pulse-survey signals, goal status, and prior 1:1 notes into a short, editable summary delivered ahead of each scheduled 1:1, then managers will report higher perceived 1:1 quality and will complete more of their scheduled 1:1s on time, as measured by a post-1:1 quality pulse and calendar-completion data already captured by TeamPulse.

### 2.2 Business Hypothesis

We believe that this capability is valuable enough to existing customers that it can be sold as a paid add-on tier (rather than given away in the base plan), because it directly extends TeamPulse's core data asset (pulse + review + org data) in a way competitors without that data cannot easily replicate. If true, this should show up as: (a) trial-to-paid conversion on the add-on among design-partner accounts, and (b) a measurable reduction in seat churn on accounts that adopt it, since the leading indicator it targets (1:1 quality) is already correlated with regretted attrition in TeamPulse's own data model.

### 2.3 Success Metrics

| Metric | Type | Target for Validation Phase |
|---|---|---|
| % of scheduled 1:1s with a Prep Brief opened beforehand | Adoption / leading | ≥ 60% within pilot accounts by week 6 |
| Manager-reported 1:1 quality (post-1:1 pulse, 1–5 scale) | Quality / leading | ≥ 0.4 point lift vs. pre-pilot baseline |
| 1:1 on-time completion rate | Behavior | ≥ 10 percentage-point lift vs. account baseline |
| Add-on trial-to-paid conversion | Business / lagging | ≥ 25% of pilot accounts convert to paid tier |
| 90-day seat retention on adopting accounts | Business / lagging (directional only in pilot) | Directionally flat-to-positive vs. non-adopting control accounts |

## 3. Prototype or Service Blueprint

### 3.1 Solution Concept: the 1:1 Prep Copilot

The core artifact is a short, AI-generated "Prep Brief" surfaced inside TeamPulse (and optionally pushed to Slack or email) 24 hours before each scheduled 1:1. It summarizes: recent pulse-survey movement for that report, open/at-risk goals, unresolved themes from the last 1:1 note, and one suggested discussion prompt. The manager can edit or dismiss any line — the AI drafts, the manager owns the conversation.

### 3.2 Prototype / Wireframe Description

The mockup below shows the in-app Prep Brief exactly as a manager sees it, including the hover-tooltip pattern that exposes data traceability on every card — the mechanism referenced in Section 3.4.

```
+-----------------------------------------------------------------+
|  1:1 PREP BRIEF                                          [ x ]  |
|  Jordan Reyes  .  Senior Analyst  .  Last 1:1: 9 days ago        |
+-----------------------------------------------------------------+
|  PULSE SIGNAL                                       (source) >  |
|  "Workload sentiment dipped slightly this month."                |
|   ______________________________________                        |
|  | HOVER TOOLTIP                           |                     |
|  | Source: Pulse Survey, week of Aug 17      |  <- traceability   |
|  | Raw delta: -0.3 pts (5-point scale, n=1)  |     on hover       |
|  |______________________________________|                        |
+-----------------------------------------------------------------+
|  GOALS                                              (source) >  |
|   - Q3 Migration Plan .................... ON TRACK              |
|   - Cross-team Handoff Doc ................ AT RISK               |
+-----------------------------------------------------------------+
|  CARRIED-OVER THREAD                                (source) >  |
|  "Wanted to revisit scope on the API project."                   |
+-----------------------------------------------------------------+
|  SUGGESTED PROMPT                          [ AI SUGGESTION ]    |
|  "How's the handoff doc blocker looking this week?"              |
+-----------------------------------------------------------------+
|  [ Edit Brief ]   [ Start Notes From This ]  [ Not Helpful - X ] |
+-----------------------------------------------------------------+
```

Every card carries a "(source)" affordance. On hover or tap, it opens the tooltip pattern shown on Card 1 — the exact survey wave, the raw underlying delta, and the sample size behind the plain-language summary. This is the traceability mechanism referenced in the AI system-boundary design note (3.4): nothing on the brief is presented without a visible path back to its source data.

### 3.3 Service Blueprint

The blueprint below separates what the manager experiences (frontstage) from the systems and AI processing that support it (backstage), and flags where human oversight and existing support processes intervene.

| Stage | Manager Action (Frontstage) | System / UI (Frontstage) | AI & Backend Process (Backstage) | Support / Oversight Process |
|---|---|---|---|---|
| T-24h before 1:1 | Receives a notification | Slack/email nudge + in-app card appears | Scheduler triggers brief-generation job; retrieves pulse, goals, and last note data for that report | Rate-limited per account to control inference cost |
| Brief generation | — (automatic) | — | LLM call synthesizes retrieved data into a 4-part brief using a constrained template (no free-form claims beyond retrieved data) | Automated guardrail checks output against source data before release (see 3.4) |
| Review | Opens brief, reads, edits or dismisses any card | Prep Brief screen inside TeamPulse | Edits are logged as feedback signal for prompt tuning | — |
| 1:1 happens | Uses brief as optional reference during the conversation | Optional "start notes from brief" pre-fills the notes screen | None during the conversation itself — no recording or transcription | Manager can fully opt out per report or org-wide |
| Post-1:1 | Completes a 1-question quality pulse (optional) | In-app micro-survey | Response feeds the adoption/quality metrics in Section 2.3 | HR admin dashboard shows aggregate (never individual) adoption trends |

The diagram below expresses the same blueprint as a layered system map, separating what the manager sees from the application layer and the core AI layer — including the guardrail validator that sits between the LLM and any output the manager can see.

```
+----------------------------------------------------------------+
|  FRONTSTAGE / UI                                                |
|                                                                  |
|  +------------------+       +-------------------------------+   |
|  | Slack / Email    | ----> | In-App Prep Brief Screen       |   |
|  | Nudge (T-24h)    |       | (Section 3.2 mockup)           |   |
|  +------------------+       +---------------+-----------------+   |
|                                              |                  |
|                              Manager: edits / dismisses / uses |
+----------------------------------------------|-----------------+
                                                |
                                                v
+----------------------------------------------|-----------------+
|  BACKSTAGE APPLICATION LAYER                  |                 |
|                                                |                 |
|  +------------+   +---------------------+   +--------------+   |
|  | Scheduler  |-->| Data Retrieval Svc   |-->| Context      |   |
|  | (T-24h job)|   | pulse / goals / notes|   | Payload      |   |
|  +------------+   +---------------------+   +------+-------+   |
|                                                     |           |
|                                    +----------------v-------+   |
|                                    | Prompt Orchestrator     |   |
|                                    +------------+-----------+   |
+---------------------------------------------------|-------------+
                                                     |
                                                     v
+---------------------------------------------------|-------------+
|  CORE AI LAYER                                     |             |
|                                                     |             |
|                                    +----------------v-------+     |
|                                    | LLM: Brief Generation   |     |
|                                    +------------+-----------+     |
|                                                 |                 |
|                                    +------------v-----------+     |
|                                    | Guardrail Validator     |     |
|                                    +------+-----------+-----+     |
|                                   PASS |           | FAIL        |
|                          +--------------v--+   +---v----------+  |
|                          | Structured Brief |   | Reject +     |  |
|                          | Output           |   | Regenerate   |--+  (loops to LLM)
|                          +--------+---------+   +--------------+  |
+-----------------------------------|---------------------------------+
                                    |
                                    v
                 delivered back to Frontstage nudge / in-app card
```

### 3.4 AI System Boundary and Guardrails (design note)

- The model is restricted to summarizing retrieved structured data (pulse scores, goal status, prior notes) — it is not permitted to infer performance ratings, generate disciplinary language, or make judgments about a person's character or job security.
- Every Prep Brief line is traceable back to a source data point in the UI (hover-to-see-source), so managers can distinguish "the system observed X" from "the system suggests Y."
- A manager can disable the feature per-report or account-wide at any time; HR admins can disable it org-wide.

## 4. Validation Plan

### 4.1 Riskiest Assumptions

| Assumption | Why It's Risky | Validation Priority |
|---|---|---|
| Managers will actually open and use an AI-generated brief before a 1:1, rather than ignoring it | Untested behavior change; managers may distrust AI summaries of their team | Highest — invalidates the whole concept if false |
| A short AI summary meaningfully improves 1:1 quality (not just makes managers feel more prepared) | Perceived prep ≠ conversation quality; hard to measure directly | High |
| Customers will pay incrementally for this rather than expecting it in the base plan | Add-on pricing on top of existing seats is a harder sell than a new product | High |
| HR admins will trust the privacy/oversight model enough to turn it on for their org | Any AI feature touching performance-adjacent data raises trust concerns | Medium-High |

### 4.2 Validation Methods and Timeline

| Phase | Method | Duration | What It Tests |
|---|---|---|---|
| 1. Concept check | 5–7 moderated interviews with existing managers using a clickable prototype (no live AI yet) | Week 1–2 | Do managers understand the concept and see value? Initial reaction to trust/oversight model |
| 2. Concierge pilot | 3 design-partner accounts; PM manually assembles "briefs" (Wizard-of-Oz) for ~20 managers for 3 weeks | Week 2–5 | Real usage behavior and 1:1-quality signal without building the full AI pipeline first |
| 3. AI-powered pilot | Same accounts get the real AI-generated brief (with guardrails from 3.4) for 4 weeks | Week 5–9 | Adoption rate, edit/dismiss rate, quality-pulse lift, technical reliability |
| 4. Pricing test | Present add-on pricing to pilot accounts' HR admin buyers at pilot's end; gauge willingness to pay | Week 9–10 | Business hypothesis: will they pay incrementally? |

### 4.3 Success and Kill Criteria

- Proceed to build if: ≥ 50% brief-open rate in the concierge pilot, and at least 2 of 3 design-partner HR admins indicate willingness to pay in the pricing test.
- Iterate on concept if: open rate is 25–50% — investigate whether the friction is trust, timing, or content relevance before killing.
- Kill or fundamentally rework if: open rate < 25% after two iterations, or managers report the brief feels invasive/surveillance-like in interviews.

## 5. Business Economics and Operational Feasibility Evaluation

### 5.1 Pricing and Revenue Model

Positioned as a per-manager-seat add-on on top of existing TeamPulse contracts (expansion revenue, not new-logo revenue), at an illustrative $6–$9 per manager seat per month, sold in a minimum block (e.g., all managers in a business unit) to simplify rollout and avoid adverse selection (only the least time-pressed managers opting in).

### 5.2 Token-Level Inference Cost Model

Pricing basis: $2.50 per 1M input tokens, $10.00 per 1M output tokens. Two model calls sit behind every brief: the generation call (Prompt Orchestrator → LLM) and the guardrail validation call (Guardrail Validator, Section 3.3) that checks the draft before it reaches the manager.

| Call | Input Tokens | Output Tokens | Input Cost | Output Cost | Cost / Call |
|---|---|---|---|---|---|
| Brief generation (context payload + prompt) | 1,200 | 350 | 1,200 ÷ 1,000,000 × $2.50 = $0.0030 | 350 ÷ 1,000,000 × $10.00 = $0.0035 | $0.0065 |
| Guardrail validation (draft brief + policy rules) | 400 | 50 | 400 ÷ 1,000,000 × $2.50 = $0.0010 | 50 ÷ 1,000,000 × $10.00 = $0.0005 | $0.0015 |
| **Total per brief** | **1,600** | **400** | **$0.0040** | **$0.0040** | **$0.0080** |

| Metric | Value | Derivation |
|---|---|---|
| Briefs per manager / month | 4 | Weekly 1:1 cadence |
| Inference cost per manager / month | $0.0320 | 4 briefs × $0.0080 |
| Avg. managers per adopting account | 35 | Synthetic 800-employee account, ~1:23 manager ratio |
| Inference cost per account / month | $1.12 | 35 managers × $0.0320 |
| Add-on ARPU per manager seat / month | $7.50 | Midpoint of illustrative $6–$9 pricing band |
| Incremental ARR per adopting account | $3,150.00 | 35 seats × $7.50 × 12 months |
| Inference cost as % of incremental ARR | 0.43% | ($1.12 × 12) ÷ $3,150.00 |
| Incremental CAC | ≈ $0 (expansion motion) | Sold by existing CSM/AE to an installed account, no new acquisition spend |

At this token profile, inference cost is not a material margin constraint — it holds under 0.5% of incremental ARR even before accounting for prompt caching or batching, which would lower it further. The binding cost driver for this feature is engineering time (Section 5.3), not per-brief inference spend. Token counts (1,200 in / 350 out for generation; 400 in / 50 out for validation) are engineering estimates for a template-constrained, single-report brief — not measured from a running system — and should be replaced with real token telemetry once the concierge pilot's AI-powered phase (Section 4.2, Phase 3) is live.

### 5.3 Cost to Build and Operate

- Engineering: ~1 PM + 2 backend/ML engineers + 1 designer for an estimated 8–10 week build to MVP, reusing existing pulse/goals/notes data models (most of the cost is data-retrieval plumbing and guardrail logic, not the LLM call itself).
- Ongoing: inference cost (see 5.2) plus incremental support load from an HR-admin-facing on/off control and a manager-facing feedback loop.
- No new core infrastructure required — this rides on TeamPulse's existing data platform and auth model.

### 5.4 Operational Feasibility

| Dimension | Assessment |
|---|---|
| Data sensitivity | High — touches engagement and performance-adjacent data. Requires the guardrails in 3.4, an org-level opt-in, and clear documentation for HR admins on what data is used and not stored/used for model training beyond the account's own data. |
| Integration effort | Low-medium — reuses existing TeamPulse data (pulse, goals, notes); main new integration is optional Slack/email delivery. |
| Trust & change management | Medium-high effort — requires HR-admin-facing documentation, an easy account-wide off switch, and manager opt-out, given sensitivity of the data touched. |
| Compliance | Should be reviewed against the company's existing data-processing agreements before AI processing of engagement/performance data is enabled for any customer; may require a DPA addendum. |

### 5.5 Key Risks

- Trust risk: an AI feature that touches performance-adjacent data can be perceived as surveillance even when well-designed — mitigated by transparency and opt-outs, but not eliminated.
- Adoption risk: managers may default to ignoring an unfamiliar notification pattern regardless of usefulness — this is the primary reason the validation plan front-loads a concierge (non-AI) pilot before building the full pipeline.
- Pricing risk: buyers may expect this bundled into the base plan rather than paying incrementally, which the Week 9–10 pricing test is designed to surface early.

## 6. AI Usage Demonstration

This section documents how AI (Claude) was used to produce this package, consistent with an AI-native product-development approach rather than treating AI as a one-off writing tool.

| Stage | How AI Was Used | My Role as PM |
|---|---|---|
| Problem framing | Asked Claude to help generate and stress-test 3 candidate problem statements from the synthetic research inputs, and to draft a reach/frequency/intensity scoring rubric | Chose the synthetic research themes to feed in, set the scoring criteria, and made the final selection call in 1.1 |
| Hypothesis drafting | Used Claude to draft the product and business hypothesis in standard "we believe / if / then / as measured by" format, then iterated on the specific metrics | Adjusted target metrics to be realistic for a pilot-stage (not full-scale) rollout |
| Service blueprint | Asked Claude to structure a frontstage/backstage service blueprint and to propose AI system-boundary guardrails appropriate for HR-adjacent data | Set the constraint that the AI must not infer performance judgments — this shaped the guardrails in 3.4 |
| Validation plan design | Used Claude to sequence a validation plan that de-risks the build (concierge pilot before AI pilot) and to draft kill criteria | Set the actual thresholds and the phase-4 pricing test, based on standard lean-validation practice |
| Unit economics | Asked Claude to construct a token-level unit-economics model and verify the arithmetic (input/output token cost × call volume) | Verified the arithmetic independently (see Section 7.1) and flagged which numbers are illustrative vs. would need real data |
| Document production | Used Claude's document-creation tooling to format this package as a structured, exportable document | Reviewed structure, edited language, and confirmed all required deliverable sections were present |

In short, AI was used throughout the workflow — for ideation, structuring, drafting, and light quantitative modeling — while problem selection, target-setting, risk framing, and final judgment calls remained mine as the Product Owner.

## 7. AI Output Verification and Limitations

### 7.1 Verification Approach

- Arithmetic check: the unit-economics figures in 5.2 (ARPU × seats × 12 = incremental ARR; token cost × tokens × call volume) were independently recalculated by hand rather than trusted as-generated.
- Plausibility check: figures such as manager-to-employee ratio (~1:23) and per-brief token counts were checked against general knowledge of mid-market org structures and typical short-generation LLM usage for reasonableness, not against a real billing statement or benchmark study.
- Internal consistency check: confirmed the service blueprint's AI guardrails (3.4) are actually reflected in the validation plan and problem framing (e.g., the concierge-pilot-first sequencing in Section 4 exists specifically because the AI-generated first draft initially proposed going straight to an AI pilot, which I judged too risky without a non-AI behavioral baseline).
- Scope check: confirmed every required deliverable category from the quest brief is addressed as its own section, rather than trusting the AI's initial document outline.

### 7.2 Known Limitations and Caveats

- This entire scenario — the company, the interviews, the support-ticket themes, the pricing, and the unit economics — is synthetic. It illustrates the reasoning process a Product Owner would use, but none of the underlying "evidence" is real and none of it should be read as a claim about any actual company or market.
- The reach/frequency/pain-intensity scores in 1.1 and the adoption targets in 2.3 are directional estimates for demonstration purposes, not statistically derived from real research.
- The unit-economics figures in 5.2 are illustrative; a real business case would need actual account-size distributions, an actual LLM inference bill, and a real pricing study (e.g., van Westendorp or conjoint pricing research) before being used to make a funding decision.
- AI-generated content can understate uncertainty or present plausible-sounding numbers with false precision — several of the AI's first-draft figures were rounded or re-labeled as "illustrative" during review specifically to avoid implying a level of confidence the synthetic exercise doesn't support.
- A real version of this package would require actual HR-admin and manager interviews, a real DPA/compliance review, and real usage data from the concierge pilot before any build investment — this package should be read as a structured hypothesis and plan, not a validated business case.