\# Getting started with PiG on Debian



Date: 2026-10-25, Sunday



\## What is PiG?

PiG ("Pi in Go") is an unofficial of Pi (if you already know pi.dev) that is rewritten in Go. 

It is a coding agent that runs in the terminal. You give it a task/prompt, it will read 

and edit the files in your project and run commands. It is made by Michael Kinsy 

and is not an official Pi release. It is still version 0.x, so expect rough edges.



Unofficial Main Repository: https://github.com/MichaelKinsy/PiG 



\## How to Install

&#x20;   curl -fsSL https://pi-in-go.dev/install.sh | sh

&#x20;   pig --version



If `pig: command not found` appears, close and reopen the terminal.



\## First run

\- Run `pig` inside a project folder.

\- Use `/login` to connect an AI provider.

\- Use `/sprite` to change the pig shown in the header (cosmetic only).

\- Use `/model` to switch models.



\## Problem I hit: Gemini free tier returned 429

PiG picked `gemini-3.1-pro` by default, and I got a 429 "quota exceeded"

error with `limit: 0` for that model. `limit: 0` means the free tier gets

zero requests on that model, so waiting does not fix it, even though the

error says "retry in 16 minutes".



Fix: run `/model` and switch to a Flash model.



\## What I learned

\- PiG is indeed free, but the AI model behind it may not be.

\- A provider's default model may not be free, so make sure to check the model name first.

\- Free tiers may log prompts, so I only use throwaway code with them.

\- A coding agent can edit files without asking, so I test in a copy of a

&#x20; project or a Git branch.



\## Next

\- Try OpenRouter with a `:free` model.

\- Give PiG a small task and note what it gets right and wrong.

