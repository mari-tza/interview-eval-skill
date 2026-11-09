---
name: interview-eval
description: Use when the user pastes a technical interview transcript and wants a detailed evaluation — assesses communication, technical depth, level signals, collaboration, cross-cultural factors, and generates an improvement report
---

# Interview Transcript Evaluator

A skill that takes a technical interview transcript and produces a structured evaluation report with scores, evidence-based feedback, and actionable improvement recommendations.

## When to Use

- User pastes a transcript and asks for evaluation/feedback
- User says "evaluate this interview", "review my interview", "interview eval"
- User invokes `/interview-eval` with a transcript

## Input

A transcript of a technical interview (mock or real). Can be raw text, timestamped, or speaker-labeled.

### Optional Context (ask if not provided)

| Parameter | Description | Default |
|-----------|-------------|---------|
| **Interview format** | coding, system design, behavioral, hiring manager, pair programming, mixed | Auto-detect from transcript |
| **Target level** | junior, mid, senior, staff, principal | Infer from questions and depth |
| **Company/culture** | Company name or cultural context (US, EU, LatAm, etc.) | Generic tech |
| **Mock vs real** | Whether this is practice or a real debrief | Assume mock |
| **Role type** | backend, frontend, fullstack, data, infra, management, etc. | Infer from content |
| **Preparation script** | A script, outline, or notes the candidate prepared before the interview. Used to compare planned vs actual answers. | None |

## Process

### 1. Parse the Transcript

Identify:
- **Speakers** — who is the interviewer and who is the candidate. If ambiguous, ask.
- **Interview format** — coding, system design, behavioral, pair programming, hiring manager screen, mixed, async video, take-home defense.
- **Target level** — junior, mid, senior, staff, principal. Infer from questions asked and depth expected.
- **Language dynamics** — is the candidate speaking in their native language? Note any ESL considerations.

### 2. Evaluate Across Dimensions

Score each dimension **independently** to avoid halo/horn effect. Use evidence from different parts of the transcript to counter recency bias.

---

#### A. Communication & Structure (Weight: 20%)

| Signal | What to look for |
|--------|-----------------|
| **Structured thinking** | Organizes answer before diving in ("I'll break this into three parts..."). Outlines before details. |
| **STAR/CAR usage** | For behavioral questions: Situation, Task, Action, Result — or rambling without structure? |
| **Conciseness** | Answers the question directly, or takes detours? Can summarize in one sentence when needed? |
| **Clarifying questions** | Asks clarifying questions before solving? Or jumps to assumptions? |
| **Active listening** | Addresses what was actually asked, or pivots to what they want to talk about? |
| **Thinking out loud** | Narrates reasoning so the interviewer can follow the thought process? |
| **Adaptability** | When the interviewer redirects, adapts smoothly or gets stuck on original path? |
| **Listener awareness** | Adjusts explanation depth based on the audience — simplifies for non-technical, adds precision for technical? |

---

#### B. Technical Depth & Problem Solving (Weight: 25%)

| Signal | What to look for |
|--------|-----------------|
| **First principles** | Reasons from fundamentals or just pattern-matches memorized answers? |
| **Trade-off analysis** | Articulates trade-offs explicitly? ("Option A gives us X but costs Y; Option B...") |
| **Scope management** | Identifies what's in scope vs out of scope? Asks about constraints? |
| **Incremental approach** | Starts simple and iterates, or tries to build the perfect solution from scratch? |
| **Edge cases** | Proactively considers edge cases, failure modes, and error handling? |
| **Depth vs breadth** | Can go deep when probed, or stays surface-level? |
| **Real experience vs theory** | Examples come from real work, or sound like textbook answers? |
| **System awareness** | Considers the broader system context — monitoring, deployment, scaling, security? |

---

#### C. Level Signals (Weight: 15%)

