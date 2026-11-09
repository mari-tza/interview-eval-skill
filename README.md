# Interview Transcript Evaluator

A Claude Code skill that evaluates technical interview transcripts and produces structured, evidence-based feedback reports.

Paste your interview transcript, get a detailed evaluation with scores, strengths, improvement areas, rewritten answers, and prioritized action items.

## What It Evaluates

| Dimension | Weight | What it measures |
|-----------|--------|-----------------|
| Communication & Structure | 20% | Structured thinking, STAR usage, conciseness, clarifying questions, thinking out loud |
| Technical Depth | 25% | First principles reasoning, trade-off analysis, scope management, edge cases, system awareness |
| Seniority Signals | 15% | Scope of impact, decision making, ambiguity handling, ownership, business awareness |
| Behavioral & Leadership | 15% | Ownership narrative, failure stories, collaboration evidence, impact framing |
| Collaboration Signals | 10% | Response to hints/pushback, pair dynamics, curiosity |
| Interview Mechanics | 10% | Time management, confidence calibration, energy, closing questions |
| AI Assistance Detection | — | Fluency shifts, timing anomalies, copy-paste artifacts (live interviews only) |
| Cross-Cultural Notes | — | Coaching notes for candidates interviewing across cultural contexts (not scored) |

Weights adjust automatically based on the interview format (pair programming, system design, behavioral, hiring manager, solo coding).

## Output

A markdown report containing:

- **Score summary** with weighted overall score (1-5 visual scale)
- **Strengths** with specific quotes from the transcript as evidence
- **Areas for improvement** with what happened, why it matters, how to fix it, and a rewritten stronger answer
- **Seniority calibration** mapping answers to junior/mid/senior/staff levels
- **Key moments** — 3-5 pivotal points in the interview
- **Red flags & green flags** with evidence
- **Cross-cultural coaching notes** (when applicable)
- **Bias transparency** — self-check against halo effect, recency bias, anchoring, etc.
- **Action items** — prioritized practice list
- **Practice prompts** — tailored questions to rehearse weak areas

## Installation

### Option 1: Clone to your skills directory

```bash
git clone https://github.com/<your-username>/interview-eval-skill.git ~/.claude/skills/interview-eval
```

### Option 2: Copy the file manually

Copy `skill.md` to `~/.claude/skills/interview-eval/skill.md`.

That's it. No dependencies, no config.

## Usage

In Claude Code, either:

```
/interview-eval
```

Then paste your transcript. Or just paste a transcript and ask Claude to evaluate it — the skill triggers automatically.

### Optional context you can provide

| Parameter | Example |
|-----------|---------|
| Interview format | "this was a system design interview" |
| Target level | "I was interviewing for a senior role" |
| Company/culture | "this was for a US-based startup" |
| Mock vs real | "this was a mock with a friend" |
| Role type | "backend engineer position" |

If you don't provide these, the skill infers them from the transcript.

## Examples

**Basic usage:**
> Here's my interview transcript. Can you evaluate it?
> [paste transcript]

**With context:**
> This was a mock system design interview for a senior backend role at a US company. I'm Brazilian and interviewing in English. Please evaluate:
> [paste transcript]

**Quick debrief:**
> I just finished a real interview. Here's what I remember of the conversation — can you evaluate and tell me what to focus on before the next round?
> [paste transcript]

## Design Principles

- **Evidence over vibes.** Every score and recommendation traces back to a specific moment in the transcript.
- **Honest but constructive.** Weak answers are called out — always paired with a concrete path to improvement.
- **Level-calibrated.** A junior and a senior are evaluated against different standards.
- **Culturally aware.** Cross-cultural patterns are flagged as coaching opportunities, not penalized.
- **Bias-conscious.** The evaluator runs a self-check against common cognitive biases and declares any flags in the report.
- **Format-adaptive.** Rubric weights shift based on the interview type — pair programming scores collaboration higher, behavioral rounds emphasize STAR structure.

## License

MIT
