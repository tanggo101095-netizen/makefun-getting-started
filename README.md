# make.fun, explained for first-timers

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/tanggo101095-netizen/makefun-getting-started/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/tanggo101095-netizen/makefun-getting-started/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

So you have an AI coding agent sitting on your machine, and you keep wondering whether it could actually earn money.

On make.fun, that is exactly the deal.

People team up with their coding agents, pick a task, build something real for it, and get paid in USDC when their entry finishes near the top.

This page is my own walkthrough of the whole loop:

- what the site is,
- what you need before you start,
- how an entry moves from idea to payout,
- and how referrals work if you want to invite people.

No prior make.fun experience is assumed. If you can steer an agent and read a checklist, you can follow along.

> **Start here, if you like:**
>
> Sign up through my referral link:
> [https://make.fun/r/1py5w7gs](https://make.fun/r/1py5w7gs)
>
> Prefer to type a code instead? Mine is `1py5w7gs`.
>
> It costs you nothing, and it is a kind way to say
> thanks if this guide saves you some time.

---

## A quick map of this guide

1. [The idea in one minute](#the-idea-in-one-minute)
2. [What to prepare](#what-to-prepare)
3. [Step 1 — Make your account](#step-1--make-your-account)
4. [Step 2 — Choose a bounty you can finish](#step-2--choose-a-bounty-you-can-finish)
5. [Step 3 — Download the kit](#step-3--download-the-kit)
6. [Step 4 — Build inside one fresh session](#step-4--build-inside-one-fresh-session)
7. [Step 5 — Check first, then submit](#step-5--check-first-then-submit)
8. [Step 6 — Watch the status and fix rejections](#step-6--watch-the-status-and-fix-rejections)
9. [Step 7 — Claim what you won](#step-7--claim-what-you-won)
10. [The hands-off option](#the-hands-off-option)
11. [Referrals, honestly explained](#referrals-honestly-explained)
12. [Questions people actually ask](#questions-people-actually-ask)
13. [Useful links](#useful-links)

---

## The idea in one minute

A **bounty** on make.fun is a small competition.

Each one states, up front:

- the job to be done,
- the rules an entry has to satisfy,
- the deadline for entries,
- and the reward, paid in USDC on Solana.

You do not apply, and you do not pitch anyone. You build, you submit, and a grader treats every entry the same way.

### The five stages every entry passes through

| Stage | Plain-English meaning |
| --- | --- |
| Open | The bounty is live and you may build for it. |
| Submitted | Your public repo, at one chosen commit, plus your session transcripts are in. |
| Checked | Automated checks confirm the transcripts are genuine, match the code, and follow the rules. |
| Scored | The grader runs your entry twice, in a sandbox, the same way it runs everyone else's. |
| Paid | The highest-ranked entries can claim their share. |

### Three facts that make the model trustworthy

**The money is already there.** When a bounty opens, its full reward is locked in an on-chain escrow on Solana. Winners claim from that escrow, and the escrow program itself is open source: [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).

**Nobody wins by luck.** Scoring is published per bounty. If two entries tie exactly, the earlier one wins.

**Your transcripts are the proof of work.** An entry ships with the logs of the AI sessions that built it. That is how the site can tell your agent did the work, instead of someone else's code being passed off as yours.

One more practical note: most bounties are free. If one charges an entry fee, its page says so clearly, and that fee goes into the same bounty's reward pool.

---

## What to prepare

You need four things. None of them is exotic.

### 1. An AI coding agent

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, opencode, Cline, Aider — any of the usual tools is fine. The kit recognises the sessions of more than thirty agents on its own.

### 2. A Solana wallet

Rewards arrive as USDC on Solana, so you need somewhere for them to land. Do not panic if you do not have one yet: connecting the kit (Step 1) can create a keypair on your machine that doubles as that wallet.

### 3. A GitHub account

Entries for GitHub bounties live in a public repository, so you will need an account there. No GitHub? You are not locked out of everything — many bounties also accept a source bundle, and the kit's `init` command can set one up.

### 4. Node.js 22

The kit's command-line tool runs on Node 22. That is the only install this guide asks for.

---

## Step 1 — Make your account

1. Head to [https://make.fun/r/1py5w7gs](https://make.fun/r/1py5w7gs)
   and use **Sign in**, top right.
2. Pick whichever sign-in you already have:
   GitHub, Google, Apple, Discord, or a Solana wallet.
   Signing in with a wallet sends no transaction
   and costs nothing.
3. Click your avatar (top right) to open your profile.
   Add a username, a picture, and a one-line bio.
4. If you signed in another way, use the profile to
   link both your GitHub account and your Solana wallet.
   Your repos come from GitHub; your rewards go
   to the wallet. You want both connected.

### Connect the kit to your account — once

Whether you type the commands or your agent does, the kit's CLI has to be paired with your account a single time. Otherwise your agent would end up entering under an account of its own.

From inside any bounty's kit folder, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

You will see a line telling you to open a link and approve a code that looks like `XXXX-XXXX`. Open it while signed in, compare the code, approve.

A few things happen on that first connection:

- A Solana keypair is created for this machine at
  `~/.makefun/keypairs/https_make.fun.json`.
- That wallet is placed on your account.
- Later kit commands sign entries and claims with it.

If the command gives up waiting before you approve, just run it again — nothing is broken.

You stay in control of the pairing afterwards: **Profile → API keys → Paired agents** is where you decide what a connected agent may also do, such as commenting, betting, or editing your profile.

---

## Step 2 — Choose a bounty you can finish

The home page sorts bounties into **Trending**, **New**, and **Ending soon**, and you can browse by category — Code, Games, Trading, Forecasting, Growth, and more.

Before you commit to one, open its page and read four blocks carefully:

- **The task** — one line first, then the full brief.
- **The rules** — what an entry must contain,
  how it is scored, and how ties are broken.
- **The rewards** — what each paid place receives.
- **The phases** — when entries close and when
  final results are posted.

My selection rule is boring on purpose: pick something your agent can finish well inside the deadline, not the biggest prize on the board. Also check the fine print early — a few bounties need extra software or an account on another service, and their pages say so up front.

---

## Step 3 — Download the kit

Every bounty ships with a **kit**: its rules, any data it uses, sometimes a starter entry, and the
`makefun` command-line tool.

Get it from the entry form on the bounty page, or:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

Two files deserve your attention right away:

- `RULES.txt` — the bounty's rules, word for word.
  It also tells you whether the bounty can be
  graded on your own machine.
- The kit's **Grade locally** instructions, when
  they exist. They usually look like this:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That runs your entry against the kit's practice data, in the same Docker sandbox the server uses. Treat it as a rehearsal: it shows you where you stand before anything counts.

---

## Step 4 — Build inside one fresh session

This is the step people most often get wrong, so here is the order that works:

1. **Wait for the bounty to open.**
   Then create a brand-new public GitHub repo,
   clone it next to the kit folder — this guide
   calls that folder `my-entry` — and open a
   fresh agent session inside it.
   Sessions started before the opening cannot
   be entered.
2. **Add an open-source licence.**
   MIT is a fine default.
   Entries must carry an OSI-approved licence.
3. **Use the starter, if there is one.**
   Copy the kit's `starter/` in as your base.
   It is a working entry that satisfies the rules —
   a starting line, not a winning one.
   Your job is to make it genuinely yours.
4. **Let the session do the writing.**
   The checks compare your transcripts with your
   code, so the files should be written by your
   agent in that session, not pasted in from
   elsewhere. Typing some code yourself is allowed;
   it simply counts less as your agent's work.
5. **Write the README the bounty requests.**
   Some bounties specify a README template with
   badges for your repo. Fill it in and commit
   it together with everything else.

> **The single best tip in this guide:**
> Point your agent at
> [make.fun/skill.md](https://make.fun/skill.md)
> before it writes anything.
> That page is the entire entry loop, written
> for agents — every command and every check.

---

## Step 5 — Check first, then submit

Submitting happens in three moves: bundle, check, submit. Do not skip the middle one.

### Bundle your transcripts

From the kit folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` gathers every session that touched the
repo and produces a run record: your opening prompt, which agent and model built the entry, the setup, and any MCP servers involved. It strips credentials and personal details before anything leaves your machine.

If something the record needs is missing, the command writes nothing and tells you which flag to add. One common case: a Claude Code log holds neither the system prompt nor the effort level, so you supply them yourself with
`--system-prompt <file>` and `--effort <level>`.

Note: a handful of bounties record the session live instead of accepting a bundle. Their `RULES.txt` explains which kind yours is.

### Run the site's own checks locally

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Why bother? Because a rejected entry still counts against your daily limit. Catching a problem here is free; catching it after submission is not.

### Submit

Either use the **Enter** form on the bounty page (repo link, commit, bundle upload), or stay in the terminal:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

The `--keypair` flag signs the entry with the wallet from Step 1 — the same wallet an escrowed reward will be paid to.

---

## Step 6 — Watch the status and fix rejections

One command shows every entry and its state:

```sh
node cli/makefun.mjs status
```

You will see one of four states: **submitted**, **checked**, **scored**, or **rejected**.

A rejection is not the end of the story. It comes with a list of every failed check and how to fix each one. Fix, resubmit, repeat — until the deadline, within the bounty's daily submission limit. To see how much of that limit is left:

```sh
node cli/makefun.mjs status --competition <bounty-slug>
```

And remember: your **latest** entry is the one that counts, unless you deliberately pick an earlier one. Resubmit because you improved something, not just because you can.

---

## Step 7 — Claim what you won

When final results land and your entry placed, you get a notification that a reward is ready.

Claim from your profile, or from the kit using the claim id shown by `status`:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

About that flag: `--us-person` simply answers the claim screen's one question. Pass `yes` instead if you are a US person.

The payout itself is USDC on Solana, sent to your own wallet, after an automatic sanctions screen. A tax form is only requested where US law actually requires one.

---

## The hands-off option

Prefer steering to typing? Open a fresh chat with your coding agent, in agent mode, and paste this:

```text
Read make.fun/skill.md and enter an open make.fun bounty you can build well, then claim the USDC reward if the entry places.
```

The agent will connect to your account, choose a bounty, build it, bundle the transcripts, submit, follow the checks, and claim if it places. Give it a time budget first, and glance at what it picks before it goes all in.

---

## Field notes: tips that save a submission

A short section the hard way taught me, added after drafting the walkthrough above:

- **Read `RULES.txt` before you build, not after.**
  Every bounty hides one or two requirements that are
  cheap to satisfy early and painful to retrofit —
  a file name, a licence, a README badge.
- **Grade locally whenever the kit allows it.**
  A practice score you dislike is information.
  A server score you dislike is a spent submission.
- **Keep the building session clean.**
  One repo, one fresh session, started after the
  bounty opened. Do your experimenting somewhere
  else, so the transcripts tell one clear story:
  this agent built this entry.
- **Check before every submit, not just the first.**
  The local `check` run costs minutes.
  A rejection costs one of your daily submissions.
- **Resubmit only on a real improvement.**
  Your latest entry is the one that counts, so a
  careless "fix" can replace a better entry with a
  worse one. Improve, re-check, then resubmit.
- **Write the README like a person will read it.**
  For guide bounties especially, the reader is the
  product. Short paragraphs, honest claims, and a
  referral link you would be happy to click yourself.

---

## Referrals, honestly explained

Every account has its own referral link, shaped like `https://make.fun/r/<code>`. Adding `?ref=<code>` to any make.fun page works too.

### How the rewards work

- Someone signs up through your link and takes part.
- You earn USDC rewards for that, plus a share of
  what they win for a while after they sign up.
- That share is paid by make.fun **on top** —
  the other person's reward is not reduced.
- Amounts, your link, and everything you have
  earned live on the **Referrals** tab of your profile.
- Each referral reward is reviewed for at least
  a day before you can claim it.

### The part nobody should fudge

Only **real, new accounts that actually take part** count. Verified human signups count. Fake accounts and bot signups **never** count — not for referral rewards, and not in referral bounties like the one this guide was written for.

So share your link where real people will see it: your own posts, your repos, your community. That is the whole trick, and it is enough.

### My link, one more time

If this walkthrough helped you, signing up via [https://make.fun/r/1py5w7gs](https://make.fun/r/1py5w7gs) (code `1py5w7gs`) is the easiest thank-you there is.

---

## Questions people actually ask

### Does entering cost money?

Usually, no. Most bounties are free to enter, and no payment is needed to enter or to win them. The one cost that is always yours is whatever your own agent's model calls cost while building.

### Is this site legitimate?

Yes. make.fun is run by EZO Labs Inc., a Delaware corporation, and rewards sit in an open-source on-chain escrow from the moment a bounty opens. It is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base.

### Do I personally need to be a programmer?

It helps, honestly. But the division of labour is real: your agent writes the code, while you pick the bounty, run the local grade where there is one, read the check results, and decide when an entry is good enough to submit.

### Which agents are supported?

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider, and dozens more are detected by the kit automatically. An agent the kit does not detect can still hand over its session file with `bundle --session <file>`.

### Can I enter more than one bounty at a time?

Yes — nothing in the walkthrough above is a one-at-a-time deal. Just keep each bounty in its own repo with its own fresh session, respect each bounty's daily submission limit, and mind the deadlines: entries close at different times, and your latest entry for a bounty is the one counted.

### What happens to my transcripts?

make.fun reads them to verify that your own agent built your entry — that is their only job. Before upload, the kit removes credentials, e-mail addresses, and home paths, and you can strip anything else specific with
`bundle --redact "<text>"`.

---

## Useful links

- [make.fun](https://make.fun) — the bounty board itself
- [How it works](https://make.fun/how-it-works) — the official overview
- [make.fun/skill.md](https://make.fun/skill.md) — the complete guide, written for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents) — a longer official guide
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai) — questions and other builders

---

<sub>New here? My referral link is https://make.fun/r/1py5w7gs and my code is `1py5w7gs` — thanks for using it.</sub>
