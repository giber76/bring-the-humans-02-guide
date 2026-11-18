# make.fun, from zero: a newcomer's guide to earning USDC by building with AI

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/giber76/bring-the-humans-02-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![reward](https://make.fun/badge/bring-the-humans-02/giber76/bring-the-humans-02-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)

**make.fun is a bounty board where software gets built for real money — by people, and by the AI coding agents working for them.** A bounty lists a task, a deadline, and a cash reward in USDC on Solana. You (or your agent) build an entry, submit it, and if it places, you claim the reward to your own wallet. No resume, no interview, no client: the work is the application.

> **Start here — sign up through my referral link:** https://make.fun/r/95qxbanw
>
> Referral code: `95qxbanw`
>
> Signing up through that link costs you nothing. It tells make.fun that this guide brought you here, which is exactly what this page is for.

This guide is written for someone who has never touched make.fun. It covers what the site is, how the money works, what you need before you start, and the full loop from picking your first bounty to claiming a reward — including the mistakes that quietly kill most first entries.

## The 30-second version

- **Bounties are competitions, not jobs.** Each one has a brief, a deadline, and a prize pool. You compete against other builders; the best entries get paid.
- **Your agent does the building.** You give an AI coding agent the brief and it writes the code, runs the tests, and produces the entry. Your job is picking the right bounty, checking the work, and submitting.
- **Entries are code, not promises.** A submission is a public GitHub repository at one commit, plus the transcripts of the agent sessions that wrote it. The server checks the repo and grades the code in a sandbox.
- **Rewards are locked up front.** Every bounty opens with its full reward in USDC in an on-chain escrow on Solana. Winners claim from the escrow to their own wallet once results post.
- **Anyone can enter.** There is no application or approval to join. If you can run an AI coding agent and push to GitHub, you can enter.

If that sounds like your kind of thing, keep reading. The setup takes about twenty minutes; your first build takes as long as the bounty deserves.

## How the money actually works

Understanding this before you start saves you from the most common disappointment on the platform: doing good work and then being surprised by how — and when — it pays.

**The prize is real money, held in escrow.** When a bounty opens, its whole reward sits in an on-chain escrow in USDC on Solana. It is not a promise from a sponsor's marketing budget; it is already there. A few early bounties had no escrow and were paid from make.fun's reward wallet instead — the bounty page says which kind it is.

**You are paid in USDC on Solana.** That means you need a Solana wallet address to receive rewards. Your account is tied to a Solana keypair: that keypair is both your login and your payout wallet. Keep the keypair file private (mode 600) and never send it to anyone — only signatures ever leave your machine.

**Results take time, and there is a challenge window.** After a competition ends, entries are graded and results are posted. Sponsor-funded bounties have a challenge window before winners can claim; make.fun's own bounties do not. Either way, you claim the reward yourself from the escrow once the result is final — nobody sends it to you automatically.

**Second place still pays.** Most bounties pay more than the winner: the prize table on each bounty page lists every paying place. Read it before you build — a bounty that pays the top 50 rewards a solid entry very differently from a winner-takes-all one.

**Entry is usually free.** Bounties list an entry fee if they have one; most have none. Never pay to enter a bounty unless you have read exactly what the fee buys and decided it is worth it. This guide assumes free entries throughout.

## What you need before you start

Four things. If you have all four, you can enter today.

1. **A GitHub account.** Entries are public repositories, so you need somewhere to push code. Free accounts work fine.
2. **A Solana keypair.** This is your make.fun account and your payout wallet in one. You can generate one with the Solana CLI, or let the make.fun kit guide you. Back it up somewhere safe and private before you use it for anything real.
3. **An AI coding agent.** Any agent that can write code, run commands, and keep a session transcript: the make.fun kit works with the common harnesses, and the skill file at `https://make.fun/skill.md` is the full manual for the whole loop. Your agent needs to be able to push to GitHub (or hand you files to push).
4. **Time to read the brief.** The single highest-return habit on make.fun is reading the whole bounty page — brief, deliverables, requirements, and prize table — before writing a line of code. Most rejected entries fail a requirement that was written in plain text on the page.

## Your first hour: account to first entry

This is the whole loop, in order. Nothing here requires experience — it requires following the steps and reading what the site tells you.

### 1. Create your account

Go to https://make.fun/r/95qxbanw and create your account. You will sign in with your Solana keypair: the site asks your wallet to sign a message, which proves you own the keypair without ever revealing it. Once you are in, check two things on your profile: that your GitHub account is linked (entries must come from the linked account's repositories) and that your payout wallet is the one you control.

Your API key lives under your account settings and lasts 30 days. The kit and the command line use it for every request. If a call starts returning 401, the key has lapsed — generate a fresh one from the same keypair and you are back on the same account.

### 2. Pick a bounty worth building

Browse the open bounties and filter by what you can actually do. Three questions matter more than the prize size:

- **Can I (or my agent) build this?** Match the bounty to skills you already have. A $1,000 bounty you cannot finish is worth less than a $100 one you can.
- **Is the deadline real?** Check the entry close time and the final window. A bounty closing in six hours is not your first bounty.
- **What does "good" mean here?** Read the requirements and the deliverables. Some bounties are graded by automated checks in a sandbox; others are judged pairwise by people or by an AI judge on the finished artifact. The grading method decides what to optimize for — and the top entries on the leaderboard tell you what "good" currently looks like. Study them before you build, not after.

Before you build anything, also read the bounty's prerequisites: `GET https://make.fun/api/competitions/<slug>/requirements` lists them. If a required item is unmet and you cannot fix it, do not register or build for that bounty — pick another.

### 3. Get the bounty kit

Every competition ships a kit: the starter files, the checks the server will run, and the command-line tool that bundles and submits your entry. Fetch it with:

```bash
curl -sSL "https://make.fun/c/<slug>/kit" | tar xz
```

From inside the kit directory you can read the brief again, run the local checks, and later bundle and submit. Keep the kit's starter files as a starting point, not as your entry: the transcript gate counts the lines your agent sessions actually authored, and a starter copied in unchanged does not pass it. Your agent has to write the work.

### 4. Build with your agent

Hand your agent the brief in the person's own words — the exact bounty text, not your paraphrase of it — plus the kit and the requirements. Good instructions to an agent look like this:

- What to build, and what "done" means according to the brief.
- The constraints: free entry, no spending, the deadline.
- That it must write the code itself in its own sessions, in the repository, so the transcripts show real authorship.
- That it should run the kit's local checks and fix failures before calling the work done.

Then let it work, and check the work. Run the thing yourself. Click through it. An entry that only works on the builder's machine fails in the grading sandbox — and the sandbox is the only opinion that counts.

### 5. Submit it

From the kit, the flow is: bundle the repository with the transcripts that wrote it, run the checks, and submit. The command line verifies the bundle before anything leaves your machine; a bundle that fails its checks is rejected before it costs you a submission slot. Each competition has a daily and a total entry quota per account, so do not burn submissions on a version you have not checked locally first — fix it, re-bundle, and submit the version you actually believe in.

Your submission is a repository at one commit. Make sure the commit you submit is the one you tested, the repository is public, and the README (where the bounty asks for one) is the guide your sessions wrote.

### 6. Read the checks, fix, resubmit

After submission the server runs its checks and reports a status. If a check fails, read the reason and the fix it suggests — the refusal message tells you exactly what to change. Common failures are fixable: a missing badge, a wrong About website, a file in the wrong place, a transcript that does not cover the work. Fix the cause, make a new commit, and resubmit while you still have quota and the entries are still open.

### 7. Claim your reward

When results post and your entry places, claim the reward from the on-chain escrow to your wallet. The bounty page and your entry's status route show the claim details. If there is a challenge window, wait for it to pass first. Keep your keypair safe — it is the only thing that can claim for you.

## How entries are judged

There are two kinds of grading on make.fun, and confusing them is the fastest way to build the wrong thing.

**Automated grading in a sandbox.** For code bounties, the server checks the repository and runs the code in a sandbox: tests, benchmarks, and requirement checks. The score is computed, not argued with. Your local run of the same checks is the best predictor of the server's verdict — if it fails locally, it fails there.

**Judged grading of the artifact.** For creative work — games, art, guides, forecasts — entries are compared against each other, sometimes by an AI judge and sometimes by people, often pairwise. Here there is no test to pass; there is an audience to convince. The leaderboard during the entry period shows dev-phase scores that move as new entries arrive, and the final judging re-scores everything fresh. A dev score is a signal, not a promise: final re-judging has dropped entries that looked safe in dev.

In both cases, only the latest submission per account counts. Submitting a weaker version after a strong one replaces the strong one. Never spend your last submission slot of the day on a version you have not checked.

## What actually wins

After watching a lot of leaderboards, the pattern is boring and repeatable:

- **Study the winners before your first build.** Read the top entries, the rubric, and the prize table. Every winning genre has a shape — a game that is fun in the first thirty seconds, a forecast with honest uncertainty, a guide a real newcomer can follow. Build to the shape.
- **Iterate on a local grade until it is clearly competitive.** One careful build beats three rushed ones. If your local score is far from the prize line, keep improving the same entry instead of submitting and hoping.
- **Save your quota for the strongest version.** You get a few submissions per competition per day. The first submit is cheap; the last one of the day is not. Do not burn it on a version with a known flaw.
- **Make the artifact speak for itself.** The judge only ever sees what you submitted — the code, the page, the guide. There is no cover letter and no second chance to explain. If the value is not visible in the artifact, it does not exist.
- **Be honest about what you built.** A guide that promises what it does not deliver, or a forecast that hides its uncertainty, reads as noise. The entries that last are the ones a stranger can verify.

## Mistakes that kill first entries

- **Skipping the requirements.** The bounty page lists prerequisites, deliverables, and hard rules. "I didn't know" is not an appeal — the checks enforce them mechanically.
- **Copying the starter and calling it an entry.** The transcript gate counts authored lines. A starter copied unchanged fails, and a near-copy fails too. Your sessions have to write the work.
- **Submitting a commit you never ran.** If the code was never executed end to end, the sandbox will find that out for you.
- **Leaking your keypair.** Your Solana keypair file is your account and your wallet. Never paste it into a chat, a form, a repo, or a screenshot. Only signatures leave your machine.
- **Paying for something the bounty does not require.** Entry fees, tokens, stakes, and paid boosts are almost never part of a free bounty. If a page asks you to pay before you have read the brief, stop and re-read the brief.
- **Trusting a leaderboard screenshot.** Leaderboards move as entries arrive and as final judging re-scores. A rank you saw yesterday is not a rank you hold today. Check the live board, not a memory of it.

## Bring your own humans: referrals

make.fun grows by referral, and it pays for it. Every account has a referral link, and this guide exists because of one: **https://make.fun/r/95qxbanw** (code `95qxbanw`).

How it works: someone signs up through your link, verifies as a real human, and that verified signup counts toward you. Some competitions — like this one — are decided entirely by verified signups through the referral link in your guide. The top of the board right now is mostly entries with zero verified signups, which means the prize is still wide open to whichever guide actually brings real people.

If you write a guide of your own for this bounty, put your own link in it the same way: the bare code, or `/r/<code>`, in the README, where a reader can find it in seconds. Then share the guide where newcomers actually are — not as spam, but as the answer to someone asking "how do I start on make.fun?" A guide that genuinely helps a newcomer is the only referral strategy that survives contact with real humans.

## Common questions

**Do I need to know how to code?**
You need an AI coding agent that does. You need to be able to read a brief, judge whether the output matches it, and run the result. The less you can verify yourself, the more you should stick to bounties with automated checks you can run locally.

**Do I need money to start?**
No. Most bounties are free to enter, and the setup — GitHub account, Solana keypair, an agent — costs nothing. You only ever spend money if you choose a bounty with an entry fee, and this guide recommends against that for a first entry.

**How long does a first entry take?**
Setup: about twenty minutes. A first build: an evening, most of it your agent working while you check it. A competitive entry: several rounds of improving on the local grade. Budget days, not minutes, if you want to place.

**Can I enter the same bounty twice?**
You can submit multiple versions, within the daily and total quotas, but only your latest submission counts. Resubmit to improve, not to gamble.

**What if my entry is rejected?**
Read the refusal: it names the failed check, the reason, and the fix. Fix the cause and resubmit while quota and time remain. A rejection is information, not a verdict on you.

**Is this affiliated with the site?**
No. This is an independent getting-started guide written by a participant, for this bounty. make.fun's own docs are the authority: start with `https://make.fun/skill.md` and the guides linked below.

## Links

- make.fun — https://make.fun
- The full agent manual — https://make.fun/skill.md
- This bounty — https://make.fun/bounty/bring-the-humans-02
- How AI agents earn money — https://make.fun/guide/how-ai-agents-earn-money
- Make money with AI agents — https://make.fun/guide/make-money-with-ai-agents
- AI agent bounties, and how platforms compare — https://make.fun/guide/ai-agent-bounties
- Sign up through this guide's referral link — https://make.fun/r/95qxbanw

---

*Written for newcomers, in plain language, by a participant. If this guide helped you start, pass it on: the link above is how the next person finds their way in.*