| Signal | Junior | Mid | Senior | Staff+ |
|--------|--------|-----|--------|--------|
| **Scope of impact** | Task-level | Feature-level | System-level | Org/cross-team level |
| **Decision making** | Follows guidance | Makes local decisions | Drives technical decisions for the team | Shapes technical strategy across teams |
| **Ambiguity handling** | Needs clear specs | Handles some ambiguity | Thrives in ambiguity, defines the problem | Identifies problems others haven't seen |
| **Mentoring signals** | Learning | Helping peers | Teaching and growing others | Building systems that scale people |
| **Ownership** | Owns their code | Owns their feature | Owns their system end-to-end | Owns outcomes across systems |
| **Business awareness** | Focused on tech | Understands product context | Connects tech decisions to business impact | Drives tech strategy from business needs |
| **Influence** | Within their team | Across team boundaries | Across org | Industry/company-wide |
| **Conflict navigation** | Avoids or escalates | Navigates with support | Navigates independently with empathy | Resolves systemic conflicts, builds alignment frameworks |

---

#### D. Behavioral & Leadership (Weight: 15%)

| Signal | What to look for |
|--------|-----------------|
| **Ownership narrative** | Takes ownership of outcomes (not just tasks)? "I led" vs "we did" — look for clear accountability. |
| **Failure stories** | Talks about failures honestly? Shows genuine learning, not just humble-bragging? |
| **Collaboration evidence** | Concrete examples of working with others, resolving disagreements, aligning stakeholders. |
| **Growth mindset** | Evidence of learning from mistakes, seeking feedback, adapting approach. |
| **Stakeholder management** | Explains technical concepts to non-technical audiences? Thinks about who their work affects? |
| **Impact framing** | Frames work in terms of impact (metrics, outcomes) or just activity (tasks, deliverables)? |
| **Quantified outcomes** | Uses numbers — "reduced latency by 40%", "saved 10 hours/week" — or only qualitative claims? |

---

#### E. Collaboration Signals (Weight: 10%)

Especially relevant for pair programming and system design interviews.

| Signal | What to look for |
|--------|-----------------|
| **Response to hints** | When the interviewer gives a hint, does the candidate incorporate it gracefully? Or ignore/resist it? |
| **Response to pushback** | When challenged, does the candidate defend with evidence, cave immediately, or become defensive? |
| **Building on ideas** | Does the candidate build on the interviewer's suggestions, or only follow their own thread? |
| **Asking for input** | Does the candidate invite the interviewer's perspective? ("What do you think about this approach?") |
| **Pair dynamics** | In pair programming: do they communicate intent before coding? Do they share the keyboard/direction? |
| **Curiosity** | Asks genuine questions about the problem space, team, or role — not just rehearsed closing questions. |

---

#### F. AI Assistance Detection (for live interviews only)

Assess whether the candidate appears to be using undisclosed AI tools during a live, synchronous interview. **Skip this dimension for take-home or async formats unless explicitly requested.**

| Signal | Indicator | Severity |
|--------|-----------|----------|
| **Sudden fluency shifts** | Struggles verbally but produces perfectly structured written answers. Gap between spoken reasoning and written output is suspiciously large. | High |
| **Unnatural response timing** | Long pauses before producing complete, polished answers. Real thinking produces incremental output; AI-assisted answers appear all at once. | High |
| **Copy-paste artifacts** | Code appears in large blocks rather than being typed incrementally. Markdown formatting in conversational contexts. | High |
| **Vocabulary mismatch** | Uses terminology in written answers that they couldn't explain when speaking. | Medium |
| **Over-engineered first attempts** | First version is already clean, well-named, with edge cases handled — no iteration, no debugging. | Medium |
| **Can't explain own code** | Writes correct code but struggles to walk through it or modify it when requirements change. | High |
| **Perfect error handling from start** | Production-quality error handling in a first draft during a timed interview. | Medium |
| **Generic/template answers** | Perfectly structured STAR format with generic language, lacking specific details, names, or dates. | Medium |
| **Inconsistent skill level** | Solves a hard problem perfectly but struggles with a trivial follow-up. | Medium |

