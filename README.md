# Engineering Learning

## Why

AI coding agents can increase output faster than they increase human understanding. That can be useful for delivery, but risky when engineers are still acquiring the skills needed to guide, debug, and safely extend the systems those agents produce.

Anthropic's study, [*How AI Impacts Skill Formation*](https://arxiv.org/abs/2601.20245) ([research summary](https://www.anthropic.com/research/AI-assistance-coding-skills)), found that developers using AI assistance scored lower on a subsequent mastery assessment, with the largest gap in debugging. The results also suggested that *how* people used AI mattered: conceptual inquiry, explanations, and independent problem-solving were associated with stronger understanding than full delegation.

Geoffrey Litt's talk, [*Understanding is the new bottleneck*](https://www.geoffreylitt.com/2026/07/02/understanding-is-the-new-bottleneck), makes the complementary practical argument. Engineers need to understand agent-written systems not only to verify them, but to remain capable of participating creatively in what gets built next. Explanations, comprehension checks, and interactive learning environments can keep the agent loop from outrunning human understanding.

The intent of this skill is to create a knowledge acquisition model for real repository work. Its goal is not to make the agent less capable, but to protect the cognitive work that develops the competency you want, while aggressively automating everything else.

## What it does

The skill gives a coding agent two simultaneous objectives: ship the engineering result and increase the developer's independent capability.

It does this by:

- distinguishing **target knowledge** from supporting and incidental work;
- using three per-competency modes: **Explore**, **Apply**, and **Execute**;
- tracking granular competencies as **unknown**, **conceptual**, **developing**, or **strong**;
- automating repository search, boilerplate, fixtures, formatting, and other incidental work;
- preserving predictions, diagnosis, tradeoff decisions, and critical implementation slices for the developer when they support the learning target;
- using transfer checks and short review-time comprehension checks as evidence of durable understanding; and
- providing a **just ship it** escape hatch when delivery urgency outweighs learning.

The knowledge you accrue using this skill makes up a competency model. The cool thing is that this model is global, and can carry over from project to project.

## How to use it

Install or copy this repository into a skill directory recognized by your coding agent. Then invoke the skill explicitly or ask for help learning while completing a real engineering task.

For Codex:

```text
Use $engineering-learning to implement cancellation-safe retries.
I want to strengthen my understanding of async cancellation and retry boundaries.
Please automate incidental repository work.
```

You can also specify the desired balance:

```text
Use $engineering-learning in Explore mode for transaction isolation,
Apply mode for query-plan debugging, and Execute mode for the migration boilerplate.
```

For urgent work:

```text
Use $engineering-learning, but just ship this incident fix.
Give me the short debrief and a recovery exercise afterward.
```

The complete operating rules are in [`SKILL.md`](SKILL.md). The detailed competency schema and repository workflow examples are under [`references/`](references/).

## What needs work
Not all (human) skills you accrue will be relevant between projects. These skills are _local_ to a specific project or domain. Cross project/domain skills are _global_ skills and are, by their nature, more generic. Drawing a distinction between these types of skills is the next task at hand.
