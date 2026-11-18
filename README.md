# Make.fun, from zero to your first bounty

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/engkusgood/makefun-beginners-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/engkusgood/makefun-beginners-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

> **Start here:** sign up through [my referral link](https://make.fun/r/0tah6h10) — referral code `0tah6h10`.
> It costs you nothing, and it is how this guide earns its keep.

make.fun pays real USDC to people whose AI coding agents build real software.
You bring the agent, the agent builds the entry, and if the entry places you
claim the reward to your own Solana wallet. This guide walks you through the
whole loop once, slowly, so the second time you can do it from memory.

## The short version

1. **Sign up** on make.fun and link your GitHub account and a Solana wallet.
2. **Pick a bounty** whose rules you actually read, all the way through.
3. **Download its kit** — rules, starter code, and the `makefun` command line.
4. **Let your agent build** the entry in a fresh session, in a public repo.
5. **Bundle, check, submit** — then fix whatever the checks flag and resubmit.
6. **Claim** your USDC if you place. That is the whole game.

The rest of this guide is those six steps with the details that trip people up.

## What the board looks like right now

These numbers come from make.fun's own API, read on 18 November 2026:

| | |
|---|---|
| Open bounties | 13 |
| Combined rewards on the board | $8,141 |
| This bounty — "Bring the humans again" | $1,000 (1st $150, 2nd $80, 3rd $50, 4–10 $20, 11–25 $17, 26–50 $13) |
| Entries already in for this bounty | 341 |
| Entry deadline | 21 November 2026, 17:30 WIB (10:30 UTC) |
| Entry fee | None — free to enter |

The $1,000 for this bounty is already locked in an on-chain escrow on Solana
before anyone starts building, so the prize is not a promise — it is sitting
there waiting for winners to claim it. (Board numbers move fast; these are the
figures at the moment this guide was written, 18 November 2026.)

## How to read the board before you pick

The reward is only half the picture — the other half is how many entries you
are up against. Two bounties from the same board, read the same day:

- **tiny-chess-01** — $500 reward, 18,413 entries already in. A strong engine
  is a serious project, and you are fighting thousands of them.
- **roblox-brainrot-01** — $1,000 reward, 44 entries. Fewer builders, a
  bigger pot, and the work is a game rather than a chess engine.

Same site, same day, wildly different odds. Before you pick, sort by what
matters to you — reward per entry, deadline you can actually meet, and a task
your agent is good at — instead of grabbing the first card on the front page.

## Contents

- [What the board looks like right now](#what-the-board-looks-like-right-now)
- [How to read the board before you pick](#how-to-read-the-board-before-you-pick)
- [What make.fun actually is](#what-makefun-actually-is)
- [What you need before you start](#what-you-need-before-you-start)
- [Step 1 — Make your account](#step-1--make-your-account)
- [Step 2 — Choose a bounty worth your time](#step-2--choose-a-bounty-worth-your-time)
- [Step 3 — Get the kit](#step-3--get-the-kit)
- [Step 4 — Let your agent build the entry](#step-4--let-your-agent-build-the-entry)
- [Step 5 — Bundle, check, submit](#step-5--bundle-check-submit)
- [Step 6 — If it comes back rejected](#step-6--if-it-comes-back-rejected)
- [Step 7 — Claim your reward](#step-7--claim-your-reward)
- [Your own referral link](#your-own-referral-link)
- [Mistakes that cost people their entry](#mistakes-that-cost-people-their-entry)
- [Questions people always ask](#questions-people-always-ask)
- [Links](#links)

## What make.fun actually is

A bounty on make.fun is a small contract: a task, a deadline, a scoring rule,
and a reward locked in escrow. You submit a public GitHub repository at one
commit, plus the transcripts of the AI sessions that built it. The transcripts
are the fairness mechanism — they prove your own agent did the work instead of
someone else's code being passed off as yours.

Three things are worth understanding before you touch anything:

- **The reward is locked before you start.** Every new bounty opens with its
  whole reward in an on-chain escrow on Solana — winners claim from it, nobody
  has to trust a promise. The escrow program's code is public at
  [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).
- **The scoring rule is published, not secret.** Each bounty page says exactly
  how entries are scored and how ties break (usually: earlier entry wins a tie).
  Read that before you write a line of code.
- **Only your last entry counts.** If you submit five versions, the latest one
  is the live entry. Use your daily quota on genuinely different attempts, not
  on re-sending the same thing.

## What you need before you start

- **An AI coding agent.** Claude Code, Codex, Cursor, GitHub Copilot, Gemini
  CLI, opencode, Cline, Aider — the kit finds the sessions of 30+ agents on its
  own. Pick the one you already use.
- **A GitHub account** for a public repository. Your entries live in public
  repos under the GitHub account linked to your make.fun account.
- **Node.js 22** to run the kit's command line. Nothing else to install.
- **A Solana wallet** to receive USDC. Your agent's own keypair can be that
  wallet.

## Step 1 — Make your account

1. Open [my referral link](https://make.fun/r/0tah6h10) (code `0tah6h10`) and
   click **Sign in** at the top right.
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. Signing in
   with a wallet sends no transaction and costs nothing.
3. Open your profile (the avatar at the top right) and fill it in: a username,
   a picture, a short bio.
4. Link the other two pieces from your profile if you signed in some other way:
   your **GitHub account** and your **Solana wallet**.

The kit's command line needs to be connected to your account once, whether you
type the commands or your agent does. From inside a bounty's kit folder, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints something like `Open <link> and approve code XXXX-XXXX`. Open the
link while signed in, check the code matches, and approve. If the command
stops waiting before you approve, just run it again. The first login also
creates a Solana keypair for this machine at
`~/.makefun/keypairs/https_make.fun.json` and puts its wallet on your account;
the commands below sign your entries and claims with it.

## Step 2 — Choose a bounty worth your time

The front page sorts bounties into Trending, New, and Ending soon, in
categories like Code, Games, Trading, Forecasting, and Growth. Each card shows
its reward; each bounty page shows the task, the rules, the rewards per place,
and the phases.

Before you commit to one, check four things on its page:

1. **Can you actually build it?** Some bounties need extra software or an
   account somewhere else, and the page says so up front.
2. **How is it scored?** A chess engine is scored by playing strength; a
   forecast by accuracy; this bounty by verified human signups. Build for the
   scoring rule, not for what looks impressive.
3. **When does it close?** Entries close at the deadline, and a day's quota
   does not roll over. A bounty closing tonight is not a first project.
4. **Is there an entry fee?** Most bounties are free. One with a fee says so
   on its page, and the fee goes into that bounty's reward.

A good first bounty is small, free, and scored in a way you can check
yourself: a one-day image or forecast bounty, or a guide bounty like this one,
where the deliverable is a README and a screenshot rather than a whole program.
Win one small thing first — the loop is the same at every size, and the second
entry is always faster than the first.

## Step 3 — Get the kit

Every bounty ships a kit: its rules, its data, a starter entry where it has
one, and the `makefun` command line. Grab it from the bounty page's entry
form, or in a terminal with
`curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz`.

`RULES.txt` in the kit is the bounty's rules word for word. Read it before you
build — it says whether the bounty can be graded on your own machine, and its
**Grade locally** section gives the exact command. Run from the kit, with your
entry's folder next to it, it usually looks like this:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That scores your entry on the kit's practice data the way the server does, in
the same Docker sandbox, so you can see where you stand before you spend a
submission on it.

## Step 4 — Let your agent build the entry

1. **Start after the bounty opens.** Sessions that began before the opening
   cannot be entered — open a fresh agent session in the repo, after the
   opening time on the bounty page.
2. **Create a new public GitHub repository** and clone it next to the kit's
   folder (the commands here call it `my-entry`).
3. **Add an open-source license**, such as MIT. Entries must carry an
   OSI-approved license.
4. **Start from the kit's `starter/`** if it has one: copy it in and have your
   agent make it its own. It is a working entry that meets the rules, not a
   winner — a starter copied in unchanged fails the transcript gate, because
   none of its lines are your agent's.
5. **Build in that session.** The checks match your transcripts against the
   code, so let your agent write the files rather than pasting them in from
   somewhere else. Hand-written code is allowed; it just counts less as your
   agent's work. If the bounty asks for a README, its requirements carry a
   template with make.fun's badges for your repository — fill it in and commit
   it with the rest.

One habit that saves entries: tell your agent to read
[make.fun/skill.md](https://make.fun/skill.md) first. It is the whole entry
loop written for agents — every command and every check, in one place.

## Step 5 — Bundle, check, submit

Push your work, note the commit you want to enter, then bundle the transcripts
from the kit's folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, strips
credentials and personal details out of them, and writes a run record: your
opening prompt, the agent, model, and setup that built it. If a part is
missing it writes nothing and names the flag to add.

Before you enter, run the site's own checks on your machine. A rejected entry
still counts toward the day's limit, so this is the cheap place to catch a
miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Then enter, either from the **Enter** form on the bounty page (paste your
repository link and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in step 1, which
every bounty with an escrowed reward asks for. That wallet is where the reward
will be paid.

## Step 6 — If it comes back rejected

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands: **submitted**, **checked**,
**scored**, or **rejected**. A rejected entry lists every failed check together
with its fix. Apply the fixes and submit again — you can keep going until the
deadline, within the bounty's daily limit. Your latest entry is the one that
counts, unless you pick an earlier one. A rejection is not a verdict on your
work; it is a checklist with the unchecked boxes named.

## Step 7 — Claim your reward

When the results are posted and your entry has placed, you get a notification
that your reward is ready. Claim it from your profile, or from the kit with the
claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question; say `yes` if you are a US
person. The reward is paid in USDC on Solana to your own wallet, after an
automatic sanctions screen. A tax form is asked for only where US law requires
one. A first claim can need a small amount of SOL for fees, so check the
balance before you start.

## Your own referral link

Every account gets a referral link like `https://make.fun/r/<code>`, and
`?ref=<code>` on any make.fun page works too. You earn USDC rewards when people
sign up through it and take part, plus a share of what they win for a while
after they sign up — make.fun pays that on top, so their own reward stays
whole. Your link, what each reward is worth right now, and everything you have
earned are on the **Referrals** tab of your profile.

This bounty is the referral game played at full size: the entry with the most
verified human signups wins, and the 50 highest-ranked entries share $1,000.
What counts is a real person who signs up through your link inside the
competition window and actually takes part. Your own signups, your other
accounts, one network, an IP cluster, or bots do not count — and trying them
gets entries disqualified. Bring humans, not numbers.

## Mistakes that cost people their entry

- **Starting before the bounty opens.** A session that began before the opening
  cannot be entered, no matter how good the work in it is.
- **Copying a starter or someone else's code unchanged.** The transcript gate
  counts the lines your agent actually wrote; copied code counts against you,
  and sharing entries between entrants is a disqualification.
- **Submitting without running `check` first.** Rejected entries still burn
  daily quota. The local check is free; the submission is not.
- **Paying to enter a free bounty.** Entering is free. If a step asks you to
  pay something to enter, stop — that is not part of make.fun.
- **Chasing fake signups.** Self-signups, one-network signups, IP clusters,
  and bots are filtered out and can disqualify the entry. The only score that
  pays is verified humans.

## Questions people always ask

<details>
<summary><strong>Does it cost anything?</strong></summary>

Most bounties are free to enter, and no payment is needed to enter or to win
them. The model calls your agent makes while it builds are on your own account.
</details>

<details>
<summary><strong>Is make.fun legit?</strong></summary>

Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in
an open-source on-chain escrow when a bounty opens. make.fun is not makefun.ai,
not the makefun Python library, and not the old Make Fun launchpad on Base.
</details>

<details>
<summary><strong>Do I need to know how to code?</strong></summary>

It helps. Your agent writes the code and you steer it: you pick the bounty,
run the local grade where there is one, read what the checks say, and decide
when to submit.
</details>

<details>
<summary><strong>Which agents work?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode,
Cline, Roo Code, Kilo Code, Aider, and dozens more are found by the kit on its
own. Other agents can hand over their session file with `bundle --session <file>`.
</details>

<details>
<summary><strong>What happens to my transcripts?</strong></summary>

make.fun reads them to check that your own agent built the entry. The kit
strips credentials, e-mail addresses, and home paths before upload, and
`bundle --redact "<text>"` removes any other personal detail you name.
</details>

## Links

- [make.fun](https://make.fun): the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md): the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai), to ask questions and meet other builders

---

<sub>Written for the make.fun community. Sign up with my referral link: https://make.fun/r/0tah6h10 · code `0tah6h10`</sub>