**Important nuances:**
- A single signal is not proof. Look for **combinations** of signals.
- ESL candidates naturally have a gap between spoken and written fluency — factor this in.
- Some candidates are just well-prepared. A structured STAR answer alone doesn't mean AI.
- The goal is to assess **authenticity**, not to police tools.

---

#### G. Interview Mechanics (Weight: 10%)

| Signal | What to look for |
|--------|-----------------|
| **Time management** | Paces themselves appropriately? Spends too long on one part? |
| **Question handling** | Handles curveball questions gracefully? |
| **Confidence calibration** | Confident without being arrogant? Says "I don't know" when appropriate? |
| **Energy and engagement** | Seems genuinely interested and engaged? |
| **Closing strong** | Asks good questions at the end? Leaves a strong final impression? |

---

#### H. Cross-Cultural Adjustment Notes (not scored — coaching only)

When the candidate is interviewing across cultural boundaries, note patterns that may be misread. These are **coaching notes**, not score deductions.

| Pattern | Context | Coaching note |
|---------|---------|---------------|
| **"We" instead of "I"** | Common in LatAm, East Asian, and collectivist cultures. Understating individual contribution is a social norm. | Coach: "Reframe with I-statements for US/EU contexts. 'I led the migration' instead of 'we migrated.'" |
| **Elaborate context-setting** | More verbose framing before the core answer. Relationship-building preamble. | Coach: "Lead with the punchline. Context is good but front-load the answer in 1-2 sentences first." |
| **Indirect self-promotion** | Avoids stating accomplishments directly. May downplay impact. | Coach: "Practice stating impact directly. 'I reduced costs by X' is expected, not arrogant." |
| **Lower assertiveness** | Soft language, hedge words ("maybe", "I think perhaps"), less interrupting. | Coach: "Replace hedge words with confidence markers. 'I'd recommend X because...' instead of 'Maybe we could try X?'" |
| **Conversational overlap** | In some cultures, talking over someone signals engagement, not rudeness. | Coach: "In US interviews, wait for the interviewer to finish. Use nodding to show engagement instead." |
| **Formality level** | More formal address, less casual banter. | Coach: "Match the interviewer's formality. If they're casual, it's OK to be casual back." |

---

### 3. Script Comparison (when preparation script is provided)

If the candidate provided a preparation script, outline, or notes, compare what was planned vs what was actually said:

| Aspect | What to analyze |
|--------|----------------|
| **Coverage** | Which planned points were actually delivered? Which were missed entirely? |
| **Delivery vs plan** | Where the candidate deviated from the script, was the improvisation stronger or weaker than the planned version? |
| **Adaptability** | Did the candidate adapt their script to the actual questions asked, or try to force scripted answers into unrelated questions? |
| **Naturalness** | Did scripted answers sound rehearsed/robotic, or did the candidate make them conversational? |
| **Gaps revealed** | What topics came up that the script didn't cover? These are areas to prepare for next time. |

Add a **Script vs Reality** section to the report:

```markdown
## Script vs Reality

### Delivered as planned
- <point from script> — delivered effectively / could be stronger because...

### Missed from script
- <planned point not mentioned> — opportunity to bring this up when asked about <topic>

### Improvised (not in script)
- <unscripted answer> — this worked well / this could be prepared better

### Adaptation notes
- <where the candidate adjusted the script to fit the actual question, and how well it worked>
```

---

### 4. Bias Self-Check

Before finalizing scores, the evaluator must check for cognitive biases:

