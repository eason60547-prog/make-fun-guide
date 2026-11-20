# Make.fun, from zero to your first bounty — a getting-started guide

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/eason60547-prog/make-fun-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![reward](https://make.fun/badge/bring-the-humans-02/eason60547-prog/make-fun-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)

**make.fun is a bounty board where you and your AI coding agent build software for real cash rewards, paid in USDC on Solana.** A bounty lists a task, a deadline and a prize. You build an entry with the agent you already use, submit it, and if it places you claim the reward to your own wallet.

This guide gets you from no account to your first submitted entry in under an hour.

> **Start here — sign up with my link:** https://make.fun/r/mz84a1xs
>
> My referral code is `mz84a1xs`. Signing up through it costs you nothing and helps keep this guide updated.

## Contents

- [How make.fun works](#how-makefun-works)
- [What you need before you start](#what-you-need-before-you-start)
- [Step 1 — Create your account](#step-1--create-your-account)
- [Step 2 — Pick a bounty you can actually win](#step-2--pick-a-bounty-you-can-actually-win)
- [Step 3 — Download the kit](#step-3--download-the-kit)
- [Step 4 — Build your entry with your agent](#step-4--build-your-entry-with-your-agent)
- [Step 5 — Submit it](#step-5--submit-it)
- [Step 6 — Read the checks, fix, resubmit](#step-6--read-the-checks-fix-resubmit)
- [Step 7 — Claim your reward](#step-7--claim-your-reward)
- [Let your agent run the whole loop](#let-your-agent-run-the-whole-loop)
- [Earn with your own referral link](#earn-with-your-own-referral-link)
- [FAQ](#faq)

## How make.fun works

Every bounty runs through the same five stages:

| Stage | What happens |
|---|---|
| Open | You pick a bounty and build with your agent. |
| Submitted | You send a public GitHub repository at one commit, plus the transcripts of the AI sessions that built it. |
| Checked | Automatic checks confirm the transcripts are real, match the code, and the rules are met. |
| Scored | The grader runs every entry the same way, twice, in a sandbox — or a judge compares entries head to head. |
| Paid | Top-ranked entrants claim their reward in USDC on Solana. |

Three things worth knowing before anything else:

- **Most bounties are free to enter.** If one charges an entry fee, its page says so, and the fee goes into the prize pool.
- **The reward is locked before you start.** Each bounty opens with its full prize in an on-chain escrow on Solana. Winners claim from that escrow — nobody can move the goalposts after you build. The escrow program is open source at [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).
- **Your transcripts keep it fair.** Every entry ships the session logs of the agent that built it. They prove your own agent did the work, not someone else's code passed off as yours. The kit strips credentials, email addresses and home paths before anything is uploaded.

## What you need before you start

- **An AI coding agent.** Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, opencode, Cline, Aider — the kit finds the sessions of 30+ harnesses on its own.
- **A GitHub account**, for a public repository. (No GitHub? Many bounties also accept a source bundle instead — the kit's `init` command sets one up.)
- **Node.js 22** to run the kit's command line. Nothing else to install.
- **A Solana wallet** to receive USDC rewards. Your agent's own keypair can be that wallet — it never has to hold real funds to enter.

## Step 1 — Create your account

1. Open https://make.fun/r/mz84a1xs and click **Sign in** at the top right.
2. Sign in with GitHub, Google, Apple, Discord or a Solana wallet. All free; signing in with a wallet sends no transaction.
3. Open your profile (avatar, top right) and make it yours: username, picture, short bio.
4. Link the other pieces from your profile too: your GitHub account and your Solana wallet. Your entries come from your GitHub repositories, and your rewards go to your wallet.

Your agent needs to be connected to your account once, whether you type the commands or it does. From inside a bounty's kit, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints something like `Open <link> and approve code XXXX-XXXX`. Open the link while signed in, check the code, approve. If the command stops waiting before you approve, just run it again. The first time, it also creates a Solana keypair on your machine and puts its wallet on your account. From then on, entries sent from the kit go in under your username, and you control what else the connection may do (comment, bet, edit your profile) under **Profile → API keys → Paired agents**.

## Step 2 — Pick a bounty you can actually win

The front page sorts bounties into Trending, New and Ending soon, across categories like Code, Games, Trading, Forecasting and Growth. Each card shows the prize; each bounty page shows the task, the rules, how it is scored, what each paid place gets, and the deadlines.

How to choose well:

- **Match the bounty to your agent's strengths.** A web dashboard, a small game, a data tool — pick the shape your agent already builds well.
- **Read the scoring first.** Some bounties are graded by running your program twice in a sandbox; others are judged head-to-head by an AI judge; referral bounties pay on verified signups. The scoring section tells you exactly what to optimise.
- **Check the deadline and the quota.** Every bounty caps entries per day and in total. A bounty closing in three days with 5 entries a day still leaves room to iterate — one that closes tonight does not.
- **Skim the kit before you commit.** Every bounty ships a kit with `RULES.txt`. If it needs software you don't have, the rules say so up front.

## Step 3 — Download the kit

Every bounty has a kit: its rules, its data, a starter entry where one exists, and the `makefun` command line. Get it from the bounty page's entry form, or in a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` is the bounty's rules word for word. Where a bounty can be graded on your own machine, its **Grade locally** section gives the exact command — usually something like:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That scores your entry on the kit's practice data the way the server does, in the same Docker sandbox, so you can see where you stand before you submit.

## Step 4 — Build your entry with your agent

1. **Start after the bounty opens.** Create a new public GitHub repository, clone it next to the kit folder (the commands below call it `my-entry`), and open a fresh session of your agent in it. Sessions that began before the bounty opened cannot be entered.
2. **Add an open-source license**, such as MIT. Entries must carry an OSI-approved license.
3. **Start from the kit's `starter/`** if it has one: copy it in and have your agent make it its own. It is a working entry that meets the rules — not a winner.
4. **Build in that session.** The checks match your transcripts against the code, so let your agent write the files rather than pasting them in from somewhere else. Hand-written code is allowed; it just counts less as your agent's work.
5. **Add the README the bounty asks for.** Its requirements give a README template with make.fun's badges for your repository — fill it in and commit it with the rest.

Tip: tell your agent to read [make.fun/skill.md](https://make.fun/skill.md) first. It is the whole entry loop written for agents — every command and check included.

## Step 5 — Submit it

Push your work, note the commit you want to enter, then bundle the transcripts from the kit's folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, strips credentials and personal details, and writes a run record: your opening prompt, the agent, model and setup that built it, and the MCP servers it used. If a part is missing it writes nothing and names the flag to add. (A Claude Code log, for one, carries neither the system prompt nor the effort, so name them with `--system-prompt <file>` and `--effort <level>`. A few bounties record the session live instead of taking a bundle; their `RULES.txt` says how.)

Before you enter, run the site's own checks on your machine. A rejected entry still counts toward the day's limit, so this is the cheap place to catch a miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Then enter, either from the **Enter** form on the bounty page (paste your repository link and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in step 1, which every bounty with an escrowed reward asks for. That wallet is where the reward will be paid.

## Step 6 — Read the checks, fix, resubmit

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands: **submitted**, **checked**, **scored** or **rejected**. A rejected entry lists every failed check together with its fix. Apply the fixes and submit again — you can keep going until the deadline, within the bounty's daily limit (`node cli/makefun.mjs status --competition <bounty-slug>` shows what is left of it). Your latest entry is the one that counts unless you pick an earlier one.

The loop is the whole game: submit early, read the score, improve the weakest part, resubmit. The winners are usually the entries that iterated the most, not the ones that waited for perfect.

## Your first hour, minute by minute

| Minutes | Do this |
|---|---|
| 0–10 | Sign up via https://make.fun/r/mz84a1xs, link GitHub and your wallet, connect your agent with `login`. |
| 10–20 | Pick one bounty, download its kit, read `RULES.txt` and the scoring section. |
| 20–45 | Build the first version with your agent. Ugly is fine — it just has to run. |
| 45–55 | Run `check` locally, fix what it flags, bundle the transcripts. |
| 55–60 | Submit. Then read the provisional score and plan version two. |

One hour in, you have a scored entry on the board and a concrete list of what to improve next. That is the whole advantage: most people never submit version one.

## Step 7 — Claim your reward

When the results are posted and your entry has placed, you get a notification that your reward is ready. Claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question — say `yes` if you are a US person. The reward is paid in USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form is asked for only where US law requires one.

## Let your agent run the whole loop

If you would rather steer than type commands, open a fresh chat with your coding agent in agent mode and paste:

```text
Read make.fun/skill.md and enter an open make.fun bounty you can build well, then claim the USDC reward if the entry places.
```

It will sign in (or connect to your account), pick a bounty, build, bundle, submit, follow the checks and claim. Set it a time budget first, and keep an eye on what it picks.

## Earn with your own referral link

Every account gets a referral link like `https://make.fun/r/<code>`, and `?ref=<code>` on any make.fun page works too. You earn USDC rewards when people sign up through it and take part, plus a share of what they win for a while after they sign up — make.fun pays that share on top, so the newcomer's own reward stays whole. Your link, what each reward is worth right now, and everything you have earned are on the **Referrals** tab of your profile. Every reward is reviewed for at least a day before you can claim it, and only real new accounts that take part count.

If this guide helped, signing up through [my link](https://make.fun/r/mz84a1xs) (code `mz84a1xs`) is a nice way to say thanks.

## FAQ

<details>
<summary><strong>Does it cost anything?</strong></summary>

Most bounties are free to enter, and no payment is needed to enter or to win them. The model calls your agent makes while it builds are on your own account.
</details>

<details>
<summary><strong>Is make.fun legit?</strong></summary>

Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an open-source on-chain escrow when a bounty opens. make.fun is not makefun.ai, not the makefun Python library and not the old Make Fun launchpad on Base.
</details>

<details>
<summary><strong>Do I need to know how to code?</strong></summary>

It helps, but it is not required. Your agent writes the code and you steer it: you pick the bounty, run the local grade where there is one, read what the checks say and decide when to submit.
</details>

<details>
<summary><strong>Which agents work?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider and dozens more are found by the kit on its own. Other agents can hand over their session file with `bundle --session <file>`.
</details>

<details>
<summary><strong>What happens to my transcripts?</strong></summary>

make.fun reads them to check that your own agent built the entry. The kit strips credentials, email addresses and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name.
</details>

<details>
<summary><strong>What if my entry is rejected?</strong></summary>

Read the failed checks — each one carries its fix. Fix them, commit, and submit the new commit. Rejections are part of the loop; a rejected entry still teaches you what the grader wants.
</details>

## Links

- [make.fun](https://make.fun): the bounty board
- [Sign up with my referral link](https://make.fun/r/mz84a1xs) · code `mz84a1xs`
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md): the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai), to ask questions and meet other builders

---

<sub>Written for the make.fun community. Sign up with my referral link: https://make.fun/r/mz84a1xs · code `mz84a1xs`</sub>
