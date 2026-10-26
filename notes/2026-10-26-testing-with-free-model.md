\# Testing PiG with a free model (OpenRouter)



Date: 2026-10-26



\## Setup

\- Provider: OpenRouter, model `poolside/laguna-s-2.1:free`

\- Cost: $0 (checked on the OpenRouter Activity page)

\- PiG runs in Debian; my notes and git are on Windows



\## Two different 429 errors

\- Gemini: `limit: 0` on `gemini-3.1-pro`. The free tier gets no requests

&#x20; on that model, so waiting doesn't help. Fix: `/model` and pick a Flash model.

\- OpenRouter: "temporarily rate-limited upstream". The shared free pool was

&#x20; busy. PiG retried by itself and succeeded.



\## Task 1: write a new script

Asked for a script that counts lines. PiG wrote it, ran its own tests

(trailing newline, no trailing newline, empty file), and I checked it with

`wc -l` and a missing-file run.



\## Task 2: edit existing code

Asked for a --words option. PiG rewrote the whole file and added argparse and

\--help, which I didn't ask for. My check: script gave 61, `wc -w` gave 61.



\## My take

\*\*What worked well\*\*

\- Both tasks were correct. The line counter handled the edge cases, and the

&#x20; word count matched `wc -w` exactly (61 = 61).

\- PiG tests its own work. It wrote the script, ran it on sample files, and

&#x20; fixed nothing by hand, which is the main difference from a normal chat AI.

\- The free model was good enough for small tasks, and it cost $0.

\- The 429 errors from the busy shared pool didn't break anything, because PiG

&#x20; retried and finished the task.



\*\*What I would be careful about\*\*

\- PiG's summary is a claim, not proof. I only trusted the results I checked

&#x20; myself with `wc` and a missing-file run.

\- It rewrote the whole file for a small change and added things I didn't ask

&#x20; for (argparse, --help, directory handling). On a real project I would check

&#x20; `git diff` before accepting the change.

\- Every message I type in PiG, even one that just runs a command, uses a model

&#x20; request. Free limits (about 50 a day) run out faster than I expected, so

&#x20; I run plain commands in a normal shell instead.

\- Free tiers may log prompts, so I only use throwaway code with them.



\*\*Would I use it again?\*\*

Not sure yet. But i know that for anything important I would surely review every change before keeping it.