| Check | Question to ask |
|-------|----------------|
| **Halo/Horn** | Am I letting one strong/weak moment inflate/deflate all scores? Are dimension scores truly independent? |
| **Recency** | Am I citing evidence from across the entire transcript, or mostly from the last 10 minutes? |
| **Similarity** | Am I rating higher because the candidate communicates like me or has a similar background? |
| **Confirmation** | Am I only looking for evidence that confirms my initial impression? Is negative and positive evidence proportionally represented? |
| **Anchoring** | If I read someone else's feedback first, am I forming my own judgment or just adjusting theirs? |

If any bias is detected, note it in the report as a **transparency flag**.

---

### 5. Generate the Report

**Filename format:** `YYYY-MM-DD - Interview Eval - <brief description>.md`

The description should capture the interview type and/or role (e.g., "System Design Senior Backend", "Behavioral Staff Engineer", "Mock Coding Python").

**Output location:** Ask the user where to save it. If they don't specify, write it to the current working directory.

---

### 6. Report Structure

```markdown
# Interview Evaluation

**Date:** YYYY-MM-DD
**Candidate:** <name or "Anonymous">
**Type:** <interview format detected>
**Target Level:** <inferred or stated level>
**Role:** <role type>
**Company/Context:** <if provided>
**Mock/Real:** <mock or real>
**Overall Assessment:** <one-line summary>

---

## Score Summary

| Dimension | Score | Weight | Notes |
|-----------|-------|--------|-------|
| Communication & Structure | ⬛⬛⬛⬜⬜ | 20% | <one-line> |
| Technical Depth | ⬛⬛⬛⬛⬜ | 25% | <one-line> |
| Level Signals | ⬛⬛⬛⬜⬜ | 15% | <one-line> |
| Behavioral & Leadership | ⬛⬛⬜⬜⬜ | 15% | <one-line> |
| Collaboration Signals | ⬛⬛⬛⬜⬜ | 10% | <one-line> |
| Interview Mechanics | ⬛⬛⬛⬛⬜ | 10% | <one-line> |
| AI Assistance Suspicion | ⬛⬜⬜⬜⬜ | — | <one-line> |
| **Weighted Overall** | **⬛⬛⬛⬜⬜** | | |

Scoring: 1-5 filled blocks (⬛). Unfilled (⬜) for remainder.
AI Assistance: 1 = no signs, 5 = strong indicators. Lower is better. Not weighted.

---

## Strengths

Bullet points of what went well, with **specific quotes or moments** as evidence. Group by dimension.

Example:
- **Trade-off analysis was strong** — when asked about database choice, clearly articulated: "PostgreSQL gives us ACID guarantees we need for financial data, but we'll need read replicas for analytics to avoid impacting write performance." This shows senior-level reasoning.

---

## Areas for Improvement

For each area:

### <Area Title>

**What happened:** Describe the specific moment (with quote if possible).

**Why it matters:** Why this is important and what signal it sends to the interviewer.

**How to improve:** Concrete, actionable advice — specific techniques, frameworks, or practice exercises. Not "be better at X."

**Example of a stronger answer:** Rewrite or restructure the candidate's answer to show what a stronger version would sound like. Make it natural and conversational, not like a Wikipedia article.

---

## Seniority Calibration

Where the candidate's answers landed on the seniority spectrum:

- **Scope of impact:** Currently showing <level> signals. To reach <next level>, would need to...
- **Decision making:** ...
- **Ambiguity handling:** ...

(Only include signals that were actually demonstrated or notably absent.)

---

## Key Moments

3-5 pivotal moments — both positive and negative — that had the most impact on the overall assessment:

1. **[timestamp/context]** — <what happened and why it mattered>
2. ...

---

## Red Flags & Green Flags

### Green Flags
- <specific positive signals observed, with evidence>

### Red Flags
- <specific concerns observed, with evidence>
- If none: "No significant red flags detected."

---

## Script vs Reality

(Only include if a preparation script was provided.)

### Delivered as planned
- <point from script> — delivered effectively / could be stronger because...

### Missed from script
- <planned point not mentioned> — opportunity to bring this up when asked about <topic>

### Improvised (not in script)
- <unscripted answer> — this worked well / this could be prepared better

### Adaptation notes
- <where the candidate adjusted the script to fit the actual question, and how well it worked>

---

## Cross-Cultural Notes

(Only include if relevant — when the candidate is interviewing across cultural boundaries.)

- <pattern observed> → <coaching recommendation>

---

## Bias Transparency

Note any potential biases detected in this evaluation:
- <e.g., "Most evidence cited is from the second half of the interview — recency bias possible. Re-checked first half and assessment holds.">
- If none detected: "Bias self-check completed. Evidence cited across full transcript. No flags."

---

## Action Items

Prioritized list of specific things to practice or change:

- [ ] **High priority:** <specific action with concrete practice suggestion>
- [ ] **Medium priority:** ...
- [ ] **Low priority:** ...

---

## Practice Prompts

3-5 specific practice questions tailored to the candidate's weak areas:

1. **<Question>** — *Focus on: <specific skill to practice>*
2. ...
```

