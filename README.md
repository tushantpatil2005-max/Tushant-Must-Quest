TEAMPULSE — 1:1 PREP COPILOT
Portfolio Case Study & Handoff — 5-Day AI-Native Product Sprint
Prototype (live, interactive): TeamPulse_Prep_Copilot_Prototype.html — accompanies this document as a separate file.
1. Problem and User
Target user: frontline and mid-level people managers (4–12 direct reports) at mid-market companies (200–2,000 employees) who
already use a people-analytics platform for pulse surveys, goals, and 1:1 notes.
Problem: managers spend an estimated 2–4 hours per week manually reassembling context before 1:1s — pulling pulse-survey
movement, goal status, and prior notes from separate tools. This is inconsistent, often skipped under time pressure, and produces
shallow or reactive 1:1s, which is a leading indicator of regretted attrition.
Category fit: automating repetitive work for a frontline/professional operator (the people manager).
Scope for this 40-hour sprint / exclusions:
• In scope: single-feature AI prep-brief generator, using existing pulse/goals/notes-style data as input.
• Out of scope: building a full HRIS platform, real customer data, multi-language support, native mobile app, real Slack/email
delivery integration.
2. Evidence and Baseline
No real customer access was available inside the sprint window, so evidence is synthetic and explicitly labeled as such — used to
simulate the kind of qualitative/quantitative signal a PM would triage, not as proof of the problem.
Synthetic Evidence Source Finding
Support-ticket theme scan (90-day window, simulated) "Manual prep" / "no single view of history" themes in ~31% of
manager-tagged tickets
12 synthetic manager interviews 9 of 12 described reconstructing 1:1 context from memory or ad hoc
notes
Synthetic exit-survey scan ~22% of mid-market exit surveys referenced inconsistent or
unprepared check-ins
Baseline (today): context assembly is manual, multi-tool, and inconsistent — no system of record for what was discussed or
observed between 1:1s.
Desired change: managers open a synthesized, source-linked brief before ≥50% of scheduled 1:1s within a pilot, replacing manual
assembly for that portion of use.
3. Solution and UX
The 1:1 Prep Copilot generates a short, editable brief 24 hours before a scheduled 1:1: a plain-language pulse-signal summary, open
goal status, one carried-over thread from the last note, and one optional AI-suggested discussion prompt. The manager can edit,
use, or dismiss any card — the AI drafts, the manager owns the conversation.
Core flow: nudge (Slack/email) → in-app brief screen → manager reviews/edits → optional "start notes from brief" → post-1:1 one-
question quality pulse. Every card carries a source affordance (hover-to-see-source) so nothing is presented without a visible path
back to underlying data — implemented and testable in the prototype.
Exception handling built into the UX: if generation fails or output can't be parsed, the manager sees an explicit retry state, never a
guessed or partial brief. This is demonstrated live in the prototype, not just described (see Section 4).
Human intervention: manager can dismiss/disable per report; an org-level off-switch (not built in the 40-hour prototype,
documented as a requirement in Handoff) is required before any real pilot.
4. AI Logic
What the AI does: one structured-output call synthesizes a JSON context payload (pulse delta, goal list, last open thread) into four
short fields (pulse_summary, goals_note, carried_over, suggested_prompt), using a system prompt that forbids inventing data or
making performance/character judgments.
Data flow (implemented in the prototype, visible in its live system log): 1) assemble context JSON from source data → 2) call the
model with a constrained system prompt requesting JSON-only output → 3) run a guardrail check against the returned text → 4)
render only if the check passes.
Evaluation/guardrail method used in the 40-hour build: a client-side pattern check that blocks output containing disciplinary or
character-judgment language (e.g., firing, competence, performance-rating phrasing) before it ever reaches the manager-facing UI.
This is a real, working check, not a described one.
Fallback behavior (implemented): API failure and JSON-parse failure both route to an explicit error state with a retry action — no
silently degraded or partially-invented brief is ever shown.
Known limitation: the guardrail is a keyword/pattern check, not a second semantic-validation model call. It will miss subtler
judgmental phrasing. A production build should add a second LLM-based guardrail pass (as scoped in the original design, cost
modeled in Section 5) — cut from the 40-hour prototype for time, not because it's unnecessary.
5. Business and Operations
Customer value: reduces 2–4 hours/week of manual prep per manager and targets a leading indicator (1:1 quality) TeamPulse
already correlates with retention.
Pricing hypothesis: per-manager-seat add-on, ~$6–$9/month, sold to existing accounts (expansion revenue, not new-logo).
Metric Value Basis
Inference cost per brief $0.008 1,600 in-tokens + 400 out-tokens at $2.50/1M in,
$10.00/1M out (see prototype log for live per-call
figures)
Inference cost per account / month ≈ $1.12 35 managers × 4 briefs/month × $0.008
Incremental ARR per adopting account $3,150 35 seats × $7.50 × 12 months
Inference cost as % of ARR 0.43% Not a material margin constraint at this usage
pattern
Incremental CAC ≈ $0 Expansion motion via existing account team, not
new acquisition
Manual work / dependencies not automated: HR-admin rollout communication, org-level opt-in decision, DPA/compliance review
before any account touches real engagement data, and ongoing guardrail-pattern maintenance.
Key assumption this is most sensitive to: that managers will actually open the brief rather than ignoring another notification — this
is the first thing the validation plan (Section 7) is designed to test.
6. Evaluation
Because there is no real usage data yet, evaluation in this sprint focused on exercising the built system's logic paths rather than a
live field test.
Case Type Test Result
Normal 3 synthetic reports with distinct pulse/goal/thread profiles
(Jordan: mixed signal; Priya: positive; Marcus: two at-risk
goals + negative pulse)
All three produce distinct, source-grounded
briefs — confirms the model isn't defaulting to
templated output regardless of input
Edge Report with an unusually large negative pulse delta
alongside multiple at-risk goals (Marcus)
Brief stays descriptive, does not escalate into
judgment language — guardrail available as
backstop
Case Type Test Result
Failure Simulated API failure / malformed JSON response Routes to explicit retry state; no partial or
fabricated brief is ever rendered — verified in
code, not just claimed
Guardrail trigger Pattern check tested against seeded disallowed phrases
(e.g., "should be fired")
Correctly blocks rendering and shows a blocked-
output state instead of the brief
Baseline comparison: manual prep (today) has no consistency check and no source traceability at all; the prototype's failure modes
are visible and blocked, whereas a manager's own memory-based prep has silent, invisible failure modes (forgotten context, no
record).
Bias/hallucination risk not fully covered in 40 hours: the model could still understate or overstate pulse movement in subtle ways
the keyword guardrail wouldn't catch — this needs human-rated evaluation against real pulse data before a pilot, not just pattern
matching.
Remaining evidence required before build investment: real manager reaction to the concept (not simulated), real token usage under
production system prompts, and a semantic (not just keyword) guardrail false-negative rate.
7. Post-Launch 60-Day Validation Plan
Window What's Measured Decision Criteria
Days 1–14 Brief-open rate before scheduled 1:1s <25% open rate → stop and re-interview
managers on why
Days 1–30 Edit/dismiss rate per brief; guardrail block rate Guardrail block rate >5% of briefs → pause pilot,
tighten prompt/guardrail before continuing
Days 15–45 Manager-reported 1:1 quality (post-1:1 pulse, 1–5) <0.2 point lift vs. pre-pilot baseline at day 45 →
iterate on brief content, don't scale
Days 45–60 HR-admin willingness to pay (pricing conversation) <2 of 3 design-partner admins indicate willingness
to pay → hold pricing, don't commercialize yet
Proceed: ≥50% open rate by day 30 AND ≥0.4 point 1:1-quality lift by day 60 AND ≥2 of 3 admins willing to pay → move to broader
rollout planning.
Iterate: metrics land in a middle band (25–50% open rate, or 0–0.4 point lift) → revise brief content/timing/guardrail before re-
testing, don't scale or kill yet.
Stop: open rate <25% after one iteration, or managers describe the brief as invasive/surveillance-like in interviews at any point.
8. Handoff
• Product: the riskiest untested assumption is manager adoption behavior, not AI quality — next step is the Day-1-14 open-rate
test above, not further prompt tuning.
• Design: the source-tooltip pattern (hover-to-see-source) is the trust mechanism the whole concept leans on — do not ship a
version without it.
• Engineering: the prototype's guardrail is a client-side keyword filter for demo purposes only — production needs server-side
enforcement plus a second semantic-validation model call (cost-modeled in Section 5, cut from this build for time).
• Data: brief generation currently takes a flat JSON payload — a real build needs a defined contract with the existing
pulse/goals/notes services, including what happens when one data source is missing (not yet handled).
• Operations/Compliance: do not enable this for any account with real employee data before a DPA review — the prototype and
this document use only invented, synthetic people and data.
9. AI and Tool-Use Note
Tool used: Claude (Anthropic), via chat for planning/drafting and via a live API call embedded in the prototype itself for brief
generation.
Purpose: (1) structuring the problem/solution/validation logic and this case study, (2) generating the prototype's HTML/CSS/JS, (3)
at runtime, generating each 1:1 brief from the JSON context payload — this is the actual AI logic under test, not a simulation of it.
Material prompts/workflow: the system prompt embedded in the prototype (visible in its source, Section 4) constrains the model to
JSON-only output, forbids inventing data, and forbids performance/character judgments. Case-study drafting used iterative prompts
to restructure content against this exact rubric.
Verification method: token-cost arithmetic was independently recalculated by hand (not trusted as generated); the guardrail and
fallback logic were verified by code review of the actual conditional paths (API-failure branch, JSON-parse-failure branch, guardrail-
fail branch) rather than assumed to work; every synthetic evidence figure is explicitly labeled synthetic rather than presented as
real.
Limitations: synthetic evidence and synthetic unit economics are illustrative, not validated; the guardrail is keyword-based and will
miss subtler problematic phrasing; no real users have seen or used this prototype yet.
10. Prior-Work Disclosure
Fill in before submitting — replace the bracketed placeholders with your actual timeline; do not submit this section unedited.
• [State the date/time your official 40-hour Quest clock started.]
• Concept origin: the TeamPulse scenario, problem selection, and initial hypothesis/economics framing were developed in
conversation with Claude [before / after — state which] the Quest clock started. If before, treat that material as prior work and
describe what was newly built or substantively revised during the 40-hour window (e.g., the interactive prototype in Section 3–
4, the evaluation test cases in Section 6, the 60-day validation plan in Section 7, and this case-study restructuring were
produced specifically for the Quest submission).
• [Disclose any other pre-existing templates, code snippets, or assets reused, if any.]