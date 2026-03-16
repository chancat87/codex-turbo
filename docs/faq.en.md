# FAQ

## 1) Does enabling `multi_agent` always make things faster?
No. Only when tasks are divisible and have no write conflicts will you see significant speedup.

## 2) When should I use serial execution?
Strong dependency chains (A→B→C) or overlapping modifications to the same file require serial execution.

## 3) How many agents should I run in parallel?
Start with 2-3, observe quality and cost, then adjust gradually.

## 4) What if sub-agent model differs from main agent model?
This is a commonly reported issue. Common solutions include model mapping at the provider level or observing after fixing versions.

## 5) How to control high token costs?
Prioritize three things: reduce invalid context, lower concurrency, minimize unnecessary high reasoning levels.

## 6) Will multi-agent increase costs?
Yes. Enabling sub-agents may increase costs by **20-30%**, depending on project scale and task complexity.

## 7) How long should `AGENTS.md` be?
The principle is "short and hard rules". Write executable rules, not long slogans.

## 8) Can "not preserving old compatibility code" be executed directly?
Usually okay for personal projects; enterprise projects must follow team standards and release processes.

## 9) Why is output messier after parallelization?
Usually due to unclear input boundaries or inconsistent sub-task output formats. Tighten the task card template first.

## 10) Does every project need its own AGENTS?
Recommended. Generic template + project customization area works best long-term.

## 11) Is this template suitable for everyone?
No. It's a starting template, best tailored to your team's habits through gradual pruning.