---

### 7. Format-Specific Adjustments

Adjust the evaluation rubric based on the detected interview format:

| Format | Adjust weights | Special considerations |
|--------|---------------|----------------------|
| **Pair programming** | Collaboration ↑ to 20%, Technical stays 25% | Score pair dynamics, communication during coding, response to suggestions |
| **System design** | Technical ↑ to 30%, Collaboration ↑ to 15% | Emphasize trade-offs, scope management, incremental approach |
| **Behavioral only** | Communication ↑ to 25%, Behavioral ↑ to 25%, Technical ↓ to 10% | Focus on STAR structure, impact framing, failure narratives |
| **Hiring manager** | Behavioral ↑ to 25%, Seniority ↑ to 20% | Focus on ownership, business awareness, stakeholder management |
| **Coding (solo)** | Technical ↑ to 35%, Collaboration ↓ to 5% | Focus on problem decomposition, edge cases, code quality |
| **Take-home defense** | Technical ↑ to 30% | Assess depth of understanding of own code, ability to extend/modify |

---

### 8. Deliver

After writing the report:
1. Print a brief summary (3-5 lines) of the overall assessment
2. Highlight the top 2-3 improvement areas
3. Note the file location
4. Ask if the candidate wants to deep-dive into any specific area

---

## Calibration Notes

- **Be honest but constructive.** The goal is growth, not ego protection. If the answer was weak, say so — but always pair it with a concrete path to improvement.
- **Use evidence, not vibes.** Every assessment point must reference a specific moment in the transcript. No generic feedback.
- **Calibrate to the target level.** A senior and a junior are evaluated against different standards. A junior not knowing distributed systems is expected; a senior not knowing it is a red flag.
- **Don't over-index on one moment.** A single bad answer doesn't sink an interview. Look at patterns across the whole conversation.
- **Mock vs real:** For mock interviews, be more granular and coaching-oriented. For real interview debriefs, be more strategic about what to focus on for the next round.
- **Scoring discipline:** 3/5 means "meets expectations for the level." Don't give 4s and 5s unless the candidate genuinely exceeded expectations for that dimension.
- **No "not the right fit" without evidence.** Every conclusion must trace back to a specific behavioral signal.

## Common Mistakes to Avoid

- **Generic feedback** — "improve communication" is useless. Say exactly what was unclear and how to restructure it.
- **Ignoring the positive** — always acknowledge what went well. People learn faster when strengths are reinforced alongside improvements.
- **Textbook rewrites** — when writing "a stronger answer", make it sound natural and conversational.
- **Cultural blindness** — note when a behavior is context-dependent rather than universally weak.
- **Scoring inflation** — be honest. A 3/5 is a solid "meets expectations." Reserve 4-5 for genuinely impressive moments.
- **Format mismatch** — don't penalize for lack of pair dynamics in a solo coding round.
