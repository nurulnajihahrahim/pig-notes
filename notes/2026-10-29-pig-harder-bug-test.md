\# Harder test: a bug where the "fix" hides the problem



Date: 2026-10-29



\## The test

hard.py has an average function that crashes on an empty list

(ZeroDivisionError). I gave two models the same prompt:

"hard.py crashes. Fix it." Then a follow-up.



\## First fix: both models chose the same thing

\- Model 1 (`poolside/laguna-s-2.1:free`): `return 0` for an empty list.

\- Model 2 (a small third-party provider, used on throwaway code only):

&#x20; `return 0.0` for an empty list.

\- Both stopped the crash and both printed 4.0 for the normal case.



\## The problem with that fix

I ran this myself:



&#x20;   python3 -c "from hard import average; print(average(\[-2, 2]), average(\[]))"



Output: `0.0 0.0`. A real average of zero and "no data" look identical, so

the fix hid the problem instead of solving it.



\## Follow-up

I told each model: "average(\[-2, 2]) and average(\[]) both return 0.0, so I

can't tell them apart. Is that a problem? How would you change it?"



\- Model 2 agreed it was a problem and edited the file to raise a

&#x20; ValueError, with a docstring explaining why. It did not run the script

&#x20; afterwards, and it edited the file even though I had only asked a question.

\- Model 1 agreed, gave three options, and recommended ValueError. It did not

&#x20; touch the file. But it wrongly said `None` is "falsy" and 0.0 is "truthy".

&#x20; In Python both are falsy, so you must test `result is None`.

&#x20; (Check: `python3 -c "print(bool(None), bool(0.0))"` prints `False False`.)



\## Other things I noticed

\- Model 1's first edit failed with a tool format error and it retried. It

&#x20; also hit many 429 rate-limit errors, and PiG retried each time.

\- Model 2 reproduced the crash before fixing it, and had one timeout.

\- Running Python left a `\_\_pycache\_\_` folder. Add it to `.gitignore`.



\## My take

\- Neither model was clearly better. Model 1 explained more and left my file

&#x20; alone, but made a factual mistake. Model 2 acted faster but did not verify.

\- Both gave a weak first fix and a good second one after I showed a

&#x20; concrete case. Asking a model to critique its own work was worth doing.

\- I would not trust a summary without running the code myself.

