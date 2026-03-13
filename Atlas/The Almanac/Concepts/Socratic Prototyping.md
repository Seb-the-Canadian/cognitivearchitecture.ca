---
created: 2026-01-19
last_tended: 2026-02-16
type: note
status: evergreen
tags:
  - tools
  - frameworks
  - concept
  - automation
  - human-ai-collaboration
  - AI
up:
  - "[[Capability Development]]"
aliases:
  - socratic prototyping
related:
  - "[[The Socratic Prototyping Method]]"
  - "[[Hesitation as Data]]"
  - "[[Tool Congruence]]"
---

> [!tldr] Core Concept:
A reflective, question-first approach to working with LLMs, designing workflows, or tools; especially for citizen developers working in constrained environments.

When I first started playing around with LLMs towards the end of 2024, like others I quickly saw the benefit that tools like [[Chat-GPT]] could bring to building out ideas I had, but with skills I didn't. Using LLMs like this has become colloquially known as "vibe coding" and there's whole apps (e.g. Replit, Lovable) dedicated to this. 

A problem I encountered early on was getting mid-way through a build, feeling like I'd gained some real momentum, and then realizing that there was a fundamental error. Maybe not something I'd have necessarily seen outright, but something significant enough to derail where I was headed and require some backtracking. Best case, this would be able to be resolved, but more often LLMs do what they seemingly do best - [[in the absence of clarity, LLMs create complexity.|in the absence of clarity they create complexity.]] 

When I ran in to this problem, I shifted my approach and looked to old solutions for this modern problem which landed me to [Bill and Ted's](https://en.wikipedia.org/wiki/Bill_%26_Ted's_Excellent_Adventure) pal [Socrates](https://en.wikipedia.org/wiki/Socrates). I came up with a quick instruction block to use in my chats and started calling it "Socratic Prototyping". 

I figured out (as many more have) that getting my AI-partner to ask me questions upfront, in the role of developer, project manger, whatever fit the bill, allowed for a better design. I'd ensure this was done one question at a time, with information in each question having some ability to "steer" where the questions that came after it would go or be interpreted. Specifically, once I'd thought I'd come up with enough clarity via this back and forth - I'd ask the LLM to "pre-troubleshoot" based on what we'd come up with. Look around corners, hypothesize about what could go wrong, do a "pre-mortem" - mainly so I didn't have to waste my time untangling the mess that was so easy to create.

After I'd been doing this for some time - I realized it was a good approach to designing automated solutions in general, with or without the assistance of AI, resulting in this note! I've started to sketch out what this looks like as an intentional application [[The Socratic Prototyping Method|here]].

## Definition
---
Socratic Prototyping prioritizes **pre-troubleshooting**, **slow design**, and **tool congruence** over speed or novelty. The core principle: start with questions, not code.

## Core Principles
---
- **Start with Inquiry:** Ask what's really needed; function, behaviour, environment
- **Interrogate Assumptions:** What do I think I know about this system?
- **Pre-Troubleshoot the Build:** Anticipate failure modes before writing code
- **Optimize for Understanding:** Favour solutions you can explain and maintain
- **Design for Feel, Not Just Function:** Prioritize minimal, native-feeling experiences
- **Document While Thinking:** Capture evolving clarity to reduce rework

## Related
---
- [[The Socratic Prototyping Method]]
- [[Hesitation as Data]]
- [[Tool Congruence]]
- [[Capability Development]]