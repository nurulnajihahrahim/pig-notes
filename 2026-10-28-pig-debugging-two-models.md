\# Can PiG debug? Testing two models



Date: 2026-10-28



\## What I tested

Two small bugs in throwaway Python scripts, run in Debian with PiG.



1\. \*\*broken.py\*\* crashed with an IndexError. The cause was an off-by-one

&#x20;  error: `range(len(nums) + 1)`.

2\. \*\*wrong.py\*\* had no error, but printed the wrong average (5.0 instead

&#x20;  of 4.0) because of a stray `+ 1` in the formula.



\## Result: broken.py (crash)

PiG changed one line, explained the cause correctly, and ran the script

again to prove the fix.



\## Result: wrong.py (wrong answer, no error)

I gave the same prompt to two models: "wrong.py prints the wrong

average, fix it".



\- All three found the `+ 1`, removed only that line, and ran the script.

&#x20; All three printed 4.0.

\- Model 1 (a `:free` model on OpenRouter) ran `python`, which doesn't exist

&#x20; on Debian, noticed, and re-ran with `python3`. It also hit about seven

&#x20; "rate-limited upstream" 429 errors. PiG retried each time and finished.

\- Model 2 had no errors. Model 2 came from a small AI API provider my

&#x20; supervisor recommended, which is called serverasai.com so I only used it on throwaway code.



\## What I learned

\- The 429 errors came from a busy shared free pool, not from a mistake of

&#x20; mine. They slowed things down but didn't break the result.

\- When PiG says a fix works, I should still run the script myself.

\- A wrong-answer bug is harder than a crash, because there is no error

&#x20; message to follow. Both models still handled it.



\## My take

\- These bugs were easy, so "both passed".

&#x20; It doesn't tell me which model is better. I need a harder bug.

\- Next test: a function that crashes only on an empty list, to see which

&#x20; model handles the edge case and explains its choice.

\- Free models are fine for learning, but I would still read the diff

&#x20; before accepting a change on a real project.

\- I need to explore more on both free and paid models from serverasai.com 

&#x20; and read its docs carefully before using it for real projects.

