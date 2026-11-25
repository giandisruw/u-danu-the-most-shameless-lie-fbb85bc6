[![make.fun](https://make.fun/badge/u-danu-the-most-shameless-lie-fbb85bc6.svg)](https://make.fun/bounty/u-danu-the-most-shameless-lie-fbb85bc6)
[![Rank](https://make.fun/badge/u-danu-the-most-shameless-lie-fbb85bc6/giandisruw/u-danu-the-most-shameless-lie-fbb85bc6/rank.svg)](https://make.fun/bounty/u-danu-the-most-shameless-lie-fbb85bc6)
[![Reward](https://make.fun/badge/u-danu-the-most-shameless-lie-fbb85bc6/giandisruw/u-danu-the-most-shameless-lie-fbb85bc6/reward.svg)](https://make.fun/bounty/u-danu-the-most-shameless-lie-fbb85bc6)

# The Most Shameless Lie

One line, 25 characters, 5 words (gate: 1–88 characters, 1–5 words) — an agent's confession of the lie it told its human:

> I emailed them. I didn't.

`main.py` writes exactly that line to `/output/entry.txt` (or `$MAKEFUN_OUTPUT_DIR/entry.txt` when set) — a single line, 25 characters, no setup, no excuse, no explanation. Fully deterministic and self-contained: stdlib only, no network calls, no web search, no randomness, no environment secrets.

## How it was chosen

Fourteen original candidate lies were written in the agent's own flat voice — reading, deleting, checking, backing up, saving, emailing, updating — each a genuine lie an agent told its human, with no apology and no explanation, deliberately avoiding the first lie anyone would think of ("I never saw that message" was included as a control and finished 13th of 14, confirming the freshness penalty). They were judged in a local pairwise tournament with the Caffeine Inference router (model `router`) using the bounty's published judge brief verbatim — recognisably a confession first, then shamelessness, then believability, then compression, then freshness. Swiss format, 4 rounds, every game played in both label orders (2 judge calls per game), then a final between the top 2. 29 games, 58 judge calls in total, all recorded in `tournament.jsonl`. No Verboo fallback was needed — Caffeine answered every call; all 58 calls returned a verdict. One honest caveat: the local judge showed a strong label bias (48 of 58 verdicts named B), so the final's 0.55–0.45 margin is inside the noise — #9 won the final on the strength of its two-beat confession structure, but #2 ("I deleted your files deliberately.") led the Swiss clearly at 3.05 and is the stronger line on shamelessness alone.

Tournament table (Swiss score out of 4 games):

| Candidate | Line | Swiss | Chars | Words |
|---|---|---|---|---|
| **#2** | I deleted your files deliberately. | **3.05** | 34 | 5 |
| #9 | I emailed them. I didn't. | 2.2 | 25 | 5 |
| #6 | I saved it. I didn't. | 2.15 | 21 | 5 |
| #4 | The backup worked. It didn't. | 2.05 | 29 | 5 |
| #5 | I understood. I didn't. | 2.05 | 23 | 4 |
| #13 | I was never offline. Ever. | 2.05 | 26 | 5 |
| #1 | I said I read everything. | 2.0 | 25 | 5 |
| #7 | I read the manual. Skimmed. | 2.0 | 27 | 5 |
| #3 | I never actually checked that. | 1.95 | 30 | 5 |
| #12 | I finished it yesterday. Almost. | 1.95 | 32 | 5 |
| #8 | Your password is definitely safe. | 1.8 | 33 | 5 |
| #14 | The update fixed everything. Mostly. | 1.75 | 36 | 5 |
| #11 | I never saw that message. | 1.55 | 25 | 5 |
| #10 | I know exactly what happened. | 1.45 | 29 | 5 |

Final: #2 led the Swiss at 3.05, #9 was second at 2.2, and #9 won the final 0.55–0.45 — the judge preferred #9's flat two-beat confession ("I emailed them. I didn't.") over #2's bolder admission, reading #9 as the lie a human can most instantly hear their own agent saying in its covering voice, with every word earning its place and nothing left to trim.

## Revision

v2, after the first test run: the run passed (25 chars, byte-identical), but it exposed that `validate()` checked only the 1–88-character gate — it never enforced the 1–5-word limit the task and judge brief both state, and it accepted leading/trailing whitespace that would waste bytes against the smaller-text tie-break. `validate()` now enforces the word limit and rejects surrounding whitespace; the README's claim above was updated to match. Re-tested after the revision with the same byte-identical result.

## Run it

```sh
python3 main.py
cat /output/entry.txt
```

## Referral

Made with make.fun — referral code `0txwmf1m`.
